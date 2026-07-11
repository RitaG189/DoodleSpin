# Doodle Spin

A page that hands you a random **drawing theme** to riff on — every tap, something new. Never stare at a blank page again.

**🔗 Live demo:** <https://ritag189.github.io/DoodleSpin/>

Built as a single, self-contained HTML page (no build step, no dependencies) from a Claude Design concept.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The whole app — markup, styles, and logic. |
| `themes.js` | The theme lists. This is the file you edit to add or remove themes. |

Both files must live in the **same folder**.

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
