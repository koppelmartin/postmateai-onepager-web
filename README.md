# PostmateAI — marketing/transparency site

The public landing page for **PostmateAI**, the LinkedIn publishing tool by [2C Ventures](https://2cventures.eu).

This URL is the one submitted in the LinkedIn app's *App Logo & URL* field for the Marketing Developer Platform application. Its job is to give LinkedIn reviewers a clear, factual description of what the product does and exactly how it uses the LinkedIn API.

## Stack

- 3 static HTML files. No framework, no build step, no JS runtime, no analytics.
- All CSS inline in `<style>` blocks. Favicon is an inline SVG data URI.
- Designed to be hosted on any static host (Vercel, Netlify, Cloudflare Pages, GitHub Pages, S3 + CloudFront, plain Nginx).

## Files

| File | Purpose |
|---|---|
| `index.html` | Landing page — hero, features, LinkedIn API usage, data & privacy, contact |
| `privacy.html` | Full Privacy Policy |
| `terms.html` | Full Terms of Service |
| `robots.txt` | Allow indexing |
| `vercel.json` | Optional clean-URL config for Vercel deployments |
| `netlify.toml` | Optional clean-URL config for Netlify deployments |

## Local preview

Open `index.html` in a browser. That's it.

If you want clean URLs locally (`/privacy` instead of `/privacy.html`):

```bash
python3 -m http.server 8000
# or
npx serve .
```

## Deploy

### Vercel

```bash
npm i -g vercel
vercel        # preview
vercel --prod # production
```

The included `vercel.json` strips the `.html` extension so the canonical URLs (`/`, `/privacy`, `/terms`) work without redirects.

### Netlify

Drag-and-drop the project folder into Netlify, or:

```bash
npm i -g netlify-cli
netlify deploy --prod --dir=.
```

The included `netlify.toml` handles clean URLs.

### GitHub Pages

Push to a repo, then in *Settings → Pages* select the `main` branch and `/` root. The site is live at `https://<user>.github.io/<repo>/`. Note: GitHub Pages does not strip `.html` extensions, so links between pages will keep the extension (already wired this way).

## Before going live

- [ ] Replace `https://postmateai.com/og.png` in the `<meta property="og:image">` tags with a real 1200×630 PNG, served from the same domain.
- [ ] Confirm the operating entity name (`2C Ventures OÜ`) and registered address with counsel.
- [ ] Have the Privacy Policy and Terms of Service reviewed by counsel.
- [ ] Update the `Last updated` date in `privacy.html` and `terms.html` when copy changes.
- [ ] Set the canonical domain on your DNS/host (`postmateai.com` is referenced in `<link rel="canonical">` and `og:url`).

## Reviewer notes (for LinkedIn Developer Platform)

The "How we use the LinkedIn API" section on `index.html` lists every scope the app requests:

- **Sign In with LinkedIn (OpenID Connect)** — `openid`, `profile`, `email` for authentication.
- **Share on LinkedIn** — `w_member_social` to publish posts as the authenticated user, only on explicit user action.
- **Marketing Developer Platform** — `w_organization_social` and `rw_organization_admin` to list the Pages the user administers and publish on their behalf.

No scraping, no data resale, no automated engagement. Tokens are encrypted at rest, users can disconnect at any time.

## License

MIT — see `LICENSE`.
