<div align="center">
  <img src="mirator-wordmark.svg" alt="mirator — stories written with love and angst, from the human heart and mind" width="640">

  <p><em>lat. <strong>mirator</strong>, noun — one who gazes, one who admires.</em></p>

  [![site](https://img.shields.io/badge/site-mirator.amor--omnia.org-B03039?style=flat-square)](https://mirator.amor-omnia.org)
  [![status](https://img.shields.io/badge/status-quietly%20updated-e8475a?style=flat-square)](#)
  [![built with](https://img.shields.io/badge/built%20with-node-e0a030?style=flat-square)](#)
  [![license](https://img.shields.io/badge/license-see%20credits-f2e2dc?style=flat-square&labelColor=2f171a)](credits.html)

</div>

<br>

**mirator** is a small, hand-kept archive of fanfiction and original fiction — no algorithm, no feed, no follower count. Just a shoebox of stories with a wax seal on the lid, meant to be opened slowly.

This repo is the source for [mirator.amor-omnia.org](https://mirator.amor-omnia.org): static HTML pages, a tiny Node build script, and a folder of markdown where every story starts its life before it's set out on the shelf.

<br>

## what's here

```
.
├── index.html                  # home — recently shelved stories
├── stories.html                # full index, generated, do not hand-edit
├── stories/                    # generated story pages, one per work
├── stories-source/              # ← you write your stories here
├── the-lighthouse-keeper.html   # example: single-chapter original work
├── salt-and-static.html         # example: multi-chapter work
├── purpose.html                 # the "why" of the archive
├── dltr.html                    # the short version, for the impatient
├── credits.html                 # fonts, fics, thanks
├── build.js                     # turns stories-source/*.md into pages
├── ao3-to-markdown.js            # pulls an AO3 export into the format below
└── assets/
    └── mirator-wordmark.svg      # the banner up top
```

Everything with a heartbeat lives in `stories-source/`. Everything else — `stories.html`, individual story pages, prev/next chapter links — is generated. Don't hand-edit generated files; they'll just be overwritten on the next build.

<br>

## adding a story

1. Write your story as a markdown file inside `stories-source/`. Filename doesn't matter, just end it in `.md`.
2. Run:
   ```
   node build.js
   ```
3. Done. Your story's page(s) land in `stories/`, and `stories.html` updates itself to link it under the right fandom heading.

No other files need to be touched by hand.

<br>

### one-shot format

```yaml
---
title: The Lighthouse Keeper
fandom: Original work
status: complete
tags: fluff, angst, gen
summary: Every year she swore she wouldn't come back to the lighthouse.
---
First paragraph.

Second paragraph.
```

### multi-chapter format

Add `chapters: true`, then split the body with `## Chapter Title | Date` headings. For a chapter that hasn't posted yet, leave the date off:

```yaml
---
title: Salt and Static
fandom: Final Fantasy XIV
status: in progress
tags: fluff, gen
summary: Every station has a frequency nobody else can hear.
chapters: true
---
## static on the frequency | June 2
First chapter's text.

## everything the radio couldn't say | June 14
Second chapter's text.

## coming soon
(leave this empty until it's actually posted, then add the date and fill it in)
```

Each posted chapter gets its own page with working prev/next navigation. Unposted chapters show up as a dimmed, unclickable circle in the chapter list — a promise, not a page yet.

<br>

## fields

| field | notes |
|---|---|
| `status` | `complete` or `in progress` |
| `tags` | comma-separated: `new, gen, fluff, pwp, angst, lime, lemon, grapefruit, xxx, oc` — `fluff` / `angst` / `lime` / `lemon` / `grapefruit` render with their own little icon; the rest stay plain text |

<br>

## re-running the build

`node build.js` is safe to run as many times as you like — it fully regenerates every story page and the Stories index from whatever currently lives in `stories-source/`. Edit an existing story's markdown and re-run, and its page *and* its index entry both update to match.

<br>

## porting stories in from AO3

If you're bringing stories over from AO3 (e.g. via `ao3downloader`) as saved HTML files, convert them automatically:

```
node ao3-to-markdown.js path/to/downloaded-work.html
```

This writes a `.md` file straight into `stories-source/`, pulling the title, fandom, summary, chapter structure, and body text out of the HTML for you.

**Check the output before running `build.js`:**

- `tags:` is left blank on purpose. AO3's freeform tags get dropped into a comment below the frontmatter so you can see them, but mapping them onto this site's fluff / angst / lime / lemon / grapefruit vocabulary is a judgment call the script won't make for you.
- For multi-chapter works, each chapter heading gets `REPLACE-WITH-DATE` where a real date needs to go — the script has no way to know when a chapter actually posted.
- This was built against AO3's standard HTML export structure, not tested against an actual `ao3downloader` output file. Run it on one story first and check the result carefully — title, chapters, and tags are all worth double-checking. If something parses wrong, share the source HTML and it can get fixed to match exactly, rather than working around it by hand.

<br>

## the shape of it

The whole site runs on the same handful of design pieces, reused page to page: a pixel wax-seal envelope as the mark and favicon, tape-card story listings with a torn-corner heart, a `Dancing Script` / `Alex Brush` pairing for anything that should feel handwritten, and `Press Start 2P` for anything that should feel stamped.

<br>

## color palette

*Mirator* — the one who gazes, who admires — is a word for looking at something so long you stop noticing you're doing it. The palette is built the same way: no bright, attention-grabbing color anywhere. Everything sits in candlelight and old wine, like a letter read by one lamp, long after everyone else has gone to bed.

Every value below is sampled directly from the site's own `:root` block (identical across all seven pages) — this isn't a proposed theme, it's the one already in production:

| swatch | name | hex | used for |
|---|---|---|---|
| ![#221014](https://img.shields.io/badge/-%23221014?style=flat-square&color=221014) | ink | `#221014` | `--bg` — the page itself, near-black wine |
| ![#2f171a](https://img.shields.io/badge/-%232f171a?style=flat-square&color=2f171a) | wax | `#2f171a` | `--panel` — cards, envelopes, anything raised off the page |
| ![#B03039](https://img.shields.io/badge/-%23B03039?style=flat-square&color=B03039) | claret | `#B03039` | `--red` — card borders, the deepest accent |
| ![#e8475a](https://img.shields.io/badge/-%23e8475a?style=flat-square&color=e8475a) | rose | `#e8475a` | `--pink` — titles, hearts, the color that does most of the talking |
| ![#e0a030](https://img.shields.io/badge/-%23e0a030?style=flat-square&color=e0a030) | candlelight | `#e0a030` | `--gold` — small warm details, the one note that isn't red or neutral |
| ![#f2e2dc](https://img.shields.io/badge/-%23f2e2dc?style=flat-square&color=f2e2dc) | parchment | `#f2e2dc` | `--cream` — primary text, envelope paper |
| ![#d8bcb8](https://img.shields.io/badge/-%23d8bcb8?style=flat-square&color=d8bcb8) | dust | `#d8bcb8` | `--text-dim` — body copy, everything quieter than a title |

```css
:root{
  --bg:       #221014;   /* ink */
  --panel:    #2f171a;   /* wax */
  --red:      #B03039;   /* claret */
  --pink:     #e8475a;   /* rose */
  --gold:     #e0a030;   /* candlelight */
  --cream:    #f2e2dc;   /* parchment */
  --text-dim: #d8bcb8;   /* dust */
}
```

This is copy-pasted verbatim from every page's `<style>` block — if you're touching the theme, that one block is the single place to do it.

<br>

## why it exists

> This archive exists because [blank]. It's built by hand, kept simple on purpose, and meant to feel like flipping through a shoebox of letters rather than browsing a platform. Nothing here is trying to grow, trend, or convert — it's just a place for stories to live.

The long version is on [`purpose.html`](purpose.html); the short version is on [`dltr.html`](dltr.html).

<br>

<div align="center">
  <sub>made with &hearts; by hand, one pixel at a time</sub>
</div>
