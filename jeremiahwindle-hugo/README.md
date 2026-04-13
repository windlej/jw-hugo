# jeremiahwindle.com — Hugo Site

Personal site built with Hugo, hosted on Cloudflare Pages.

## Stack
- **Hugo** — static site generator
- **Cloudflare Pages** — hosting + CDN
- **GitHub** — source of truth for all content

## Local Development

```bash
# Install Hugo (https://gohugo.io/installation/)
brew install hugo   # macOS
choco install hugo  # Windows

# Clone and run
git clone https://github.com/jeremiahwindle/jeremiahwindle.com
cd jeremiahwindle.com
hugo server -D
# → http://localhost:1313
```

## Content Structure

```
content/
├── blog/          # Blog posts — add .md files here
│   └── _index.md
├── tools/         # Scripts & tools — one .md per tool
│   └── _index.md
├── about.md       # About page
├── lab.md         # Lab page
└── _index.md      # Homepage (no content — layout handles it)

data/
└── videos.yaml    # YouTube video list — update manually
```

## Adding a Blog Post

Create `content/blog/my-post-title.md`:

```yaml
---
title: "Your Post Title"
date: 2026-04-15
description: "One sentence summary shown in cards and meta tags."
categories: ["Networking"]   # Networking, Security, Cloud, Automation, Career, Homelab
tags: ["cisco", "ospf", "lab"]
draft: false
---

Your content here in Markdown.
```

## Adding a Tool

Create `content/tools/tool-name.md`:

```yaml
---
title: "Tool Name"
description: "Short description shown on the tools grid."
icon: ">_"           # Text shown as the icon (mono font)
language: "Python"   # Badge label
github: "https://github.com/jeremiahwindle/repo"
tags: ["python", "automation"]
date: 2026-04-15
---

Longer description and usage instructions here.
```

## Updating Videos

Edit `data/videos.yaml`. Replace `id` with the real YouTube video ID from the URL (`youtube.com/watch?v=VIDEO_ID`).

```yaml
- id: "abc123xyz"
  title: "Video Title"
  category: "Networking"
  duration: "24:30"
  date: "Apr 2026"
```

## Deployment

Push to `main` → GitHub Actions builds Hugo → deploys to Cloudflare Pages automatically.

**First-time setup:**
1. Create a Cloudflare Pages project connected to your GitHub repo
2. Add `CLOUDFLARE_API_TOKEN` and `CLOUDFLARE_ACCOUNT_ID` to GitHub Secrets
3. Set build command: `hugo --minify`, output dir: `public`

Or skip GitHub Actions entirely — Cloudflare Pages can build directly from GitHub with the same settings.
