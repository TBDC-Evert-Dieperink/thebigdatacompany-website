# The Big Data Company — website

Bilingual (NL / EN) Hugo site for The Big Data Company.

## Local development

```powershell
hugo server
```

Open <http://localhost:1313>.

## Structure

- `content/` — Markdown content. Dutch is the default language; English files use the `.en.md` suffix.
- `layouts/` — Custom layouts and partials. No external theme.
- `assets/css/main.css` — Site styling, processed via Hugo Pipes.
- `static/` — Static assets (favicon, etc.).
- `hugo.toml` — Site configuration, including language and menu setup.

## Deployment

Automatic via GitHub Actions (`.github/workflows/hugo.yml`).
Every push to `main` builds the site and publishes to GitHub Pages.

Site is served at <https://tbdc-evert-dieperink.github.io/thebigdatacompany-website/>.
