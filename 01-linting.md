
# Linting

The two linting tools we'll implement are:

- [eslint](https://eslint.org/)
- [stylelint](https://github.com/stylelint/stylelint)

Add the following packages to your `package.json` as `devDependencies`:

```
"babel-eslint": "^8.2.2",
"eslint": "^4.19.0",
"eslint-config-standard": "^11.0.0",
"eslint-config-standard-react": "^6.0.0",
"eslint-plugin-import": "^2.9.0",
"eslint-plugin-node": "^6.0.1",
"eslint-plugin-promise": "^3.7.0",
"eslint-plugin-react": "^7.7.0",
"eslint-plugin-standard": "^3.0.1",
```

`eslint-config-standard` is tedious to install because you need to install 6 other peer dependencies manually.

```
"stylelint": "^9.1.3",
"stylelint-config-standard": "^18.2.0",
```

Let's run `npm install` to install these dependencies,
then let's add configuration files for each at the root of the repository.

[`.eslintrc`](https://eslint.org/docs/user-guide/configuring):

```yaml
---
extends:
  - standard
  - standard-react
parser: babel-eslint # necessary for some futuristic syntax
```

[`.stylelintrc`](https://stylelint.io/user-guide/configuration/):

```yaml
---
extends:
  - stylelint-config-standard
```

Finally, we'll add the linting commands to `package.json`'s `scripts`:

```
"eslint": "eslint .",
"stylelint": "stylelint '**/*.css'",
```

Now, let's see what happens when we run these commands:

```bash
npm run eslint
```

Hmmm... that's a lot of errors for packages in `node_modules`!
Let's ignore all files in our `.gitignore`!
Let's update our commands to:

```
"eslint": "eslint . --ignore-path .gitignore",
"stylelint": "stylelint '**/*.css' --ignore-path .gitignore",
```

Now, when we run `npm run eslint` or `npm run stylelint`,
we'll only see errors concerning our own code.

However, notice that when we run `npm run eslint`, we get errors
in our tests files that look like `'test' is not defined`.
This is because `jest` adds globals to the runtime to make tests authoring easier.
We want `eslint` to understand that these files are tests.
There are multiple ways to enable this:

My preferred method is to the following `.eslintrc` to all `__tests__` folders:

```yaml
---
env:
  jasmine: true
  jest: true
```

This is the correct method, but it's also tedious.
We could also just add this to our root `.eslintrc` file.

You may also get errors like `'fetch' is not defined`. The reason is that we did
not specify the `client/`'s environment as a browser! Create this `client/.eslintrc` file:

```yaml
env:
  browser: true
```

Now notice that when you run `npm run eslint`,
there are `semicolon` errors as `standard` does not like semicolons.
Instead of manually fixing these errors, just run `npm run eslint -- --fix`.
`npm run` passes all arguments after the `--` to the underlying command.

## Advanced

Here are my [final commands for linting](https://github.com/jonathanong/ims/blob/3afd07310577e17fe64d1e988eacc5d32ff5917e/package.json#L8-L9).
Run `npx eslint -h` and `npx stylelint -h` for more information:

```
"eslint": "eslint . .storybook --cache --cache-location node_modules/.cache/eslint --ignore-path .gitignore",
"stylelint": "stylelint '**/*.css' --cache --cache-location node_modules/.cache/stylelint --ignore-path .gitignore",
```
