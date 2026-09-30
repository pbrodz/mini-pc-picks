# Tiny Server Lab

A tiny static site — "best mini PC for home server" top picks plus a blog —
built as an experiment to see if a niche site can earn real Google traffic.
Pure HTML/CSS/JS, no build step, no frameworks, no external fonts. GitHub Pages ready.

## Site structure

```
mini-pc-site/
├── index.html                          # Homepage = current top picks comparison
├── about.html                          # About / the experiment
├── blog/
│   ├── index.html                      # Blog listing
│   ├── beelink-eq14-vs-gmktec-g3-plus.html
│   ├── how-much-idle-power-home-server.html
│   ├── n100-vs-n150-docker-plex.html
│   └── new-post-template.html          # Copy this to start a new post (not linked in nav)
├── style.css
├── script.js                           # Footer year only
├── sitemap.xml
├── robots.txt
├── CNAME                               # Placeholder — replace with your real domain
└── README.md
```

**Pages:** 6 public pages (home, about, blog index, 3 posts) + 1 unlisted template.

## Push to GitHub Pages

1. Create a new repo on GitHub (e.g. `mini-pc-picks`). Don't initialize with a README — this folder already has one.
2. From this folder:
   ```bash
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin git@github.com:YOUR-USERNAME/mini-pc-picks.git
   git push -u origin main
   ```
3. On GitHub: **Settings → Pages** → Deploy from branch → `main`, folder `/ (root)` → Save.
4. Your site goes live at `https://YOUR-USERNAME.github.io/mini-pc-picks/` within a minute or two.

### Custom domain (Porkbun → GitHub Pages)

1. In `CNAME`, replace `REPLACE-WITH-YOUR-DOMAIN` with your domain (e.g. `tinyserverlab.com`), commit, push.
2. In Porkbun DNS for that domain:
   - **Apex domain** (`@`): add four A records pointing at GitHub Pages IPs:
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - **www subdomain**: add a CNAME record → `YOUR-USERNAME.github.io`
3. On GitHub: **Settings → Pages** → Custom domain → enter your domain → Save.
   Tick **Enforce HTTPS** once the certificate is issued (can take ~an hour).
4. Update `sitemap.xml` and `robots.txt`: replace every `REPLACE-WITH-YOUR-DOMAIN`
   with your real domain, commit, push.

## Add a new blog post

1. Copy `blog/new-post-template.html` to `blog/your-slug-here.html`.
   Keep slugs short, lowercase, hyphenated — they become the URL.
2. Fill in the `TODO` spots: `<title>`, meta description, H1 (use the target
   search keyword naturally), and the `<time datetime="...">` publish date.
3. Write the post. Tips that actually matter for ranking:
   - Answer one specific question; put the keyword in the H1 and first paragraph.
   - Use h2/h3 subheadings; keep paragraphs short.
   - End with a direct verdict — posts that conclude outrank posts that waffle.
   - Link to `/` (top picks) and 1–2 related posts.
   - Keep the honesty box. It's the site's whole brand.
4. Add the post to `blog/index.html` (newest first) and to `sitemap.xml`
   (with today's `<lastmod>`).
5. Commit, push. GitHub Pages rebuilds in ~1 minute.

## Update the top picks

Everything lives in `index.html`:
- Edit the comparison `<table>` rows and the `.pick` article cards.
- Update the **"Last updated"** line near the top — readers and Google both
  notice stale "best of" pages.
- Update `<lastmod>` for `/` in `sitemap.xml`.
- Commit, push.

## Enable Cloudflare Web Analytics (private visitor counts)

1. Sign up at cloudflare.com → **Web Analytics** → add your site/hostname.
2. Cloudflare gives you a beacon token. In **every** HTML file, find this
   commented block near `</body>`:
   ```html
   <!-- Cloudflare Web Analytics: paste your beacon token ... -->
   ```
   Replace `PASTE-YOUR-CLOUDFLARE-BEACON-TOKEN-HERE` with your token and
   remove the `<!--` / `-->` comment markers so the `<script>` is live.
3. Commit, push. Visits appear in your private Cloudflare dashboard —
   nothing visible on the site itself.

## Google Search Console (the real traffic scoreboard)

1. Go to [search.google.com/search-console](https://search.google.com/search-console),
   add your domain as a **Domain** property.
2. Verify via the DNS TXT record it gives you (add it in Porkbun DNS).
3. Submit `https://YOUR-DOMAIN/sitemap.xml` under **Sitemaps**.
4. Wait. Impressions/clicks per query show up under **Performance** —
   usually within a few days of Google discovering the site. This is the
   honest answer to "did anyone visit."

## Notes

- Specs and prices on the site are vendors' claimed numbers at time of
  writing, clearly labeled. Where figures are illustrative (idle-power
  ranges, yearly cost math), pages say so — no invented benchmarks
  presented as measured.
- Keep it fast: no frameworks, no webfonts, no third-party requests
  (until you enable the Cloudflare beacon). The whole site is a few
  dozen kilobytes.
