# Ship 5 — Edit, Delete, and Don’t Break the Data (Oct 22–Oct 28)

Ship 4 gave you a working CLI loop. Now it has to feel like a **real app**: you can **add things, see them, edit them, delete them**, and your data **doesn’t get lost**.

We keep using the **same repo you started in Ship 3**. No new templates or forks.

---

## What you’re building this week

* **CRUD:** add / list / search / **edit** / **delete** your main items.
* **Safe saving:** don’t trash people’s data. Make a quick backup before saving.
* **Friendly behavior:** confirm before deleting, handle bad input, don’t crash.
* **A tiny bit of testing:** just enough to prove the basics work.
* **Docs:** short examples in your README so someone else can use it.

---

## What to turn in

* A CLI that runs a menu and supports add/list/search/edit/delete.
* **Safe save**:

  * Before you overwrite your data file (like `data.json`), copy it to `data.bak`.
  * Write new data to a temp file (like `data.tmp`) and then **rename** it to `data.json`.
  * Put a simple number at the top of your file like `"version": 2` so if you change the file later you can tell versions apart.
* **Tests** in `tests/` for: create/read/update/delete, duplicate handling, invalid IDs, plus one simple “run-through” test.
* **Git hygiene:** make a branch, do a few small commits, open a PR, merge to `main`.

---

## Track tasks

### Choose-Your-Own-Adventure (CYOA)

* Add an **Admin menu** to manage your story:

  * Add a scene
  * Edit a scene
  * Delete a scene
  * Add/remove a choice
* **Don’t break the story graph:** if a choice points to a scene that doesn’t exist, warn the user. Don’t let someone delete the start scene.
* **Search scenes** by id/title/keyword.
* Save to `story.json` with a `story.bak` backup and a `"version"` number.

**Quick demo path**

1. Add a scene → 2) link a choice → 3) edit text → 4) delete a dead end → 5) play start-to-finish.

---

### Password Manager

*(No encryption yet—that’s next week.)*

* Each entry should have: `id`, `site`, `username`, `password`, `notes`, `tags`, `last_updated`.
* CLI should support: add / list / search / edit / delete.
* **Duplicates:** if `(site, username)` already exists, ask what to do (skip/overwrite/keep both).
* **Display:** mask passwords by default; add a one-time “reveal” action.
* **Import/Export:** JSON (CSV optional). On import, handle collisions clearly.
* Save safely (temp → rename) and keep `passwords.bak`. Include `"version"`.

**Quick demo path**
Fresh start → add 2 entries → list → search → edit one → export → delete one → re-import → looks correct.

---

### Flashcard Quiz App

* Cards have: `id`, `question`, `answer`, `tags`, `times_seen`, `times_correct`.
* Manage cards with add / list / search / edit / delete.
* Quiz loop keeps stats (update `times_seen` / `times_correct`).
* Save safely with a backup and a `"version"`.
* **Optional:** simple study boxes (1–5) and a “study today” set.

**Quick demo path**
Make 5 cards → quiz by a tag → stats update → fix a typo → delete a card → filter shows the right set.

---

## Testing (keep it light but real)

* **Unit tests:**

  * create → read → update → delete on a temp file
  * duplicates behave as you designed (block or allow with a prompt)
  * editing/deleting a bad ID is handled without crashing
* **One integration test:** a scripted run that does add → list → search → edit → delete cleanly.
* Run `pytest`. Keep it passing in your PR.

---

## Implementation tips (plain English)

* **IDs:** give every item a unique string (use a library function to make one).
* **Backups:** copy old file to `*.bak` before you replace it.
* **Safe write:** write to `*.tmp` first, then rename it to the real file name. Renaming is basically instant and safer.
* **Version:** put `"version": 2` at the top of your JSON. If you change the file layout later, you can spot old versions and upgrade them.
* **Menu UX:** show the current item before editing; ask “Are you sure?” before deleting; print clear success/failure messages.

---

## Grading

* **Works (50%)** — CRUD + search work and don’t silently fail.
* **Keeps data safe (25%)** — backup + safe save + version number.
* **Usable (15%)** — confirmations, helpful errors, readable output.
* **Docs/Tests (10%)** — short examples in README, basic tests pass.

---

## Stretch goals (optional)

* Use SQLite instead of JSON (switchable with an env flag).
* “Undo last action” (keep a tiny change log).
* Batch import/edit.
* A config file in the home folder.

---

**Next week (Ship 6):** security hardening. For the password manager, that means real encryption and key handling. For CYOA/Flashcards, it’s input hardening and laying groundwork if you ever want multiple users.
