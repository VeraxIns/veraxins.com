# veraxins.com

Static site for Verax Insurance Consulting, LLC, hosted on GitHub Pages with the custom
domain `veraxins.com` (the `CNAME` file). Three pages: home, privacy policy, terms.

The privacy and terms pages exist first for **carrier compliance** -- the Twilio A2P 10DLC
campaign for +1 727-353-5900 was rejected (errors 30882/30908) for lacking a public
privacy-policy URL and terms URL. Their SMS-program language follows the CTIA / Campaign
Registry requirements, including the exact "No mobile information will be shared with
third parties or affiliates for marketing or promotional purposes" sentence carriers look
for. Do not paraphrase that sentence.

## Deploy

Push to the `main` branch of the GitHub repo; Pages serves it. Custom domain is set in the
repo's Pages settings and enforced-HTTPS once the certificate issues.

## GoDaddy DNS records for GitHub Pages

| Type  | Name | Value                     |
|-------|------|---------------------------|
| A     | @    | 185.199.108.153           |
| A     | @    | 185.199.109.153           |
| A     | @    | 185.199.110.153           |
| A     | @    | 185.199.111.153           |
| CNAME | www  | `<github-user>.github.io` |

The GoDaddy "parked" A record on `@` was already removed (2026-09-07). An existing
`CNAME www` record must be **deleted or edited** to the value above -- GoDaddy will not
allow a second `www`. Mail (MX) records are untouched -- tkane@veraxins.com keeps working.

GoDaddy prompts "Verify your identity" once per editing session; do all five in one go.
