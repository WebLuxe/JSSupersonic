# JS Supersonic: online store

A concept online shop for JS Supersonic, the electronics store at Bagatelle Mall and Jumbo Phoenix in Mauritius, with an admin panel. Plain HTML, CSS and JavaScript with no frameworks, so it is fast on phones and runs on GitHub Pages or any web host.

## This is a concept preview, not the live shop

`"demo": true` in `data/catalog.json` keeps the site in preview mode:

- A slim bar at the top of every page says it is a design proposal with sample products and prices. `demo_by` is the name shown, and `demo_link` (optional) makes that name a link.
- Every page is marked `noindex` and `robots.txt` blocks search engines, so shoppers cannot find sample prices under the store's name on Google.

Set `"demo": false` and rebuild when the business has approved the content and it is ready to launch.

## What's in it

**Shop pages:** home, all products, 7 category pages, 40 product pages, deals, new in, brands, pay monthly, stores, help and contact, track my order, my account, wishlist, cart, checkout, privacy, terms and a 404 page.

**Motion:**
- An intro plays once per visit.
- A slanted orange and black curtain sweeps across between pages.
- The hero slider wipes between slides and the headline rises word by word.
- A ticker strip and a brand strip scroll across the page.
- Product photos fly into the cart when you add them.
- Tabs have a sliding underline.

All of it switches off for visitors who set "reduce motion" on their device.

**Admin panel** (`/admin/`): dashboard with sales chart, products (add, edit, hide, delete), orders with status updates, customers, messages, promo codes, announcement bar and store settings. The first visit asks you to create the admin password. Only a scrambled (hashed) version is saved, never the password itself.

## How the admin panel saves changes

This version has no server. The admin panel saves changes in the browser it is used in, and the shop shows them straight away on that same device. To publish changes for every visitor:

1. In the admin panel, go to **Settings** and click **Download catalogue**.
2. Replace `data/catalog.json` in this repo with the downloaded file.
3. Run `python3 build.py` and commit the result.

Orders, messages and accounts placed on the live site are also stored in each visitor's own browser. The next step before taking real orders is to connect a hosted database (for example Supabase or Firebase) so orders reach the admin panel from every device.

## Before going live

- **Contact details to confirm with the owner:** the phone number (`+230 698 5974`), email, Facebook link and the two store locations come from the store's public Facebook page. They are in `data/catalog.json` under `site` and `stores`. The WhatsApp number is empty, so no WhatsApp link is shown. Add a mobile number to bring it back.
- **Opening hours:** shown as "Open every day during mall hours" because the real hours are not confirmed. Set `hours` for the site and for each store.
- **Services to confirm with the owner:** free delivery over Rs 5,000, Click & Collect, pay monthly, air con installation, trade-ins and the promo codes are proposals, not the store's current policies.
- **Products and photos:** all 40 products, prices and stock levels are samples. Photos come from Unsplash (free to use under the Unsplash License) and should be replaced with real product photos. A product shows one photo. To add more, list extra photo ids or full image URLs under `"imgs"` for that product.
- **Payments:** checkout is a demo. Card, Juice, my.t money, Blink, cash on delivery and pay monthly are shown, but none are connected to a payment provider.
- **Policies:** delivery, returns, warranty, privacy and terms text are starting templates. The business and a lawyer should check them.
- **Domain:** `site.url` in `data/catalog.json` is used for canonical tags, the sitemap and the share image. Change it when you connect a custom domain, then rebuild.
- **Analytics:** add a Google Analytics 4 ID in admin Settings, or in `site.ga_id`. It only loads for visitors who accept cookies.

## Editing and building

Everything is generated from `data/catalog.json` by `build.py`:

```bash
python3 build.py          # rebuilds every page, sitemap.xml, robots.txt and llms.txt
python3 -m http.server    # preview at http://localhost:8000
```

On Windows the command is `python build.py`. Pages for products or categories that were removed from the catalogue are deleted by the build.

Do not edit the generated `.html` files by hand. Change `build.py`, `data/catalog.json`, `assets/css/site.css` or `assets/js/site.js`, then rebuild.

## Publish on GitHub Pages

1. In the repo, go to **Settings → Pages** and choose **Deploy from a branch**, then `main` and `/ (root)`.
2. Turn on **Enforce HTTPS**.
3. The site appears at `https://webluxe.github.io/JSSupersonic/`. This address is also `site.url` in `data/catalog.json`, which the share image, canonical tags and the 404 page depend on.

## Launch checklist status

- **Launch:**
  - Privacy, terms and 404 pages are in.
  - No secrets are in the code. HTTPS is forced.
  - A small cookie card asks for consent and waits until the visitor scrolls.
  - Every page has its own title and description, plus a share image and favicons.
  - `sitemap.xml` and `robots.txt` are in (search engines stay blocked while `demo` is on). Every image has alt text.
  - Images are compressed and resized per screen. The font is self-hosted.
  - Every page has one main button.
  - Forms are validated and protected against spam with a hidden field and a time check.
  - Analytics only loads after consent.
- **Mobile:**
  - Nothing scrolls sideways from 320px up, and pages work turned sideways too.
  - A bottom tab bar keeps the main actions in thumb reach.
  - Buttons are at least 44px. Phone numbers are tap-to-call.
  - Scrolling down on a phone tucks the logo row away and keeps the search bar.
  - Images keep their space while loading, so the page doesn't jump.
- **Design:** one typeface (Archivo, not Inter), with no gradient text, glass panels, emoji in headings, badges above headlines or fade-in-on-scroll. All text colours pass WCAG AA contrast.
- **SEO:**
  - Every page is real HTML, not built by JavaScript in the browser.
  - Canonical tags, breadcrumbs and structured data are in, including Product, store, FAQ and breadcrumb data.
  - `llms.txt` is in, and pages link to each other.
  - No source maps or large JavaScript bundles.
