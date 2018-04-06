
# Code Coverage

Now that we have some tests running, let's setup code coverage so we can see
how much of our code is tested over time!

To see the code coverage of our Storybook snapshot tests, run:

```bash
npm run test:jsdom -- --coverage
```

Again, `npm run` passes all arguments after `--` to the underlying command.
Notice you have some coverage. Great!

Now, let's update our `npm run test:jsdom` command in CircleCI to report coverage.

## Codecov

There are multiple code coverage services, I use Codecov because it looks the prettiest.
Because are working with a public repository, setting up Codecov is easy.
After we run `npm run test:jsdom -- --coverage`,
we just need to run the `codecov` executable afterwards.

To do so, install it: `npm install --save-dev codecov`,
then add `npx codecov` after your test command:

```yaml
- run: npx codecov
```

After your first run, you should be able to go to your repository's
Codecov page and see the coverage.
To go directly, go to [https://codecov.io/gh/\<github-handle\>/\<repo-name\>](https://codecov.io/gh/\<github-handle\>/\<repo-name\>).

## Codecov Badge

Let's add a Codecov badge to your readme!
Go to the settings page, go to the left and select "Badge",
then copy the markdown snippet to your readme. Done!

## Advanced

- Private repositories are a little harder. When you go to your repository page,
  you'll be given a copy token. Add this to your CircleCI job as a `CODECOV_TOKEN`
  environment variable, then you'll be squared away.
- You may want to require all PRs to have sufficient code coverage and enforce this with a GitHub Required Status Check. This can be done with a [Codecov yaml](https://docs.codecov.io/v5.0.0/docs/codecov-yaml).
