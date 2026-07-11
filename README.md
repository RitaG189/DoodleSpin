# Doodle Spin

A playful landing page that hands you a random **drawing theme** to riff on — every tap, something new. Never stare at a blank page again.

**🔗 Live demo:** <https://ritag189.github.io/DoodleSpin/>

Built as a single, self-contained HTML page (no build step, no dependencies) from a Claude Design concept.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The whole app — markup, styles, and logic. |
| `themes.js` | The theme lists. This is the file you edit to add or remove themes. |
| `og-image.png` | 1200×630 social share preview image (referenced by the Open Graph / Twitter tags). |
| `robots.txt` | Tells search-engine crawlers they may index everything, and points to the sitemap. |
| `sitemap.xml` | Lists the site's URL(s) so search engines can discover them. |

`index.html` and `themes.js` must live in the **same folder**. For SEO to work once
deployed, `og-image.png`, `robots.txt`, and `sitemap.xml` must sit in the site root
alongside `index.html`.

## Running it

Because the page loads `themes.js` via a `<script>` tag, you can open it two ways:

- **Double-click** `index.html` to open it directly in your browser (`file://`), **or**
- Serve the folder over HTTP, e.g.:
  ```bash
  python -m http.server 8823
  ```
  then visit <http://127.0.0.1:8823/>

No installation or internet connection is required (the Google Fonts link degrades gracefully to system fonts if offline).

## How it works

1. Pick a **mode** with the toggle above the button:
   - **Categories** *(default)* — draws from the `DOODLE_CATEGORIES` list (broad subjects).
   - **Creative** — draws from the `DOODLE_CREATIVE` list (more imaginative prompts).
2. Tap **🎲 Randomize my theme** to get a theme from the active list.
3. The result appears in a card below. Each tap never repeats the theme shown immediately before.
4. Use the **☀️ / 🌙 toggle** in the header to switch between light and dark mode.

## Editing the themes

Open `themes.js`. There are two lists — one per mode:

```js
window.DOODLE_CATEGORIES = [
  "Ocean",
  "Forest",
  // ...
];

window.DOODLE_CREATIVE = [
  "Underwater Worlds",
  "Floating Islands",
  // ...
];
```

Rules:

- **One theme per line**, wrapped in quotes (`"..."`) and ending with a comma.
- **To add:** insert a new line into the correct list.
- **To remove:** delete the line (or comment it out with `//`).
- **Save** the file and **reload** the page.

If a list is ever missing or empty, the page falls back to a single default theme instead of breaking.

## Customizing the look

The visual defaults are set near the top of the `<script>` block in `index.html`:

```js
const state = {
  palette: 'Sunset Punch',  // 'Sunset Punch' | 'Bubblegum Pop' | 'Citrus Splash'
  energy: 'Calm',           // 'Calm' | 'Playful' | 'Wild'  (background motion)
  shapeStyle: 'Scribble',   // 'Blobs' | 'Confetti' | 'Scribble'
  dark: false,
  mode: 'categories',
};
```

Change these values and reload to alter the palette, background animation speed, and shape style.

## SEO

The page ships with search-engine and social-sharing metadata baked into the `<head>`:

- A keyword-focused `<title>` and `<meta name="description">`.
- A `<link rel="canonical">` pointing at <https://ritag189.github.io/DoodleSpin/>.
- **Open Graph** and **Twitter Card** tags, using `og-image.png` as the preview image.
- An emoji favicon (🎨) embedded as an inline SVG (no extra request).
- **JSON-LD structured data** describing the app as a free `WebApplication`.
- `robots.txt` and `sitemap.xml` in the root.

If you change the site URL (e.g. move to a custom domain), update it in **all** of these
places: the `canonical`, `og:url`, `og:image`, `twitter:image`, and JSON-LD `url` inside
`index.html`, plus `robots.txt` and `sitemap.xml`.

### Still to do manually (outside the code)

1. **Commit & push** `index.html`, `og-image.png`, `robots.txt`, and `sitemap.xml` so GitHub Pages serves them.
2. Register the site in [Google Search Console](https://search.google.com/search-console) and submit `https://ritag189.github.io/DoodleSpin/sitemap.xml`.
3. Verify the share preview with the [Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/) and [Twitter Card Validator](https://cards-dev.twitter.com/validator).
4. Longer term: earn a few backlinks and consider a custom domain (ranks better than a `github.io` subdomain).
