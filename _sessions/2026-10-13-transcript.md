# Adelaide as a single page - session transcript

Transcript of the Adelaide part of a Claude Code session on 2026-10-13. Earlier in the same session, Tome and Word Perhect were worked on; that part is in the `tome` and `wordperhect` repositories' `_sessions` folders. Tool calls are shown as one-line notes; their output is omitted. Message times weren't recorded, so only the date is given. Claude's longer replies are shortened where they repeat what the summary records.

---

## User - 2026-10-13

Can you take a look at repos/adelaide - I'd like the code in this project to be modernised - ditch all the loading stuff and frameset and just have a SPA

## Claude

> *Bash: Survey the adelaide repo*

> *Bash: Read the loading and frameset pages*

> *Bash: Read the two viewer pages and list images*

Adelaide is small and simple. 51 GIFs make a 93-step sequence: scene 1 plays forward, scenes 2 to 9 each play forward and then back, and scene 1 plays back to the start. Clicking the drawing moves to the next frame. There are two generations of wrapper around it: `preadelaide.html` → `wait.html` + `cache.html` (frameset) → `adelaide.html`, and the later `load_adelaide.html` (progress bar) → `adelaide2.html`. Checking which addresses other sites link to before I remove pages:

> *Bash: Find links to adelaide pages in other repos (stopped)*

## User (sent while Claude was working) - 2026-10-13

The original used preadelaide.html as the launcher

## User (sent while Claude was working) - 2026-10-13

I'd like it to just use index.html

## Claude

Understood: one `index.html` and nothing else, replacing the `preadelaide.html` launcher and all the pages behind it. The search for links from other sites isn't needed now, so I'm stopping it.

> *TaskStop: the link search*

Writing `index.html`. Rather than 93 hand-written entries, it builds the sequence from a short table of the nine scenes. I'll check the result against the original list exactly.

> *Write: index.html*

> *Bash: Compare generated sequence with the original*

The generated sequence matches the original 93 frames exactly, and `adelaide2.html` used the same list. Removing the six old pages (they stay in git history):

> *Bash: Remove the old frameset and loader pages*

Testing in headless Chrome: click through the whole loop, check every frame against the sequence, then look at it on desktop and phone widths.

> *Bash: Click through the full loop in Chrome*

The click-through matches the original exactly, including the wrap back to the start. All 51 GIFs load and there are no errors. The keyboard check was a flaw in my test: the button already had focus from the clicks, so pressing Tab moved focus off it. Rechecking with the button focused directly:

> *Bash: Recheck keyboard activation*

Enter and Space both work.

Adelaide is now a single page, `index.html`, and the six old pages are removed. I tested it in Chrome by clicking through the full 93-frame loop, and it shows the same frames in the same order as the original, wrapping back to the first drawing at the end.

- **The drawing is a button.** Clicking it, or pressing Enter or Space, shows the next drawing.
- **No loading screen.** The first drawing shows straight away, and the other 50 GIFs are fetched in the background.
- **The sequence comes from a short table of the nine scenes**, identical to the original's list.
- **Layout:** the same centred 594×600 drawing on white, shrinking to fit narrow screens.
- **Removed:** the dead Google Analytics snippet and the old cross-browser library, and the pages `preadelaide.html`, `wait.html`, `cache.html`, `load_adelaide.html`, `adelaide.html` and `adelaide2.html`.
- **To decide:** links to `preadelaide.html` or `adelaide.html` will now get a 404, so they need updating, or redirect pages could be added. The `WS_FTP.LOG` upload logs were left alone.

## User - 2026-10-13

Can you add a suymmary and transcript in _sessions for me please

## Claude

> *Write: _sessions/2026-10-13-summary.md*

> *Write: _sessions/2026-10-13-transcript.md*

Added the summary and transcript in `adelaide/_sessions/`.
