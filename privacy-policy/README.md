# ZenDrop Privacy Policy (GitHub Pages)

This folder contains a simple, static privacy policy webpage for the Android app **ZenDrop**.

## Files

- `index.html` — the privacy policy page
- `style.css` — simple responsive styling

## Publish with GitHub Pages

You can host this page for free using GitHub Pages.

### Option A (recommended): Publish from `privacy-policy/` using GitHub Pages (GitHub Actions)

1. Push this repository to GitHub (if you haven’t already).
2. In your GitHub repository, go to **Settings → Pages**.
3. Under **Build and deployment**, set:
   - **Source**: **GitHub Actions**
4. Add a workflow file at `.github/workflows/pages.yml` that publishes the `privacy-policy/` folder.

Use this minimal workflow (adjust the branch name if needed):

```yml
name: Deploy Privacy Policy to GitHub Pages

on:
   push:
      branches: ["main"]
      paths:
         - "privacy-policy/**"
         - ".github/workflows/pages.yml"

permissions:
   contents: read
   pages: write
   id-token: write

concurrency:
   group: "pages"
   cancel-in-progress: true

jobs:
   deploy:
      runs-on: ubuntu-latest
      environment:
         name: github-pages
         url: ${{ steps.deployment.outputs.page_url }}
      steps:
         - uses: actions/checkout@v4

         - uses: actions/configure-pages@v5

         - uses: actions/upload-pages-artifact@v3
            with:
               path: "privacy-policy"

         - id: deployment
            uses: actions/deploy-pages@v4
```

After it deploys, GitHub will show your site URL in **Settings → Pages**.

### Option B: Publish from `/docs` (branch-based Pages)

GitHub Pages can also publish directly from a branch, but in this mode it can only publish from the repository root (`/`) or `/docs`.

If you want to use this mode, copy the privacy policy files to one of those locations:

- Copy `privacy-policy/index.html` → `docs/index.html`
- Copy `privacy-policy/style.css` → `docs/style.css`

Then:

1. Go to **Settings → Pages**.
2. Under **Build and deployment**, set:
   - **Source**: **Deploy from a branch**
   - **Branch**: `main` (or your default branch)
   - **Folder**: `/docs`

## Use the URL in Google Play

In Google Play Console, set your app’s **Privacy Policy** URL to the GitHub Pages URL that points to this `index.html`.

## Customization checklist

Before publishing, you should update:

- The **Data Controller** name in `index.html`
- The contact email address (currently `privacy@zendrop.app`)
- The effective/last-updated dates if needed
