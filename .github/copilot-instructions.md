# GitHub Copilot Instructions for this Repo

## 1. Current State & Big Picture
- This repo is a very small static site with two HTML pages: [index.html](index.html) (home) and [portfolio.html](portfolio.html).
- Pages are plain HTML with inline `<style>` blocks (no JavaScript, no build step, no backend).
- Both pages share the same overall layout: dark sticky header with brand "MY PORTFOLIO", navigation links, and a centered main content area with max-width 960px.
- Older Joomla-oriented files (e.g., .gitignore/.gitattributes patterns) are historical; treat the active "application" as this static portfolio, not a Joomla app.

## 2. Layout & Conventions
- Each page is self-contained: HTML, meta viewport, title, and CSS are defined directly in the file.
- Navigation is duplicated between pages; keep the header structure and class names (`brand`, `nav-links`, `active`) consistent when adding new pages.
- Styling is mobile-first and centered: `max-width: 960px`, body background `#f5f5f7`, header `#111827`, accent blue `#3b82f6`, and gray text `#4b5563`.
- Content uses simple cards/sections (`.card` on the home page, `.projects` grid and `.project-card` on the portfolio page) for elevation and spacing.

## 3. Architecture Guidance for New Code
- Treat this as a static site first; favor additional HTML pages and shared CSS over introducing heavy frameworks unless the user explicitly asks.
- When adding new pages, copy the existing `<header>`/`<nav>` structure so the brand and navigation remain visually identical across the site.
- Consider extracting common styles into a shared CSS file (e.g., `styles.css`) if the site grows, but keep class names and current visual design intact unless the user wants a redesign.
- Use progressive enhancement if you add JavaScript: pages should remain usable with HTML/CSS alone.

## 4. Workflows, Preview, and Tooling
- There is no build system, package manager, or tests configured; you can open [index.html](index.html) or [portfolio.html](portfolio.html) directly in a browser to preview.
- It is safe for an agent to suggest using a static file server or VS Code Live Server extension for live-reload previews, but do not add Node/CLI tooling without user confirmation.
- If you introduce any tooling (e.g., a CSS bundler or static site generator), document commands and new files clearly and keep the default workflow (open HTML in browser) working.

## 5. Assets and File Organization
- There are currently no image or font assets; if adding them, prefer creating an `assets/` or `images/` directory at the repo root and linking with relative paths.
- Avoid committing large binary media; use compressed web-friendly formats (SVG, optimized PNG/JPEG) and small demo assets unless the user instructs otherwise.
- Leave existing `.gitignore`/`.gitattributes` patterns in place unless the user asks to clean them up; do not rely on them as evidence of a Joomla app.

## 6. Collaboration Guidelines for AI Agents
- Keep changes small and composable: update one page or component at a time and preserve the current visual style unless explicitly asked to redesign.
- Match existing HTML and CSS style: semantic elements (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`), consistent spacing, and system-ui font stack.
- When introducing new patterns (e.g., a project card layout or a contact form), add them first to [portfolio.html](portfolio.html) or a new page and keep markup simple and readable.
- If you cannot infer a workflow (e.g., deployment target, preferred tooling), state that clearly and present 1–2 concrete options instead of guessing.
