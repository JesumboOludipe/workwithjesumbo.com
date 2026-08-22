# workwithjesumbo.com

Static landing page for Jesumbo Spreadsheet Automation. No build step, no
dependencies. Everything is plain HTML, CSS and vanilla JS in one file per page.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The landing page. All styles and scripts are inline. |
| `privacy.html` | Privacy policy. Required for Meta ads. |
| `thanks.html` | Post-enquiry confirmation page. Set to `noindex`. |
| `robots.txt` | Allows everything except `/thanks.html`. |
| `sitemap.xml` | Two URLs. Update `lastmod` when the page changes. |
| `og-image.png` | 1200x630 social preview, referenced by the Open Graph tags. |
| `apple-touch-icon.png` | 180x180 home-screen icon. The favicon is an inline SVG. |
| `brand/` | Facebook page assets: profile picture and cover image. |

## Configuration

Everything configurable lives in one block near the top of `index.html`,
in `window.SITE_CONFIG`:

```js
PIXEL_ID              // Meta Pixel ID from Events Manager. Empty = no tracking loads.
FORM_ENDPOINT         // Where the enquiry form posts. Empty = falls back to mailto.
WEB3FORMS_KEY         // Only needed when FORM_ENDPOINT is the Web3Forms API.
THANKS_URL            // Where a successful submit lands. Default /thanks.html.
REQUIRE_COOKIE_CONSENT// true shows a consent bar and gates the pixel behind it.
```

### Form endpoint

Two options, both free and both work from a static page:

- **Web3Forms** — set `FORM_ENDPOINT` to `https://api.web3forms.com/submit`
  and paste the key you receive by email into `WEB3FORMS_KEY`.
- **Formspree** — set `FORM_ENDPOINT` to `https://formspree.io/f/yourFormId`
  and leave `WEB3FORMS_KEY` empty.

Until one is set the form opens the visitor's email client instead, which
works but converts poorly on mobile.

### Cookie consent

`REQUIRE_COOKIE_CONSENT` is `true` because UK and EU rules require consent
before advertising cookies load. The pixel does not load at all until the
visitor presses Accept. Only set it to `false` if you never advertise to
UK or EU visitors.

## Conversion tracking

A Meta `Lead` event fires when the enquiry form is submitted and when the
Calendly button is clicked. `/thanks.html` is a clean page-view target if you
would rather define the conversion by URL in Events Manager.
