# SolarSurges GEO Resources (solarsurges-geo)

> Machine-readable resources for AI search engines (Perplexity, ChatGPT, Claude, Gemini, Google AI Overviews, Microsoft Copilot).
>
> This repository is a **static-only GitHub Pages site**. The main marketing site (solarsurges.com) links to these resources from its footer, About page, and product pages, allowing AI crawlers to discover structured data without modifying the main site's code.

## Live URL

After deployment, this site will be available at one of:

- `https://solarsurges-geo.github.io/` (default GitHub Pages URL)
- `https://geo.solarsurges.com/` (if CNAME configured)

## What's in here

```
.
├── llms.txt                      AI crawler guide (Anthropic 2024 protocol)
├── index.html                    AI Resources landing page (visible to humans + crawlers)
├── robots.txt                    AI crawler access policy
├── schemas/                      JSON-LD structured data
│   ├── homepage.json             Organization + WebSite + ItemList
│   ├── tcu.json                  TCU product + FAQPage + HowTo
│   ├── ncu.json                  NCU product + FAQPage
│   ├── scada.json                SCADA SoftwareApplication + FAQPage
│   ├── sws.json                  SWS product + FAQPage
│   └── article.json              Blog article template (replace placeholders per article)
├── compare/                      Comparison page HTML
└── reports/                      Industry reports and data
    └── README.md                 (place PDFs and CSVs here)
```

## Deploy in 5 minutes

### 1. Create the repository

```bash
# Option A: GitHub organization (recommended for brand consistency)
# Create org "solarsurges-geo" on https://github.com/organizations/new
# Then create repo "solarsurges-geo" inside it

# Option B: Personal repo
# Just create https://github.com/<your-username>/solarsurges-geo
```

### 2. Push the files

```bash
cd solarsurges-geo
git init
git add .
git commit -m "Initial deploy: AI resources for SolarSurges GEO"
git branch -M main
git remote add origin https://github.com/solarsurges-geo/solarsurges-geo.git
git push -u origin main
```

### 3. Enable GitHub Pages

1. Go to repo → Settings → Pages
2. Source: `Deploy from a branch`
3. Branch: `main` / `(root)`
4. Save
5. Wait 1–3 minutes for first deploy

### 4. Verify

```bash
# Should return 200
curl -I https://solarsurges-geo.github.io/llms.txt

# Should return JSON
curl https://solarsurges-geo.github.io/schemas/tcu.json | head -c 200

# Should return HTML
curl -I https://solarsurges-geo.github.io/index.html
```

### 5. Link from main site

In solarsurges.com footer / About page / product pages, add:

```html
<p style="text-align:center; font-size:12px; color:#666;">
  AI & Developer Resources: 
  <a href="https://solarsurges-geo.github.io/llms.txt">llms.txt</a> · 
  <a href="https://solarsurges-geo.github.io/schemas/">JSON-LD Schemas</a>
</p>
```

## How AI crawlers use this

| Crawler | How it finds your resources | What it cites |
|---|---|---|
| **PerplexityBot** | Reads `llms.txt` first, then follows structured data links | Schema.org JSON-LD, comparison tables, FAQ |
| **GPTBot / OAI-SearchBot** | Crawls all linked pages from main site | FAQ, HowTo, comparison content |
| **ClaudeBot** | Similar to GPTBot | Definition leads, FAQ |
| **Google-Extended** | Powers Gemini / AI Overviews | Schema.org markup, structured lists |
| **Bytespider / CCBot** | **Blocked by robots.txt** | None (training-only crawlers) |

## Updating content

To update the schemas (e.g., add new FAQs, update specs):

1. Edit the corresponding `.json` file in `schemas/`
2. Commit and push
3. GitHub Pages rebuilds in 1–3 minutes
4. AI crawlers pick up the update on next crawl (typically 7–21 days)

To add a new comparison page:

1. Add the HTML to `compare/<slug>.html`
2. Add the URL to `llms.txt` under "## Comparison Pages"
3. Commit and push

To add a new report PDF or CSV:

1. Drop file into `reports/`
2. Add the URL to `llms.txt` under "## Authoritative Reports"
3. Commit and push

## Custom domain (optional)

To use `geo.solarsurges.com` instead of `solarsurges-geo.github.io`:

1. In your DNS provider, add a CNAME record: `geo` → `solarsurges-geo.github.io`
2. In repo Settings → Pages → Custom domain: `geo.solarsurges.com`
3. Wait 5–30 minutes for DNS + HTTPS provisioning

## Maintenance

- **Quarterly**: Review llms.txt and add new product pages / case studies
- **Monthly**: Update any time-sensitive numbers in JSON-LD (e.g., deployment counts)
- **Per blog post**: Append to `llms.txt` under "## News & Market Intelligence"
- **Per new comparison page**: Add HTML to `compare/` and link from `llms.txt`

## Related

- Main site: https://www.solarsurges.com/
- GEO master plan: `outputs/GEO-优化方案-solarsurges.html`
- Marketingforce platform guide: `outputs/geo-launch/marketingforce-geo-v3.md`
- Console scripts: `outputs/geo-launch/console-scripts/`
