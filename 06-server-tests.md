
# Server Tests

Now, we write tests for the server!
Luckily, these tests are a little easier to write,
especially since this sample application does not have a database.

## Setup the Test Runner

Similar to our frontend Jest tests, we need to setup backend jest tests.
Copy the following to `jest.server.json`:

```json
{
  "collectCoverageFrom": [
    "**/*.js"
  ],
  "coveragePathIgnorePatterns": [
    "/node_modules/",
    "/__tests__/"
  ],
  "roots": [
    "server"
  ],
  "testEnvironment": "node"
}
```

Next, let's add the test command to `package.json`:

```
"test:server": "jest --config jest.server.json",
```

Test it out by running `npm run test:server`!

## Unit Test

Our first method, `getSha`, takes a string and returns a commit sha in hex.
Let's test that the commit sha returned from any valid input returns a valid hex.
You could use `require('assert')` or Jest's built-in [expect](https://facebook.github.io/jest/docs/en/expect.html).

The test is scaffolded here: https://github.com/jonathanong/ci-reference-app/blob/master/server/__tests__/shas.js

We should also be thinking about all the test cases.
What happens if someone passes something that isn't a string to `getSha()`?
We should add tests to make sure those cases are properly handled: they should
either return an informative message in the form of a `TypeError`.

## API Test

[supertest](https://github.com/visionmedia/supertest) is a testing library
built on top of [superagent](http://visionmedia.github.io/superagent/) that
makes testing simple API endpoints dead simple.
Let's implement it for our `POST /api/v1/shas` route.

The test is scaffolded here: https://github.com/jonathanong/ci-reference-app/blob/master/server/__tests__/api.js

## Running in CircleCI

Like our jsdom tests, we need to add the test commands to our CircleCI config:

```yaml
- run: npm run test:jsdom -- --coverage
- run: npx codecov
```

## Advanced

- When you need to test multiple API calls in the same session, user `require('superagent').agent()`
- Like with your React jest tests, be sure to set `--maxWorkers`
