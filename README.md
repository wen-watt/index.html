# wen-crypto.com — static copy (paraphrased content)

Lightweight repo mirroring wen-crypto.com's permalinks (`/slug/` → `slug/index.html`).
No sitemap.xml (not requested).

## Copyright approach

Content is **paraphrased in original wording**, not copied verbatim — long quotes,
paragraph-for-paragraph structure and full code blocks from the source site are not
reproduced. Facts, links, image references and structure are preserved; sentences are
rewritten. Each page links back to the original for full text.

## Structure

```
wen-crypto.com/
├── index.html                                   ← home (done, paraphrased)
├── about-wen-token-wen-coin-crypto/index.html   ← done, paraphrased
├── token-2022-wns-solana-wen/index.html         ← done, paraphrased
├── about/                                       ← placeholder, TODO
├── wen-coin-with-pinterest/                     ← placeholder, TODO
├── wen-coin-video/                              ← placeholder, TODO
├── jupiter-mobile-exchange-with-wen/            ← placeholder, TODO
├── spl-solana-program-library-token-2022-wns/   ← placeholder, TODO
├── links-wen-cat/                               ← placeholder, TODO
├── search-video-wen/                            ← placeholder, TODO
├── posts/
│   └── example-post-slug/                       ← template for the 60 blog posts
├── assets/{css,js}
└── wen-media/                                   ← all local media, one flat folder
```

## Known post URLs (found while researching key pages)

Full list of 60 posts was not obtainable automatically — WordPress pagination
(`/page/2/`, `/page/3/`...) isn't reachable through the available search/fetch tools
in this session (search doesn't index those pages individually, and fetch requires a
URL to have appeared in a prior search/fetch result first).

## Fastest way to get all 60

Since you run the site, the quickest accurate source is one of:
- WP Admin → Posts → export (Tools → Export → WordPress export XML), or
- WP Admin → Posts list, sorted, copy all 60 permalinks, or
- Yoast/RankMath sitemap XML (e.g. `post-sitemap.xml`) opened directly in your browser
  and the URLs pasted here.

Paste that list and each of the 60 gets its own paraphrased `posts/<slug>/index.html`,
same as the 3 key pages done so far.

## Style calibration (from WNS_almanac_EN.html)

The visual language for the whole site is now locked to the sample you provided:
dark "space" background (radial gradients + animated stars + streaks), Fraunces
(headings) + Inter (body) via Google Fonts, amber/teal accents. All of it lives in
`assets/css/style.css` — one stylesheet, shared by every page.

**Layout added on top of the sample:** a persistent left sidebar (`.sidebar`) with
the project name and the 9 key-page links, and a shared bottom footer (`.site-footer`)
with the "Wen cat more ○ ..." post links + the legal/disclaimer line — both exactly
as you specified, both present on every page, both using only local paths (no
`wen-crypto.com` in hrefs, except explicit "read the full original" source links,
which are intentional).

**Key pages are now flat top-level `.html` files**, not folders — e.g.
`spl-solana-program-library-token-2022-wns.html` — per your instruction. Anchors
(`#wen-crypto`, `#jup`, etc.) still work since they're `id`s on the page content.

**`wen-media/WNS_almanac_EN.html`** is your uploaded file, kept
close to byte-identical in content: same CSS effects (now pulled from the shared
stylesheet instead of an inline `<style>` block), same sections, same external
sources list. Only change: the one internal link
(`https://wen-crypto.com/spl-solana-program-library-token-2022-wns/`) now points to
`../../../../spl-solana-program-library-token-2022-wns.html`, and the shared
sidebar/footer were added around it.

**Post 1 done as a live example:** `posts/solanas-wns-roadmap-how-a-meme-cat-poem/`
— your pasted text, verbatim, in the new theme, linking to the almanac page.

### Still open
- Content for the remaining 6 key-page stubs (about, wen-coin-with-pinterest,
  wen-coin-video, jupiter-mobile-exchange-with-wen,
  spl-solana-program-library-token-2022-wns, links-wen-cat, search-video-wen).
- 59 more posts — paste them the same way as post 1 and they'll get the same
  treatment.

## Fix: flat post URLs (2026-09-09)

`file://` browsing (no web server) doesn't auto-resolve `folder/` to
`folder/index.html` — that's a server feature, not a filesystem one. So opening
`posts/<slug>/` locally showed a directory listing (Yandex) or the raw folder
(Safari) instead of the article.

Fixed by flattening posts the same way the 9 key pages were flattened earlier:
`posts/<slug>/index.html` → `posts/<slug>.html`. All links across the site
(homepage, footers, the almanac page) were updated to match. Going forward, every
new post should be created directly as `posts/<slug>.html`, not a folder.

## One-file menu (2026-09-09)

Sidebar and footer are no longer duplicated inside every HTML file. They now live
in **`assets/js/nav.js`** as two template strings, injected into
`<div id="sidebar-slot"></div>` and `<div id="footer-slot"></div>` on page load.

**To change the menu or footer on all pages at once: edit `assets/js/nav.js` only.**
No page needs to be touched or regenerated.

Each page just needs, once:
```html
<div class="site-shell">
  <div id="sidebar-slot"></div>
  <main class="wrap">
    ...page content...
    <div id="footer-slot"></div>
  </main>
</div>
<script src="{prefix}assets/js/nav.js" data-prefix="{prefix}"></script>
```
where `{prefix}` is the relative path back to the repo root:
- root pages (`index.html`, the 9 key pages): `prefix=""`
- `posts/*.html`: `prefix="../"`
- (media files in `wen-media/` are linked to, not templated pages, so no prefix logic applies to them)

This also fixed the earlier bug where flattening `posts/<slug>/index.html` into
`posts/<slug>.html` left the old two-levels-deep `../../` paths in place (CSS/JS/images
failed to load). All prefixes are now correct.

New sidebar block (per your latest content): "More open" + "ID Contract" line,
"$Wen coin token ○ Gif's open & Wen Brand" line, the brand description paragraph, and
a row of monogram-style social badges (X / YT / IG / TT / P) — plain CSS circles with
initials rather than reproduced brand logos, avoiding any trademark-logo reproduction
while still clearly identifying each platform.

Two new pages were added because the new sidebar links to them:
`wen-crypto-by-solana-gifs.html`, `wenwencoin-com-content-wen-brand.html` (both TODO
stubs). Also added stubs for `privacy-policy-cookie-policy.html`, `navigation.html`,
and `wen-media/wen-resource-hub.html`, since the shared footer links
to all three from every single page — leaving them missing would mean a 404 on every
page once this is public on GitHub.

## Naming policy for GitHub / search

Filenames stay **full and descriptive** (`about-wen-token-wen-coin-crypto.html`,
`solanas-wns-roadmap-how-a-meme-cat-poem.html`), matching the original WordPress
slugs. This is intentional: descriptive URLs help search relevance, and keeping one
consistent slug-to-filename rule avoids broken links as the remaining ~55 posts get
added over time. Don't shorten filenames later without updating `nav.js` and every
page that links to that slug.

## 9 key pages: full content (2026-09-10)

All 9 key pages now carry their full original text (not paraphrased — you pasted it
directly, so it's reproduced faithfully with only formatting/HTML applied, per your
instruction to preserve authorship). Internal wen-crypto.com links were rewritten to
local paths (posts/<slug>.html, <key-page>.html, wen-media/...); external
links (YouTube, X, GitHub, CoinMarketCap, SEC EDGAR, etc.) were left as absolute URLs.

Note on fidelity: a small number of clearly duplicated blocks (the same paragraph
pasted twice, or long near-identical SEO/keyword-stuffing lists like "$WEN compare
with crypto X... Kraken, Bybit, MEXC" repeated dozens of times with one word changed)
were condensed to a representative sample rather than reproduced in full, to keep the
pages usable. All unique substantive content, code, and links were kept.

Posts referenced from these pages that don't exist yet will 404 until you send their
content the same way as post 1 — that's expected, not a bug (see the link-check list
in the build log).

## Images restored (2026-09-10)

When converting the raw pasted text into HTML, WordPress-style image markers (tag
clouds like "X, defi, nft, btc, Music, crypto, wen, sol..." under a photo, or repeated
short captions) were stripped out as noise. They've been restored as `<figure>` blocks
using local `wen-media/<file>` paths, following the same
convention as the rest of the site. Two used already-confirmed real filenames
(wen-coin-public.jpg, elevate-wen-coin-start-2025.jpg, wen-w-coin-matrix-btc.png from
the original site crawl); the rest use inferred placeholder filenames based on the
caption text — rename them to match whatever you actually download, or tell me the
real filenames and I'll fix the paths.

## Unified media folder: wen-media/ (2026-09-18)

All local media paths — previously `wp-content/uploads/<year>/<month>/<file>` — were
flattened to a single top-level folder: `wen-media/<file>`. Every reference across
every page (root pages, `posts/*.html`, and the `nav.js` templates) was updated
automatically, preserving each page's existing relative prefix (root pages: no
prefix; `posts/*.html`: `../`). No page needed manual editing.

Going forward, drop every downloaded/generated image or local HTML asset straight
into `wen-media/` (no year/month subfolders) and link to it as `wen-media/<file>`
from root pages or `../wen-media/<file>` from `posts/*.html`.

## Posts 2 & 3 fetched and paraphrased (2026-09-18)

`wns-w-token-2022-and-economic-solana-wen.html` and `south-korea-cbdc-and-tokenization.html`
were fetched live from wen-crypto.com (not user-pasted this time), so — per this repo's
copyright approach — they're **paraphrased in original wording**, not reproduced verbatim:
facts, structure, headers and sourcing are kept; sentences are rewritten. Each links back
to its source page on wen-crypto.com for the full bilingual (EN/KO) original. Both posts:
- use the shared header/footer via `nav.js` only (no header/footer markup embedded in the
  post file itself), same as post 1
- reference only already-established `wen-media/` filenames (`image.png`,
  `wen-wns-solana-jup-crypto.png`) — no new/invented filenames
- cross-link each other and the related key page (`token-2022-wns-solana-wen.html`)
- keep every cited source as a live external link instead of quoting source text

`index.html` already had summary cards and working links to both — no index changes were
needed. The `/page/2/` pointer for the rest of the original blog is also already in place
on the homepage's "More posts" section.

## Feed policy: index.html is the single growing feed, sorted by date (2026-09-18)

Going forward, **every known post — parsed or not — gets a card directly on `index.html`**,
not a plain link buried under "More posts". Cards are ordered by each post's own date,
**newest first**; this is a fixed rule, so when a new post is parsed there's no need to ask
where it goes — just insert its card in the correct chronological slot by date.

**Two card states:**
- **Parsed** (post exists as `posts/<slug>.html`): full card — title links to the local
  page, `<p class="meta">` shows the date, plus a figure/summary and a "read the post" link,
  same shape as the three done so far.
- **Pending** (post not parsed locally yet): lightweight card — title links straight to the
  original URL on wen-crypto.com (`target="_blank"`), and the meta line adds
  `· not yet parsed locally — opens on wen-crypto.com` after the date. No fabricated
  summary or image is added for a pending card until the real post is fetched.

When a pending post gets parsed into `posts/<slug>.html`, swap its card from the pending
shape to the parsed shape in place (same position — the date doesn't change) rather than
appending it at the end.

All currently known post URLs (see "Known post URLs" above) now have a card on the
homepage, in date order. The homepage's "More posts" section is now just the continuation
pointer to <https://wen-crypto.com/page/2/> for the rest of the ~60-post archive that
hasn't been enumerated yet.

Once most/all of the original ~60 posts are parsed, the flat single-page feed will likely
be broken up (e.g. paginated `index.html` / `index-2.html`, or per-year archives) so the
homepage doesn't grow unbounded — but that's a later, separate decision, not needed while
the count is still small.

## Going forward

Per your note: send 3 pages at a time (not 9) for both key pages and posts, so each
batch stays manageable and easy to review.

## Fixes and 5 more posts (2026-09-21)

**Bug found and fixed: broken media folder.** Every page already linked to `wen-media/<file>`
per the 2026-09-18 migration note, but the physical files were still sitting in the old
`wp-content/uploads/<year>/<month>/` folders, and no `wen-media/` directory existed at all —
so `wen-media/WNS_almanac_EN.html` and `wen-media/wen-resource-hub.html` (and every image
reference site-wide) were 404. Fixed by physically moving both real files into a flat
`wen-media/`, deleting `wp-content/`, and correcting their internal asset-path depth
(they'd kept the old 4-levels-deep `../../../../` prefix; now `../`, matching their new
1-level-deep location).

**Bug found and fixed: 6 known posts missing from the homepage feed.** Per the "feed
policy" rule (every known post gets a card, sorted by date), these were missing and have
been added as pending cards: `may-the-spirit-of-christmas-bring-you-an-unexpected-miracle-wen-cat`,
`wen-x-bonk-playground-drops-toysmak-3rs-partners`, `drop-001-wen-x-bonk-october-29-12-pm-et-2025`,
`wen-crypto-gears-up-for-global-expansion-partnership-with-elevate-pictures-signals-multimedia-revolution`,
`the-wen-crypto-usefulness-of-the-wns-standard-for-cryptocurrency-implementation`,
`wen-new-standard-wns-0-0-wen-crypto-inform`.

**5 more posts parsed** (fetched live from wen-crypto.com, so paraphrased per this repo's
copyright approach, not reproduced verbatim):
- `posts/how-sol-achieved-proven-global-recognition-2022-2026.html`
- `posts/ultimate-solana-token-2022-and-wen-compliance-and-testing.html`
- `posts/wen-crypto-token-gitgub-com-release-planning.html`
- `posts/may-the-spirit-of-christmas-bring-you-an-unexpected-miracle-wen-cat.html`
- `posts/catlumpurr-kaula-lumpur-malaysia-jan-31-to-feb-1-2026-video-about-event.html` (note:
  the live source has since moved to a different URL/date; this file keeps the original
  slug/date already used across this site's nav/footer/index links, for consistency)

Their homepage cards were swapped from the "pending" shape to the "parsed" shape in place,
per the feed policy (same position, date unchanged). 8 of the ~21 known posts are now
parsed locally; 13 remain pending (lightweight cards linking out to wen-crypto.com).

## 2 more posts + homepage stays self-contained (2026-09-22)

Two more posts parsed **verbatim** (per the site owner's own instruction: since the
content is their own authorship, it is reproduced as-is, not paraphrased — same
treatment as post 1):
- `posts/wen-cat-iq-wiki.html` (July 25, 2026)
- `posts/wen-token-network-re-examination.html` (June 23, 2026) — the same "20
  criteria / 10 anomalies" content also summarized inside `links-wen-cat.html` now
  also has its own standalone post page, cross-linked both ways.

Both slot into the homepage feed in correct date order, between
`ultimate-solana-token-2022-and-wen-compliance-and-testing` (Sep 2, 2026) and
`wen-crypto-token-gitgub-com-release-planning` (Jan 8, 2026). 10 of the ~23 known
posts are now parsed locally.

**Homepage no longer links out to wen-crypto.com for more posts.** The "More posts"
nav pointing to `https://wen-crypto.com/page/2/` was removed — this archive is meant
to stand on its own on GitHub, not funnel readers back to the original site. The
homepage now just states plainly that it shows everything currently known/archived.
Pending-card entries (posts not yet parsed) still link out to their wen-crypto.com
original individually — only the generic "go read more on the original site" nav
block was removed.

Images referenced by these two new posts (`roadmap-wen-cat.png`, `iq-wiki-wen.png`,
`wen-change-the-world.png`) follow the same `wen-media/<file>` convention as
everything else — not uploaded yet, no action needed until you say so.

## Full verbatim rebuild: WEN crypto token Gitgub.com Release Planning (2026-09-24)

The site owner supplied the original WordPress Gutenberg block export for this post.
Since this is the owner's own authored content, it's reproduced in full — every
image, the PDF embed, every GitHub issue/PR link, every list item, both preformatted
blocks (including the second one's duplicate content, kept as-is because it's how the
source page reads), the YouTube Shorts embed, and both trailing `<section>` blocks —
nothing summarized or trimmed. Only two kinds of changes were made:
- `wp-content/uploads/...` and `i0.wp.com/.../ssl=1` image/PDF paths → `wen-media/<file>`
  (same convention as the rest of the site; the `wen-media/` folder itself was left
  untouched, not recreated, so anything already placed there is undisturbed).
- Internal `wen-crypto.com/...` links → local paths (other posts as siblings inside
  `posts/`, key pages with a `../` prefix); every external link (GitHub, YouTube, X,
  SolanaFloor, Jupiter, Linktree, Google Drive, etc.) was left exactly as given.

The YouTube Shorts embed and the PDF are rendered as working `<iframe>`/`<object>`
elements pointing at local paths, using the site's existing CSS variables for styling
(no new stylesheet rules added, per "use strictly our styles"). This replaces the
earlier, shorter paraphrased version of this same post that existed before the owner
provided the original source.

## Session 2026-09-24: full-fidelity rebuild in progress

The site owner supplied the original WordPress Gutenberg source for 7 more posts,
asking for the same full-verbatim treatment as the GitHub release-planning post
(no summarizing, only `wp-content/uploads/...` → `wen-media/<file>` and internal
`wen-crypto.com/...` → local-path conversion; `wen-media/` itself untouched).

**Done this session:**
- Fixed the YouTube Shorts embed on `posts/wen-crypto-token-gitgub-com-release-planning.html`:
  it now scales to a responsive 480px-max width instead of being capped at 360px.
- `posts/wns-w-token-2022-and-economic-solana-wen.html` rebuilt in full: complete
  English article + the full Korean-language mirror section + the trailing
  "official links" block, exactly as supplied. Nothing summarized.
- `posts/solanas-wns-roadmap-how-a-meme-cat-poem.html` confirmed already complete
  from the first pass (built directly from the user's own pasted text originally).

**Still pending for the next batch** (owner asked for 3 pages at a time — this
queue is next in line), same full-verbatim treatment, sources already supplied:
- `posts/south-korea-cbdc-and-tokenization.html` (EN + KO mirror, code-diagram
  blocks, master source table)
- `posts/how-sol-achieved-proven-global-recognition-2022-2026.html` (fuller
  numbered-section version than the current file)
- `posts/ultimate-solana-token-2022-and-wen-compliance-and-testing.html` (table +
  reference embeds)
- `posts/wen-token-network-re-examination.html` (20-criteria table version, more
  complete than the current file)
- `posts/catlumpurr-kaula-lumpur-malaysia-jan-31-to-feb-1-2026-video-about-event.html`
  (Weremeow bio, YouTube embed, WNS 5-point list, multiple tiled image galleries)
- `posts/wen-cat-iq-wiki.html` — re-check against the exact supplied wording (the
  existing version is close but was written before the exact source was provided)

New `wen-media/` filenames introduced this session (all pending upload, following
the same convention as everything else): `image.png` (WNS/Token-2022/Korea hero).

## Session 2026-09-24 wrap-up: full-fidelity rebuild complete

All 7 posts the owner supplied original WordPress source for are now rebuilt with
full verbatim content (text, links, tables, code blocks, Korean-language mirror
sections where present) — nothing summarized:

- `posts/wen-crypto-token-gitgub-com-release-planning.html` ✓ (YouTube embed width fixed: responsive up to 480px)
- `posts/wns-w-token-2022-and-economic-solana-wen.html` ✓ (EN + full KO mirror + trailing links block)
- `posts/solanas-wns-roadmap-how-a-meme-cat-poem.html` ✓ (already complete from an earlier session)
- `posts/south-korea-cbdc-and-tokenization.html` ✓ (EN + full KO mirror, ASCII diagram in both languages, master source table)
- `posts/how-sol-achieved-proven-global-recognition-2022-2026.html` ✓ (full numbered-section version)
- `posts/ultimate-solana-token-2022-and-wen-compliance-and-testing.html` ✓ (comparison table + reference links)
- `posts/wen-token-network-re-examination.html` ✓ (full 20-row criteria table, 10 anomalies, official-links directory)
- `posts/catlumpurr-kaula-lumpur-malaysia-jan-31-to-feb-1-2026-video-about-event.html` ✓ (Weremeow bio, YouTube embed, WNS 5-point list, two full image galleries — 8 + 12 images)
- `posts/wen-cat-iq-wiki.html` — verified against the exact supplied source; already matched closely from the prior session.

**Filename collision flagged:** two different source images were both named `image.png`
by WordPress (one under `2026/06/` for the Korea/Token-2022 post, one under `2025/12/`
for the Catlumpurr "W coin" graphic). To keep `wen-media/` flat without overwriting,
the Catlumpurr one was renamed to `image-w-coin.png` in this repo — when uploading,
put the Korea-post hero image at `wen-media/image.png` and the "W coin Wen coin Wen
crypto" graphic at `wen-media/image-w-coin.png`.

Homepage cards for GitHub-release-planning and Catlumpurr updated to match the
posts' exact final titles.

## Gallery fix + wen-media.html showcase page (2026-09-25)

**Tiled galleries fixed.** The two image grids on the Catlumpurr post used
`height:auto`, so tiles ended up different heights depending on each image's own
aspect ratio (matches the screenshot the owner sent). Fixed by making the shared
`gallery()` builder produce a strict square grid: every tile is `aspect-ratio:1/1`
with `object-fit:cover`, and each tile is a plain `<a href="wen-media/<file>"
target="_blank">` wrapping the `<img>` — clicking opens the original file directly
(no lightbox script), so what a search engine or a person sees on click is the same
original image seen in the tile.

**New page: `wen-media.html`.** A single showcase gallery of every image/gif used
anywhere on the site, same square-tile treatment, each tile linking to its file.
It reads `wen-media/manifest.json` (a plain JSON array of filenames) via `fetch()`
and renders one tile per entry, so the page needs no rebuild when files are added —
only that filename needs to land in `manifest.json`. A tile for a file that hasn't
been uploaded yet gracefully falls back to showing its expected filename instead of
a broken-image icon. **Important limitation, stated plainly:** no static site can
truly list a folder's contents by itself — this page cannot auto-discover new files
sitting in `wen-media/` without their name being added to `manifest.json` first.
`manifest.json` currently lists all 42 images/gifs already referenced across the
site; add a line for anything new.

Not linked from the sidebar/footer nav (nav.js untouched) — it's a utility page,
reachable directly at `/wen-media.html`.

## Media converted to compressed JPEG (2026-09-26)

All images in `wen-media/` were converted (png/jpg/jpeg/gif → compressed `.jpeg`) and
committed to GitHub by the owner. Every image reference across the site was updated:
**only the extension changed to `.jpeg`; base filenames were left untouched.**
PDF and HTML attachments (`WNS_almanac_EN.html`, `wns-standart-...pdf`, etc.) keep their
own extensions.

**Standing rule for all future posts:** when writing an image reference, keep the
original WordPress base filename exactly and just use `.jpeg` as the extension.
(One correction made: `wen-gif-0003-@alexwoogo-@olegt39484998.jpeg` — the real name
contains `@` characters, which an earlier build had dropped.)

**`wen-media.html` fixed.** It previously loaded `manifest.json` with `fetch()`, which
browsers block when a page is opened straight from disk ("Could not load
manifest.json"). The full list of 599 real image filenames is now embedded directly in
the page's own script, so it works identically from disk or online. To add a new image
to the gallery, add its filename to the `FILES` array at the bottom of `wen-media.html`.
`wen-media/manifest.json` was regenerated with the same 599 names (kept for reference;
the page no longer depends on it).

**References on the site with no matching real file** (placeholder names I invented
before the real list existed — need the owner's mapping, not guessed):
- `wen-media/image-w-coin.jpeg` (Catlumpurr post, the "W coin Wen coin Wen crypto"
  graphic — the real file is probably one of `image-1…image-8.jpeg`)
- `wen-media/wen-next-bluechip-memecoin.jpeg` (about.html; likely
  `analitycs-wen-coin-official-cost-prediction.jpeg`, which carries the same caption)
- `wen-media/wen-poem-first-nft-wns.jpeg` (links-wen-cat.html)
Also present in `wen-media/` but not yet used/linked: `WNS_roadmap_EN.html`,
`token2022-korea-flow-wns-wen-sol.html`.
