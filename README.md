# Parmod Traders

A static, bilingual business website for Parmod Traders in Loharu, Haryana. It presents configurable product categories and sends enquiries directly to WhatsApp, phone, Instagram, or Google Maps. There is no backend, checkout, customer account, analytics, or payment processing.

## Preview

Open `index.html` in a browser, or run a local static server from this folder:

```powershell
python -m http.server 8000
```

Then visit `http://localhost:8000`. No build step or package installation is required.

## Configuration

Business and catalogue settings are in the `SITE_CONFIG` object in the `<script>` near the bottom of `index.html`.

- `business`: shop name, phone and WhatsApp numbers, Instagram URL, address, directions URL, map embed URL, opening hours, English/Hindi WhatsApp message templates, and an optional verified `googleReviewsUrl`. The review link stays hidden unless it is an HTTPS URL on Google Maps, `g.page`, or `maps.app.goo.gl`.
- `delivery`: translated delivery wording and configurable `areas` list. Leave `areas` empty until delivery locations are confirmed.
- `categories`: category IDs, icon names, English/Hindi names, and English/Hindi descriptions. Category enquiry links are generated from `business.messageTemplates.category`.
- `gallery`: empty by default, which hides the showroom gallery. Add only genuine shop media. Image items use `{ type: "image", src: "assets/photo.jpg", alt: "...", caption: "..." }`; video items use `{ type: "video", src: "assets/video.mp4", title: "...", poster: "assets/poster.jpg", captions: "assets/captions.vtt" }`. Local relative assets and HTTPS media URLs are supported; gallery images load lazily.
- `offers`, `newArrivals`, `testimonials`: empty by default. Add only confirmed text-only offers or announcements and genuine customer quotes. The sections remain hidden when their arrays are empty. Announcement entries use `{ text: { en: "...", hi: "..." } }`; testimonial entries use `{ quote: { en: "...", hi: "..." }, name: "..." }` with customer permission.
- `website.publicUrl`: intentionally blank until deployment. Enter only the verified stable public HTTPS address here; syntax validation cannot determine whether a domain is deployed or a preview. Local, non-HTTPS, and malformed URLs are rejected. A valid value enables the website QR, canonical URL, `og:url`, and the URL field in LocalBusiness structured data. No Open Graph image is set because no suitable sharing image is currently provided.
- `qrImageEndpoint`: external QR image service used for the WhatsApp enquiry QR and, after deployment, the website QR. The WhatsApp QR encodes the language-specific `wa.me` enquiry link for `918307362602`, not a payment link. The service receives only that fixed enquiry URL or the configured public website URL; it does not receive visitor/customer data. A local QR encoder is not bundled because this static site has no package/build setup. If the image service is unavailable, a direct WhatsApp link remains available beside the code.

The supplied Google Maps directions URL is retained independently of the embedded map. The embed query names Parmod Traders and uses the supplied Fartiya Road / Loharu address; change `mapEmbedUrl` only to a verified Google Maps embed URL for this shop. A directions link remains visible if the map cannot load.

## Content and safeguards

The catalogue intentionally shows category names and descriptions only. It has no product photos, listings, prices, stock claims, cart, checkout, product popups, ratings, reviews, or payment details. Offers, arrivals, testimonials, the gallery, and the Google review link are not displayed until configured. The supplied logo at `assets/parmod-traders-logo.png` is used in the header; a text brand fallback and inline SVG favicon prevent a missing logo from becoming a broken image. LocalBusiness structured data uses only the supplied business name, phone number, and postal address; it does not assert opening hours, coordinates, or ratings.

English is the default. Use the `EN | हिन्दी` controls to switch language without reloading. Important visible copy and category content have English and Hindi versions. Keep business names, phone numbers, and URLs unchanged when editing translations.

## Deployment

Upload this folder's `index.html` and `README.md` to any static host, such as GitHub Pages, Netlify, Cloudflare Pages, or a standard web host. No deployment has been performed. After the site is publicly available, paste its real HTTPS address into `SITE_CONFIG.website.publicUrl` in `index.html`, then publish the updated file; this enables the website QR code.
