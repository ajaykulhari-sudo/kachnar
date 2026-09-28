# Kachnar House — website

The website for **Kachnar House**, 2/195 Vikas Nagar, Lucknow, Uttar Pradesh 226022.

Static HTML/CSS/JS. No build step, no framework, no dependencies. Open
`index.html` in a browser and it runs.

Built from the [`ramdev`](https://github.com/ajaykulhari-sudo/ramdev) site
(DigiStay template-1, the boutique/heritage design), re-themed and rewritten for
this property.

## Structure

```
├── index.html          Home — hero, booking bar, rooms, cafe, essentials, location
├── rooms.html          Classic, Deluxe and Super Deluxe, with specs and amenities
├── facilities.html     "The House" — cafe, courtyard, functions, safety + house rules
├── gallery.html        Photographs, grouped by area and room
├── contact.html        Enquiry form, phone, email, address, map
├── styles.css          Design system + all page styles
├── script.js           Nav, booking-engine deep link, enquiry form, Book Now button
└── images/             45 photographs of the property
```

## Booking

The site does not hold rooms, quote totals, or take payment. It hands the
guest's dates to the **DigiStay booking engine**, which owns availability,
rates, taxes and checkout.

Deep-link contract (verified live 2026-09-28):

```
https://digibooking.in/hotel/<propertyId>?checkIn=DD-MM-YYYY&checkOut=DD-MM-YYYY&rooms=<adults>-<children>
https://digibooking.in/H548    short code, same property, no dates
```

| Thing | Value |
|---|---|
| Property ID | `c835b49d-3b91-4de3-a778-0101ce60f817` |
| Short code | `H548` |
| Date format | `DD-MM-YYYY` (the `<input type="date">` value is converted in `toEngineDate`) |
| `rooms` param | `<adults>-<children>` — **not** a room count |

All of this lives in the `BOOKING` object at the top of `script.js`. The date
form on the homepage builds a full deep link; the `Book Now` buttons on every
page carry `data-book` and are pointed at the short code at runtime.

There is **no WhatsApp button** on this site, by request. The only floating
action is `Book Now`.

## Content provenance

Every fact on this site comes from the property's own booking-engine record
(`H548`): the description, address, phone and email, the three room types with
their occupancy, room counts and amenities, the 23 property amenities, the
cancellation / child / smoking / payment policies, check-in and check-out
times, and the nearby-landmark distances.

- **Cafe Andheri West** is named from the signage in the property's own
  photographs (the station board, the porch sign listing meetings and
  get-togethers).
- **Second phone number** (+91 75250 23889) is taken from the property's logo
  file, which lists both numbers.
- **No rates on the page.** Prices on the engine change by date, so the site
  links to live rates instead of printing a number that goes stale.
- **No room sizes.** The record doesn't carry them.
- **No testimonials.** The record contains none; the Reviews section links to
  Google instead of inventing quotes.
- **No GSTIN.** Add the real one to the footer once it's confirmed.

## Images

45 photographs, chosen from the ~70 unique images on the property record and
committed locally — no CDN dependency. Screenshots with carousel UI baked in,
promo flyers and exact duplicates were dropped. All were resized (max 2400px
for the hero, 1920px elsewhere) and recompressed: ~29 MB → ~7 MB.

Room-type photos (`classic-*`, `deluxe-*`, `super-deluxe-*`) are the ones the
record files against that room type. The wood-panelled `guest-room-*` shots are
filed under generic "Rooms", so they're captioned as guest rooms, not tied to a
type.

To replace a photo, keep the filename and drop the new file in `images/`. No
HTML change needed.

## Local preview

```bash
python3 -m http.server 4508
# → http://localhost:4508
```

## Deploying

Pure static — any host works, no build step.

```bash
# Netlify
netlify deploy --prod --dir=.

# Vercel
vercel --prod
```

Or upload the folder to S3 + CloudFront, Cloudflare Pages, or GitHub Pages.

## Design

Inherited from template-1: Fraunces (headings) + Inter (body), 1280px
container, breakpoints at 980px and 580px.

The palette is drawn from the property — the kachnar leaf in the logo and the
palms at the gate (`--accent: #2E5A43`, `--accent-dark: #1E3A2F`), warm ivory
(`--bg: #F6F1E7`) and the brass of the wall lamps (`--brass: #B08D57`). Tokens
are at the top of `styles.css`.

## Credits

- Template-1 design by Dhruv (Digistay marketing lead)
- Photographs: the property's own
