# Voight Docs

Source of `docs.voight.xyz` — built with [Mintlify](https://mintlify.com).

## Editing

Every page is an `.mdx` file (Markdown + JSX). Edit any page with any text editor, commit, push — Mintlify auto-deploys within ~30 seconds.

### Edit an existing page

Find the file matching the URL:

| URL | File |
| --- | --- |
| `docs.voight.xyz/` | `introduction.mdx` |
| `docs.voight.xyz/quickstart` | `quickstart.mdx` |
| `docs.voight.xyz/concepts/agents` | `concepts/agents.mdx` |
| `docs.voight.xyz/privacy/overview` | `privacy/overview.mdx` |
| (etc.) | (mirrors the folder structure) |

Make changes, commit:

```bash
git add -p
git commit -m "docs: tweak quickstart wording"
git push
```

Mintlify deploys automatically.

### Add a new page

1. Create `your-new-page.mdx` anywhere (root or inside a folder)
2. Add the frontmatter at the top:

   ```mdx
   ---
   title: Your page title
   description: "Short description for SEO / search."
   ---

   Page content here.
   ```

3. Add it to `mint.json` `navigation` array so it shows in the sidebar:

   ```json
   {
     "group": "Resources",
     "pages": ["pricing", "changelog", "your-new-page"]
   }
   ```

4. Commit + push.

### Change a section title in the sidebar

Edit `mint.json` `navigation` array. Each object has a `group` (the section header) and a `pages` array.

### Change colors / theme

Edit `mint.json` `colors` block. Hex values supported. Mintlify uses `primary` for buttons + headings, `light` and `dark` for hover/active states.

### Preview locally (optional)

```bash
npm install -g mintlify
cd /path/to/this/repo
mintlify dev
# Opens http://localhost:3000
```

Live-reloads on file changes. Useful for big edits before pushing.

## Structure

```
voight-docs/
├── mint.json              ← Mintlify config — colors, navigation, branding
├── favicon.svg            ← Browser tab icon
├── logo/
│   ├── light.svg          ← Logo for light theme
│   └── dark.svg           ← Logo for dark theme
├── images/                ← Inline images referenced from MDX
├── introduction.mdx       ← Homepage at docs.voight.xyz/
├── quickstart.mdx
├── concepts/              ← What an agent / event / trace / session is
├── privacy/               ← The 3-level privacy model, PII patterns, data handling
├── sdk/                   ← Claude Code / library / HTTP integration guides
├── api-reference/         ← Endpoint specs for /v1/events, /v1/agents, /v1/me/*
├── pricing.mdx
└── changelog.mdx
```

## Deployment

This repo is connected to Mintlify's free tier via GitHub. Pushing to `main` auto-deploys to `docs.voight.xyz`.

### Initial setup (one-time, already done)

1. Create the GitHub repo `voightxyz/voight-docs`
2. Push this folder
3. Sign in to [mintlify.com](https://mintlify.com) with GitHub
4. Install the Mintlify GitHub app on the `voightxyz/voight-docs` repo
5. Mintlify auto-detects `mint.json` and starts deploying
6. In Mintlify dashboard → Settings → Custom Domain → add `docs.voight.xyz`
7. In your DNS provider → add a CNAME `docs → cname.vercel-dns.com` (or whatever Mintlify gives you)
8. Wait 5-10 min for SSL provisioning

### Day-to-day

Just commit + push. Mintlify deploys automatically. If something breaks, check Mintlify's dashboard for build logs.

## License

The Voight product is proprietary. The docs content is published publicly at docs.voight.xyz but the source in this repo follows the same license as the rest of Voight.
