# Rocher's Waffle Chips — Landing Page

**One file: [`index.html`](index.html).** No React, no npm, no build step, no
dependencies. Double-click it to open, or upload it to any host.

```
Landing_page/
├── index.html      ← the entire page (85 KB)
├── images/         ← drop the product photos here
└── README.md
```

---

## 🚨 Two things before this goes live

### 1. The Razorpay link

Open `index.html`, scroll to the `<script>` near the bottom. **Line 1 of it:**

```js
var RAZORPAY_LINK = "https://rzp.io/l/REPLACE_ME";
```

Paste the real Payment Link there. All five Buy Now buttons (header, hero,
offer band, final CTA, sticky bar) read that one value. Nothing else to change.

**Right below it, set the offer deadline:**

```js
var OFFER_ENDS = "2026-08-31T23:59:59+05:30";   // +05:30 = IST
```

That one date drives every timer on the page — the announcement bar, the hero
urgency chip, the big four-box countdown in the offer band, the final CTA line
and the sticky bar. It's a **fixed** deadline rather than a per-visitor 24-hour
timer that resets on reload: a countdown to a deadline that doesn't exist is a
misleading trade practice under the Consumer Protection (E-Commerce) Rules 2020,
and a real date costs nothing. When it passes, every timer hides itself
automatically instead of counting negative — just move the date forward to run
the offer again.

They open Razorpay in a **new tab** on purpose — if the customer bails on the
payment page, the landing page and the ad click that paid for it are still
sitting there behind them.

### 2. The photos

Save the two pack photos the client sent into `images/`:

| Save as                  | Which photo         |
| ------------------------ | ------------------- |
| `images/pack-front.jpg`  | Front of the pack   |
| `images/pack-back.jpg`   | Back of the pack    |

Every other image slot shows a labelled panel describing the shot that belongs
in it — see [`images/README.md`](images/README.md) for the full list. Drop a
file in with the right name and the panel disappears. No code change.

---

## Editing the page

It's plain HTML. Find the text, type over it. Every section has a big comment
banner above it (`ANNOUNCEMENT BAR`, `HERO`, `USP GRID`, `THE PACK`, …).

The repeating lists — gallery, reviews, comparison rows, FAQs — are short arrays
at the bottom of the `<script>`, one line per item, so they're easy to add to or
delete from.

| To change                | Where                                                    |
| ------------------------ | -------------------------------------------------------- |
| Razorpay link            | `RAZORPAY_LINK`, top of the `<script>`                    |
| Price (all 5 places)     | `PRICE`, right underneath it                              |
| Offer deadline / timers  | `OFFER_ENDS`, right underneath that                       |
| Offer bar text           | `<div class="announce">`, very top of the `<body>`        |
| Headline / subheadline   | the `HERO` section                                        |
| Brand colours            | the `:root { }` block at the top of the `<style>`         |
| FAQs                     | the `FAQS` array in the `<script>`                        |
| Reviews                  | the reviews array in the `<script>`                       |
| Comparison table         | the `CMP` array in the `<script>`                         |

---

## What's real and what isn't

Every fact on this page comes from the printed pack. **Nothing was invented.**

**Confirmed and safe to ship** — taken off the pack front and back:

> Whole Grain Jowar Flour · Zero Maida · Gluten Free · Not Fried, Just Waffled ·
> Real dark chocolate drizzle · 40 g net weight · 100% vegetarian ·
> full ingredients list · allergens (Contains Milk & Soy; facility also
> processes Wheat Flour & Tree Nuts) · FSSAI Lic. 22722758000068 ·
> rochersbakeshop@gmail.com · +91 88581 75027 · ₹249 for 2 packs

**Everything else was removed, not guessed.** There is no placeholder text left
on the page. Where a fact wasn't known, the element is gone — with a `▸` comment
where it used to be saying exactly what's needed to bring it back.

| # | Removed | Bring it back by |
| - | ------- | ---------------- |
| 1 | Nutrition table | Sending real per-100g lab values. **Never guess these** — it's an FSSAI labelling problem and a Meta ad-review problem, in that order. |
| 2 | Strike-through MRP + "Save %" badge | Confirming the MRP. The markup is commented out in the `HERO`, ready to uncomment. |
| 3 | Customer reviews section | Having real, verified reviews. See warning below. |
| 4 | Lifestyle gallery | Shooting the six lifestyle photos. |
| 5 | Shelf-life period + storage line | Confirming a standard shelf life. The pack states a per-batch USE BY date only, so the page says "check the stamp on your pack" instead of claiming a period. |
| 6 | FAQ: shipping time, COD, cancellations/returns | Client answering them. |
| 7 | "Limited first batch" scarcity line | Confirming it's actually a limited batch. |

### One thing worth raising with the client

**⚠️ "Gluten Free" + the allergen line.** The pack front says GLUTEN FREE while
the back says the facility also processes Wheat Flour. Both are reproduced on
the page exactly as printed, but that combination is worth a second look before
running ads on it.

---

## How the break-apart scroll works

The brief's critical feature — *"as the user scrolls, the large waffle gradually
breaks into individual pieces"* — with **no video, no canvas, no 3D**.

One piece of artwork is drawn six times, each copy clipped to a different shard
region. The regions are cut by *shared* crack polylines, so at rest the six
copies stack into one seamless waffle and the broken edges always match. Scroll
slides each copy outward along its own vector, with a cheap per-frame spring so
it reads as a drift rather than a value snapped to the scrollbar.

Only `transform` and `opacity` animate, so scrolling never triggers layout or
paint. Under `prefers-reduced-motion` it renders one still waffle and never
subscribes to scroll at all.

**To use a real photo instead of the drawn waffle:** save a square,
background-removed PNG of the chips as `images/hero-chips.png`. The shards pick
it up automatically.

---

## Analytics

Every Shop Now click pushes a `purchase_intent` event into `dataLayer`, `gtag`
and `fbq` — with which button was clicked (`header`, `hero`, `offer`, `final`,
`sticky-bar`) and the price. It no-ops safely if no tracker is installed.

**To wire it up:** paste the GA4 and Meta Pixel base snippets into `<head>`,
where the TODO comment is. Nothing else.

⚠️ This is purchase *intent*, not a sale — payment completes on Razorpay's
hosted page, which this site never sees. Track real conversions with a Razorpay
webhook, and don't report these clicks as purchases in ad reporting.

---

## Hosting

Upload `index.html` and the `images/` folder to any static host — Netlify,
Vercel, Cloudflare Pages, GitHub Pages, Hostinger, or plain cPanel. There is no
server, no database and no environment config.

Tested at 390px, 1440px and 1920px: no horizontal overflow (`scrollWidth ==
clientWidth` at every width), no console errors, reduced-motion honoured,
keyboard-operable menu and FAQ accordion. Content column is capped at 1440px.
