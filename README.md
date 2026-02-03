# Uniswap Developer Documentation

This repository contains the documentation content for the Uniswap Developer Portal.

## Contributing

### Editing via GitHub (Recommended for non-technical contributors)

1. Navigate to the file you want to edit
2. Click the pencil icon ("Edit this file")
3. Make your changes
4. Scroll down and add a commit message describing your changes
5. Select "Create a new branch for this commit and start a pull request"
6. Submit the pull request for review

### Local Development

If you need to preview changes locally:

```bash
# Clone this repo
git clone https://github.com/Uniswap/docs-content.git

# Or, work within the universe monorepo
git clone --recurse-submodules https://github.com/Uniswap/universe.git
cd universe
bun install
bun dev-portal dev
```

## File Structure

```
├── meta.json           # Root navigation configuration
├── index.mdx           # Docs homepage
├── getting-started/    # Getting started guides
│   ├── meta.json       # Section navigation
│   └── *.mdx           # Content pages
└── trading-api/        # Trading API documentation
    └── *.mdx           # Content pages
```

## Frontmatter

Each `.mdx` file should include frontmatter at the top:

```yaml
---
title: "Page Title"
description: "Brief description for SEO and previews"
---
```

## Navigation (meta.json)

The `meta.json` files control sidebar navigation:

```json
{
  "title": "Section Title",
  "pages": ["page-slug", "another-page"]
}
```

- Page slugs reference file names without `.mdx` extension
- Use `---Section Name---` for section separators
- Order in the array determines sidebar order

## Deployment

Changes merged to `main` trigger an automated process:
1. GitHub Action notifies the universe monorepo
2. A PR is created to update the submodule reference
3. After review and merge, changes deploy to production
