
# Dependency Upgrades and Security Checks

With so many `npm` modules out there, one of the most annoying parts about
being a JS developer is keeping up with the latest packages.
Luckily, there are tools to help you keep things up to date!

## Node Security

[Node Security](https://nodesecurity.io/) checks that your dependencies
have no security vulnerabilities and recommends upgrades if they've also fixed them.

Install this in your app and add the badge to your readme!

## Greenkeeper

[Greenkeeper](https://greenkeeper.io/) is a service that makes PRs for your app
instantly after a dependency publishes a new version. You'll be able to quickly
know whether a dependency broke your app if your tests fail.
If your tests pass, you can upgrade your dependency with a "merge" click!

Install this in your app and add the badge to your readme!

## Automatic Merging

At DSC, our test suite could take up to 30 minutes since our review apps are not
as fast as Heroku's and we test against them. Instead of waiting around all day
for tests to pass, we have a tool that automatically merges passing PRs for you!
This has been open sourced as [gh-automerge](https://github.com/jonathanong/gh-automerge).

This has allowed us to upgrade our dependencies (and push code) a lot quicker
as we simply automerge all dependency upgrades that have passing tests.
