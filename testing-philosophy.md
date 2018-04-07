
# Testing Philosophy

## Types of Tests

### According to Stakeholders

- Acceptance tests – test that business/product requirements are fulfilled
  - Given X, user can buy Y
-  Regression tests – test for bugs or outages we previously had and/or tests for previous features
  - X went down, costing us $Y. This should not happen again.

### According to Engineers
- Unit – testing a component in isolation
  - React shallow snapshots
  - Testing methods on a class
- Integration – testing multiple components together
  - React snapshots
  - API tests that call multiple other functions
- Automation – testing devices or browsers
  - Selenium tests on browsers
  - Whatever mobile uses to test mobile
  - Requires spinning up an entire application
- Smoke – simple tests that test breadth, but not depth of problems
  - A page doesn’t load in Internet Explorer
  - Code doesn’t compile
- Monitor – tests that continuously run against production
  - Test every minute that the homepage loads
- End-to-End – tests that go through a series of steps
  - Generally ran in Automation
- Acceptance – any type of test that tests a user requirement
  - Generally End-to-End test, but could be setup as an integration

## Write Tests as Close To Code As Possible

## Delete Expensive Tests No One Cares About

## Only Run Tests That Matter For This Code
