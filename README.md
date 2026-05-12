# manleviet.github.io

Personal academic website of **Viet-Man Le** — PhD candidate at TU Graz, Austria, working on knowledge-based diagnosis, configuration systems, and explanations in AI.

Live site: **<https://manleviet.github.io>**

## Stack

- [Jekyll](https://jekyllrb.com/) static site generator, built and deployed by **GitHub Pages** (vanilla pipeline — no GitHub Actions needed)
- Plugins: `jekyll-remote-theme`, `jekyll-seo-tag` (both in GH Pages whitelist)
- Theme: customized fork of the [Researcher](https://github.com/ankitsultana/researcher) Jekyll theme — see [Credits](#credits) below.

## Pages

| File | URL | Content |
|---|---|---|
| `index.md` | `/` | About + bio + News + Featured publications |
| `research.md` | `/research.html` | Research interests + ongoing projects |
| `publications.md` | `/publications.html` | Selected publications + theses |
| `service.md` | `/service.html` | Academic service (reviewing, organizing, chairing) |
| `teaching.md` | `/teaching.html` | Courses taught + thesis supervision |
| `awards.md` | `/awards.html` | Awards & grants |
| `assets/pdf/cv.pdf` | `/CV` | Full CV (PDF) |

## Local development

```bash
bundle install
bundle exec jekyll serve
```

The site renders at `http://localhost:4000`. Edit any `.md` file and Jekyll regenerates on save.

## Features customized in this fork

- **Dark / light mode toggle.** Sun/moon button in the navbar (right of the social icons). Honors `prefers-color-scheme` on first visit; the user's explicit choice persists via `localStorage` and overrides the OS preference thereafter. An inline boot script in `<head>` sets the theme attribute *before* `<body>` renders to prevent a flash of the wrong theme.
- **Theme palette.** GitHub Primer "dimmed" family for dark mode (warmer neutral gray, not slate). All color tokens live as CSS custom properties on `:root` (light) and inside `@mixin dark-palette` (dark), applied to both `[data-theme="dark"]` and `@media (prefers-color-scheme: dark)`. Defined in `_sass/vars.scss`.
- **Social-icons header.** Email, Google Scholar, ORCID, GitHub, LinkedIn rendered as FontAwesome icons in the navbar (right side), replacing the upstream template's plain text links.
- **Hand-curated `.pub` cards** in `publications.md`. Each card carries venue/ranking annotations (CORE A*, SCIMAGO Q2, etc.). Year sections are grouped under `### YEAR` headings inside `<div markdown="1" class="pubs"> … </div>` wrappers.
- **External-link auto-targeting.** A small script in `_layouts/default.html` adds `target="_blank" rel="noopener noreferrer"` to every off-domain link at `DOMContentLoaded`.

## Adding a new publication

Edit `publications.md` and append a card under the right year section:

```html
<div class="pub" markdown="1">
**[Paper Title](URL){:target="_blank"}**

**Viet-Man Le**, Co-author 1, Co-author 2

*Venue full name*, vol. X, pp. Y. **CORE A*** (Year)
</div>
```

If the year section doesn't exist yet, create it before the next-newer section:

```html
### YYYY

<div markdown="1" class="pubs">

  ...cards here...

</div>
```

## Credits

This site is a customized fork of:

- [Ruben Branco's personal site](https://github.com/RubenBranco/rubenbranco.github.io), which itself customizes
- The [Researcher Jekyll theme](https://github.com/ankitsultana/researcher) by [Ankit Sultana](http://ankitsultana.com) — *"A clean, single-column, monospace resume template built for Jekyll"* — originally derived from
- [bk2dcradle/researcher](https://github.com/bk2dcradle/researcher).

The Researcher theme provides the underlying single-column layout, the Inconsolata monospace typography, and the configuration conventions (`_config.yml` keys: `title`, `tagline`, `nav`, `tracking_id`, `favicon`, `ins_logo`, `footer`, etc.). For the upstream README and theme-level customization options, see the [Researcher repository](https://github.com/ankitsultana/researcher#readme).

## License

[GNU GPL v3](https://github.com/bk2dcradle/researcher/blob/gh-pages/LICENSE) — inherited from upstream.
