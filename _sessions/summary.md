# Adelaide as a single page: session summary

13 October 2026, working with Claude Code on `main`. The same session also worked on Tome and Word Perhect (see the `tome` and `wordperhect` repositories). The Adelaide part of the conversation is in [transcript.md](transcript.md).

## Aim

Modernise Adelaide (Simon Faithfull, technical direction by Michiel Dethmers, produced by e-2). The loading pages and frameset go, leaving a single page, `index.html`.

## What was there

- **The piece.** 51 GIF line drawings (594×600) in `images/adelaide/`, shown one at a time. Each click on the drawing shows the next, in a 93-step loop: scene 1 forward (`1_01`–`1_06`), scenes 2 to 9 each forward and back (`2_00`–`2_06`–`2_00`, `3_01`–`3_06`–`3_01`, …), then scene 1 back (`1_06`–`1_02`), round to `1_01` again.
- **The original launcher** was `preadelaide.html`, a frameset of `wait.html` ("Please wait while the document loads") and a hidden `cache.html`. That loaded every GIF as an `<img>`, then sent the window to `adelaide.html`. `adelaide.html` preloaded the 93 steps again as `im1`…`im93`, moved through them with `eval`, and carried a Google Analytics (`ga.js`) snippet.
- **A later version** was `load_adelaide.html`, with a progress bar using the X cross-browser library, which went on to `adelaide2.html`. It had the same 93 steps in an array.
- **Also present:** `WS_FTP.LOG` upload logs from 1999–2001, in the root and in `images/adelaide/`.

## What was done

**`index.html`**, the only page:

- The drawing is a `<button>`. A click, or Enter or Space when it has focus, shows the next drawing.
- The sequence is built from a table of the nine scenes, `[scene, first, last]`, rather than 93 hand-written entries. The generated list was compared with the original's: identical, 93 steps in the same order.
- There's no loading screen. The first drawing shows at once, and the other 50 GIFs are fetched in the background, so each click shows the next drawing straight away.
- The layout is the same: a centred 594×600 drawing on white, shrinking to fit narrow screens without sideways scrolling. A dotted outline shows only with keyboard focus.
- The analytics and the X library are gone.

**Removed:** `preadelaide.html`, `wait.html`, `cache.html`, `load_adelaide.html`, `adelaide.html` and `adelaide2.html`, with `git rm`, so they're still in history.

## Checks

These were run in Chrome (Playwright):

- clicking through all 93 steps matched the original order, including the wrap back to `1_01`
- Enter and Space each move to the next drawing
- all 51 GIFs load, with no errors and no missing files
- screenshots at 1200 and 390 pixels wide; at 390 the page doesn't scroll sideways

## Status

Uncommitted: `index.html` is new, and the six old pages are deleted.

To decide:

- Links to `preadelaide.html` or `adelaide.html`, for example from c-ship, will now get a 404. They need to point at `adelaide/` (or `index.html`), or small redirect pages could be added under the old names.
- Whether to keep the `WS_FTP.LOG` files. They were left as they were.

Noted: on very narrow screens the one-pixel lines are scaled down slightly and soften a little.
