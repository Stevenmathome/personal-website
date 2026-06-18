# stevenmendelsohn.com

A minimalist personal website (plain HTML/CSS, no build step) inspired by the
clean, text-focused style of [andrewmccalip.com](https://andrewmccalip.com).
Hosted free on Cloudflare Pages.

## Editing content

Everything lives in two files:

- `index.html` — your name, tagline, bio, project links, and social footer.
  Look for the `<!-- TODO -->` comments and replace the placeholder text.
- `styles.css` — colors, fonts, and spacing (via CSS custom properties at the
  top under `:root`).

No framework, no build — just edit and save.

## Preview locally

```bash
cd "/Users/stevenmendelsohn/Personal Website"
python3 -m http.server 8000
# open http://localhost:8000
```

## Deploy

The site auto-deploys: pushing to the `main` branch on GitHub triggers a new
Cloudflare Pages build.

### One-time setup

1. **Push to GitHub** — create a repo (e.g. `personal-website`) and push this
   folder to it.
2. **Cloudflare Pages** — in the Cloudflare dashboard:
   *Workers & Pages → Create → Pages → Connect to Git*, select the repo.
   Build settings:
   - Framework preset: **None**
   - Build command: *(blank)*
   - Build output directory: `/`

   Deploy and confirm it works at the `*.pages.dev` URL.

### Point stevenmendelsohn.com at it (replaces the old Google Site redirect)

1. In Cloudflare: **Add a site** → `stevenmendelsohn.com` → Free plan. Cloudflare
   gives you two nameservers.
2. In **GoDaddy → Domain → DNS → Nameservers**, switch to Cloudflare's two
   nameservers. (You still own the domain at GoDaddy; only DNS management moves.)
3. In **GoDaddy → Domain → Forwarding**, remove the old Google Site forwarding so
   it stops redirecting.
4. In Cloudflare Pages → your project → **Custom domains**, add
   `stevenmendelsohn.com` and `www.stevenmendelsohn.com`. Cloudflare creates the
   DNS records and provisions HTTPS automatically.
5. Wait for nameserver propagation (minutes up to ~24h), then load
   `https://stevenmendelsohn.com` to confirm.

## Adding interactive project pages later

Drop new pages in `projects/` (e.g. `projects/my-thing.html`) and link to them
from `index.html`. For in-browser interactivity, add a `<script>` to that page.
For server-side/computed pages, a small separate service (e.g. Flask) can be
added without changing this static setup.
