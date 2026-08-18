# Copilot Instructions for nw-circle

## Project Overview

nw-circle is a documentation repository that shares networking circle resources and knowledge. The project publishes technical articles and documents for the Network Circle (ネットワークサークル) at a technical college.

## Repository Structure

- **articles/** - Source markdown files with Zenn frontmatter. Each article has:
  - YAML frontmatter (title, emoji, type, topics, published status)
  - Markdown content (tables, technical specifications, configurations)
  - Naming convention: `{description}_{revision}.md` (e.g., `cisco-cli-config_rev1.md`)

- **documents/** - HTML output files auto-generated from articles. Named to match article sources with `.html` extension.

- **notes/** - Knowledge-sharing resources from circle leadership (bookmarks, reference materials).

- **images/** - Images used in articles.

## Build and Deployment

### Setup
```bash
npm install
```

### Content Publishing
Articles in `articles/` are published via Zenn CLI. To convert markdown to HTML:
```bash
npx zenn  # Run Zenn CLI commands (preview, build, etc.)
```

The site is deployed to Vercel and accessible at https://nw-circle.vercel.app/

### Entry Point
- **index.html** - Browser navigation hub providing links to documents and notes directories
- No automated tests are configured (package.json indicates testing is not yet set up)

## Article Format and Conventions

### Frontmatter Structure
All articles must include YAML frontmatter:
```yaml
---
title: "Article Title"
emoji: "🌐"
type: "tech" # tech or idea
topics: ["topic1", "topic2"]
published: true
---
```

### Content Guidelines
- Use markdown with tables for reference material (especially for command lists, configurations, etc.)
- Include descriptive headers organizing information hierarchically
- Add practical examples or notes in table remarks column
- Japanese language is the primary language for documentation

### Versioning
- Use revision numbers in filenames: `_rev1.0`, `_rev1.1`, `_rev2.0`, etc.
- Increment revision when making updates to existing articles

## Key Topics

The repository covers technical documentation for:
- Cisco CLI configuration commands and network setup
- NAS (Network Attached Storage) configuration
- Network Circle planning and strategy
- IPv4 and IPv6 configuration

## Important Notes

- Gitignored directories include: `books/`, `tests/`, `pictures/`, `trash/`, `node_modules/`
- All published content uses Japanese language
- Document organization prioritizes accessibility through the HTML index
- Changes to articles in `articles/` should be reflected in corresponding HTML files in `documents/`
