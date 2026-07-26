# Email Signature

A clean, table-based HTML email signature built to survive **Gmail's signature editor** — which is
far more destructive than most people realise.

```
━━━━━                                            ← 3px accent tab + hairline
┌────────┐  │  Nimit Jalan
│        │  │  FULL-STACK DEVELOPER              ← tracked, accent-coloured
│ 112×140│  │
│        │  │  hi@nimit.is-a.dev
└────────┘  │  nimit.is-a.dev
            │  ◍  ⌾  in                          ← 18px monochrome icons
```

Renders at **320 × 165 px**. No JavaScript, no web fonts, no external CSS.

---

## Why it looks like this

Gmail does not render your HTML as written. When you paste into
**Settings → General → Signature**, Gmail sanitises the markup and throws away:

| Thrown away by Gmail                        | Consequence                                    |
| ------------------------------------------- | ---------------------------------------------- |
| `<style>` blocks and `class` attributes     | All CSS defined there silently vanishes         |
| `@keyframes`, `:hover`, `@media`            | Animations and hover effects never run          |
| `position`, `float`                         | Overlays and absolute positioning collapse      |
| `object-fit`                                | Non-square images get **stretched**, not cropped |

So this signature follows four rules:

1. **Every style is inline.** There is no `<style>` block to lose.
2. **Layout is `<table>`-based.** Spacing comes from `padding` on `<td>`, which every client honours.
3. **Images are pre-cropped** to their exact final aspect ratio, because `object-fit` won't save you.
4. **Images are served at 2×** and displayed at 1× so they stay sharp on retina screens.

> A previous version of this file used CSS `@keyframes` for entrance animations and a sheen sweep.
> None of it ever rendered in Gmail. It has been removed rather than left as dead code.

---

## Install it in Gmail

1. Open `signature.html` in a browser.
2. <kbd>Ctrl</kbd>/<kbd>Cmd</kbd> + <kbd>A</kbd>, then <kbd>Ctrl</kbd>/<kbd>Cmd</kbd> + <kbd>C</kbd>.
3. Gmail → ⚙️ **Settings** → **See all settings** → **General** → **Signature**.
4. Create a signature, click into the box, paste.
5. Scroll down and hit **Save Changes**.

> Copy from the **rendered page**, not from the source code. Pasting raw HTML gives you a wall of text.

The file deliberately contains no page chrome or headings, so *Select All* grabs the signature and
nothing else.

---

## Fork it and make it your own

### 1. Fork and clone

```bash
git clone https://github.com/<you>/<your-repo>.git
cd <your-repo>
```

**Your repo must be public.** Gmail loads the images over plain HTTPS from
`raw.githubusercontent.com`; a private repo returns 404 and every image breaks.

### 2. Swap the image host

Every image URL in `signature.html` points at this repo. Replace all four:

```
https://raw.githubusercontent.com/NimJal/Email-Signature/main/assets/...
                                  ^^^^^^^^^^^^^^^^^^^^^^^
                                  change to <you>/<your-repo>
```

If your default branch isn't `main`, change that segment too.

### 3. Replace the portrait

The layout expects a **4:5 portrait at 224 × 280** (displayed at 112 × 140).

With ImageMagick — this scales to fill and crops, keeping the head in frame:

```bash
magick your-photo.jpg -resize "224x280^" -gravity north -extent 224x280 -strip assets/profile.png
```

No ImageMagick? Any image editor works — just export **exactly 224 × 280**. Do not skip this and
rely on the `width`/`height` attributes: Gmail will squash a mismatched photo rather than crop it.

Then **bump the cache-buster** at the end of the photo URL, or Google's image proxy will keep serving
your old picture for days:

```html
assets/profile.png?v=6   →   ?v=7
```

### 4. Edit your details

All in `signature.html`, one line each:

| What          | Find                   | Also update                    |
| ------------- | ---------------------- | ------------------------------ |
| Name          | `Nimit Jalan`          | the photo's `alt` attribute    |
| Role          | `FULL-STACK DEVELOPER` | keep it uppercase — see below  |
| Email         | `hi@nimit.is-a.dev`    | appears in `href` **and** text |
| Website       | `nimit.is-a.dev`       | appears in `href` **and** text |
| Social links  | the three `<a href>`s  | in the icons table             |

The role is typed in capitals rather than styled with `text-transform`, so it still reads correctly
if a client strips the CSS.

### 5. Change the social icons

Icons live in `assets/icons/` as 120 × 120 transparent PNGs, all drawn in slate `#0f172a`. Use any
file in that folder — the signature currently wires up `website`, `github`, `linkedin` and `medium`.

The original set also included Behance, Discord, Dribbble, Facebook, Instagram, Telegram, Threads,
TikTok, WhatsApp, X and YouTube. If you want one back, it's still in git history:

```bash
git checkout b021bdb -- assets/icons/x.png
```

To swap one, change the filename in the `src`. To add another, copy a `<td>` inside the icons table:

```html
<td style="padding:0 15px 0 0;">
  <a href="https://your-link" title="X" style="text-decoration:none;">
    <img src="https://raw.githubusercontent.com/<you>/<your-repo>/main/assets/icons/x.png"
         alt="X" width="18" height="18"
         style="display:block;width:18px;height:18px;border:0;outline:none;text-decoration:none;">
  </a>
</td>
```

The **last** icon cell must use `padding:0;` so the row doesn't end with trailing space.

Three to five icons is the sweet spot — more starts to look like a link farm.

### 6. Re-check the vertical rhythm

The photo is 140 px tall and the text column is engineered to total **exactly 140 px**, so the two
line up. If you add or remove a line, the columns will drift apart.

```
name       27   (21px @ line-height 27)
role     6+15   (padding-top 6, 11px @ 15)
email   16+21   (padding-top 16, 13px @ 21)
website  2+21   (padding-top 2,  13px @ 21)
icons   14+18   (padding-top 14, 18px tall)
──────────────
total     140   = photo height
```

Adding a phone line (`2+21`) means dropping 23 px elsewhere — or raising the photo to 112 × 163 and
re-cropping at that ratio.

---

## Colours

Change these and the whole thing stays coherent. Each appears only a handful of times.

| Role     | Hex       | Used for                                     |
| -------- | --------- | -------------------------------------------- |
| Ink      | `#0f172a` | Name, and the icon artwork itself            |
| Accent   | `#0f766e` | Role label, and the 44 px tab on the top rule |
| Body     | `#475569` | Email and website links                      |
| Hairline | `#e3e7ed` | Top rule and the vertical divider            |

The accent appears exactly twice on purpose. If you change it, note that the **icons are baked at
`#0f172a`** — re-tint the PNGs if you want them to match:

```bash
magick assets/icons/github.png -fill "#0f766e" -colorize 100 assets/icons/github.png
```

---

## Known limitations

**Dark mode.** The Gmail mobile app inverts light backgrounds but leaves PNGs alone, so the dark
slate icons lose contrast against an inverted background. There is no fix that survives Gmail's
sanitiser — media queries and `prefers-color-scheme` are stripped along with everything else in
`<style>`. If dark mode matters more to you than light mode, re-tint the icons to a mid grey like
`#94a3b8`, which is legible on both at the cost of some punch on white.

**Outlook for Windows.** Uses the Word rendering engine: `border-radius` is ignored, so the portrait
renders as a hard-cornered rectangle. Everything else — layout, spacing, type, colour — holds.

**Image blocking.** Some recipients block remote images by default and will see `alt` text instead.
Every image here carries a meaningful `alt`, so the signature still reads as text.

---

## Files

```
signature.html      the signature — open, select all, copy, paste
assets/profile.png  portrait, 224×280 (4:5)
assets/icons/       social icons, 120×120 transparent PNG
LICENSE             MIT
```

---

## License

[MIT](LICENSE) — fork it, change it, ship it.

The portrait in `assets/profile.png` is a personal photograph and is **not** covered by the license.
Replace it with your own.
