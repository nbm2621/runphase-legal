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
| `privacy-policy.html` | `https://nbm2621.github.io/runphase-legal/privacy-policy.html` |
| `terms-of-service.html` | `https://nbm2621.github.io/runphase-legal/terms-of-service.html` |
| `index.html` | `https://nbm2621.github.io/runphase-legal/` |

`.nojekyll` is present deliberately. These are plain static files with no build
step, so the URLs cannot break because a Jekyll build failed — which matters,
because they are recorded in a vendor record that users see at install time.

## The published values

| | |
|---|---|
| Vendor | Skram Systems, LLC |
| Public name | Runphase |
| Contact | support@runphase.com |
| Effective | 2026-10-16 |
| Governing law | Commonwealth of Virginia, United States |

The contact address is not decorative: the privacy policy names it as the
channel for a data deletion request, so it has to keep receiving mail for as
long as the app is listed.

The `.fill` rule in `style.css` is kept although nothing uses it now. It renders
a placeholder as a **loud highlighted box**, which is what made it impossible to
publish an unfilled one by accident the first time round; the next time one of
these values has to be decided rather than typed, wrap it in
`<span class="fill">` and the same guard applies.

## Keeping them accurate

Both documents make specific, checkable claims about the app — three scopes, no
egress, no writes to Jira, what redaction reaches, the display-name cache's
limits. They were written from the app's `manifest.yml` and product rules, not
from a template.

So: **if a scope is added, if a `remotes` or `external` block ever appears in
the manifest, or if the app starts writing to Jira, these pages are wrong and
have to change in the same breath.** A privacy policy that overstates its
restraint is worse than a vague one.
