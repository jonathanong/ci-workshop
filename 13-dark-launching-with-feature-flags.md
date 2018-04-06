
# Dark Launching with Feature Flags

Feature flags are just flags for showing or enabling features of the site.
Sometimes, these feature flags are just for dark launching,
i.e. you push code, but don't want to use it yet.
Other times, feature flags are used for personalization.
At DSC, we use feature flags to hide or show features based on their country
as not all products are sold in all countries.

The idea behind feature flags is that you want to make small commits often.
The bigger your commits are, the higher chance that you'll end up with merge
conflicts or that you'll introduce a bug.
Once the feature is ready to be tested, QA will enable the feature flag
in their own browser and test the feature in __production__.
When it passes QA, you turn that feature on by default!

## Dark Launching a Feature

Let's dark launch a feature where our table has a red border.
By default, it will not be red, but if you enable the feature flag,
it should become and stay red.

## Creating a Feature Flag Service

Copy and paste this file to `client/feature-flags.js`:

```js

const key = 'feature-flags'

// all feature flags and their defaults
const defaultFeatureFlags = {
  redTable: false
}

const persistedFeatures = (() => {
  try {
    return JSON.parse(localStorage.getItem(key) || '{}')
  } catch (_) {
    return {}
  }
})()

export const featureFlags = Object.assign({}, defaultFeatureFlags, persistedFeatures)

export function assignFeatureFlag (feature, value) {
  if (!defaultFeatureFlags.hasOwnProperty(feature)) throw new Error(`Invalid feature: ${feature}`)

  const newPersistedFeatures = Object.assign({}, persistedFeatures, {
    [feature]: !!value
  })

  try {
    localStorage.setItem(key, JSON.stringify(newPersistedFeatures))
  } catch (err) {}

  console.log(`Feature '${feature}' set to '${!!value}'. Refresh the page to for it to take effect.`)
}

window.assignFeatureFlag = assignFeatureFlag
```


This creates a list of feature flags and their defaults,
reads persisted feature flags via `localStorage`,
and exposes a `assignFeatureFlag()` function toggle features.
Note that assigning a feature flag will require a browser refresh in this
implementation as we haven't hooked it up to our Redux store.

Next, in [client/components/SubmitShaForm/View.js](https://github.com/jonathanong/ci-reference-app/blob/master/client/components/SubmitShaForm/View.js), let's import the feature flags:

```js
import { featureFlags } from '../../feature-flags'
```

And toggle a red table when `featureFlags.redTable` is true:

```js
<form className={featureFlags.redTable ? 'red-table' : ''} onSubmit={this.onSubmit}>
```

We'll of course need to add the styling, so let's create `index.css` in the same folder:

```css
.red-table table {
  border: 1px solid red;
}
```

And import it from `View.js`:

```js
import './index.css'
```

## Testing the Feature Flag

Load the page, open the console, and type `assignFeatureFlag('redTable', true)`.
Refresh the page, and the table is red!
Refresh again, and the table is still red!
