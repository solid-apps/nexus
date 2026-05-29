# nexus

A faithful recreation of **WorldWideWeb** — Tim Berners-Lee's 1990 browser on the
NeXT (the one he renamed *Nexus* so people wouldn't confuse the app with the Web
itself) — rebuilt as a window manager over **your own pod**. One self-contained
HTML file, no build, signs in with the universal **xlogin** pill.

WorldWideWeb wasn't just the first browser — it was a browser **and an editor**:
the **read-write web**. That's exactly what [Solid](https://solidproject.org) is
bringing back, so `nexus` is built to grow into the real thing, in phases.

## Faithful by source, not by eyeballing

- **NeXTSTEP chrome** — draggable, resizable grey windows on the teal workspace,
  beveled toolbars, the floating top-left menu. Modelled on CERN's 2019
  [recreation](https://worldwideweb.cern.ch/browser/).
- **Real WWW typography** — the genuine NeXT webfonts, self-hosted (~74KB total).
- **Tim's actual rendering** — documents are styled from his 1991 `default.style`
  (`H1` Helvetica-Bold 18, `H2` 14, `H3` Helvetica-Oblique 14, `address`
  oblique 12, …), and links are drawn **boxed + underlined** as they were in 1990.

## Phase 1 (this) — browse your pod

- Open any URL in a window (a pod resource, or any readable web page) and read it
  in true WorldWideWeb style.
- **Click boxed links** to follow them; **&lt;** / **&gt;** walk your history.
- **New** spawns another window; drag title bars to move, drag the corner to size.
- **Containers are clickable** — a pod folder (any URL ending `/`) renders as a
  WWW-style index of boxed links (sorted folders-first, with size/date), so you
  click through your pod like hypertext. `../` walks up.
- HTML renders faithfully; data resources (Turtle, JSON-LD, text) show as source —
  but every URL in them is a live link, so the whole pod stays click-through.
- Scripts/styles in fetched pages are stripped — nexus draws the document, the
  page can't take over the chrome.

Cross-origin pages may refuse reads (CORS); **your own pod always works**.

## Phase 2 (this) — edit in place & save

The read-write turn. On any HTML document you can write to:

- Hit **Edit** (or ⌘E) — the document becomes editable right in the window; change
  the text, headings, anything.
- **Save** (⌘S) writes it **straight back to your pod** (`PUT`). The original
  `<head>`/`<title>` is preserved; your edited body is swapped in.
- **Revert** discards and reloads. A `403`/`401` is reported as *no write access*.
- Open a URL that **doesn't exist yet** on your pod → nexus offers to **create**
  it (edit a blank page, Save to bring it into being).
- Data resources (Turtle, JSON-LD, text) are editable **as source** and saved with
  their original content type.

Editing strips page scripts from the rendered body (nexus draws documents, not
apps); the saved file keeps its original `<head>`. Use it for prose/pages.

## Phase 3 (this) — make links by hand

The signature WorldWideWeb move, the thing that made it a read-*write* web:

- Open the page you want to link **to** and choose **Mark Document** (⌘M) — it's
  held as the marked target (shown under the menu).
- Go to the page you're writing, hit **Edit**, **select** some text, then
  **Link to Marked** (⌘L) — nexus wraps your selection in an `<a href>` to the
  marked target. **Save** and the link is written to your pod.
- You can mark a page that **doesn't exist yet**, link to it, then create it
  (P2's create-on-404) — authoring a little web by hand, exactly like 1990.

## Later / stretch

- A **Style** menu (bold / headings) for richer editing.
- Mark a *selection* as a named-anchor target (deep links within a page).

## Run

Static — open `index.html`, or install via the **store** to `/public/apps/nexus/`.

AGPL-3.0-only.
