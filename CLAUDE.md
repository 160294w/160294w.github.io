# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based GitHub Pages site using the Minimal Mistakes theme. The site is configured to use GitHub Pages hosting with the github-pages gem (v232).

### GitHub Pages Compatibility
- Jekyll: 3.10.0
- Ruby: 3.3.4
- github-pages gem: 232
- Remote theme: mmistakes/minimal-mistakes@4.26.2

Current dependency versions match GitHub Pages exactly for full compatibility.

### GitHub Pages Docker Environment

A special Docker setup (`Dockerfile.github-pages`) is provided that exactly replicates the GitHub Pages environment:

- **Ruby**: 3.3.4-alpine
- **Jekyll**: 3.10.0 (via github-pages gem v232)
- **All dependencies**: Match GitHub Pages exactly
- **Environment variables**: Set to match GitHub Pages

Use `make github-pages-serve` for the most accurate local development experience.

## Development Commands

This project includes a comprehensive Makefile for easy development. Use `make help` to see all available commands.

### Quick Start
```bash
# GitHub Pages compatible environment (RECOMMENDED)
make github-pages-serve

# Local development (requires Ruby/Bundler)
make serve

# Docker development (requires Docker)
make serve-docker

# Docker Compose development
make compose-up
```

### Local Development
```bash
# Install dependencies
make install
# or: bundle install

# Serve the site locally with auto-reload
make serve
# or: bundle exec jekyll serve --host 0.0.0.0 --port 4000 --livereload

# Build the site for production
make build
# or: bundle exec jekyll build

# Test the build
make test
```

### Docker Development
```bash
# GitHub Pages compatible (RECOMMENDED - exact environment match)
make github-pages-serve

# GitHub Pages with Docker Compose
make github-pages-up
make github-pages-down

# Build and serve using custom Docker image
make serve-docker

# Use official Jekyll Docker image (fastest setup)
make quick-serve

# Docker Compose (recommended for development)
make compose-up
make compose-down

# Build only using Docker
make build-docker
```

### Utility Commands
```bash
# Clean generated files
make clean

# Open shell in Docker container
make docker-shell

# Show all available commands
make help
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