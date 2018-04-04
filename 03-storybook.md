
# Storybook

[Storybook](https://storybook.js.org/) is a tool for UI development,
allowing you to build and play with UI components outside of your application.
This makes development in large, complex applications a lot easier and faster
as you don't need to spin up the entire application.

Storybook is already setup for the sample application, although it's easy to setup.
Look at these files and folders:

- `package.json` - all the `@storybook` modules added to `devDependencies` as well as the `scripts` commands
- `.storybook` - the storybook configuration
- `client/ui/` and `client/components/` - the components and styles for storybook (and the application)
- `client/stories/` - the stories for storybook

To build the storybook statically, run `npm run build-storybook`.
However, for development, we just want to run `npm run storybook`.

## Implement Storyshots

Following the 80/20 principle, [Jest snapshots](https://facebook.github.io/jest/docs/en/snapshot-testing.html)
are an easy way to get coverage on your React components without much effort.
[@storybook/addon-storyshots](https://github.com/storybooks/storybook/tree/master/addons/storyshots)
turns your Storybook stories into snapshot tests, killing two birds with one stone.
Now, whenever you write a story for visual testing and component authoring,
you're also writing a snapshot test!

Storyshots is already installed in the example app.
We want to install it by adding the following test at `client/stories/__tests__/index.js`:

```js
import initStoryshots from '@storybook/addon-storyshots'

initStoryshots()
```

Next, let's setup our `jest` tests for the client. Install `jest`:

```bash
npm install --save-dev jest jest-css-modules babel-jest
```

Next, let's add the following `jest` config file at `jest.jsdom.json`:

```json
{
  "collectCoverageFrom": [
    "**/*.js"
  ],
  "coveragePathIgnorePatterns": [
    "/node_modules/",
    "/__tests__/",
    ".css"
  ],
  "roots": [
    "client"
  ],
  "testEnvironment": "jsdom",
  "transform": {
    "\\.css$": "<rootDir>/node_modules/jest-css-modules",
    "\\.js$": "<rootDir>/node_modules/babel-jest"
  },
  "transformIgnorePatterns": [
    "/node_modules/.*\\.js$"
  ]
}
```

You can read more about the configuration here: https://facebook.github.io/jest/docs/en/configuration.html

Next, let's add the test command to `package.json`:

```
"test:jsdom": "jest --config jest.jsdom.json",
```

Now, let's run it!

```bash
npm run test:jsdom
```

And, let's add it to our CircleCI config:

```yaml
- run: npm run test:jsdom
```

### Passing Options

To get code coverage:

```bash
npm run test:jsdom -- --coverage
```

To update snapshots:

```bash
npm run test:jsdom -- --updateSnapshot
```

To run specific tests:

```bash
npm run test:jsdom -- 'client/stories/__tests__/*.js'
```

## Implement storybook-deployer

[@storybook/storybook-deployer](https://github.com/storybooks/storybook-deployer)

## Advanced

- Look into implementing addons: https://storybook.js.org/addons/addon-gallery/
- Look into continuous visual regression testing: https://percy.io/
