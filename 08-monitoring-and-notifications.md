
# Monitoring

The primary purpose of monitors is to check whether the production site is up or down.
It does not check for correctness – that should be done with actual tests.
Monitors should be simple, fast, reliable, and cheap as they should be ran
against production as often as possible.
At Dollar Shave Club, we run about 250 monitors every minute.

For this workshop, we use a tool I built at DSC to accomplish this:
[@dollarshaveclub/monitor](https://github.com/dollarshaveclub/monitor),
and run it as a CRON job in a [CircleCI Scheduled Workflow](https://circleci.com/docs/2.0/workflows/).

## Environment Variables

Notice in `tests/config/index.js`, we have a `DOMAIN` env var.
This allows us to pass the domain as an env var so we can run the monitor
against any host we want. By default, it runs against `localhost`,
but you may want to switch it to production in the future.

Let's install the monitor runner: `npm install --save-dev @dollarshaveclub/monitor`
and add the script to `package.json`:

```
"monitors": "dsc-monitor 'tests/monitors/**/*.js'"
```

## API Monitor

Let's add a simple API monitor that checks that the `POST /api/v1/shas`
endpoint works. I would use the `request` module for this.
If the request failed, an error should be thrown.

You can run this monitor just by running `npx dsc-monitor tests/monitors/api.js`.

## Browser Monitor

Let's do a simple browser monitor that asserts that the input field and the submit button exists.
We'll use [`puppeteer`](https://github.com/GoogleChrome/puppeteer) for this.

You can run this monitor just by running `npx dsc-monitor tests/monitors/browser.js`.

## Slack Notifications

## Running Monitors as Test

Now we have monitors against production, but we might as well make them tests as well.
Let's test them against our server in CircleCI.
First, after we run our previous tests, we should serve the current application in the background:

```yaml
- run:
    name: serve
    command: node server
    background: true
```

Let's `sleep 3` just to make sure the app is up. Obviously, there are better ways
to do this, but this is easy:

```yaml
- run: sleep 3
```

Then, let's run our monitors against this server:

```yaml
- run: npm run monitors
```

Remember, it's hitting our server because the default `DOMAIN` is localhost!
Let's push a commit and see what happens.

Okay, you probably got an error about some browser dependencies.
Switch the docker image from `circleci/node:8` to `circleci/node:8-browsers`,
which includes all the browsers!

## Running Monitors as a CRON Job

Let's create a new CircleCI workflow called `monitor` (the other being `commit`, which runs on every commit).
First, we need to make the monitor jobs:

```yaml
monitor-production:
    <<: *browser-defaults
    steps:
      - checkout
      - run: npm install # TODO: restore from cache
      - run: DOMAIN=https://<your-app>.herokuapp.com npm run monitors

monitor-staging:
    <<: *browser-defaults
    steps:
      - checkout
      - run: npm install # TODO: restore from cache
      - run: DOMAIN=https://<your-staging-app>.herokuapp.com npm run monitors
```

Now, let's create the CRON workflow that runs these jobs:

```yaml
monitor:
  triggers:
    - schedule:
        # cron syntax to run every minute
        cron: "* * * * *"
        filters:
          branches:
            only:
              # only run master's version of monitors
              - master
  jobs:
    # the monitor jobs
    - monitor-production
    - monitor-staging
```

Let's push and see what happens!

## Advanced

There are many things to consider when running monitors:

- You want it to run frequently, say every 1 minute, so you want all monitors to run within a minute.
  If you have a lot of monitors, that means you need to shard them across multiple workers.
  Fortunately, this is easy to do with CircleCI.
- Puppeteer has a lot of cool features like request interception (i.e. block analytics requests so you don't screw your company's analytics),
  screenshots, and tracing timelines.

YAML also has variable-like syntax to avoid copy and paste.
In the above monitor jobs, we don't want to `npm install` from scratch every time
because that might take a minute. Instead, we want to restore from cache, but
we don't want to copy and paste that one gigantic `restore_cache` section from above.
Look at this [CircleCI config](https://github.com/jonathanong/ims/blob/master/.circleci/config.yml) for inspiration.
