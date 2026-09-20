# Going multi-user with Firebase

The site already has all the code. It runs **local-only** until you paste a config,
so you can push right now and wire this up whenever.

- No config → every visitor's questions stay in their own browser (what you have now)
- Config pasted → one shared queue, and answers you write go live for everyone

---

## 1. Turn on the two services — 3 minutes

In the `frontrowyp` project:

1. **Build → Firestore Database → Create database** → **Production mode** →
   location `europe-west2` (London).
2. **Build → Authentication → Get started → Google** → Enable → pick a support
   email → Save.

Until Firestore exists, the site simply stays local. Nothing breaks.

## 2. Paste the config — ALREADY DONE

Project `frontrowyp` is wired in at the bottom of `index.html`. Nothing to change.

## 3. Get your UID

Load the site, go to **My desk**, click **Sign in**, sign in with Google.
Then Firebase console → **Authentication → Users** → copy the **User UID**.

## 4. Lock it down — do not skip

Firestore console → **Rules** → paste everything in `firestore.rules`, replacing
both `PASTE_YOUR_UID_HERE` with that UID → **Publish**.

Without this, anyone can write answers in her voice on her own site. The rules are
the security — the config in the HTML is public by design and authorises nothing.

## 5. Check it

- Open the site in a normal window → ask something you have not answered → you should
  get "I have not answered this one yet"
- Open **My desk** in your signed-in window → the question is in **Waiting on me**
- Type a reply → Send
- Back in the normal window → ask it again → your answer comes back

That round trip is the whole product.

---

## What it stores

**`requests`** — one row per question asked: `label`, `themes`, `matched`, `typed`,
`ev`, `at`. No names, no emails, no accounts. Visitors never sign in.

**`answers`** — the answers you write at your desk. Public to read, only you can write.

## Cost

Free tier is 50,000 reads and 20,000 writes a day. A demo uses a few hundred. You'd
need thousands of daily visitors before this costs anything.

## If it breaks

The site never hard-fails. If Firebase doesn't load, the console logs
`Firebase did not load - staying local` and everything falls back to localStorage.

- **"Could not publish"** on send → you're signed out, or the UID in the rules is wrong.
- **Desk queue empty when it shouldn't be** → the `requests` read rule doesn't match
  your UID. Check for a stray space.
- **Sign-in popup closes instantly** → add your Netlify domain under
  Authentication → Settings → Authorized domains. `frontrowyp.firebaseapp.com` and
  `localhost` are there by default; your Netlify domain is not.
- **Opening index.html by double-clicking it** → Firebase will not load from a
  `file://` page (browsers block it). It works on Netlify, or via a local server
  (`python3 -m http.server`). The site still runs locally in the meantime.
