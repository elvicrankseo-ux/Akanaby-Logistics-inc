# Akanaby Logistics Inc. — website

A single-page, mobile-first site for a 24/7 towing and roadside assistance company in Lowell, MA.
No build step, no framework, no npm, no image files. Upload the folder and it runs.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole site — markup, CSS, JS and JSON-LD in one file (~110 KB) |
| `privacy.html` | Privacy policy (template — have a lawyer review it) |
| `terms.html` | Terms of service (template — have a lawyer review it) |
| `logo.png` | Your logo, background removed, transparent — used in the header and footer |
| `apple-touch-icon.png` | 180×180 icon for when someone saves the site to a phone home screen |
| `og-image.jpg` | 1200×630 preview card shown when the link is shared on Facebook, WhatsApp, iMessage or X |
| `robots.txt` | Crawl rules + sitemap pointer |
| `sitemap.xml` | The homepage URL (the legal pages are `noindex`, so they stay out) |

## Deploy

Drag the folder into Netlify, Vercel or Cloudflare Pages, or upload it to any host's `public_html`. Then:

1. Point the domain at it and force HTTPS.
2. Find and replace `https://www.akanabylogistics.com` across all five files with the real domain. Both `robots.txt` and `sitemap.xml` carry a comment reminding you.
3. Submit `sitemap.xml` in Google Search Console.

## Before it goes live — checklist

**Must do**

- [ ] **Replace the five sample reviews.** They are labelled as samples on the page on purpose. Paste in real Google reviews, keep the reviewer's first name and town, then delete the amber "sample content" banner and the `Sample` chips. Do not add `aggregateRating` to the structured data until you have real ratings — invented review markup violates Google's policy and can get the listing suppressed.
- [ ] **Decide how the quote form should send.** Right now, submitting it opens the visitor's email app with every field pre-filled and addressed to `info.akanaby@gmail.com`. That works with zero setup but loses leads on phones with no mail app configured. To capture leads properly, sign up for Formspree / Basin / Web3Forms and replace the `window.location.href='mailto:...'` block near the bottom of `index.html` with a `fetch()` POST to your endpoint. The comment above that block marks the spot.
- [ ] **Check the WhatsApp number.** The floating green button and the footer icon link to `wa.me/13512358976`. If (351) 235-8976 isn't registered on WhatsApp, register it or delete those two links.
- [ ] **Verify the map pin.** The JSON-LD and the `geo.position` / `ICBM` meta tags use approximate coordinates for 50 Tanner Street (`42.6301, -71.3078`). Right-click the exact spot in Google Maps, copy the real lat/long and paste them in.
- [ ] **Confirm the payment answer in the FAQ.** It currently tells people to confirm payment methods on the call, because the accepted methods weren't supplied. Once you list them (cash, card, insurance billing, motor clubs), update the FAQ answer *and* the matching answer inside the JSON-LD `FAQPage` block so they stay identical.
- [ ] **Upload the three image files** (`logo.png`, `apple-touch-icon.png`, `og-image.jpg`) to the same folder as `index.html`. If they're missing, the header shows a broken-image icon and shared links lose their preview card.
- [ ] **Add the real social links.** The Facebook, Instagram and Google icons in the footer point to `#`. Add the real URLs, and add them to `sameAs` in the JSON-LD so Google connects the profiles to the Business Profile.

**Worth doing**

- [ ] Test the share card. After the domain is live, paste the URL into Facebook's Sharing Debugger and X's Card Validator so they cache the new `og-image.jpg`. Both cache aggressively — if you change the image later, you have to force a re-scrape there.
- [ ] Add photos of the actual trucks and crew. The hero illustration and the "about" illustration are hand-built SVG (they load instantly and never blur), but real photos of your own equipment build more trust than any drawing. Swap them by replacing the `<svg>` inside `.hero-art` with `<img src="hero.jpg" alt="Akanaby Logistics flatbed tow truck loading a car at night in Lowell, MA" width="1440" height="820">` and keeping the same alt-text pattern.
- [ ] Install Google Analytics 4 or Plausible. Every call button carries a `data-cta` attribute (`hero-call`, `mobile-bar`, `exit-modal`, `float-call`, …) and there's a commented-out click handler at the end of the script ready to fire an event — so you can see exactly which button earns the phone calls.
- [ ] Claim and complete the Google Business Profile with the identical name, address and phone (NAP) used here. Local ranking depends on that matching exactly.

## How the conversion pieces work

- **Sticky header** with a permanent orange Call button, plus a phone number that disappears on small screens to leave room.
- **Mobile bottom bar** (under 640 px) — "Call now" + "Free quote", always visible.
- **Floating WhatsApp bubble** on every screen size; a floating call button appears on tablet/desktop where the bottom bar is hidden.
- **A call button closes every section**, so the phone is never more than one thumb-reach away.
- **Exit-intent modal** fires once per page view, on desktop only, and only after the visitor has been on the page 8 seconds — so it never interrupts someone who is mid-emergency.

## Accessibility & performance notes

- No external images, no JS libraries, no web fonts beyond Poppins + Inter. Both maps are `loading="lazy"` iframes, so nothing blocks first paint.
- All artwork is inline SVG with explicit `viewBox` — zero layout shift (good CLS).
- Keyboard focus is visible everywhere, the FAQ and service cards use real `aria-expanded` buttons, and `prefers-reduced-motion` switches off the light-bar sweep, the reveals and the pulsing call ring.
- Colour contrast on the orange buttons and navy sections was chosen to clear WCAG AA for body text.

## Content honesty

Everything on the page comes from the supplied business information. Nothing was invented about certifications, response-time guarantees, fleet size, years of awards or customer counts. Where a fact wasn't supplied — exact arrival times, prices, accepted payment methods — the copy says "call and we'll tell you" instead of making a number up. Keep it that way: on a Google Business Profile, a claim you can't back up is a liability.
