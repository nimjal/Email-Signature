# ✉️ Animated Email Signature — free, customizable in minutes

A clean, professional email signature for the bottom of every email you send: your photo, name, title, a verified check, and swappable social icons — with a smooth intro animation and a subtle idle shine.

**Preview it live (once you've pushed this repo to GitHub):**
👉 https://htmlpreview.github.io/?https://raw.githubusercontent.com/NimJal/email-signature/main/signature.html

> **No coding needed.** You can either hand-edit a few lines, or let **Claude** do the whole thing for you (below).

---

## 🅰️ Put it in your Gmail (2 minutes)

1. **Open the signature** (link above) so you see just the card in your browser.
2. Click it → **Select All** (`Cmd`/`Ctrl`+`A`) → **Copy** (`Cmd`/`Ctrl`+`C`).
3. Gmail → **⚙️ gear → See all settings → General → Signature → ＋ Create new** → **Paste**.
4. Under **Signature defaults**, set it for **“For new emails”** and **“On reply/forward.”**
5. Scroll down → **Save changes.** ✅ Now it’s on every email automatically.

**Two Gmail quirks (not the file — Gmail does these):**
- **The `--` line above it?** Gmail → Signature settings → tick **“Insert signature before quoted text in replies and remove the ‘--’ line that precedes it.”** → Save.
- **Photo/icons hidden?** Gmail → **General → Images → “Always display external images”** → Save.

---

## 🅱️ Make it your own — the EASY way (let Claude do it)

1. Click **Fork** (top-right) to get your own copy.
2. Open your copy in **[Claude Code](https://claude.com/claude-code)** (or paste the files into Claude), and give it this prompt — fill in the brackets:

```text
Customize signature.html in this repo for me. Change ONLY the content, not the layout/animations/styling:

- Name:     [YOUR NAME]
- Title:    [YOUR TITLE]
- Email:    [YOUR EMAIL]        (it appears twice — update both)
- Website:  [YOUR WEBSITE]

Left icon rail — I want these icons, in this order:  [e.g. Website, Instagram, LinkedIn]
(remove any that aren't listed — e.g. remove GitHub)
My links:  LinkedIn = [...], Instagram = [...], Website = [...]

Photo: I'll save my picture as assets/profile.png (keep it a square).
Update the photo URL and the icon URLs to use MY GitHub username: [YOUR-USERNAME]

Available icons are in assets/icons/. If I ask for one that isn't there, create a
matching PNG the same style. Then show me the result.
```

3. Add your photo: in your repo, open **`assets`** → delete `profile.png` → **Add file → Upload files** → upload your picture **named exactly `profile.png`** (square looks best).
4. Open **your** live preview and copy it into Gmail (Section 🅰️):
   `https://htmlpreview.github.io/?https://raw.githubusercontent.com/NimJal/email-signature/main/signature.html`

---

## 🅱️ Make it your own — by hand (no Claude)

Open **`signature.html`** on GitHub → pencil ✏️ → change only these (use `Cmd`/`Ctrl`+`F` to find):

| Find | Currently |
|------|-----------|
| name | `Nimit Jalan` |
| title | `Full-Stack Developer` |
| email *(2 places)* | `hi@nimit.is-a.dev` |
| website *(2 places)* | `nimit.is-a.dev` |
| LinkedIn | `linkedin.com/in/nimit-jalan` |
| GitHub | `github.com/NimJal` |
| image host (every `src`) | `raw.githubusercontent.com/NimJal/email-signature` |

**Commit changes**, then copy your live preview into Gmail.

### Swapping / adding / removing icons
Each icon in the rail is one small block in `signature.html`. To **change** an icon, point its `src` at a different file in `assets/icons/` and update its `href`. To **remove** one, delete its `<tr>…</tr>` block. To **add** one, copy an existing block and change the two lines.

**Icons already included** (in `assets/icons/`):
`website` · `linkedin` · `github` · `instagram` · `x` · `facebook` · `youtube` · `tiktok` · `threads` · `dribbble` · `medium` · `whatsapp` · `telegram` · `discord` · `behance`
*(Need another? Ask Claude to generate it, matching the same style.)*

---

## 🎬 About the animation
The intro + subtle shine play in **Apple Mail**, **Outlook for Mac**, and any browser. **Gmail shows the card without motion** — every signature is static in Gmail; that’s Gmail’s rule, not this file. Your photo, badge, icons, and links look right either way.

## License
[MIT](LICENSE) — free to use, share, and remix.
# Email-Signature
