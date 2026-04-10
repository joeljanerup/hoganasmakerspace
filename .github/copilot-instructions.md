# Copilot Instructions – Höganäs Makerspace

This is a Jekyll-based GitHub Pages website for the non-profit association **Höganäs Makerspace**.
All visible content is in **Swedish**. All code, filenames, front matter keys, and YAML keys are in **English**.

---

## Project overview

- **Theme**: [Forty by andrewbanchich](https://github.com/andrewbanchich/forty-jekyll-theme) (Jekyll port of Forty by HTML5 UP)
- **Deployment**: GitHub Pages via GitHub Actions (`.github/workflows/github-pages.yml`)
- **Local preview**: Docker — `bretfisher/jekyll-serve`, volume mount at `/site`
- **Base URL**: empty string `""` (org-level GitHub Pages repo)

---

## File structure

```
hoganasmakerspace/
├── .github/
│   ├── copilot-instructions.md   # This file
│   └── workflows/
│       └── github-pages.yml      # Auto-deploy to GitHub Pages on push to main
├── _data/
│   └── annual_meetings.yml       # Data for Årsmöten page (years + PDF paths)
├── _includes/
│   ├── footer.html               # Social icons (Facebook + Instagram only), JS scripts
│   └── header.html               # Logo link + hamburger nav menu (sorted by nav-order)
├── _layouts/                     # Page templates (rarely changed)
├── _sass/                        # Styles (rarely changed)
├── assets/
│   ├── images/                   # Theme images (pic01.jpg – pic11.jpg + custom)
│   └── pdfs/                     # Annual meeting PDFs, organised by year
│       ├── 2022/
│       ├── 2023/
│       ├── 2024/
│       ├── 2025/
│       └── 2026/
├── _config.yml                   # Site-wide settings: name, socials, address, SEO
├── index.md                      # Home page (layout: home)
├── om.md                         # About page – equipment, rules, address, contact, sponsors
├── bli-medlem.md                 # Membership page – two membership types + registration
├── styrelse.md                   # Board members page – full board table
├── stadgar.md                    # Statutes page – §1–§6
├── arsmoten.md                   # Annual meetings page (data-driven from _data/)
├── kontakt.md                    # Legacy page (hidden from menu)
├── robots.txt                    # SEO robots file
└── README.md                     # Swedish maintenance guide (MUST be kept up to date)
```

---

## Pages and menu

Pages are Markdown files in the root. The navigation menu is controlled entirely by front matter:

| Front matter key | Purpose |
|-----------------|---------|
| `nav-menu: true` | Include page in the hamburger menu |
| `nav-order: N`   | Sort position in menu (lower = earlier) |
| `show_tile: true` | Show page as a tile on the home page |

**Current menu order:**

| nav-order | Page file    | Swedish title |
|-----------|-------------|---------------|
| –         | index.md    | Hem           |
| 2         | om.md       | Om oss        |
| 3         | bli-medlem.md | Bli medlem  |
| 4         | styrelse.md | Styrelse      |
| 5         | stadgar.md  | Stadgar       |
| 6         | arsmoten.md | Årsmöten      |

The header template (`_includes/header.html`) sorts nav pages using:
```liquid
{% assign nav_pages = site.html_pages | where_exp: "item", "item.nav-menu == true and item.layout != 'home'" | sort: "nav-order" %}
```

---

## Theme Colors

The site uses a **Swedish/Nordic color palette** defined in `_sass/libs/_vars.scss`:

| Color | Hex | Usage |
|---|---|---|
| Mörkbrun (Dark Brown) | #4A3B29 | Backgrounds |
| Krämvit (Cream White) | #F3EFE7 | Text, foreground |
| Tegelröd (Brick Red) | #9E6C54 | Highlights, links, buttons |

**To change colors:** Edit `_sass/libs/_vars.scss` and update the `$palette` map. All theme colors will update automatically.

**To revert:** Uncomment the original palette block at the end of `_sass/libs/_vars.scss`.

See `THEME_COLORS.md` for detailed instructions.

`_data/annual_meetings.yml` drives `arsmoten.md`. Structure per year:

```yaml
- year: 2026
  documents:
    invitation:          assets/pdfs/2026/kallelse.pdf
    activity_report:     assets/pdfs/2026/verksamhetsberattelse.pdf
    business_plan:       assets/pdfs/2026/verksamhetsplan.pdf
    selection_committee: assets/pdfs/2026/valberedningens-forslag.pdf
    protocol:            assets/pdfs/2026/protokoll.pdf
```

Set a document to `pending` if it is expected but not yet uploaded (shown as greyed-out "Kommer snart").
Set it to `null` (or omit the key) if the document simply doesn't exist for that year — it will be hidden entirely.
New years go **at the top** of the file (newest first). PDF files go in `assets/pdfs/YYYY/`.

**Three document states:**

| YAML value  | Rendered as                       |
|-------------|-----------------------------------|
| File path   | Clickable link                    |
| `pending`   | Greyed-out document name (no link, no suffix) |
| `null`      | Hidden — not shown at all         |

---

## Key technical details

- **`relative_url` is mandatory** for all asset `src`/`href` attributes and JS script tags. Never use `absolute_url` — it breaks local preview because it resolves to the production URL.
- **SEO**: `jekyll-seo-tag` and `jekyll-sitemap` are active. Use `{% seo title=false %}` in `head.html` to avoid duplicate `<title>` tags.
- **`_config.yml` changes** require a Docker container restart to take effect locally.
- **Social links**: Only Facebook and Instagram are configured. No Twitter/X or other platforms.
- **No contact form** — the footer contact section has been removed.

---

## README maintenance rules

`README.md` is the **Swedish-language maintenance guide** for non-technical editors of this site.
It must always reflect the current state of the project.

**Update `README.md` whenever you:**
- Add, rename, or remove a page (`.md` file)
- Change the menu order or `nav-order` values
- Add a new PDF year folder under `assets/pdfs/`
- Change the data structure of `_data/annual_meetings.yml`
- Change how `header.html` or `footer.html` works in a user-visible way
- Add or remove front matter keys that editors need to know about
- Change the `_config.yml` fields documented in the README

**Sections to check in README.md:**
1. **Projektstruktur** — file tree must match actual files
2. **Sidhuvud (front matter)** — must list all relevant keys with current descriptions
3. **Aktuell menyordning** — table must match actual `nav-order` values across all pages
4. **Lägga till ett nytt menyval** — template must include all required front matter keys
5. **Hantera årsmöten och PDF-filer** — must reflect actual YAML structure and folder layout

---

## Coding conventions

- All code, filenames, and YAML/front matter keys: **English**
- All visible text content: **Swedish**
- Use `relative_url` for all internal links and asset paths
- Follow existing HTML structure within `_includes/` when making layout changes
- Do not add new Jekyll plugins without also updating `Gemfile` and `_config.yml` under `plugins:`
