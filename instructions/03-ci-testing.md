
# Continuous Integration Testing

Now, we setup a continuous integration pipeline and add our tests!
With CI testing enabled, our tests will run on every push to GitHub.

## Workflow Improvements

### Status Check Requirements

You can enable status check requirements in GitHub,
which require certain checks, such as your tests, to pass,
otherwise you would disable merges. This blocks people from committing bad
code and encourages people to fix things.

### Only Running a Subset of Tests Locally

For very large projects, running tests locally could take 5-10 minutes and
destroy your battery. With CI testing, you just run tests for code you changed
locally (ex. `npm run test-server -- 'server-lib/images/__tests__/*.js'`),
push your changes to GitHub, then let your CI platform run the whole suite of tests.

## Set Up CircleCI

[CircleCI](https://circleci.com/) is one of many CI providers.
However, the reason I like CircleCI is for its [Workflows](https://circleci.com/docs/2.0/workflows/),
which allow you to create sophisticated CI pipelines.
At Dollar Shave Club, we use it to run multiple E2E tests in parallel and
hundreds of monitors every minute.
It's also Docker-based, allowing it to be blazing fast and supporting
basically any use-case.

## Set Up Codecov

[Codecov](https://codecov.io/) is a SaaS for creating dashboards
of code coverage and blocking checks as necessary.

## TODO

- In the `test` job, add the following checks:
  - Run `eslint`
  - Run `stylelint`
  - Run server tests, then report code coverage to `codecov`
  - Run react tests, then report code coverage to `codecov`

Every time you run `jest`, a `coverage/` directory is created with coverage,
so after sending results to codecov, delete the `coverage/` folder.
