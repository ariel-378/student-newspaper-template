# Student Newspaper Platform

A framework-free (vanilla HTML/CSS/JS) website for a student newspaper — section
pages, articles, sports, videos, puzzles & games, search, and an in-app
**editor dashboard**. No build step, no dependencies.

**▶ Live demo: <https://ariel-378.github.io/student-newspaper-template/>**

The demo runs in standalone mode with no host platform behind it, so you can
open the editor yourself: use the **"Editor preview"** link in the account bar,
top right. Changes you make are saved to your own browser and visible only to
you — click **Reset demo data** in the dashboard to put it back.

## Highlights

- **Editor dashboard** — create and edit articles, and manage staff, sports, ads,
  videos, and the puzzles & games pages.
- **Editor-managed sections** — add, rename, reorder, and remove sections, and
  choose which section fills each home-page slot. The nav, section pages, home
  page, and search all update automatically.
- **Rearrange any page in place** — signed in as an editor, every page has a
  *Edit layout* toggle: drag its blocks into new rows and columns, or move them
  with the keyboard. Article pages, the video index, staff, search, tags, team
  pages and the centerspread all included. Each page keeps its own layout.
- **Brand config** — one file (`config.js`) sets the masthead, school, colors,
  logo, and footer across every page.
- **Host-ready auth** — designed to sit behind a platform such as Finalsite, which
  provides login and decides who is an editor.

## Sample content

The repo ships with a demo newsroom so a fresh copy looks like a working paper
rather than an empty page: eleven stories, three teams with brackets, two
videos, four sidebar ads, and flat SVG illustrations standing in for photos.

**All of it is invented** — East High School, The Wildcat Times, every byline,
every person quoted, every score. None of it refers to a real school or a real
person. To start clean, empty the objects in `articles.js`, `teams.js`,
`videos.js` and `ads.js`; each file says so at the top.

## Tests

```bash
npm install   # once — pulls jsdom, the only dependency
npm test
```

856 checks across 17 suites: every page loads clean, every editor control is
pressed without throwing, and content added in the editor reaches the reader
pages. See [tests/README.md](tests/README.md).

## Run it locally

No build step and nothing to install:

```bash
npm run serve      # http://localhost:8781
```

`serve.py` sends no-cache headers, so a reload always shows your latest edit.
Pass a port if you want a specific one (`npm run serve 9000`); with no argument
it steps past a busy port rather than failing, which is what lets a second copy
of the site run alongside the first.

Any static server works just as well — `python3 -m http.server 8000` and open
`http://localhost:8000`. Opening the files directly with `file://` does not:
every editor change is kept in `localStorage`, which browsers restrict on
`file://` origins, so the dashboard cannot save.

With no host platform present, the site runs in **demo mode** — use the
**"Editor preview"** link in the account bar to open the dashboard. Editor changes
persist only in your browser's `localStorage`.

### Dashboard controls

Inside the editor dashboard, the toolbar has three buttons:

- **+ New Article** — create a new article.
- **Reset all changes** — discard your article edits and restore the original articles.
- **Reset demo data** — clear **all** saved changes in this browser (articles,
  sections, brand, layout, videos, sports, etc.) and restore the shipped content.

Because editor changes are saved to `localStorage` and override the shipped files,
if the demo ever shows stale content, click **Reset demo data** (or open the site
in a private window) to get back to the shipped version.

## Documentation

- **[FINALSITE.md](FINALSITE.md)** — how the site integrates with Finalsite: the
  identity contract (`WL_CONTEXT`), the **editors-group logic**, and a phased plan
  for hosting, authentication, and content persistence.
- **[CUSTOMIZE.md](CUSTOMIZE.md)** — rebrand the paper for your school (the Brand
  design tab, or editing `config.js`).
- **[EDITORIAL.md](EDITORIAL.md)** — who publishes, how corrections work, when a
  story comes down, and who holds the accounts. The half of running a paper that
  isn't software.

## Project layout

| Path | Purpose |
|------|---------|
| `*.html` | Pages — public surfaces plus the `editor*.html` dashboard |
| `config.js` | Brand config (`WL_CONFIG`); the only per-school file |
| `articles.js`, `writers.js`, `teams.js`, … | Content sources (`window.WL_*`) |
| `*-store.js` | CRUD / data layer — the seam for server-backed persistence |
| `auth.js` | Identity adapter (`window.WLAuth`; reads `WL_CONTEXT`) |
| `nav.js`, `brand.js`, `section.js`, … | Shared rendering |

## Licence

[MIT](LICENSE) — take it, rename it, run your own paper on it. No attribution
required in the site itself, though a line in your colophon is welcome.

The sample content is invented (East High School, The Wildcat Times, every
byline and score) and is covered by the same licence. Real student journalism
lives in each school's own deployment, not here.
