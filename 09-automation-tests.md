
# Automation Tests

Automation tests run actual browsers or devices users use
such as a browser via Puppeteer or Chrome.
They are generally more expensive as they actually spin up a browser and go
through a flow. These tests are generally what QA and product cares about the most
as they should test actual User Acceptance Criteria, which would label the test
as Acceptance tests or End to End tests.

We distinguish between End to End vs Automation because at DSC, we also
run browser smoke tests (i.e. make sure our page loads in Edge) within our E2E suite,
though it's only a portion of it.

We'll use another tool I've built at DSC called
[@dollarshaveclub/e2e](https://github.com/dollarshaveclub/e2e)
to run our Selenium test.

The setup should be very similar to the monitors.

Let's install the monitor runner: `npm install --save-dev @dollarshaveclub/e2e`
and add the script to `package.json`:

```
"automation": "dsc-e2e 'tests/automation/**/*.js'"
```

We'll then add the test command to our CircleCI config after our monitors:

```yaml
- run: npm run monitors
- run: npm run automation
```

## Writing your E2E Test

Let's write an E2E test that:

1. Adds random text to the input field
1. Submits the text
1. Expects a row to appear in the table

This test has been scaffolded for you: https://github.com/jonathanong/ci-reference-app/blob/master/tests/automation/home.js

## Advanced

[@dollarshaveclub/e2e](https://github.com/dollarshaveclub/e2e) is a complex tool
that solves a lot of problems with automation tests:

- They're slower
- They're more expensive
- They're more flaky

Read more on how [@dollarshaveclub/e2e](https://github.com/dollarshaveclub/e2e) solves these problems.

You may also want to look into running your automation tests in different browsers
using services like:

- [Sauce Labs](https://saucelabs.com/)
- [Browser Stack](https://www.browserstack.com/)


Remember, E2E tests are at the top of the testing trophy.
Very few should be written!
