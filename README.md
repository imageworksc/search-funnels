# Search Funnels (Google + AI)

Service page for ImageWorks Creative.
Staging (GitHub Pages): https://imageworksc.github.io/search-funnels/

## Structure

```
index.html        Page markup (no inline styles or scripts)
css/styles.css    All styles: tokens, base, components, sections, responsive
js/main.js        Scroll reveal, navigation drawer, steps accordion
assets/img/       Logos
```

## Running inside Drupal

The live page is pasted into the `field--name-field-html-code` field of the
imageworkscreative.com theme (Bootstrap 3 plus the theme's own CSS), not served
on its own. These rules keep it rendering the same in both places:

- **Paste only `<main id="sf-main">`** plus the stylesheet and script links.
  The utility bar, navbar and footer in `index.html` are staging copies of the
  site's own header and footer, which Drupal already renders.
- **Everything is prefixed `sf-`**: classes, ids and CSS custom properties. The
  theme styles `.btn`, `.nav`, `.lead`, `.dropdown` and `.wrap`, and defines
  `--navy`, `--green` and `--blue` on the field itself, so unprefixed names
  would be overridden.
- **Element rules are scoped with `:where(.sf-scope)`**. They reset the theme's
  `p`, `h1`–`h4`, `address`, `a:hover` and list rules inside the page only, and
  never reach the site's header and footer. `:where()` adds no specificity, so
  component classes still win without `!important`.
- **Sizes are in px.** The theme sets `html { font-size: 10px }`, so any `rem`
  would shrink. Media queries are in px too.
- **`#sf-main` clears floats** and carries `html-wrapper`, the theme's opt-out
  class for its link and list rules. Never use `id="main"` or the class
  `section`: the theme caps them at 975–1000px.
- **Sticky column:** the theme puts `overflow-x: hidden` on the field, which
  disables `position: sticky`. `styles.css` switches it to `overflow-x: clip`
  only when the field contains `#sf-main`.
- No inline width patches in the field. If one seems needed, the fix belongs in
  these files.

`index.html` wraps `<main>` in a stand-in `field--name-field-html-code` div so
staging matches.

## Testing

Before handing off, test inside a copy of the live page with the theme CSS
loaded, at 390, 768, 1440, 1920 and 2560 wide, plus 3840 and 5120. Staging alone
won't show theme conflicts. Above 2200px the layout scales up with `zoom` so it
keeps its proportions on QHD, 4K and 5K displays.
