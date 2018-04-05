
# Continuous Delivery

Next, let's actually deploy our application!
I'm going to assume you have a Heroku account!

Let's create a new pipeline. Call it whatever you want:

![](./images/heroku/01-create-new-pipeline.png)

![](./images/heroku/02-create-new-pipeline-form.png)

Now, we'll see a page that shows your pipeline.
Read more about Heroku Pipelines here: [https://devcenter.heroku.com/articles/pipelines](https://devcenter.heroku.com/articles/pipelines).
The idea is that once you deploy to staging, you can then instantly deploy to production. No tests need to run, no new container needs to built, nothing.

![](./images/heroku/03-pipeline-overview.png)

Let's create your staging and production apps.
Here, I've added `-staging` to my staging app.

![](./images/heroku/04-create-staging-app.png)

Next, let's go to the "Deploy" section of our staging application.
Let's "Enable Automatic Deploys" from the `master` branch,
and also "Wait for CI to pass before deploy".
Now, staging will automatically deploy after your tests pass on `master`!

![](./images/heroku/05-connect-staging-app-to-github.png)

Next, let's setup our review apps.
Review apps are just apps specifically for your PRs.
This makes QA and testing easier.
You could even run Automation tests against it if you really want!
Read more here: [https://devcenter.heroku.com/articles/github-integration-review-apps](https://devcenter.heroku.com/articles/github-integration-review-apps).

![](./images/heroku/06-enable-review-apps.png)

![](./images/heroku/07-enable-review-apps-form.png)

Now, let's push a commit to master and see what happens!
