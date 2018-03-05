
# Server Tests

The first tests we'll write are server tests.
Server tests are generally easier to write (compared to browser or Selenium tests) as the environment is controlled.

## Example Server

We've split up our server into several top level folders:

- `server-lib` - our "model" or business logic.
- `server-api` - our API routes
- `server-routes` - our non-API routes, i.e. our React routes
- `server` - our server, which ties all of the above folder together

The dependency tree is as follows:

```
          server
            |
    -------------------
    |                 |
server-api      server-routes
    |                 |
    -------------------
            |
        server-lib
```

By modularizing the server from the beginning, we are able to:

- Define a clear separation of concerns
- Allow us to easily find code
- Ability to run tests for a specific concern
- Separate any of these folders, specifically `server-lib`, to a separate module if it will be re-used elsewhere, i.e. in other microservices
- Improving overall test speed by running tests in only their concern

For example, running the entire server is much more expensive than just running
a few files, so we want to run tests at the lowest abstraction level possible
(in this case, at the bottom of the diagram).

## Jest

Throughout this workshop, we'll be using `jest` as our test runner.
This is the de factor runner for React apps as it includes all the packages
you may need to run tests. It also works very well for server tests
as it automatically runs all your tests in parallel.

## Supertest

`supertest` is a useful server testing library based on `superagent`.

## Test Structure

Tests are not distinguished between unit vs. integration test.
Instead, they are separated by concern or component.
For example, we have our `server-lib/images/` folder which holds
all our image logic. Any tests (whether they are unit/integration) that are just concerned with images will be in a test folder `server-lib/images/__tests__`.

```
server-lib/images/
  index.js
  upload.js
  check.js
  __tests__/
    flow-1.js
    upload.js
    check.js
```

The reasons to do this are:

- Your tests will have a clear separation of concern
- Easier to delete code
- Running tests for a specific concern will be a lot easier (see below)

To just run `server-lib/images/` tests, run the following command:

```bash
npm run test-server -- 'server-lib/images/__tests__/*.js'
```

`--` in any `npm run` command will pass any arguments after `--` to the original
command. In this case, the command will be expanded to
`jest --coverage --config jest.server.config.json 'server-lib/images/__tests__/*.js'`.
We use quotes around the globs (`*`s) so that `jest` searches for files instead
of the shell, which differs between environments.

What if tests are concerned with more than just images?
Then you move the `__tests__` folder up to the closest ancestor of the concerns.

## Node.js Tests

Write a test that checks the metadata of an image.

Write a test that, given an image URL, streams it and resizes it.

## API Tests

Write a test that
