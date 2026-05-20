# The Big Data Company — site instructions

Bilingual (NL / EN) Hugo site for The Big Data Company. Hosted on GitHub Pages
under a project subpath: <https://tbdc-evert-dieperink.github.io/thebigdatacompany-website/>.

## Stack

- Hugo 0.153.0 extended (pinned in `.github/workflows/hugo.yml`).
- No external theme — all layouts live in `layouts/`.
- Styling: `assets/css/main.css`, processed via Hugo Pipes.
- Languages configured in `hugo.toml`: `nl` is the default (no subdir), `en` lives at `/en/`.

## Deployment

Push to `main` triggers `.github/workflows/hugo.yml`, which builds with
`--baseURL "${{ steps.pages.outputs.base_url }}/"` (so the project subpath is
applied) and deploys to GitHub Pages.

To verify a production build locally:

```powershell
hugo --gc --minify --baseURL "https://tbdc-evert-dieperink.github.io/thebigdatacompany-website/"
```

Then inspect `public/` to confirm internal hrefs include `/thebigdatacompany-website/`.

## Internal links — important

`relLangURL` is broken under our setup: it drops the project subpath when the
input has a leading slash (`"/about" | relLangURL` → `/en/about` instead of
`/thebigdatacompany-website/en/about`), and it double-prepends the language
when the input already contains the project path.

Use page lookups instead:

- Home: `{{ .Site.Home.RelPermalink }}`
- Internal page: `{{ (.Site.GetPage "/contact").RelPermalink }}`
- With fragment: `{{ (.Site.GetPage "/products").RelPermalink }}#blink`
- Menu items (defined with `pageRef`): use `.Page.RelPermalink` (see
  [layouts/partials/header.html](layouts/partials/header.html))

External URLs and `mailto:` / `tel:` links can stay as plain `href` values.

## Writing style

- No em-dashes (`—`, U+2014) or en-dashes (`–`, U+2013) in user-facing content.
  After a bold list-item lead use `:` (`**Term**: definition`); in running prose
  use `,`; in number ranges use a plain hyphen (`4-16`).
- The page-title separator in `<title>` uses the middle dot `·`.

## Brand

- Logo: `assets/img/logo.svg` (inlined via [layouts/partials/logo-inline.html](layouts/partials/logo-inline.html)).
- Accent color: `#00B4FF` (TBDC blue), defined in `assets/css/main.css`.

## Local dev

```powershell
hugo server
```

Opens at <http://localhost:1313>. Hugo serves the site at `/` locally
regardless of the configured `baseURL`, so subpath bugs only surface on the
deployed GitHub Pages URL — always verify there after non-trivial changes.

## Maintaining this file

Keep this file in sync with reality. When a project convention, deployment
detail, or non-obvious gotcha changes, update the relevant section in the same
commit as the change. Don't accumulate stale instructions.
