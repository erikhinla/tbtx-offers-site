# HANDOFF: Offers site (/offers/)
A static nested, no-scroll offers page: start > Keystones path (#keystones, #together, #price) or Work with Erik (#erik, #mini, #fact). Deep links work.

## Where it runs
- VPS path: /srv/www/tbtx-offers/, served by nginx as an alias at https://transformby10x.ai/offers/.
- Files: index.html, nks.css (current), k2-tbtx-wordmark-ink.png / -white.png, context-keystones-one-sheet.pdf. Older oks.css, ks.css and style.css aren't linked any more.
- The live count comes from /proof/screen/api/keystones/offer (PROOF app).

## Deploy
1. `tar czf /root/backups/tbtx-offers-pre-X-<ts>.tgz -C /srv/www tbtx-offers`
2. Copy the files into /srv/www/tbtx-offers/. No build step.
3. Check every screen at 390x844 and 1440x900: no page scroll, no inner scroll, CTA in the same spot.

## Env vars
None.
## Infrastructure
- VPS: root@159.195.251.226 (netcup). Reached over SSH with a key from Erik's Mac.
- Backups on the VPS: /root/backups/ (tgz per deploy) plus docker image tags `proof-app:pre-*`.

## Offers and pricing
- Context Keystones: intro $49 for the first 50 buyers, then $349.
  - $349 price price_1UTtb7CMxQwcbhDnQIvS6O51, payment link plink_1UTtbECMxQwcbhDnHyV8ZqQv.
  - Other ids in the code: price_1UThXWCMxQwcbhDnF4MLaeOL, price_1UTtQbCMxQwcbhDnwRozaDDm, plink_1UThXd…, plink_1UThXf…, plink_1UThXh…, plink_1UThXj…, plink_1UTtQm… (see src/lib/keystones-server.ts).
  - At 50 sales, closeIntroIfCapped() deactivates the intro link via STRIPE_LINK_KEY, or emails Erik if that key isn't set.
- Remote mini FACT: $1,750, remote, call first.
- Friction Audit FACT: $4,500 plus travel ($2,250 plus travel up front, $1,125 on arrival, $1,125 on completion).
- Booking link for both calls: https://calendar.app.google/4mgKAmouyucz7jk79

## Open items (2026-10-23)
- Test promo codes KSLIVETEST1023, KSLIVE2 and KSDIAG10 are still active; deactivate them in the Stripe dashboard.
- STRIPE_LINK_KEY isn't set (cap fallback is an email).
- Coupon fAfUeZeF can only be deleted; left as is.
- Resend templates unpublished.
- The long /about page is still reachable via "The longer story".
- The home page "What's after PROOF" list uses small "TBTX" text tags per offer (a brand label, not the logo). Erik to decide.
## Erik's key rules (apply to every page, email and visual)
- Copy: contractions, plain speech. No em dashes, no "free", no "desk", no tool names, no rhetorical questions, no you/your in headings. Say "Digital Friction", never "Fog". No URLs in visuals.
- Logo: always the real file `k2-tbtx-wordmark-white.png` (lowercase MuseoModerno, tight kerning on purpose). Never retype or re-kern it. On light backgrounds use `k2-tbtx-wordmark-ink.png`, which is the same PNG with its pixels filled #1F1F1F.
- Pages: nested, click-driven, no page scroll. Each screen fits 390x844 and 1440x900. One big headline per screen; price and CTA always in the same spot; nothing scrolls inside a box.
- Value before price, always.
- CTA labels match their destinations: Keystones "Start with PROOF", Remote mini FACT "Book a mini FACT call", Friction Audit FACT "Book a FACT call".
- Brand colors are accents only: tbtx #d01e98, bbai #b37157, bbm #69f2c4, ink #1F1F1F, bg #E9E5DE.
- Source: /root/tbtx-next-ecosystem/hermes/COPY-RULES.md, COPY-STYLE-GUIDE.md, DESIGN-GUIDE.md on the VPS.
- Never commit or print secrets.
