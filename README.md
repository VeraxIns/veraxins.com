# veraxins.com

Static site for Verax Insurance Consulting, LLC, hosted on GitHub Pages with the custom
domain `veraxins.com` (the `CNAME` file). Four pages: home, privacy policy, terms, SMS consent.

The privacy and terms pages exist first for **carrier compliance** -- the Twilio A2P 10DLC
campaign for +1 727-353-5900 was rejected (errors 30882/30908) for lacking a public
privacy-policy URL and terms URL. Their SMS-program language follows the CTIA / Campaign
Registry requirements, including the exact "No mobile information will be shared with
third parties or affiliates for marketing or promotional purposes" sentence carriers look
for. Do not paraphrase that sentence.

## sms-consent.html

Added 2026-09-09 after the A2P campaign was rejected a **third** time with error 30896 on
`MESSAGE_FLOW` -- "rejected because of provided Opt-in information". All three earlier
`message_flow` texts only *asserted* consent ("recipients consented directly", "the owner
entered his own number"). Reviewers read an assertion they cannot check as "no opt-in
mechanism exists". Twilio's own guidance for 30896/30917 is that when opt-in is not a
public web form, the flow has to be **evidenced at a publicly reachable URL**.

So this page is the evidence: the complete two-person recipient roster, the four-step
manual enrollment procedure written so a reviewer can follow it, and the **verbatim
consent statement** each recipient agrees to. The page IS the artifact rather than a
description of one.

Deliberately **no sign-up form** -- there is no public enrollment, and inventing a form
would be a worse misrepresentation than what was already rejected.

GitHub Pages resolves extensionless paths, so `veraxins.com/sms-consent` returns 200
directly with no redirect. That is the URL cited in `message_flow`; keep the filename.

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
