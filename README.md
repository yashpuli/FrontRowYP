# Pretty Ambitious — ask me

One file. Open `index.html` in any browser and it works. No build step, no
dependencies, no API keys, no server. Everything stays in the visitor's browser.

## Deploy

**GitHub** → New repository → *uploading an existing file* → drag in `index.html`,
`netlify.toml`, `README.md` → Commit.

**Netlify** → Add new site → Import an existing project → GitHub → pick the repo →
build command **empty**, publish directory `.` → Deploy.

## Editing

Everything the site says is in one `DATA` object at the top of the `<script>`.
Search for `var DATA =`.

| Key | Controls |
|---|---|
| `corpus` | Every answer: `q`, `call`, `cost`, `unless`, `do`, `how`, `tags` |
| `topics` | The eight tiles, and the groups on the Answers page |
| `stages` | The five points on the career map |
| `picks` | Things you recommend. `approved: true` shows the **Aditi approves** badge |
| `links` | Substack, Instagram, Club, LinkedIn, Luma, Eventbrite |
| `events` | The Club and any dated events |
| `posts` / `frameworks` / `gaps` | Writing page, methods, and the "what to make next" list |
| `lexicon` | Words that map to themes when someone types, pastes or dictates |

## Dictation

The mic uses the browser's own speech recognition — works in Chrome, Edge and
Safari, and **hides itself automatically** in browsers that don't support it
(Firefox). Wispr Flow is an OS-level tool that types into any focused field, so it
works in the box without any integration.

## Events

Put your Luma calendar ID in `links.lumaCalendarId` and real dates embed on The Club
page. An Eventbrite organiser ID in `links.eventbriteOrgId` adds a tickets button.
Leave them blank and the site quietly hides the section. True two-way sync needs API
keys and a server — the embeds are the no-backend equivalent.

## Quick vs detailed

Every answer has a **Just the answer / Give me the detail** toggle. Quick shows the
call plus the one action. Detailed adds the cost, when you'd say the opposite, and
"Why I say this". The choice is remembered.

## My desk — answering live

Unanswered questions appear under **Waiting on me** as a chat thread. Type a reply,
press Send, and it becomes a real answer on the site: the next person who asks
something similar gets it without you. Live answers are matched by wording as well
as tags, so they work even when the question uses words the lexicon has never seen.

Reset before a demo: open the site, run `localStorage.clear()` in the console, reload.

## Two settings

- `FLOOR` (2) — minimum score before the site answers at all.
- `NEEDS_KIND` (true) — the match must agree on the *kind* of decision. This is what
  makes "I have not answered this one yet" possible. Answers you wrote yourself skip
  this check.

## Demo path

1. Home — type or dictate a real question, get an answer
2. Toggle **Just the answer** to show the one-liner mode
3. Answers — tap a heading, watch it open in place
4. Ask something you have not answered → "I have not answered this one yet"
5. **My desk** — that question is waiting. Type a reply. Send.
6. Go back and ask it again → your own answer comes back

Step 6 is the loop. It's the whole product in fifteen seconds.

## Tested

Chromium, 1440×950 and 390×844: typed search, suggestion chips, depth toggle,
accordion, paste and file upload, live reply round-trip, all nine pages, no
horizontal overflow, no JS errors, no third-person copy anywhere.
