
# GitHub Copilot Instructions for this Repo

## 1. Big Picture & Architecture
- This repo is a static portfolio site with multiple HTML pages: [index.html](index.html) (home), [portfolio.html](portfolio.html), [request.html](request.html), and [templates.html](templates.html).
- All pages are standalone HTML with inline `<style>` blocks. There is **no JavaScript, build step, or backend**.
- The site uses a consistent layout: dark sticky header (brand: "MY PORTFOLIO"), navigation links, and a centered main content area (`max-width: 960px`).
- Treat the project as a static site only; ignore legacy Joomla-related files and patterns.

## 2. Layout, Patterns & Conventions
- Each HTML file is self-contained: includes its own `<head>`, meta viewport, title, and CSS.
- The `<header>` and navigation markup (with classes `brand`, `nav-links`, `active`) is duplicated across all pages. **Always copy this structure for new pages.**
- Mobile-first, centered design: body background `#f5f5f7`, header `#111827`, accent blue `#3b82f6`, text `#4b5563`.
- Use `.card` for home page sections, `.projects` grid and `.project-card` for portfolio items. Follow these class names and spacing for new content.
- If the site grows, consider extracting shared CSS to a `styles.css` file, but **do not change class names or layout unless requested**.

## 3. Workflows & Tooling
- **No build, test, or package manager**: open any HTML file directly in a browser to preview.
- You may suggest using a static file server or VS Code Live Server for live preview, but do **not** add Node.js or CLI tooling unless the user asks.
- If adding tooling (e.g., CSS bundler, static site generator), document all commands and keep the default open-in-browser workflow working.

## 4. Assets & File Organization
- No images or fonts by default. If adding, create an `assets/` or `images/` directory at the repo root and use relative paths.
- Use web-friendly formats (SVG, optimized PNG/JPEG) and keep assets small unless instructed otherwise.
- Do not modify `.gitignore`/`.gitattributes` unless asked.

## 5. AI Agent Collaboration
- Make small, composable changes: update one page/component at a time, preserve the current style unless a redesign is requested.
- Match existing HTML/CSS: use semantic elements, consistent spacing, and the system-ui font stack.
- Add new patterns (e.g., cards, forms) to [portfolio.html](portfolio.html) or a new page first, using simple, readable markup.
- If workflow or deployment is unclear, state so and offer 1–2 concrete options.

## 6. Examples & References
- See [index.html](index.html) for the home layout and `.card` usage.
- See [portfolio.html](portfolio.html) for the project grid and `.project-card` pattern.
- [request.html](request.html) and [templates.html](templates.html) follow the same header/nav structure.
