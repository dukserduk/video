
## GitHub Copilot Instructions for this Repo

### 1. Big Picture & Architecture
- Static brochure/portfolio site for a small "VIDEO&PHOTO DESIGN STUDIO" with standalone HTML pages: [index.html](../index.html) (home), [portfolio.html](../portfolio.html), [request.html](../request.html), [templates.html](../templates.html), [terms.html](../terms.html), [business.html](../business.html), and [help.html](../help.html).
- All pages are pure HTML/CSS with inline scripts; there is **no build system or backend**. Pages are intended to open directly in a browser or via a simple static server.
- Shared styling lives in [assets/styles.css](../assets/styles.css); do not introduce frameworks or bundlers unless explicitly requested.

### 2. Layout, Styling & Navigation
- Global look: pink header background `#ffb3b3`, light main background `#ffe4e6` (`body.page-main`) and light grey doc background `#f5f5f7` (`body.page-doc`), system-ui font, main content centered at `max-width: 960px`.
- Navigation pattern repeats across pages: brand text plus links for Home / Portfolio / Request / Templates / Terms / Business / Help. Keep nav and footer links in sync on all pages when adding or renaming sections.
- Home and main marketing pages (`body.page-main`) use `.card` containers for primary content blocks; portfolio uses `.projects` + `.project-card`; templates uses `.templates-grid` + `.template-card` + `.preview-box` as the core card pattern.
- Terms, business, and help pages (`body.page-doc`) put long-form text inside a white `.container` card for readability.
- When adding new sections, reuse the existing classes from [assets/styles.css](../assets/styles.css) instead of inlining new styles.

### 3. Multilingual Content Pattern
- Most pages include a `.language-module` with a `<select id="languageSelect">` for `en`, `es`, `ru`, `uk`, and `zh`, plus an inline IIFE script that:
	- Defines a `translations` object keyed by language.
	- Looks up content elements by stable `id` values (e.g., `page-title`, `lead-text`, `proj1-title`).
	- Updates `document.documentElement.lang` and replaces `textContent`/`innerHTML` on language change.
- When you change text that participates in translations, update the corresponding `translations` entry instead of hardcoding new copy.
- If you add new translated fields, follow the same pattern: assign an `id` in HTML and wire it into the `translations` object and `applyLanguage` function on that page.

### 4. Request Form & JavaScript Behavior
- The main interactive form is in [request.html](../request.html): it uses vanilla JS for:
	- Language switching (same pattern as other pages, including translated labels and option text).
	- Showing the template hint: the `projectType` `<select>` toggles visibility of `#templates-link-wrapper` when the "Build From Template" option is selected.
	- Form submission via mailto: the `submit` handler prevents default, reads field values, builds a subject/body, and navigates to a `mailto:` URL to open the user’s email client.
- If you rename or add form fields, update:
	- The DOM queries in the script (`getElementById` targets and IDs in HTML).
	- The `translations` entries for labels, hints, and button text.
	- The email composition logic so the message still includes all important user input.
- Keep interactivity small and inline, in the same style as the existing IIFEs; prefer vanilla JS and avoid adding dependencies.

### 5. Assets & Media
- Shared CSS is under [assets/styles.css](../assets/styles.css); background images and any future media should live under the assets, images, or videos folders.
- Use relative links from HTML files (e.g., `assets/styles.css`, `images/...`) and prefer lightweight formats (compressed PNG/JPEG, SVG) and external video hosting (YouTube embeds) where possible.

### 6. Workflows & Preview
- There is no CLI build or test step. To preview changes, either:
	- Open any `*.html` file directly in a browser, or
	- Use a simple static server such as VS Code Live Server pointing at the repo root.
- Keep all pages self-contained and working when opened individually (each page includes its own `<head>` and script block).

### 7. AI Agent Collaboration
- Make small, focused edits to one page or feature at a time and keep header/nav/footer consistent across all pages.
- Preserve the overall visual style (colors, typography, spacing) and reuse existing utility classes (`.card`, `.projects`, `.templates-grid`, `.container`, `.language-module`, etc.).
- When adding new UX elements (cards, sections, or translated text), copy existing patterns from the closest page (home, portfolio, templates, or doc pages) instead of inventing new structures.
- If deployment or hosting behavior matters, assume a static host (GitHub Pages, Netlify, etc.) and avoid adding server-side code.
