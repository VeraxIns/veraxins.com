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

So this page is the evidence: the enrollment procedure written so a reviewer can follow
it, the **verbatim consent statement** each recipient agrees to, and a description of the
consent record kept for each person. The page IS the artifact rather than a description of
one.

Deliberately **no sign-up form** -- there is no public enrollment, and inventing a form
would be a worse misrepresentation than what was already rejected.

GitHub Pages resolves extensionless paths, so `veraxins.com/sms-consent` returns 200
directly with no redirect. That is the URL cited in `message_flow`; keep the filename.

### Roles, not names -- rewritten 2026-09-09

The first version of this page published a two-row recipient table and the sentence
"there are two recipients, and there has never been a third." **Both were false.** An
elderly family member was already receiving automated calls from the same number, and the
intended roster is five people. A carrier reviewer who checked would have found a
disclosure that did not match the system, which is the same class of defect that had
already caused five rejections.

The rewrite describes the roster **by role** and publishes the mechanism instead of the
people. That is a deliberate choice, not a hedge: naming a private individual and her
phone number on a public page in order to prove she consented is a worse outcome than any
carrier form is worth. What is published is checkable -- the categories, the five-step
procedure, the consent statement, and the fields of the consent record. What is withheld is
only the identities.

If a reviewer asks for the records themselves, they are retained and can be produced. Do
not resolve that request by publishing them here.

### The sample messages on this page are not decoration

Round 4 of the campaign was rejected with 30886 (USE_CASE_DESCRIPTION) + 30893
(SAMPLE_MESSAGE_2): the description promised "no marketing" while sample 2 was a
back-in-stock ticket announcement. This page carried **the same two samples**, and it is
the URL a reviewer follows out of `message_flow` and out of the toll-free submission's
`OptInImageUrls`. Fixing the campaign alone would have left the finding sitting on the
page it points at.

So the samples here are kept identical to `MESSAGE_SAMPLES` in `scripts/twilio_a2p.py`,
which are **built** from `lib/alerts.py` and the real format strings in `jobs/sweep.py`,
`jobs/position_check.py` and `jobs/mom_reminders.py` rather than retyped. **If you change
one, change the other.** Same for the program description: page, campaign `Description` and
toll-free `UseCaseSummary` all have to describe one program in the same words, because
"the submission disagrees with itself" is the finding that has now cost five rounds.

The page lists all three numbers -- the 10DLC sender, the toll-free, and the voice line
that also answers inbound STOP and HELP -- since a reviewer of either registration should
find their own number here.

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
