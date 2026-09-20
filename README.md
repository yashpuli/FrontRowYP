# Front Row

Bring Aditi your decision. Get the call she would make, the room it came from, the honest
cost, and one thing to do this week.

Two files do everything:

- `index.html` — the app. Layout, behaviour, matching.
- `corpus.js` — everything the product **says**. Edit this, not the HTML.

No build step. No dependencies. No API keys. No model calls. Nothing leaves the browser.

---

## Deploy in about four minutes

**1. GitHub**
- github.com → New repository → name it `front-row` → Public → Create
- On the empty repo page, click **uploading an existing file**
- Drag in `index.html`, `corpus.js`, `netlify.toml`, `README.md` → Commit

**2. Netlify**
- netlify.com → Log in with GitHub → **Add new site** → **Import an existing project**
- Choose GitHub, authorise, pick `front-row`
- Build command **empty**, publish directory `.` → Deploy

Site configuration → Change site name to something readable before you demo.
Every push redeploys. Editing `corpus.js` on github.com and hitting Commit is enough.

---

## What's in it

| Page | What it does |
|---|---|
| Bring your decision | Six questions → one verdict |
| Paste or upload it | Drop an email, doc or screenshot. Reads it in-browser, detects themes, matches |
| For you | Sign-up quiz (1 min or 3 min) → a curated feed |
| Career mapper | Short or long term, three questions, five ranked calls |
| Feeling stuck / Shape my career / CV and LinkedIn / Events and rooms / Building something | Filtered views over the corpus |
| You are not alone | Real reader messages and her actual replies |
| Her frameworks | The Pace Audit, the Fear Rebrand and others, in her steps |
| Her writing | Substack and Instagram, and the posts these calls came from |
| For Aditi | The dashboard |

Dark and light mode, follows the system setting, toggle in the sidebar, remembered per browser.

---

## How to change things

**A verdict's wording** — find the row by `id` in `corpus.js`, edit the text.

**Add a decision** — copy a row in `CORPUS`, paste below, change the fields. Rules:
- `call` — one decisive sentence. No "it depends", no three options.
- `room` — never blank.
- `next_step` — one action with a day attached.
- `again` — only `yes`, `no`, or `not like that`.
- `source` — sheet ref or post title and date. This is the trust claim.
- `tags` — 4–6, **only names already used by other rows**.

**Re-theme a page** — change its `tags` array in `SECTIONS`. Pages are live filters, so
re-tagging one row re-themes it everywhere it appears.

**Add a page** — add to `SECTIONS`:
```js
{"id":"money","label":"Money","kind":"list",
 "tags":["salary","negotiate","pay-cut","side-income"],
 "blurb":"What she would do about pay."}
```
`kind` can be `list`, `intake`, `mapper`, `evidence`, `foryou`, `voices`,
`frameworks`, `channels`, `console`.

**Teach it to recognise new words in uploads** — `LEXICON` in `corpus.js` maps words to
themes. Add phrases to any theme; they take effect immediately.

**Her links** — `LINKS` in `corpus.js` holds the Substack, the Instagram, and the posts.
A verdict automatically shows "read the piece this came from" when its `source` names a post.

**The sign-up quiz** — `QUIZ_QUICK` (3 questions) and `QUIZ_DEEP` (7) in `corpus.js`.

**Matching strictness** — top of the script in `index.html`:
- `MATCH_FLOOR` (default 2) — the minimum score to answer at all.
- `NEEDS_DECISION_TAG` (default true) — the match must also agree on the *kind* of
  decision. This is what makes "Aditi has not ruled on this yet" reachable. Turn it off
  and the product answers more often, less honestly.

---

## Uploads: what actually happens

Files are read with the browser's `FileReader`. Text formats (`.txt .md .csv .json .eml
.html .log .vtt .srt`) are read in full. Everything else — images, PDFs, spreadsheets —
is kept by filename only and the filename is still scanned for themes.

Detected themes come from `LEXICON`, a word list. No OCR, no model, no upload. The page
shows which words it picked up on, so the reasoning is visible rather than magic.

**Nothing is sent anywhere.** There is no server.

---

## Storage

`localStorage`, private to one browser:

- `fr_requests` — every decision brought, with themes. Powers the dashboard.
- `fr_profile` — the sign-up quiz result.
- `fr_seen` — first view of each verdict. Powers the day-7 "did you do it?" prompt.
- `fr_did` — whether someone acted.
- `fr_theme` — light or dark.

Reset before a demo: open the site, run `localStorage.clear()` in the browser console, reload.

---

## Demo path

1. `#/decide` as Priya — spending money / deciding now / £500–£2,000 / London / tech →
   the £600 week verdict. Point at **the room** and the **source** line.
2. **Send this to someone** — copies a permalink with a forward line.
3. `#/evidence` — paste an offer email. Watch it name the themes, then answer.
4. `#/foryou` — quick quiz, curated feed.
5. `#/console` — the decisions you just asked are already there, ranked, with the gaps under them.
6. `#/decide` → "Something else — it is not in this list" → **"Aditi has not ruled on this yet."**

Step 6 proves it isn't generating. Don't skip it.

---

## Tested

Chromium, desktop 1280×900 and mobile 390×844: every route renders, both flows complete,
paste and file upload both produce verdicts, binary files don't crash it, the dashboard
logs and charts, dark and light both pass, no horizontal overflow on any page, no JS errors.
