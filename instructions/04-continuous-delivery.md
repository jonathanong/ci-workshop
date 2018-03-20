
# Continuous Delivery

## Heroku Pipelines

[Heroku Pipelines](https://devcenter.heroku.com/articles/pipelines) allows
you to deploy a Heroku app throughout every stage of development.

- Every PR will create a review application
- When you merge to master, automatically deploy to staging
- Manually deploy to production

Because we are going to setup the pipeline so that we deploy to production manually,
this is considered continuous delivery, not deployment.
However, it wouldn't be hard to automatically deploy to production.

Let's setup Heroku:

## Papertrail

https://papertrailapp.com

Papertrail stores your logs and allows you to easily search them.
You can set up search triggers that slack you when an error occurs.

Let's setup papertrail on all our apps.
Let's also setup a Slack hook for any mention of "error".
