# runphase-legal

The published policy pages for the Runphase Atlassian Forge app, served by
Cloudflare Pages so they have stable public URLs.

**This repository is public on purpose, and holds nothing else on purpose.**
Atlassian requires a privacy policy URL and a terms-of-use URL before a Forge
app's distribution status can be set to *Sharing*, and both must be reachable by
anyone installing the app. The application repository stays private: its
implementation plan, security audit and permissions walk name internal hosts,
spaces and issue keys, and none of that belongs behind a public URL.

## Pages

| File | Published URL |
|---|---|
| `privacy-policy.html` | `https://legal.runphase.com/privacy-policy` |
| `terms-of-service.html` | `https://legal.runphase.com/terms-of-service` |
| `index.html` | `https://legal.runphase.com/` |

Cloudflare Pages strips the `.html` and 307s to the extensionless path, so both
forms work. **Record the extensionless ones**, which is what the Atlassian
vendor record uses. The in-page cross-links keep `.html` on purpose, so the
pages stay correct if they are ever served from somewhere that does not rewrite.

Cloudflare rather than GitHub Pages because `runphase.com` already uses
Cloudflare nameservers, so the certificate and the DNS record for
`legal.runphase.com` are handled in the account that owns the zone. Pushes to
`main` redeploy. `.nojekyll` is kept even though nothing reads it now, so
GitHub Pages stays a working fallback.

The custom domain is the part that matters. Atlassian points at
`legal.runphase.com`, so whatever serves these files can change later without
touching the vendor record.

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

Both documents make specific, checkable claims about the app: four scopes, no
egress, no writes to Jira, what redaction reaches, the display-name cache's
limits. They were written from the app's `manifest.yml` and its product rules,
not from a template.

So: **if a scope is added, if a `remotes` or `external` block ever appears in
the manifest, or if the app starts writing to Jira, these pages are wrong and
have to change in the same breath.** A privacy policy that overstates its
restraint is worse than a vague one.

That warning was collected the same day it was written. The pages went up on
2026-10-16 saying "three permission scopes and no others". Hours later the app
needed a fourth, `report:personal-data`, because Atlassian's personal data
declaration turned out to cover account ids held in Forge app storage and not
only data held on a vendor's own servers. The scope and this revision are one
change, which is the only way the rule above means anything.
