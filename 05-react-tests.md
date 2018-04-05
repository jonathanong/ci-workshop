
# React Tests

## Snapshot Test

Next, we'll add more frontend tests.
First, we'll do a snapshot test,
although Storyshots already handles this.
You should be able to follow [Jest's documentation](https://facebook.github.io/jest/docs/en/snapshot-testing.html).

## Redux Action Dispatcher Test

Our redux store is very simple.
It has a structure like so:

```json
{
  "shas": [
    {
      "input": "some input",
      "sha": "abcdabcd123123"
    }
  ]
}
```

Let's call the `getSha()` action dispatcher and assert that the
latest input is appended to the redux store.

Notice that this action dispatcher uses an API call,
but we don't have an API setup for this test.
We should look into using [`jest-fetch-mock`](https://github.com/jefflau/jest-fetch-mock)!

## Advanced

- For more advanced tests, checkout [react-test-renderer](https://reactjs.org/docs/test-renderer.html) and [Enzyme](https://github.com/airbnb/enzyme).
- As you add more tests to Jest, you'll notice that the tests become a lot slower.
  The reason is that Jest, by default, uses the # of CPUs your VM has as the number
  of parallel tests to run. However, in CircleCI and many VMs, the VM returns
  the # of CPUs of the host machine, which may be a high number like 16 or 32.
  To fix this, add `--maxWorkers 2` or some other reasonable value to the end of your test command.
