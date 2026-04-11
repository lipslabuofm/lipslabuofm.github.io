# LIPS Lab website

Static site for the **Language and Information Processing (LIPS) Lab** at the University of Memphis. It is built with **[Jekyll](https://jekyllrb.com/)**, styled with Bootstrap (via SCSS) and a custom theme in `_sass/_lips-theme.scss`.

---

## Repository layout (what each folder does)

| Path | Purpose |
|------|--------|
| **`_config.yml`** | Global site settings: `title`, `description`, `url`, `baseurl`, email, Markdown/Kramdown options. **Change `url` and `baseurl` when you move the site to a new GitHub account or repo name.** |
| **`_pages/`** | One Markdown file per public page (front matter + body or includes). Jekyll turns these into HTML. |
| **`_layouts/`** | HTML shells: `default` wraps header/footer; pages pick a layout (`homelay`, `gridlay`, `textlay`, `contactlay`, etc.). |
| **`_includes/`** | Reusable HTML fragments included with `{% include ... %}`. |
| **`_data/`** | YAML data files (`*.yml`). Edited like spreadsheets in text form; Liquid loops read them on the site. |
| **`_sass/`** | SCSS partials; the LIPS look-and-feel lives mainly in **`_sass/_lips-theme.scss`**. |
| **`css/main.scss`** | Entry point: imports Bootstrap + `lips-theme`, plus a few global rules. Jekyll compiles this to `css/main.css`. |
| **`images/`** | Photos and logos (e.g. `lab.jpg` hero, `images/teampic/` for team headshots, affiliation logos). |
| **`js/`** | Bootstrap and other scripts loaded from the footer. |

Built output goes to **`_site/`** when you run `jekyll build` (do not commit `_site/`).

---

## Main navigation (what visitors see)

The top menu is defined in **`_includes/header.html`**: Home, Team, Research, Publications, Contact.

---

## Page-by-page content

### Home (`/`)

- **Layout:** `_layouts/homelay.html` — full-width hero (image, title, lead, buttons) then page content.
- **Page file:** `_pages/home.md` (permalink `/`).
- **Contains:**
  - Intro paragraphs (Markdown in `home.md`).
  - **Research focus** band: `_includes/research-focus-home.html` → data from **`_data/research_areas_home.yml`** (cards, emojis, tags, gradients `g1`–`g6`).
  - **Affiliations** band: `_includes/affiliations-home.html` — hard-coded three cards; images under `images/` (`cs-department-logo.png`, `fitlogo.png`, `iis-logo.png`).

**To edit:** hero text/buttons → `homelay.html`; intro copy → `home.md`; focus cards → `research_areas_home.yml` + optional class tweaks in `_lips-theme.scss`; affiliation copy/images → `affiliations-home.html` + `images/`.

---

### Team (`/team/`)

- **Layout:** `gridlay` (Bootstrap grid wrapper for the main column).
- **Page file:** `_pages/team.md`.
- **Contains:** Section titles and structure in `team.md`; each person is rendered with **`_includes/team-card.html`**.
- **Data:**
  - **`_data/team_members.yml`** — current members. `category: pi` = Principal Investigator block; any other `category` (e.g. `phd`) = PhD Students block. Fields used include `name`, `role`, `bio` (shown for PI), `photo` (filename under `images/teampic/`), `email`, `website`, `scholar`, `linkedin`, `tags` (PI), optional `education1`…`education3`.
  - **`_data/alumni_members.yml`** — Alumni section (same card template with `alumni=true`).

**To edit:** section headings/intro → `team.md`; people → the YAML files; card layout/links → `team-card.html`; styling → `_lips-theme.scss` (search for `team-page`, `team-card`).

---

### Research (`/research/`)

- **Layout:** `textlay`.
- **Page file:** `_pages/research.md` — only includes **`_includes/research-page.html`**.
- **Contains:** Page title and lede in the include; project cards from **`_data/research_projects.yml`** (`title`, `description` with Markdown supported via `markdownify`).

**To edit:** hero copy → `research-page.html`; projects → `research_projects.yml`; layout/styles → `_lips-theme.scss` (`research-page`, `rp-card`).

---

### Publications (`/publications/`)

- **Layout:** `gridlay`.
- **Page file:** `_pages/publications.md` → **`_includes/publications-page.html`**.
- **Contains:** Only publications with **`highlight: 1`** in **`_data/publist.yml`** appear. Each card uses the shared lab image (`/images/lab.jpg`) unless you change the include. Optional `authors` (hidden if exactly `LIPS Lab Researchers`), `link.url` / `link.display`, and notes `news1` / `news2`.

**To edit:** page intro → `publications-page.html`; papers → `publist.yml` (set `highlight: 1` to show a row; use real `link.url` for the paper link).

---

### Contact (`/contact/`)

- **Layout:** `contactlay`.
- **Page file:** `_pages/contact.md` — address, hours, and contact copy are **inline HTML** in that file (two cards).

**To edit:** all contact text and structure → `_pages/contact.md`; shared footer blurb → `_includes/footer.html`.

---

### Other pages (not in the main nav)

These are leftover or auxiliary routes from the original template; update or remove if you do not need them.

| URL (approx.) | File | Notes |
|---------------|------|--------|
| `/vacancies` | `_pages/openings.md` | Template text (another lab). |
| `/pictures/` | `_pages/pictures.md` | Gallery driven by **`_data/pictures_Leiden.yml`**. |
| `/instrumente.html` | `_pages/Instrumente.md` | Instrument photos. |
| `/allnews.html` | `_pages/allnews.md` | Lists **`_data/news.yml`**. |
| `/aboutwebsite.html` | `_pages/aboutwebsite.md` | Old template instructions. |
| `/404.html` | `_pages/404.md` | Not found page. |

`_includes/news.html` can show recent news (not currently wired on the home page in this fork).

---

## Global chrome (every page)

| What | Where to edit |
|------|----------------|
| Site title, meta description, `url` / `baseurl` | `_config.yml` |
| Navigation links and labels | `_includes/header.html` |
| Footer columns, address, copyright | `_includes/footer.html` |
| `<head>`, fonts, CSS link, analytics hook | `_includes/head.html` |
| Production analytics snippet | `_includes/analytics.html` |

---

## Styling

- **Primary theme:** `_sass/_lips-theme.scss` (layout, hero, cards, footer, page-specific sections).
- **Bootstrap + small globals:** `css/main.scss` and other `_sass` partials as imported there.

After SCSS changes, run a build (below) to refresh `css/main.css` in `_site/`.

---

## Local preview

From the project root:

```bash
jekyll serve
```

Open the URL Jekyll prints (usually `http://127.0.0.1:4000` **plus** your `baseurl` path, e.g. `http://127.0.0.1:4000/labwebsite-test/` if `baseurl` is `/labwebsite-test`).

Production build:

```bash
jekyll build
```

If you use Bundler: `bundle exec jekyll serve` / `bundle exec jekyll build`.

**Tip:** If you change `_config.yml`, restart `jekyll serve`.

---

## Publishing on GitHub Pages (short tutorial)

GitHub Pages can host this Jekyll site from the same repository.

### 1. Create or use a GitHub repository

Push this project to GitHub (e.g. `main` as default branch).

### 2. Align `url` and `baseurl` in `_config.yml`

- **Project site** (most common): site is at  
  `https://<username>.github.io/<repository-name>/`  
  Set:

  ```yaml
  url: "https://<username>.github.io"
  baseurl: "/<repository-name>"
  ```

  Use the **exact** repo name (case-sensitive). Leading slash on `baseurl`, no trailing slash on `url`.

- **User or organization site** (repo named `<username>.github.io`): often `baseurl: ""` and `url: "https://<username>.github.io"`.

Wrong `baseurl` breaks CSS, images, and internal links.

### 3. Turn on GitHub Pages

1. On GitHub: **Settings → Pages**.
2. Under **Build and deployment**, choose **GitHub Actions** (recommended for Jekyll 4 + current dependencies) or **Deploy from a branch** (classic `gh-pages` or `/ (root)` from `main`).

If you use **Actions**, add a workflow that runs `jekyll build` and uploads `_site/` (GitHub documents the “Jekyll” starter workflow). If you use **branch deployment**, GitHub’s Jekyll build may differ slightly from your local Gemfile; keep dependencies compatible with [GitHub Pages versions](https://pages.github.com/versions/).

### 4. Push your changes

```bash
git add .
git commit -m "Update site content"
git push origin main
```

After the build finishes (Actions or Pages build), the site updates at your `url` + `baseurl`.

### 5. Optional: custom domain

In **Settings → Pages**, set the custom domain and add the DNS records GitHub requests. Put a `CNAME` file in the site root if you use a subdomain workflow described in GitHub’s docs.

### 6. Workflow file in this repo

The **GitHub Actions** workflow lives at **`.github/workflows/jekyll-gh-pages.yml`**. It runs on pushes to **`main`** or **`master`**. If you use another default branch, add it under `on.push.branches` or rename the branch so deploys actually run.

---

## Troubleshooting: plain HTML / no CSS on GitHub Pages

If the site looks like a default browser page (bulleted nav, Times-like font, broken layout) **only on GitHub Pages** but **`jekyll serve` looks fine locally**, work through the items below.

### 1. Wrong `url` / `baseurl` (broken asset paths)

| Where the site actually loads | Repository type | `_config.yml` |
|--------------------------------|-----------------|---------------|
| `https://lipslabuofm.github.io/` (no extra path) | User/org site: repo name is exactly **`lipslabuofm.github.io`** | `url: "https://lipslabuofm.github.io"` and **`baseurl: ""`** |
| `https://lipslabuofm.github.io/<repo-name>/` | Project site: any other repo name | `url: "https://lipslabuofm.github.io"` and **`baseurl: "/<repo-name>"`** (must match the repo name) |

If `baseurl` does not match how GitHub serves the site, the HTML will request `/css/main.css` at the **wrong path** (404), so no styles load. Fix `_config.yml`, commit, push, and wait for Actions to finish.

**Local preview with a project `baseurl`:** run `jekyll serve` and open `http://127.0.0.1:4000/<repo-name>/` (include the same path as `baseurl`).

### 2. Live site is an old build (not the same as your laptop)

GitHub Pages serves whatever the **last successful** Actions deploy built—not your uncommitted files.

- Push all changes to the repo that powers the site (usually **`lipslabuofm/lipslabuofm.github.io`**).
- **Actions** → latest **Deploy Jekyll site to Pages** → must be **green**.
- **Settings → Pages → Source** should be **GitHub Actions** (not an old “Deploy from branch” you forgot about).

You can edit files **on github.com** (pencil icon → commit) if you do not use Git locally; still wait for Actions after each commit.

### 3. Google Fonts `@import` inside compiled `main.css` (strict browsers / networks)

Older Bootswatch setups inject a CSS line like:

`@import url("https://fonts.googleapis.com/css?family=Source+Sans+Pro...");`

inside **`main.css`**. On some networks, privacy tools, or browsers, a failing **`@import`** can prevent the **rest of that stylesheet** from applying, so the whole site looks unstyled even though `main.css` returns HTTP 200.

**In this repo**, those lines are removed from **`_sass/bootstrap/_bootswatch.scss`** (the site loads **Inter** from **`_includes/head.html`** instead). If you merged an older template or edited on GitHub, ensure **`_bootswatch.scss`** does **not** contain `$web-font-path` and **`@import url($web-font-path);`**.

**Check what is actually deployed:**

```bash
curl -s https://lipslabuofm.github.io/css/main.css | head -c 400
curl -s https://lipslabuofm.github.io/css/main.css | grep -E 'Source\+Sans|@import url\("https://fonts'
```

If the second command prints lines with **`Source+Sans`** or **`fonts.googleapis.com`** inside **`main.css`**, fix `_bootswatch.scss`, commit, push, and re-run Actions. After a good deploy, that `grep` should print **nothing** (or only unrelated matches).

This repo may also include a build marker near the top of **`css/main.scss`** (e.g. a comment mentioning **`LIPS main.css v3`**) so you can tell a new deploy from cached output—if you do not see it in the first ~500 bytes of the live file, the new build may not be live yet.

### 4. Browser cache and privacy tools

After fixing the server:

- Hard refresh (**Cmd+Shift+R** / **Ctrl+Shift+R**) or try a **private window**.
- **Brave Shields** (or similar) can interfere with fonts or scripts; try lowering shields for `*.github.io` once to test.

### 5. Still stuck?

1. In DevTools → **Network**, reload the homepage and select **`main.css`**: confirm **status 200** and type **stylesheet**.
2. Compare the default branch on GitHub with your machine: open **`_config.yml`** and **`_sass/bootstrap/_bootswatch.scss`** on github.com and confirm they match what you expect.

---

## YAML editing tips

- Indentation must be spaces (2 spaces per level), consistent under each list item.
- Quote strings that contain `:` or special characters.
- After editing `_data/*.yml`, run `jekyll build` or `jekyll serve` locally to catch parse errors.

---

## License / credits

This project grew from an academic lab Jekyll template (historically the Allan Lab site). Adapted for LIPS Lab. Adjust copyright and license in this README and in-repo license files to match your group’s policy.
