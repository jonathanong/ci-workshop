
# React Tests

## Jest

We again use `jest` for our React tests.

## Enzyme



## Snapshot Tests

https://facebook.github.io/jest/docs/en/snapshot-testing.html

Snapshots are the easiest types of React tests to write as they just
render your component to a DOM tree, then save the tree. Your test is just then
comparing your component DOM tree to the saved snapshot of the DOM tree. If something
has changed, you can update the snapshots manually.

For declarative, stateless components, this may be all you need.
It's a great 80/20 to get test coverage.
However, it does not test functionality, just DOM structure.
If you are creating components with state, you're going to need more than just snapshot tests.

## Redux Tests

Redux

## Enzyme Tests

## `connect()` Tests

## Further Reading

- http://mttyng.com/the-enzyme-jest-survival-guide-react-testing-101/
