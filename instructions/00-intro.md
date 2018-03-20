
# Intro

## What is Continuous Integration/Delivery?

- Deliver small commits often.
  - No gigantic PRs, no gigantic merge conflicts
  - Dark launch code behind a feature flag so you can ship features without enabling it for all users
- An automated delivery pipeline
  - Automatically going to the next step after tests pass
  - Automatically triggering jobs when a specific event occurs
- Monitoring in production and elsewhere in your stack to create a feedback loop

There is a lot of resources online about this.

## Why Continuous Integration/Delivery?

- Scale your code
- Scale your team
- Minimize downtime
- Pinpoint regressions

## Setup

Install `node@8.9` or later:

```bash
brew install node
# brew upgrade node
```

Install (or `upgrade`) Selenium and friends:

```bash
brew install selenium-server-standalone chromedriver geckodriver
# brew upgrade selenium-server-standalone chromedriver geckodriver
```

Install Heroku's CLI: https://devcenter.heroku.com/articles/heroku-cli
