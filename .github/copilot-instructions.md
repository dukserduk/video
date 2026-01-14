
## GitHub Copilot Instructions for this Repo

### 1. Big Picture & Architecture
- Static brochure site for a small "VIDEO&PHOTO DESIGN STUDIO" with standalone HTML pages: [index.html](../index.html) (home), [request.html](../request.html), [terms.html](../terms.html), and [business.html](../business.html).
- All pages are pure HTML/CSS with minimal inline scripts; there is **no build system, bundler, or backend**. Pages are meant to open directly in a browser or via a simple static server.
- Shared styling lives in [assets/styles.css](../assets/styles.css); do not introduce JS frameworks, CSS frameworks, or tooling unless explicitly requested.

### 2. Layout, Styling & Navigation
- Global look: pink header background `#ffb3b3`, light marketing background `#ffe4e6` on `body.page-main`, and light grey doc background `#f5f5f7` on `body.page-doc`, with a system‑UI font and main content centered at `max-width: 960px`.
- Navigation is duplicated across all pages: brand line plus links for Home / Request / Terms / Business. When adding or renaming sections, keep header nav and footer links in sync on **every** HTML file.
- Home and other marketing pages (`body.page-main`) use `.card` as the main content container; doc pages (`terms.html`, `business.html`) wrap long text inside `.container`.
- Reuse existing classes from [assets/styles.css](../assets/styles.css) when adding UI elements instead of inlining new styles; match the existing spacing and typography.

### 3. Multilingual Content Pattern
- Most pages include `.language-module` with `<select id="languageSelect">` for `en`, `es`, `ru`, `uk`, `zh` and an inline IIFE that:
  - Defines a `translations` object keyed by language.
  - Grabs elements by stable `id`s (e.g., `page-title`, `lead-text`, `proj1-title`, `t3-body`).
  - Calls `applyLanguage(lang)` to set `document.documentElement.lang` and update `textContent` or `innerHTML`.
- When changing any translatable text, update the corresponding entries in that page’s `translations` object instead of hardcoding new copy in HTML.
- For new text that should be localized, assign an `id` in the HTML and wire it into both the `translations` object and `applyLanguage` logic on that page; follow the per‑page patterns in [index.html](../index.html), [request.html](../request.html), [terms.html](../terms.html), and [business.html](../business.html).

### 4. Request Form & JavaScript Behavior
- The only real form is in [request.html](../request.html); its inline script handles:
  - Language switching for labels, option text, hints, and the submit button.
  - Toggling `#templates-link-wrapper` when `projectType` is set to the "template" option.
  - Mailto submission: on `submit`, it prevents default, reads all fields, formats a plain‑text body, and navigates to `mailto:request@makememovie.org?...`.
- If you rename/add form fields or options, update:
  - HTML `id` attributes and all corresponding `getElementById` calls.
  - The `translations` entries (labels, option strings, hints, terms text, button label).
  - The email composition logic so the mail body still includes all critical inputs.
- Keep any new interactivity small and inline (another IIFE in the same file), using vanilla JS only.

### 5. Assets, Media & External Embeds
- Shared CSS is under [assets/styles.css](../assets/styles.css); background image is referenced as `back.jpg` from that folder. Additional images/videos should go under `assets/`, `images/`, or `videos/` and be linked with relative paths.
- Prefer lightweight media: compressed images, optional external embeds (YouTube, etc.), and short clips.
- Do not add heavy client‑side libraries (no large JS bundles) unless the user explicitly requests them; this site targets simple static hosting.

### 6. Workflows, Preview & Testing
- There are **no** build, lint, or automated test steps in this repo.
- To check changes, open any `*.html` file directly in a browser or run a simple static server (e.g., VS Code Live Server) from the repo root.
- Each page is self‑contained (has its own `<head>` and script block); ensure any new page follows that pattern and works when opened on its own.

### 7. AI Agent Collaboration Guidelines
- Make small, focused edits to one page or feature at a time and keep shared structures (header nav, footer, `.language-module`, `.container`) consistent across all HTML files.
- When extending content, copy the closest existing pattern (e.g., add another section in [index.html](../index.html) or extend doc sections in [terms.html](../terms.html) / [business.html](../business.html)) instead of designing a new layout.
- Preserve the existing visual style (colors, typography, spacing) and avoid introducing new design systems.
- Assume deployment on a static host (GitHub Pages, Netlify, etc.); do not introduce server‑side code or dynamic backends.
