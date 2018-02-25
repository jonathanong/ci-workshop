
# Dark Launching

The purpose of continuous integration is to commit quickly and often,
allowing you to pinpoint regressions to small commits.
Without continuously delivering, you're going to end up
with gigantic diffs and painful merge conflicts.

But what if you do you have large changes that need to be made to your code base?
You can't merge that large branch without also enabling that feature, can you?
Of course you can! You push it to production, but turn that feature off.

Benefits:

- Push smaller commits to production more often.
- Fewer merge conflicts as there should be smaller commits.
- QA can test features in production with real data.

Risks:

- Your new code will be in production, and if not architected correctly, could
  introduce regressions with your old code.

Costs:

- Let me know if you know of any.

## Setting up Feature Flags

Setting up a feature flag is easy. Create a feature flag file:

```json
{
  "feature": false
}
```

Serve it in your application to expose it to the client:

```pug
script featureFlags = !{JSON.stringify(featureFlags)}
```

## Enabling Feature Flags
