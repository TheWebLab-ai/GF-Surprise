# Two Sides of You — personalisation guide

A one-page interactive love story. Everything lives in **`index.html`** (design, text and code), plus your pictures in `assets/images/`.

```
project/
├── index.html
├── README.md
└── assets/images/
    ├── her.png            ← her illustrated portrait
    ├── memory-01.jpg      ← your photos (any names you like)
    └── …
```

**How to edit:** open `index.html` in VS Code, press `Ctrl+F` (`Cmd+F` on Mac) and search for the words in **bold** below. Save, then refresh the browser (`Cmd+Shift+R` / `Ctrl+F5` to bypass the cache).
**How to preview:** install the *Live Server* extension, right-click `index.html` → *Open with Live Server*.

---

## 1. Quick settings (the important ones)

Search for `SITE_CONFIG` (near the bottom of the file):

```js
const SITE_CONFIG = {
  passcode: "0610",
  birthday: "2026-10-06T00:00:00",
  totalChapters: 6
};
```

| What | How |
|---|---|
| **Passcode** | Change `"0610"`. It must be **exactly 4 digits** (the box has 4 digit slots). The code is asked **once**, when she goes from Home to Our Story. After that, everything is open. |
| **Birthday** | Change `birthday` to `"YYYY-MM-DDT00:00:00"`, e.g. `"2027-10-06T00:00:00"`. It uses the visitor's local time. |

> The passcode is only for the experience. Anyone can read it in the page source, so it is **not** real security.

**If you change the birthday, also update the words "06 OCTOBER"** in two places (search for `06 OCTOBER`): the Home countdown label and the "today is your day" message in the JavaScript (`updateCountdown`).

**Wrong-code / success messages:** search for `Not quite` and `UNLOCKED`.

---

## 2. Her name and the Home page

- **Name in the header:** search for `HER<span`. Change `HER` to her name (keep the `<span…>.</span>` for the red dot, or delete it).
- **Browser tab title:** search for `<title>`.
- **Home headings and one-liners:** search for `class="lede"`.
  - `GIRLFRIEND` → "The girl I love."
  - `BEST FRIEND` → "My favorite person."
- **Countdown label:** search for `COUNTING DOWN`.

### Her portrait
Save it as **`her.png`**, either next to `index.html` or in `assets/images/`. Keep the name lowercase. The portrait has a white background; the page blends it in, so you don't need to cut it out.

---

## 3. Our Story (timeline)

Search for `timeline-card`. Each card looks like this:

```html
<article class="timeline-card">
  <small>01 · THE BEGINNING</small>
  <h3>Where it started</h3>
  <p>Your text here.</p>
</article>
```

Edit the small label (date or chapter), the title `<h3>` and the paragraph `<p>`. Copy a whole `<article>…</article>` block to add another one (4–5 cards fit best).
Also change the intro sentence: search for `A few chapters from a story`.

**Add a photo to a card (optional):**
1. Put `<img src="assets/images/story-01.jpg" alt="Describe the photo">` inside the card, under the `<p>`.
2. Add this line to the CSS (search for `.timeline-card p{`):
   ```css
   .timeline-card img{width:100%;height:90px;object-fit:cover;margin-top:10px}
   ```

---

## 4. Memories (polaroid photos)

Search for `polaroid`. There are **6** blocks (3 in each group):

```html
<div class="polaroid p1">
  <img src="assets/images/memory-01.jpg" alt="Us at the beach">
  <span>our first trip</span>
</div>
```

Change three things per block:
1. `src` → your photo path (the starter file uses sample online photos, so replace them all)
2. `alt` → a short description (helps accessibility)
3. `<span>` → the handwritten caption

The **first 3** appear under 🌹 GIRLFRIEND on phones and the **last 3** under 🌻 BEST FRIEND. Keep the classes `p1`, `p2`, `p3` (they set the tilt and position).

**Heading and intro text:** search for `Moments<br>we keep` and `Replace the placeholder`.

**Photo tips**
- Roughly square photos look best (they're cropped to fill the frame).
- Keep each under ~500 KB and use `.jpg`.
- No spaces or capitals in file names: `memory-01.jpg`, not `Memory 01.JPG`.

---

## 5. For You

Search for `note-list`. Each line is:

```html
<div class="note"><strong>Your smile</strong><span>01</span></div>
```

Change the text inside `<strong>`. There are 5 on the girlfriend side and 5 on the best-friend side.
- Section headings: search for `The girl<br>I love` and `My<br>person`.
- The closing lines: search for `But honestly` (desktop only; hidden on phones).

---

## 6. Us (quiz and choices)

### Quiz
Search for `const quiz`:

```js
{q:"Who sends more random messages?", a:["Me","Her","Both"], c:1},
```

- `q` – the question
- `a` – the answer options (2–4 options work well)
- `c` – the **correct answer's position, counting from 0** (`0` = first option, `1` = second, `2` = third)

Copy a line to add a question. Reply messages: search for `YOU KNOW US TOO WELL` and `Nice try`.
The first question shown is written in the HTML too (search for `quizQuestion`), so update it to match your first entry in `quiz`.

### Choose-one cards
Search for `class="choice`. Edit the title in `<b>`, the line in `<small>` and the emoji. The pop-up message after tapping is in the JS: search for `Good choice`.

---

## 7. Final page

Search for `final-line`. Each line fades in one after another:

```html
<div class="final-line">You started as someone I could talk to.</div>
```

Rewrite them freely. The big closing sentence is `class="final-main"`. Her faded portrait uses `her.png` automatically.
**Start again ↺** slides back to Home (it stays unlocked).

---

## 8. Colours and mood

Search for `:root` at the top of the file:

```css
--paper:#f7f5ef;   /* page background */
--rose:#d8293d;    /* girlfriend red */
--sun:#f5b82e;     /* best-friend yellow */
```

Change the hex values to restyle the site. The ◐/☼ button in the header switches between the cream and a soft blush background (search for `#fff2ed` to change the blush tone).

---

## 9. Publishing on GitHub Pages

First time:
1. Create a GitHub repository, then in VS Code: **Source Control → Initialize Repository → Commit → Publish Branch**.
2. On GitHub: **Settings → Pages → Deploy from a branch → `main` → `/ (root)` → Save**.
3. After 1–3 minutes your site is at `https://YOUR-USERNAME.github.io/REPO-NAME/`.

Every time you edit:
1. Save the file.
2. **Source Control** → type a message → **Commit** → **Sync Changes** (or run `git add .`, `git commit -m "update"`, `git push`).
3. Wait a minute, then refresh the site with `Cmd+Shift+R`.

`index.html` and `assets/` must sit at the **top level** of the repository, not inside a sub-folder.

---

## 10. Troubleshooting

| Problem | Fix |
|---|---|
| A photo doesn't show | The file name or folder doesn't match exactly (it's case-sensitive online). Check `src="assets/images/…"`. |
| Changes don't appear online | Wait 1–2 minutes after pushing, then hard-refresh (`Cmd+Shift+R`). |
| 404 on GitHub Pages | `index.html` isn't at the top level of the repository, or Pages isn't set to `main` / `(root)`. |
| Can't type the code | Use 4 digits only. Click the first box, then type. |
| Countdown shows the wrong day | Check `birthday` in `SITE_CONFIG` and that your device's date and time zone are right. |
| Page breaks after editing | You probably deleted a `<` `>` `"` or `}`. Undo with `Ctrl+Z`, or compare with your last commit in Source Control. |

Tip: before big edits, commit your working version first. If anything breaks, you can always go back to it.
