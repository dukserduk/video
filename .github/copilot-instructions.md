
# GitHub Copilot Instructions for this Repo

## 1. Big Picture & Architecture
- Static brochure/portfolio site for "DESIGN STUDIO Dukserduk" with multiple standalone HTML pages: [index.html](index.html) (home), [portfolio.html](portfolio.html), [request.html](request.html), [templates.html](templates.html), [terms.html](terms.html), and [business.html](business.html).
- Each page is self-contained (own `<head>`, meta viewport, inline `<style>`). There is **no build system or backend**; everything is pure HTML/CSS with a small inline JavaScript snippet.
- The only JavaScript is in [request.html](request.html): a vanilla script that shows/hides a templates hint and builds a `mailto:` URL from the form, then redirects `window.location.href` to open the user’s email client.
- Treat this as a static site; do not introduce frameworks or bundlers unless explicitly requested.

## 2. Layout, Patterns & Conventions
- Shared look and feel: pink header background `#ffb3b3`, light background (`#ffe4e6` on main pages, `#f5f5f7` on terms/business), system-ui font, centered content with `max-width: 960px`.
- Header + nav pattern is repeated across pages (brand text + nav links for Home/Portfolio/Request/Templates/Terms/Business). When adding pages or changing navigation, update all headers/footers to stay consistent.
- On the home page [index.html](index.html), use `.card` sections for key content blocks.
- On the portfolio page [portfolio.html](portfolio.html), use `.projects` + `.project-card` for grid items; follow the spacing and typography already used there when adding projects.
- On the templates page [templates.html](templates.html), use `.templates-grid` + `.template-card` + `.preview-box` when adding new template slots or real YouTube embeds.
- Terms and business pages ([terms.html](terms.html), [business.html](business.html)) use a white `.container` card centered in the page for long-form text (terms list, business info).

## 3. Forms & JavaScript
- Keep any new interactivity simple and inline (like the existing script in [request.html](request.html)); prefer vanilla JS over frameworks.
- The request form relies on standard HTML validation (`required`, `maxlength`) plus a JS `submit` handler that:
	- Prevents default submission.
	- Reads values from visible fields.
	- Builds a multi-line email body and subject.
	- Navigates to a `mailto:` link to open the default email client.
- If you add or rename form fields, update the script’s DOM queries and `lines` array to match, preserving the mailto-based workflow.
- The project-type `<select>` toggles a text hint linking to [templates.html](templates.html) when the "Build From Template" option is selected; keep that behavior aligned if options change.

## 4. Assets & File Organization
- Static files live at the repo root (HTML pages) plus asset folders: [assets](assets), [images](images%20), and [videos](videos).
- When adding images or video thumbnails, place them under these folders and reference via relative paths from the HTML pages.
- Favor lightweight formats (SVG for icons, compressed PNG/JPEG for images, embedded/linked YouTube for video previews) to keep the site small.

## 5. Workflows & Tooling
- There is **no npm/pip/CLI workflow**. To preview, open any HTML file directly in a browser or use a simple static server (e.g., VS Code Live Server).
- If you propose additional tooling (e.g., a CSS file shared across pages), keep the current open-in-browser behavior working and document any new steps in this repo.

## 6. AI Agent Collaboration
- Make small, focused edits: adjust one page or section at a time and maintain visual consistency across headers, nav, and footer.
- Preserve existing colors, typography, and layout unless a redesign is explicitly requested.
- When adding new content, mirror existing patterns: cards on [index.html](index.html), project cards on [portfolio.html](portfolio.html), template cards on [templates.html](templates.html), and long-form text inside `.container` on [terms.html](terms.html) / [business.html](business.html).
- If something about deployment or hosting is unclear, state assumptions and suggest 1–2 concrete static-hosting options rather than introducing complex infrastructure.
