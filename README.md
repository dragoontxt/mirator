# Adding a story

1. Write your story as a markdown file inside `stories-source/`. Filename doesn't matter, just end it in `.md`.
2. Run `node build.js` from this folder.
3. Done — your story's page(s) are in `stories/`, and `stories.html` (the Stories index) is automatically updated to link to it under the right fandom heading.

That's the whole workflow. No other files need to be touched by hand.

## One-shot format

```
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

## Multi-chapter format

Add `chapters: true`, then split the body with `## Chapter Title | Date` headings.
For a chapter that hasn't been posted yet, just leave the date off:

```
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

Each posted chapter gets its own page with working prev/next navigation. Unposted chapters just show up as a dimmed, unclickable circle in the chapter list.

## Fields

- **status**: `complete` or `in progress`
- **tags**: comma-separated, any of: `new, gen, fluff, pwp, angst, lime, lemon, grapefruit, xxx, oc`
  (fluff / angst / lime / lemon / grapefruit show with their icon; the rest are plain text)

## Re-running the build

Safe to run `node build.js` as many times as you want — it fully regenerates every story page and the Stories index from whatever's currently in `stories-source/` each time. If you edit an existing story's markdown file and re-run, its page and index entry both update to match.

## Porting stories in from AO3 (ao3downloader, etc.)

If you're bringing stories over from AO3 as downloaded HTML files, use `ao3-to-markdown.js` to convert one into the markdown format above automatically:

```
node ao3-to-markdown.js path/to/downloaded-work.html
```

This writes a `.md` file straight into `stories-source/`, pulling the title, fandom, summary, chapter structure, and body text out of the HTML for you.

**Important — check the output before running `build.js`:**
- The `tags:` line is left blank on purpose. AO3's freeform tags get dropped into a comment right below the frontmatter so you can see them, but mapping them to this site's fluff/angst/lime/lemon/grapefruit/etc. vocabulary is a judgment call the script won't try to make for you.
- For multi-chapter works, each chapter heading gets `REPLACE-WITH-DATE` where a real date needs to go — the script has no way to know when each chapter was actually posted.
- **This was built against AO3's standard HTML export structure**, not tested against an actual ao3downloader output file. Run it on one story first, check the result carefully, and if anything's parsed wrong (title, chapters, tags all worth double-checking), share the source HTML and it can get fixed to match exactly rather than you working around it by hand.
