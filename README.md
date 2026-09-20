# Pretty Ambitious — ask me

One file. Open `index.html` in any browser and it works. No build step, no
dependencies, no API keys, no server.

## Deploy

**GitHub** → New repository → *uploading an existing file* → drag in `index.html`,
`netlify.toml`, `README.md` → Commit.

**Netlify** → Add new site → Import an existing project → GitHub → pick the repo →
build command **empty**, publish directory `.` → Deploy. Rename the site under
Site configuration before you demo.

Every push redeploys. Editing `index.html` on github.com and hitting Commit is enough.

## Editing

Everything the site says lives in one `DATA` object at the top of the `<script>`.
Search for `var DATA =` and edit the JSON.

| Key | What it controls |
|---|---|
| `corpus` | Every answer. `q` question, `call` your answer, `cost`, `unless`, `do`, `how`, `tags` |
| `topics` | The eight tiles on the home page. Change `tags` to re-theme a tile |
| `stages` | The five points on the career map |
| `links` | Substack, Instagram, Club, **LinkedIn**, **Luma**, **Eventbrite** |
| `events` | The Club and any dated events |
| `posts` | Newsletter pieces shown on Home and Writing |
| `frameworks` | The Pace Audit and the rest |
| `gaps` | Questions with no answer yet — these drive "what to make next" |
| `lexicon` | Words that map to themes when someone pastes or uploads something |

Three links are intentionally blank — `links.linkedin`, `links.luma`,
`links.eventbrite`. Paste a URL into any of them and the button appears by itself.
Leave them blank and the site quietly hides them.

Adding an answer: copy any object in `corpus`, change the text, reuse tag names that
already appear elsewhere. A tag nothing else uses will never match.

## Two settings worth knowing

- `FLOOR` (2) — minimum score before the site answers at all.
- `NEEDS_KIND` (true) — the match must also agree on the *kind* of decision. This is
  what makes "I have not answered this one yet" possible. Turn it off and the site
  answers more often, less honestly.

## What's where

- **Home** — the ask, eight topic tiles, the career map, the Club, recent writing
- **Ask me** — six taps to an answer
- **Show me** — paste or drop a file; themes detected in-browser, nothing uploaded
- **Answers** — all 41, filterable
- **Career map** — five stages, tap one for the answers and a method
- **The Club** — links to the Club's Instagram, ready for Luma/Eventbrite dates
- **Writing** — Substack, Instagram, Club, recent pieces, the frameworks
- **My desk** — the private dashboard

## My desk

Counts questions brought, how many were answered without you, which need you, and
how many arrived with a document. A donut for the share your answers already handle,
a sparkline for the last seven days, a bar chart of what people are dealing with,
the queue, and **what to make next** — each with a format, where to put it, and six
filming steps.

Reset before a demo: open the site, run `localStorage.clear()` in the browser console,
reload. All data is local to one browser; nothing is collected.

## Tested

Chromium, 1440×950 and 390×844: every page renders, both flows complete, paste and
file upload both produce answers, binary files don't crash it, the dashboard charts
from real data, no horizontal overflow, no JS errors, no third-person copy anywhere.
