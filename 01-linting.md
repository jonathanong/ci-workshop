
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

Next let's add configuration files for each at the root of the repository.

[`.eslintrc`](https://eslint.org/docs/user-guide/configuring):

```yaml
---
extends:
  - standard
  - standard-react
parser: babel-eslint # necessary for some futuristic syntad
```

[`.stylelintrc`](https://stylelint.io/user-guide/configuration/):

```yaml
---
extends:
  - stylelint-config-standard
```
