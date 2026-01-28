# CLAUDE.md - AI Assistant Guide for PersonalSite

This document provides context for AI assistants working with this codebase.

## Project Overview

This is **Alan Tanner's personal portfolio website** built with Hugo static site generator and the Blowfish theme. The site serves as a professional landing page, blog, and digital presence.

- **Live Site**: https://www.alanctanner.com/
- **Hosting**: Azure Static Web Apps
- **CI/CD**: GitHub Actions (auto-deploys on push to master)

## Technology Stack

| Component | Technology | Version/Details |
|-----------|------------|-----------------|
| Static Site Generator | Hugo | v0.154.5 |
| Theme | Blowfish v2 | v2.97.0 - Git submodule in `themes/blowfish/` |
| Language | Go | 1.22 (for Hugo modules) |
| Hosting | Azure Static Web Apps | Serverless |
| Content Format | Markdown | With TOML frontmatter |
| Analytics | Google Analytics, Firebase, Fathom | Configured in params.toml |

## Directory Structure

```
PersonalSite/
├── config/_default/          # Hugo configuration files
│   ├── config.toml           # Main site config (URL, theme, taxonomies)
│   ├── params.toml           # Theme parameters and feature flags
│   ├── markup.toml           # Markdown rendering settings
│   ├── module.toml           # Hugo module imports (Blowfish)
│   ├── menus.en.toml         # Navigation menu structure
│   └── languages.en.toml     # Language and author settings
├── content/                  # All Markdown content
│   ├── _index.md             # Homepage content
│   ├── about-me.md           # About page
│   ├── resume.md             # Resume page (embeds PDF)
│   ├── alanbot.md            # AI chatbot demo page
│   └── posts/                # Blog posts directory
│       └── [PostName]/       # Each post in its own folder
│           └── index.md      # Post content
├── layouts/shortcodes/       # Custom Hugo shortcodes
│   ├── audio.html            # Audio player with captions
│   └── embed-pdf.html        # PDF viewer using PDF.js
├── assets/                   # Media assets (processed by Hugo)
│   ├── img/                  # Images
│   └── audio/                # Audio narration files (MP3)
├── data/authors/             # Author metadata (JSON files)
├── static/                   # Static files served as-is
│   ├── AlanTannerResumePublic.pdf
│   └── [favicons, icons, images]
├── themes/blowfish/          # Theme (Git submodule - DO NOT EDIT)
├── .github/workflows/        # GitHub Actions deployment workflow
└── go.mod                    # Hugo module dependencies
```

## Configuration Files

### Main Configuration (`config/_default/config.toml`)
- Base URL, site title, theme selection
- Taxonomies: tags, categories, authors, series
- Pagination settings (10 items per page)
- Output formats (HTML, RSS, JSON)

### Theme Parameters (`config/_default/params.toml`)
- Visual appearance (dark mode default, color scheme)
- Homepage layout configuration
- Article display settings (date, author, TOC, etc.)
- External service integrations (Firebase, Buy Me a Coffee)
- Feature flags (search, code copy, etc.)

### Navigation (`config/_default/menus.en.toml`)
- Menu items with weights for ordering
- Links: About, Blog, Resume, LinkedIn

## Development Workflow

### Local Development
```bash
# Start Hugo development server with live reload
hugo server

# Preview at http://localhost:1313
```

### Building for Production
```bash
# Build static site to public/ directory
hugo
```

### Deployment
Deployment is **automatic** via GitHub Actions:
1. Push changes to `master` branch
2. GitHub Action builds with Hugo 0.154.5
3. Deploys to Azure Static Web Apps

The workflow file: `.github/workflows/azure-static-web-apps-thankful-bush-037ae690f.yml`

## Content Creation

### Creating a New Blog Post

1. Create a new directory under `content/posts/`:
   ```bash
   mkdir -p content/posts/My-New-Post
   ```

2. Create `index.md` with frontmatter:
   ```markdown
   ---
   title: "My Post Title"
   date: 2026-01-23T12:00:00-05:00
   summary: "Brief description for listings"
   draft: false
   categories: ["Category"]
   tags: ["tag1", "tag2"]
   authors: ["alanctanner"]
   showAuthor: false
   toc: false
   ---

   Post content in Markdown...
   ```

3. Place any post-specific images in the same directory as `index.md`

### Frontmatter Options

| Field | Type | Description |
|-------|------|-------------|
| `title` | string | Post title |
| `date` | ISO 8601 | Publication date with timezone |
| `summary` | string | Short description for listings |
| `draft` | boolean | Set `true` to hide from production |
| `categories` | array | Content categories |
| `tags` | array | Content tags |
| `authors` | array | Author IDs from `data/authors/` |
| `showAuthor` | boolean | Display author info |
| `toc` | boolean | Show table of contents |

### Using Custom Shortcodes

**Audio Player** (for narrations):
```markdown
{{< audio src="audio/filename.mp3" caption="Audio description" >}}
```

**PDF Embed**:
```markdown
{{< embed-pdf url="/document.pdf" >}}
```

**Note**: Static PDFs go in `static/`, audio files in `assets/audio/`

## Key Conventions

### Code Style
- TOML for Hugo configuration
- Markdown with TOML frontmatter for content
- HTML for shortcodes

### Naming Conventions
- Post directories: `PascalCase` or `Snake_Case` (e.g., `Hello-World`, `Built_with_Hugo`)
- Config files: lowercase with hyphens
- Authors: lowercase IDs matching JSON filenames

### Theme Customization
- **DO NOT** modify files in `themes/blowfish/` - it's a Git submodule
- Override theme templates by creating files in `layouts/` with the same path
- Custom shortcodes go in `layouts/shortcodes/`

### Static Assets
- Favicons and site icons: `static/`
- Images for posts: Same directory as post's `index.md`
- Shared images: `assets/img/`
- Audio files: `assets/audio/`

## Important Commands

```bash
# Development
hugo server              # Start dev server with live reload
hugo server -D           # Include draft posts

# Build
hugo                     # Build to public/
hugo --minify            # Build with minification

# Check theme submodule
git submodule update --init --recursive
```

## Dependencies & Updates

Dependencies are managed via:
- **Go Modules** (`go.mod`): Blowfish theme v2
- **Git Submodules** (`.gitmodules`): Blowfish theme source
- **Dependabot** (`.github/dependabot.yml`): Automated updates for:
  - GitHub Actions
  - Git submodules
  - Go modules

## External Integrations

| Service | Purpose | Configuration Location |
|---------|---------|----------------------|
| Google Analytics | Site analytics | `config.toml` (googleAnalytics) |
| Firebase | Analytics/engagement | `params.toml` (firebase section) |
| Fathom Analytics | Privacy-friendly analytics | `params.toml` |
| Buy Me a Coffee | Donations widget | `params.toml` (buymeacoffee) |
| Azure Static Web Apps | Hosting | GitHub Actions workflow |

## Troubleshooting

### Theme Not Loading
```bash
git submodule update --init --recursive
```

### Build Errors
- Check Hugo version matches workflow (v0.154.5)
- Verify frontmatter TOML syntax
- Check for broken shortcode references

### Local Preview Issues
- Ensure `hugo server` is running
- Check for port conflicts (default: 1313)
- Clear `resources/_gen/` if caching issues occur

## File Reference

| File | Purpose |
|------|---------|
| `config/_default/config.toml` | Main Hugo configuration |
| `config/_default/params.toml` | Theme and feature settings |
| `content/_index.md` | Homepage content |
| `data/authors/alanctanner.json` | Primary author metadata |
| `layouts/shortcodes/*.html` | Custom shortcodes |
| `static/AlanTannerResumePublic.pdf` | Public resume |
| `.github/workflows/*.yml` | CI/CD deployment |
