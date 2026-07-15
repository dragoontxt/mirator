<div align="center">
  <img src="./mirator-banner.svg" alt="mirator — stories written with love and angst, from the human heart and mind" width="640">

  <p><em>lat. <strong>mirator</strong>, noun — one who gazes, one who admires.</em></p>

  [![site](https://img.shields.io/badge/site-mirator.amor--omnia.org-B03039?style=flat-square)](https://mirator.amor-omnia.org)
  [![status](https://img.shields.io/badge/status-quietly%20updated-e8475a?style=flat-square)](#)
  [![built with](https://img.shields.io/badge/built%20with-node-e0a030?style=flat-square)](#)

</div>

<br>

**mirator** is a small, hand-kept archive of fanfiction and original fiction — no algorithm, no feed, no follower count. This repo is the source for [mirator.amor-omnia.org](https://mirator.amor-omnia.org).

<br>

## color palette

*Mirator* — the one who gazes, who admires — is a word for looking at something so long you stop noticing you're doing it. The palette follows: candlelight and old wine, nothing bright enough to break the spell. Sampled directly from the site's own `:root` (identical across every page):

| swatch | name | hex | used for |
|---|---|---|---|
| ![#221014](https://img.shields.io/badge/-%23221014?style=flat-square&color=221014) | ink | `#221014` | `--bg` |
| ![#2f171a](https://img.shields.io/badge/-%232f171a?style=flat-square&color=2f171a) | wax | `#2f171a` | `--panel` |
| ![#B03039](https://img.shields.io/badge/-%23B03039?style=flat-square&color=B03039) | claret | `#B03039` | `--red` |
| ![#e8475a](https://img.shields.io/badge/-%23e8475a?style=flat-square&color=e8475a) | rose | `#e8475a` | `--pink` |
| ![#e0a030](https://img.shields.io/badge/-%23e0a030?style=flat-square&color=e0a030) | candlelight | `#e0a030` | `--gold` |
| ![#f2e2dc](https://img.shields.io/badge/-%23f2e2dc?style=flat-square&color=f2e2dc) | parchment | `#f2e2dc` | `--cream` |
| ![#d8bcb8](https://img.shields.io/badge/-%23d8bcb8?style=flat-square&color=d8bcb8) | dust | `#d8bcb8` | `--text-dim` |

```css
:root{
  --bg:#221014; --panel:#2f171a; --red:#B03039; --pink:#e8475a;
  --gold:#e0a030; --cream:#f2e2dc; --text-dim:#d8bcb8;
}
```

<br>

## adding a story

Write markdown into `stories-source/`, then `node build.js`. Regenerates every story page + the index. Safe to re-run anytime.

Chapters: add `chapters: true`, split body with `## Chapter Title | Date`. Leave the date off an unposted chapter and it shows dimmed in the nav.

`tags:` → `new, gen, fluff, pwp, angst, lime, lemon, grapefruit, xxx, oc`

**AO3 import:** `node ao3-to-markdown.js path/to/work.html` → writes into `stories-source/`. Tags and chapter dates aren't guessed — check the output before building.
