# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based GitHub Pages site using the Minima theme. The site is configured to use GitHub Pages hosting with Jekyll 4.x through the github-pages gem.

## Development Commands

### Local Development
```bash
# Install dependencies
bundle install

# Serve the site locally with auto-reload
bundle exec jekyll serve

# Build the site for production
bundle exec jekyll build
```

The local development server runs on http://localhost:4000 by default.

### Dependency Management
```bash
# Update all gems
bundle update

# Update GitHub Pages gem specifically
bundle update github-pages
```

## Site Structure

- **_config.yml**: Main Jekyll configuration file containing site metadata, theme settings, and build configuration
- **_posts/**: Blog posts following Jekyll's `YEAR-MONTH-DAY-title.MARKUP` naming convention
- **_site/**: Generated static site files (auto-generated, not version controlled)
- **Pages**: Markdown files in root directory (index.markdown, about.markdown, hobby.md) become site pages
- **Gemfile**: Ruby gem dependencies for Jekyll and GitHub Pages

## Content Creation

### Blog Posts
Create new posts in `_posts/` directory with filename format: `YYYY-MM-DD-title.markdown`

Required front matter:
```yaml
---
layout: post
title: "Post Title"
date: YYYY-MM-DD HH:MM:SS +0900
categories: category1 category2
---
```

### Pages
Create new pages as `.markdown` or `.md` files in root directory.

Required front matter:
```yaml
---
layout: page
title: "Page Title"
permalink: /page-url/
---
```

## Theme and Styling

This site uses the Minima theme (version ~2.5). Theme customization should follow Jekyll's theme override patterns by creating corresponding files in the site directory structure.

## Deployment

The site is automatically deployed to GitHub Pages when changes are pushed to the `gh-pages` branch. No manual build step is required for deployment.