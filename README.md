# runphase-legal

The published policy pages for the Runphase Atlassian Forge app, hosted on
GitHub Pages so they have stable public URLs.

**This repository is public on purpose, and holds nothing else on purpose.**
Atlassian requires a privacy policy URL and a terms-of-use URL before a Forge
app's distribution status can be set to *Sharing*, and both must be reachable by
anyone installing the app. The application repository stays private: its
implementation plan, security audit and permissions walk name internal hosts,
spaces and issue keys, and none of that belongs behind a public URL.

## Pages

| File | URL once Pages is enabled |
|---|---|
| `privacy-policy.html` | `https://<user>.github.io/runphase-legal/privacy-policy.html` |
| `terms-of-service.html` | `https://<user>.github.io/runphase-legal/terms-of-service.html` |
| `index.html` | `https://<user>.github.io/runphase-legal/` |

`.nojekyll` is present deliberately. These are plain static files with no build
step, so the URLs cannot break because a Jekyll build failed — which matters,
because they are recorded in a vendor record that users see at install time.

## Before publishing

Every placeholder renders as a **loud highlighted box** in the page itself, so
an unfilled one cannot be shipped by accident. Search for `class="fill"` and
replace each `<span>…</span>` with the value:

- Effective date — the day distribution is set to Sharing
- Vendor name, as it should appear publicly
- Support email address
- Governing jurisdiction (terms only)

## Keeping them accurate

Both documents make specific, checkable claims about the app — three scopes, no
egress, no writes to Jira, what redaction reaches, the display-name cache's
limits. They were written from the app's `manifest.yml` and product rules, not
from a template.

So: **if a scope is added, if a `remotes` or `external` block ever appears in
the manifest, or if the app starts writing to Jira, these pages are wrong and
have to change in the same breath.** A privacy policy that overstates its
restraint is worse than a vague one.
