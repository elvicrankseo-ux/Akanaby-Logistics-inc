# Akanaby Logistics Inc. — website

A single-page, mobile-first site for a 24/7 towing and roadside assistance company in Lowell, MA.
No build step, no framework, no npm.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole site — markup, CSS, JS and JSON-LD in one file (~110 KB) |
| `privacy.html` | Privacy policy (template — have a lawyer review it) |
| `terms.html` | Terms of service (template — have a lawyer review it) |
| `logo.png` | Your logo, background removed, transparent — used in the header and footer |
| `apple-touch-icon.png` | 180×180 icon for when someone saves the site to a phone home screen |
| `og-image.jpg` | 1200×630 preview card shown when the link is shared on Facebook, WhatsApp, iMessage or X |
| `truck-akanaby-branded.jpg` | Real photo of the Akanaby fleet truck showing the "Akanaby Logistic Inc and Towing" door signage, phone numbers and USDOT #3808852 — used in the "Real trucks. Real local service." section |
| `truck-akanaby-front.jpg` | Real front-view photo of the same truck — used in the About section and the fleet section |
| `robots.txt` | Crawl rules + sitemap pointer |
| `sitemap.xml` | The homepage URL (the legal pages are `noindex`, so they stay out) |
| `404.html` | Branded not-found page with a call-to-action, served automatically by Vercel for unmatched routes |

## Deploy

Drag the folder into Netlify, Vercel or Cloudflare Pages, or upload it to any host's `public_html`. Then:

1. Point the domain at it and force HTTPS.
2. Find and replace `https://www.akanabylogistics.com` across all five files with the real domain. Both `robots.txt` and `sitemap.xml` carry a comment reminding you.
3. Submit `sitemap.xml` in Google Search Console.

## Before it goes live — checklist

**Must do**

- [x] **The placeholder reviews are gone.** The old "sample review" cards have been replaced with an honest trust section (`#reviews`, headed "Your trust matters") that makes no claims about ratings or testimonials. When you have real, verified reviews on your Google Business Profile, replace that section with real review cards — keep names to first name + town, and only add `aggregateRating` to the JSON-LD once you have real ratings to report. Invented review markup violates Google's policy and can get the listing suppressed.
- [x] **Real truck photos are live.** `truck-akanaby-branded.jpg` (the truck with door signage, phone numbers and USDOT #3808852) and `truck-akanaby-front.jpg` power the About section and a new "Real trucks. Real local service." fleet section (`#fleet`). The hero keeps its original hand-built SVG illustration — a real portrait phone photo behind the hero's text scrim washed out the branding and didn't read as a truck, so the fleet section is the primary place these photos do their job. If a proper landscape/wide shot of the truck becomes available later, it would work better as a hero background than the current portrait crop does.
- [ ] **Second phone number on the truck.** The branded photo shows a second number, 432-855-9269, alongside (351) 235-8976 on the door. The site only publishes (351) 235-8976 everywhere (nav, hero, schema, tel links). Decide whether 432-855-9269 should also be listed anywhere before launch, or whether it's a retired/alternate number that shouldn't be public.
- [ ] **Decide how the quote form should send.** Right now, submitting it opens the visitor's email app with every field pre-filled and addressed to `info.akanaby@gmail.com`. That works with zero setup but loses leads on phones with no mail app configured. To capture leads properly, sign up for Formspree / Basin / Web3Forms and replace the `window.location.href='mailto:...'` block near the bottom of `index.html` with a `fetch()` POST to your endpoint. The comment above that block marks the spot.
- [ ] **Check the WhatsApp number.** The floating green button and the footer icon link to `wa.me/13512358976`. If (351) 235-8976 isn't registered on WhatsApp, register it or delete those two links.
- [ ] **Verify the map pin.** The JSON-LD and the `geo.position` / `ICBM` meta tags use approximate coordinates for 50 Tanner Street (`42.6301, -71.3078`). Right-click the exact spot in Google Maps, copy the real lat/long and paste them in.
- [ ] **Confirm the payment answer in the FAQ.** It currently tells people to confirm payment methods on the call, because the accepted methods weren't supplied. Once you list them (cash, card, insurance billing, motor clubs), update the FAQ answer *and* the matching answer inside the JSON-LD `FAQPage` block so they stay identical.
- [ ] **Upload the three image files** (`logo.png`, `apple-touch-icon.png`, `og-image.jpg`) to the same folder as `index.html`. If they're missing, the header shows a broken-image icon and shared links lose their preview card.
- [ ] **Add the real social links.** The Facebook, Instagram and Google icons in the footer point to `#`. Add the real URLs, and add them to `sameAs` in the JSON-LD so Google connects the profiles to the Business Profile.

**Worth doing**

- [ ] Test the share card. After the domain is live, paste the URL into Facebook's Sharing Debugger and X's Card Validator so they cache the new `og-image.jpg`. Both cache aggressively — if you change the image later, you have to force a re-scrape there.
- [ ] If you get a wide/landscape shot of a truck (not a portrait phone photo), it could replace the hero's SVG illustration — swap the `<svg>` inside `.hero-art` for an `<img>` and update the `.hero-art img` rule in the CSS. A portrait photo was tried there first and reverted: behind the hero's text-legibility scrim, the branding washed out and it didn't read as a truck. A landscape shot with the cab and signage across the frame would crop much better.
- [ ] Get a few more truck/crew photos over time and rotate them into the `#fleet` section so it doesn't always show the same two shots.
- [ ] Install Google Analytics 4 or Plausible. Every call button carries a `data-cta` attribute (`hero-call`, `mobile-bar`, `exit-modal`, `float-call`, …) and there's a commented-out click handler at the end of the script ready to fire an event — so you can see exactly which button earns the phone calls.
- [ ] Claim and complete the Google Business Profile with the identical name, address and phone (NAP) used here. Local ranking depends on that matching exactly.

## How the conversion pieces work

- **Sticky header** with a permanent orange Call button, plus a phone number that disappears on small screens to leave room.
- **Mobile bottom bar** (under 640 px) — "Call now" + "Free quote", always visible.
- **Floating WhatsApp bubble** on every screen size; a floating call button appears on tablet/desktop where the bottom bar is hidden.
- **A call button closes every section**, so the phone is never more than one thumb-reach away.
- **Exit-intent modal** fires once per page view, on desktop only, and only after the visitor has been on the page 8 seconds — so it never interrupts someone who is mid-emergency.

## Accessibility & performance notes

- No JS libraries, no web fonts beyond Poppins + Inter. Both maps are `loading="lazy"` iframes, so nothing blocks first paint.
- Decorative artwork (hero, service icons) is inline SVG with explicit `viewBox` — zero layout shift. The two real truck photos declare `width`/`height` for the same reason and are `loading="lazy"`, since both sit below the fold.
- Keyboard focus is visible everywhere, the FAQ and service cards use real `aria-expanded` buttons, and `prefers-reduced-motion` switches off the light-bar sweep, the reveals and the pulsing call ring.
- Colour contrast on the orange buttons and navy sections was chosen to clear WCAG AA for body text.

## Content honesty

Everything on the page comes from the supplied business information. Nothing was invented about certifications, response-time guarantees, fleet size, years of awards or customer counts. Where a fact wasn't supplied — exact arrival times, prices, accepted payment methods — the copy says "call and we'll tell you" instead of making a number up. Keep it that way: on a Google Business Profile, a claim you can't back up is a liability.

The two truck photos are genuine photos of an Akanaby vehicle, not stock or AI-generated images. The USDOT number in the fleet section is transcribed directly from the door signage in the photo — it has not been separately verified against FMCSA records, so double-check it before treating it as authoritative.
