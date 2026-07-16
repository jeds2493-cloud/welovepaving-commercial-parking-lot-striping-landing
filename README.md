# We Love Paving — Commercial Parking Lot Striping (SEM landing)

Standalone, static SEM landing page for We Love Paving's commercial parking lot
striping service (Northern California). Deployed on its own so the team can
review it without touching the main site or the other landing prototypes.

Built on the **same design system as the ADA accessibility landing**
(`welovepaving-ada-landing`) — utility bar, sticky header, hero, before/after
wipe, service cards, process, testimonial, FAQ, legal footer and modals are the
shared components. Only the striping-specific sections, copy and accent colours
differ. The striping palette (Construction Yellow / charcoal / white, ADA blue
reserved for accessible references) is already the design system's token set.

## Structure

```
index.html            the landing (10 sections)
striping-landing.css   shared design system + a striping additions/overrides block at the end
striping-landing.js    tracking, sticky header, marquee, before/after, lightbox, legal modals, gallery
legal/                 flattened copies of the legal pages, opened in modals
images/  video/        PLACEHOLDER assets reused from the ADA landing (see below)
tools/                 build-time only (excluded from deploy via .vercelignore)
```

## Sections

1. Utility trust bar + conversion header
2. Hero + short estimate form
3. Immediate trust strip
4. Before-and-after transformation
5. Striping and marking services (5 cards)
6. Property benefits (4 cards)
7. Why WLP + written protection (Panda Pledge microblock)
8. Four-step process
9. Project proof + property types + testimonial
10. FAQ + final compact form + legal footer

## Running locally

Any static server from the repo root (`npx serve .`). The dev config runs it on
port 3016.

Note: the two lead forms are cross-origin iframes from `quote.welovepaving.com`,
whose CSP only allows `welovepaving` domains and `*.vercel.app`. On `localhost`
they render blank — expected, not a bug. They render once deployed to Vercel or
to a `welovepaving.com/lp/` path.

## Forms — read before wiring

Both forms are the **WLP form library embed** (`loader.js`), the same mechanism
every `welovepaving.com/lp/` landing uses. The loader owns validation,
attribution (utm/gclid/first-touch) and the thank-you redirect; the `sem_*`
form_source fires the Google Ads conversion.

The brief specified extra fields (Property ZIP code, a "What does your lot need?"
select, a Company field, plus a success state and optional photo upload). **The
cross-origin embed can't add those** — they would need a striping-specific
variant built on WLP's side (`quote.welovepaving.com`). Current variants used:
`sem3` (hero: Name/Email/Phone) and `full` (final: 5 fields + step 2). The
success state and optional upload are handled by the WLP server (it redirects on
submit), so there is no inline success screen in this page.

## Placeholder inventory (must be replaced before launch)

- **Hero / gallery / before-after / project photos** — reused ADA parking-lot
  photos as stand-ins. Swap with striping-specific photography (a same-frame
  before/after pair, a project gallery, a striping hero shot).
- **Testimonial** — the video, quote and attribution are placeholders. Replace
  with a verified, striping-specific testimonial (do not use a generic paving
  quote).
- **Project case specs (S9)** — every field is marked `[placeholder]`.
- **Final `/lp/` slug** — canonical is `/lp/commercial-parking-lot-striping/`
  (the site already has `/lp/parking-lot-striping/`); the team confirms the slug.
- **Striping form variant** — see Forms above.

Confirmed real WLP data reused from the ADA landing (not placeholders): phone
`(888) 273-0077`, CSLB `#1049649`, CA `571708`.

## Guardrails honoured (from the brief)

- Parking lot striping is the primary service; asphalt and concrete are framed
  as complementary, never competing.
- **No 15-year warranty as a striping standard.** The hero seal was repurposed to
  the free-estimate offer; S7 and the FAQ only say striping includes the
  workmanship/application assurance in the approved terms, and qualifying
  asphalt/concrete work *may* be eligible for additional Panda Pledge protection.
- No ADA-compliance guarantee, no inspection/lawsuit framing.
- ADA blue is reserved for accessible references (the accessible service card);
  eyebrows, service tags and benefit icons use the yellow/charcoal signage palette.

## Notable decisions

- **`noindex`**: paid-traffic landing; kept out of search so it can't cannibalize
  the main site. `canonical` points to the eventual production home.
- **Mobile sticky bar** carries both actions `[Call Now] [Free Estimate]` per the
  brief; the header CTA is hidden below the desktop breakpoint to avoid
  duplicating the estimate action, and the phone shows in the header instead.
- **Legal modals**: the live legal pages are GenerateBlocks builds whose text
  sits in collapsed accordions, so they can't be fetched and injected as-is.
  `tools/extract-legal.js` flattens them into `legal/`; see `tools/README.md`.
  The Accessibility Statement has no local copy yet — its link opens the live page.

Destined for WordPress (GeneratePress/GenerateBlocks); this repo is the review
prototype, not the production home.
