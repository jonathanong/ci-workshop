
# Continuous Integration Testing

Now, we setup continuous integration testing!
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

## CircleCI

## Codecov

## TODO

- In the `test` job, add the following checks:
  - Run `eslint`
  - Run `stylelint`
  - Run server tests, then report code coverage to `codecov`
  - Run react tests, then report code coverage to `codecov`

Note: every time you run `jest`, a `coverage/` directory is created with coverage.
