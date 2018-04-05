
# CI Workshop

This workshop guides you through setting continuous integration and delivery in a sample React and Node application. You will learn:

- How to setup CI/CD with Heroku Pipelines
- How to write and setup unit and automation tests
  - Unit tests with Jest
  - Automation tests with Puppeteer and Selenium
- How to setup production monitoring
  - Custom uptime/downtime monitoring with Slack notifications
  - Error monitoring with Rollbar
- How to keep your dependencies up to date
  - Automatic testing dependency upgrades with Greenkeeper
  - Checking for security issues with Node Security

The goal is to dip your hands in enough aspects of CI/CD,
but not go into depth on any one aspect.
This workshop consists mostly of reading and copying and pasting,
just like real web development ;)

## Lessons

1. [Linting](01-linting.md)
2. [Continuous Integration](02-continuous-integration.md)
3. [Storybook](03-storybook.md)
4. [Code Coverage](04-code-coverage.md)
5. [React Tests](05-react-tests.md)
6. [Server Tests](06-server-tests.md)
7. [Continuous Delivery](07-continuous-delivery.md)
8. [Monitoring and Notifications](08-monitors-and-notifications.md)
9. [End-to-End Tests](09-automation-tests.md)
10. [Error Monitoring](10-error-monitoring.md)
11. [Dependency Upgrades and Security Checks](11-dependency-upgrades-and-security-checks.md)
12. [GitHub Status Checks](12-github-status-checks.md)
13. [Dark Launching with Feature Flags](13-dark-launching-with-feature-flags.md)
14. [Learn More](14-learn-more.md)

Please read the background below before starting on the lessons.

## Contact

Contact me:

- GitHub: [@jonathanong](https://github.com/jonathanong)
- Twitter: [@jongleberry](https://twitter.com/jongleberry)
- Email: [me@jongleberry.com](mailto:me@jongleberry.com)

## What is Continuous Integration/Delivery?

There are a lot of blog posts on this topic. Here is one graph that explains it:

[![](https://www.nastel.com/wp-content/uploads/blogpic-32-600x342.png)](https://www.nastel.com/blog/devops-continuous-integration-vs-continuous-delivery-vs-continuous-deployment/)

We will be implemented continuous integration and delivery,
but not continuous deployment.
We will also be implementing a barebones version feature flags.
See this post and company for more details:

[![](http://blog.launchdarkly.com/wp-content/uploads/2016/06/software_dev_graph.jpg)](http://blog.launchdarkly.com/powering-continuous-delivery-with-feature-flags/)

What is CI/CD in a few bullet points?

- Deliver small commits often.
  - No gigantic PRs, no gigantic merge conflicts
  - Dark launch code behind a feature flag so you can ship features without enabling it for all users
- An automated delivery pipeline
  - Automatically going to the next step after tests pass
  - Automatically triggering jobs when a specific event occurs
- Monitoring in production and elsewhere in your stack to create an automated feedback loop

[![](https://jelastic.com/blog/wp-content/uploads/2015/07/devopsimage.png)](https://jelastic.com/blog/devops-tools-continuous-delivery-jelastic-private-cloud-part-2-configure-jenkins-app-life-%D1%81ycle-automation/)

## Why Continuous Integration/Delivery?

- Scale your code and team - with sufficient testing, monitoring, and automation, you can be confident that new code works as intended and does not break existing features. Existing CI/CD pipeline will be your guide to your engineering culture.
- Minimize downtime - with sufficient tests and monitors, downtime should be minimal. With sufficient monitors, the time to incident response should be very quick,
- Pinpoint regressions - with small commits and a robust CI/CD pipeline, if a regression even makes it to production, you can easily find the cause.


## Testing Philosophy

There's a lot of testing philosophies on the internet.
The most common is the testing pyramid:

[![](https://martinfowler.com/bliki/images/testPyramid/test-pyramid.png)](https://martinfowler.com/bliki/TestPyramid.html)

The latest philosophy, which I prescribe to, in the JS community is the testing trophy:

[![](images/testing-trophy.jpg)](https://blog.kentcdodds.com/write-tests-not-too-many-mostly-integration-5e8c7fff591c)

What do each of these sections mean?
It depends on a lot on the context.
Here's one breakdown (actual definitions do not matter in real life):

- Static Testing - validate that your code is syntactically correct
  - [eslint](https://eslint.org/) - validate your JS
  - [stylelint](https://github.com/stylelint/stylelint) - validate your CSS
- Unit Testing - validate that your components work correctly in isolation
  - React examples:
    - Shallow snapshot tests
    - Testing methods on React components, perhaps with mocking
    - Testing that one reducer works correctly
  - Server examples:
    - Test that a function works correctly
    - Test that a single API call returns a valid response
- Integration Testing - validate that your components work correctly together
  - React examples:
    - Snapshot tests w/ different props
    - Testing the entire redux store
  - Server examples:
    - Test that multiple models interact with each other correctly
    - Test that multiple API calls work correctly together
- End-to-End testing:
  - Go through a flow on your actual site with a browser

This list is just a guideline, but definitions could change based on your scenario.
The main tenets of the testing trophy is:

- Lint!
- Spend time on integration tests instead of unit tests
  - Avoid mocking and spying on functions as it takes a lot of effort to write those tests
- Focus on tests that fulfill actual acceptance criteria.
  - Unit tests are tests for engineers. End-to-End tests are tests for stakeholders. It's more important to write tests for stakeholders as that's how your work is measured.
- If your tests become too slow, parallelize and shard your tests!

## Tools

Backend:

- [Koa](http://koajs.com/)

Frontend:

- [React](https://reactjs.org/)
- [Redux](https://redux.js.org/)
- [Storybook](https://storybook.js.org/)

Testing:

- [eslint](https://eslint.org/)
- [stylelint](https://github.com/stylelint/stylelint)
- [Jest](https://facebook.github.io/jest/) - for both frontend and backend tests
- [supertest](https://github.com/visionmedia/supertest) - for testing APIs
- [Puppeteer](https://github.com/GoogleChrome/puppeteer) - for monitors and automation tests
- [Selenium](https://www.seleniumhq.org/) - for automation tests
- [@dollarshaveclub/e2e](https://github.com/dollarshaveclub/e2e) - an end-to-end test runner for Puppeteer and Selenium
- [@dollarshaveclub/monitor](https://github.com/dollarshaveclub/monitor) - a monitoring framework

SaaS:

- [CircleCI](https://circleci.com/)
- [Codecov](https://codecov.io/)
- [Heroku](https://www.heroku.com/)
- [Rollbar](https://rollbar.com)
- [Greenkeeper](https://greenkeeper.io/)
- [Node Security](https://nodesecurity.io/)
- [Slack](https://slack.com/)

## Setup

Install `node@8.9` or later:

```bash
# If you install via homebrew:
brew install node
# brew upgrade node

# If you install via nvm:
nvm install 8
```

Install (or `upgrade`) Selenium and friends:

```bash
brew install selenium-server-standalone chromedriver
# brew upgrade selenium-server-standalone chromedriver
```

Install Heroku's CLI: https://devcenter.heroku.com/articles/heroku-cli

## Implicit Steps

- We expect you to commit small and often. We won't tell you to `git commit` and `git push`.
