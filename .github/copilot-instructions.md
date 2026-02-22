# Copilot Instructions for Digital Heritage Studio Website

## Project Overview
Static marketing website for Digital Heritage Studio (www.makememovie.org), a video/photo storytelling service. Built with vanilla HTML, CSS, and JavaScript with no build tools or frameworks.

## Key Architecture Patterns

### Configuration-Driven Design
All site-wide settings are centralized in [config.js](../config.js). This is the **single source of truth** for:
- Brand name, tagline, copyright info
- Video player settings (source, dimensions, autoplay, controls)
- Social media links
- Contact email
- SEO metadata (title, description, keywords)

**When modifying site content**: Update config.js first, then reference `window.siteConfig` in HTML where applicable.

### Page Structure & Styling Pattern
Each HTML page uses a two-class pattern on `<body>`:
- **First class**: `page-home` / `page-request` / `page-business` / `page-terms` (specific page)
- **Second class**: `page-main` (marketing pages) or `page-doc` (document pages like business/terms)

In [assets/styles.css](../assets/styles.css):
```css
body.page-main { /* Home, Request: pink background */ }
body.page-doc { /* Terms, Business: light gray background */ }
body.page-home header { /* Home-specific header styling */ }
```

This pattern enables efficient page-specific styling without separate CSS files.

### Contact Form Integration
[request.html](../request.html) uses EmailJS for form submission:
- Public Key: `nYLEW5Sa31jlwJM6g`
- Service ID: `service_sldhkm7`
- Template ID: `template_xpj0sz7`

The form has inline JavaScript that falls back to `mailto:` if EmailJS fails. Keep EmailJS credentials in the inline script - do not extract to config.js for security.

### Shared Components
- **Navigation**: Identical header with brand logo (SVG camera icon) and nav links on all pages
- **Footer**: Social media links (Facebook, Instagram, YouTube) and copyright, consistent across all pages
- **Color scheme**: Primary `#ffb3b3` (pink/salmon), secondary `#3b82f6` (blue for links/icons)

## Development Workflow

### File Organization
```
/
├── config.js              # Site configuration (update first for content changes)
├── index.html             # Home page
├── request.html           # Contact/Request form (has EmailJS script)
├── business.html          # Business services page
├── terms.html             # Terms & conditions
├── CNAME                  # GitHub Pages custom domain
├── assets/
│   ├── styles.css         # Single CSS file (~811 lines)
│   └── background.jpeg    # Page background
└── .github/workflows/
    └── auto-merge.yml     # Auto-merges PRs with "auto-merge" label
```

### Deployment
- Hosted on GitHub Pages (`www.makememovie.org` via CNAME)
- Automatic deployment on push to `main` branch
- PRs labeled `auto-merge` are auto-merged via workflow

### No Build Process
This is a static site - changes are deployed immediately on merge. No npm, webpack, or build steps. Keep it simple.

## Common Tasks

### Updating Site-Wide Text
1. Edit values in `config.js` (brand name, email, copyright year, etc.)
2. Reference via `window.siteConfig` in HTML if needed
3. For fixed content not in config, edit HTML directly

### Adding a New Page
1. Create new HTML file (e.g., `gallery.html`)
2. Add appropriate body classes: `<body class="page-main page-gallery">` or `<body class="page-doc page-gallery">`
3. Copy navigation header and footer from existing page (keep consistent)
4. Add CSS rules in styles.css using page-specific selectors if needed
5. Update nav links in ALL pages to include new page

### Modifying Styling
- Edit [assets/styles.css](../assets/styles.css) directly
- Use page-specific selectors: `body.page-name selector { }`
- Test across different page types (page-main vs page-doc) for consistency

### Updating Social Media/Contact Links
Edit `config.js` under `social` and `contact` sections. Footer will auto-generate links from these values where implemented.

## Conventions

- Use semantic HTML (`<header>`, `<main>`, `<footer>`, `<section>`, `<article>`)
- Include `aria-label` on interactive elements and `aria-hidden="true"` on decorative SVGs
- Responsive layout: Use flexible widths, `max-width: 960px` for content containers
- Colors: Primary `#ffb3b3`, text `#222` or `#4b5563`, links `#3b82f6`
- All pages must include brand logo SVG in header and footer social links for consistency

## Key Dependencies
- EmailJS (CDN, form only): https://cdn.jsdelivr.net/npm/@emailjs/browser@4/dist/email.min.js
- No other external dependencies except CDN-hosted Email.js

## Branch Strategy
- Default branch: `main`  
- Current branch: `newmain`
- Feature branches should target appropriate branch for merging
- Use "auto-merge" label on PRs to auto-merge via GitHub Actions
