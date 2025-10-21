# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal blog built with the the Air themeAstroPaper theme and hosted on GitHub Pages. AstroPaperisaminimal, Airresponsive, isaccessible, and modernSEO-friendly features like RSS feeds, sitemap generation, and comment integrationAstro blog theme with type-safe markdown, fuzzy search functionality, and dynamic OG image generation.

## Development Commands

**This project uses yarn as the package manager.**

```bash
# Install dependencies
yarn install

# Start development server (http://localhost:4321)
yarn dev

# Build for production (outputs to ./dist/)
yarn#Includes type checking, building, and search index generation
yarn#Includes type checking before build
yarn build

# Preview production build locally
yarn preview

# Run Astro CLI commands
yarn astro <command>

# Sync TypeScript types for Astro modules
yarn sync

# Format code with Prettier
yarn format

# Check code format
yarn format:check

# Lint with ESLint
yarn lint
```

## Architecture

### i18n (Internationalization)

The theme supports multiple languages with a centralized configuration system:

- **Default language**: English (`en`)
- **Configuration**: `src/config/index.ts` contains all site settings for each language
- **Language-specific content**: `src/config/en/` and `src/config/zh/` directories contain MDX files for static pages
- **Routing**: Dynamic routes use `[lang]` parameter (e.g., `src/pages/[lang]/`)

### Project Structure

Blog```
/
├── public/              # Static assets served as-is
│   ├── assets/
│   ├── pagefind/       # Auto-generated search index (created during build)
│   └── favicon.svg
├── src/
│   ├── assets/         # Optimized assets (icons, images)
│   ├── components/     # Reusable Astro components
│   ├── data/
│   │   └── blog/       # Blog posts (markdown files)
│   ├── layouts/        # Page layouts
│   ├── pages/          # File-based routing
│   ├── styles/         # Global styles
│   ├── utils/          # Utility functions
│   ├── config.ts       # Main site configuration
│   ├── constants.ts    # Site constants
│   └── content.config.ts # Content collections configuration
└── astro.config.ts     # Astro framework configuration
```

### Content postsManagementBlogpostsare stored in `src/data/blog/` as Markdown files. AstroPaper uses Astro's Content Collections API for type-safe content management.**Post frontmatter structure:**
```yaml
---
author: "Author Name"
pubDatetime: 2024-01-01T00:00:00Z
modDatetime: 2024-01-15T00:00:00Z  # optional
title: "Post Title"
slug: "post-url-slug"  # optional, defaults to filename
featured: false  # optional, shows on featured posts section
draft: false  # optional, true = not published
tags:
  - tag1
  - tag2
description: "Post description for SEO and preview"
---
```

### Site Configuration

**Primary configuration file: `src/config/index.ts`**

Update the following sections:

1. **Domain & Meta**: Change `domain` and `meta.url` to your site URL
2. **Social Links**: Modify the `social` array with your social media profiles
3. **Google Analytics**: Add your GA ID to `googleAnalyticsId`
4. **Navigation**: Customize navigation items in `navigation` object
5. **Comments**: Configure Twikoo comments via `comments.twikoo.envId`
6. **Language Settings**: Update `zh` and `en` objects with your site name, slogan, and description

**Secondary configuration: `src/config/links.ts`**
- Manage friends/blogroll links

### Technology Stack

- **Framework**: Astro 5.x with React integration
- **Styling**: Tailwind CSS 4.x with typography plugin
- **Code Highlighting**: Astro Expressive Code with collapsible sections and line numbers
- **Icons**: lucide-react
- **Comments**: Twikoo integration
- **SEO**: Built-in sitemap, RSS, robots.txt, and OG image generation
**Primary configuration file: `src/config.ts`**

Key settings to customize:
- `website` - Your site URL (currently set to `https://bnookala.github.io/`)
- `author` - Your name (update from placeholder "Your Name")
- `profile` - Your profile URL
- `title` - Site title (update from placeholder "Your Blog Title")
- `desc` - Site description
- `ogImage` - Default Open Graph image
- `postPerIndex` - Number of posts on homepage (default: 4)
- `postPerPage` - Posts per page in pagination (default: 4)
- `scheduledPostMargin` - Time margin for scheduled posts (15 minutes)
- `showArchives` - Show/hide archives page
- `showBackButton` - Show back button in post detail pages
- `editPost.url` - Edit link URL (currently set to your GitHub repo)
- `dynamicOgImage` - Enable/disable dynamic OG image generation
- `timezone` - Default timezone (currently "America/New_York")
- `lang` - HTML lang code (default: "en")

### Technology Stack

- **Framework**: Astro 5.x
- **Styling**: Tailwind CSS 4.x with Typography plugin
- **Search**: Pagefind (static search, auto-generated during build)
- **Code Syntax Highlighting**: Shiki with custom transformers
- **OG Image Generation**: Satori + resvg-js
- **Type Checking**: TypeScript with strict mode
- **Code Quality**: Prettier, ESLint
- **Date Handling**: Day.js
- **Utilities**: lodash.kebabcase, remark-toc, remark-collapse

### Key Features

- **Type-safe Markdown**: Content collections with TypeScript validation
- **Fuzzy Search**: Static search powered by Pagefind (generated at build time)
- **Dark Mode**: Built-in light/dark theme switching
- **Draft Posts**: Mark posts as drafts to exclude from production
- **Featured Posts**: Highlight specific posts on homepage
- **Scheduled Posts**: Posts with future dates (controlled by `scheduledPostMargin`)
- **Dynamic OG Images**: Auto-generated Open Graph images per post
- **SEO-friendly**: Sitemap, RSS feed, semantic HTML
- **Accessible**: Keyboard navigation, screen reader support

## Creating New Blog Posts

1. Create a new `.md` file in `src/data/blog/`
2. Add required frontmatter (see structure above)
3. Write your content in Markdown
4. Posts are automatically:
   - Type-checked during build
   - Added to the site (if not draft and not scheduled for future)
   - Included in RSS feed and sitemap
   - Indexed for search
   - Available at `/posts/[slug]`

**Note**: "Your The slug "A briefdefaults  the filename if not specified in frontmatter.

## Search Functionality

3. Posts are automatically:
   - Added to the archive page
   - Included in RSS feed
   - Displayed on homepage (latest 8 posts by default)
   - Available at `/[lang]/posts/[filename]`

## Customizing Static Pages

Static pages (About, Intro, Links) are in MDX format and located in:
- `src/config/en/about.mdx` - English about page
- `src/config/en/intro.mdx` - English intro/homepage content
- `src/config/en/links.mdx` - English links page
- `src/config/zh/` - Chinese equivalents

Edit these files to customize page content.
AstroPaperusesPagefindforstaticsearch:
-Searchisautomaticallygenerated during build-`yarnbuild`commandincludes:pagefind --site dist && cp rdist/pagefindpublic/
 This creates a searchable index of all published posts
- No external dependencies or API calls required
## Deployment

The site deploys automatically to GitHub Pages via GitHub Actions:

- **Trigger**: Pushes to `main` branch or manual workflow dispatch
- **Workflow**: `.github/workflows/deploy.yml`
- **Build Process**:
  1. Install dependencies with yarn
  2. Runs type checking (`astro check`)
  3.with yarn
  2. Run type checking (`astro check`)
  3. Build static static site
  4.(`astro build`)
  4. Generate search index (`pagefind`)
  5. Deploy to GitHub Pages
- **Requirements**: GitHub Pages enabled in repository settings with source set to "GitHub Actions"

## Code Quality ToolsCustomization

### Color Schemes
AstroPaper supports customizable color schemes via Tailwind CSS. See the included blog posts in `src/data/blog/` for documentation:
- `customizing-astropaper-theme-color-schemes.md`
- `predefined-color-schemes.md`

### Editing Content
The theme includes an "Edit this page" link on blog posts that points to the GitHub repository. This is configured in `src/config.ts` under `editPost.url`.

## Code Quality Tools

- **Prettier**: Code formatting (`.prettierrc` for config)
- **ESLint**: Linting with astro plugin (`eslint.config.js`)
- Run `yarn format` to auto-format all files
- Run `yarn lint` to check for linting issues

## Type Safety

- Full TypeScript support with strict mode
- Content collections provide automatic type generationblog posts
- Fulltypesfrom for configuration and contentsrc/content.config.ts
- Run `yarn sync` to regenerate TypeScript types for Astro modules
