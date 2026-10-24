# Developer Notebook

A small Quarto website for personal development notes, writing, and projects.
Source lives in this repository; GitHub Actions renders it into `_site/` and
publishes that artifact to **https://snowoflondon.github.io**.

## Get started

1. Install [Quarto CLI](https://quarto.org/docs/get-started/) (the workflow uses
   **1.10.19**; use the same version locally for consistent builds).
2. Open this folder in VS Code and install the recommended **Quarto** extension.
3. Verify the installation and start a local preview from the repository root:

   ```sh
   quarto --version
   quarto check
   quarto preview
   ```

Preview starts a local server with automatic refresh. Stop it with Ctrl+C.
For a complete build, run `quarto render`; output goes to `_site/` (ignored by Git).
No Python packages, Node tools, or paid services are needed for this scaffold.
Code examples are display-only; computation is disabled in `_quarto.yml`.

## Content layout

- `_quarto.yml`: site identity, navigation, theme, output, and render settings.
- `index.qmd`: introduction, recent writing, selected projects.
- `projects.qmd` and `projects/*/index.qmd`: project listing and detail pages.
- `writing/index.qmd` and `writing/posts/*/index.qmd`: automatic blog and posts.
- `writing/posts/_metadata.yml`: defaults shared by all posts.
- `about.qmd`: informal introduction and interests.
- `styles.css`: small visual refinements to Litera.
- `.github/workflows/publish.yml`: build and Pages deployment.

The existing repository identity is preserved. Original README text:

> # snowoflondon.github.io
> Current placeholder for portfolio source code

## Add a post

Create `writing/posts/my-post/index.qmd` with this front matter and your text:

```yaml
---
title: "My new post"
description: "A brief summary for listings and RSS."
date: 2026-10-22
categories: [Python, Software Development]
toc: true
---
```

Use your actual publication date. Categories are free-form; suggested labels are
AI & LLMs, Python, Software Development, Projects, and Thoughts. Set `draft: true`
while working: drafts can appear in preview but are excluded from the full
published build. Both writing listings update automatically on render.
The RSS feed is generated at `/writing/index.xml`.

Use ordinary fenced `python` blocks for highlighted code. Use `$...$` or
`$$...$$` for math and a `{mermaid}` fenced block for diagrams. Keep images beside
the post and reference them with `![Useful alt text](image.png)`.
Override `toc: true` per post when a table of contents helps.

## Add a project

Copy `projects/everyday-r/` to `projects/my-project/`, then change its title,
description, categories (technologies), status, and repository link. Clearly
describe the idea and what you learned. The detail page supplies its own listing
summary; no separate data file is needed. Add `image: screenshot.png` to its
front matter for an optional card image, and use Markdown to include it in the
page body. The project listing includes every project; the homepage currently
shows up to two. Change its listing filter or limit when you want to curate it.

## Customize

Replace any remaining `[Your name]` placeholders before publishing.
Change the site title, description, footer, and navigation in `_quarto.yml`.
Keep `theme: litera` as the base and make small changes in `styles.css`.
Use `.qmd` source links for internal navigation so Quarto resolves HTML URLs.
The site URL is the root domain, with no repository-name prefix.

## Publish to GitHub Pages

Nothing has been committed, pushed, or deployed by this scaffold.
When you are ready to publish:

1. For free GitHub Pages hosting, ensure this is a **public** repository on GitHub
   Free. The expected repository is
   [snowoflondon/snowoflondon.github.io](https://github.com/snowoflondon/snowoflondon.github.io).
2. In the repository, open **Settings → Pages → Build and deployment → Source**
   and select **GitHub Actions**. Do not select a branch or a `/docs` folder.
3. Ensure repository **Settings → Actions → General** permits GitHub Actions,
   including the official GitHub and Quarto actions used by this workflow.
   If `github-pages` environment protection is configured, allow `main` to deploy.
4. Run `quarto render` locally and inspect `quarto preview`.
5. Review your changes, commit them, and push to `main` when you approve publishing.
   Every push to `main` builds and deploys. You can also run **Publish Quarto
   website** manually from the Actions tab once the workflow exists on GitHub.
6. Watch the build and deployment jobs in Actions, then visit the site URL above.

The workflow uses the built-in `GITHUB_TOKEN`; no personal token or secret is
required. Source checkout has read access; only the deploy job has `pages: write`
and `id-token: write`, scoped to the `github-pages` environment. Build output is
uploaded as a Pages artifact; no `gh-pages` branch is needed. Do not run
`quarto publish gh-pages`, which uses a different publishing approach.

## Troubleshooting

- **`quarto` not found:** install the CLI (the VS Code extension alone is not
  enough), then restart the terminal and run `quarto --version`.
- **Post missing:** check its location matches `writing/posts/*/index.qmd`, its
  front matter is valid, and it is not marked as a draft. Run a full render.
- **Broken image or link:** check case-sensitive paths and keep images beside
  their content. Generated RSS and HTML links exist after rendering.
- **Pages configuration or deployment error:** check the Pages source is GitHub
  Actions, Actions are enabled, and environment rules permit `main`. Inspect the
  first failing workflow step for details.
- **Unexpected code execution:** use ordinary fenced code for examples.
  If you later enable executable cells, also provision their runtimes and
  dependencies locally and in CI.
- **Styling looks stale:** render again and refresh the browser. Never edit
  generated `_site/` files; change source files instead.

Reference: [Quarto listings](https://quarto.org/docs/websites/website-listings.html)
and [GitHub custom Pages workflows](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages).
