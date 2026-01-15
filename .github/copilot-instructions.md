
## GitHub Copilot Instructions for this Repo

### 1. Big Picture & Architecture
- Static brochure site for "VIDEO&PHOTO DESIGN STUDIO" with four standalone HTML pages: [index.html](../index.html) (home), [request.html](../request.html) (form), [terms.html](../terms.html) (legal), and [business.html](../business.html) (B2B offer).
- Pure HTML/CSS with small inline scripts; **no build system, bundler, backend, or tests**. Pages must work when opened directly in a browser.
- Shared styling lives in [assets/styles.css](../assets/styles.css). Do not add JS/CSS frameworks or tooling unless explicitly requested.

### 2. Layout, Styling & Navigation
- Global look: header `#ffb3b3`, marketing background `#ffe4e6` on `body.page-main`, doc background `#f5f5f7` on `body.page-doc`, system‑UI font, content centered at `max-width: 960px`.
- Navigation (brand + Home / Request / Terms / Business) is duplicated in all HTML pages. When adding/renaming links, keep header nav and footer links in sync everywhere.
- Marketing pages (`index.html`, `request.html`) use `.card` or `form` blocks as main content; doc pages (`terms.html`, `business.html`) wrap text in `.container`.
- Reuse existing classes from [assets/styles.css](../assets/styles.css) and match spacing/typography; avoid new layout systems.

### 3. Multilingual Content Patterns
- All pages use a `.language-module` with `<select id="languageSelect">` for `en`, `es`, `ru`, `uk`, `zh` and an inline IIFE that sets `document.documentElement.lang`.
- Home + Request pages ([index.html](../index.html), [request.html](../request.html)):
  - `translations` is a JS object keyed by language; text is wired to specific elements via stable `id`s (e.g., `page-title`, `lead-text`, `label-name`).
  - When changing copy, edit the `translations` entries and keep the element `id` list in sync with `applyLanguage`.
  - New localizable text should get an `id` and be added to both `translations` and `applyLanguage`.
- Terms + Business pages ([terms.html](../terms.html), [business.html](../business.html)):
  - `translations[lang].body` contains the full inner HTML for the main content container (`#terms-body` / `#business-body`), which is replaced wholesale on language change.
  - To change or add sections there, edit all language `body` strings consistently; do not rely on the initial static HTML since it is overwritten.

### 4. Request Form & JavaScript Behavior
- The only form is in [request.html](../request.html); its inline script handles:
  - Language switching for labels, select options, hints, terms text, and the submit button.
  - Showing/hiding `#templates-link-wrapper` when `projectType === 'template'`.
  - Mailto submission: `submit` handler prevents default, reads all fields, builds a plain‑text body, and navigates to `mailto:request@makememovie.org?...`.
- If you modify form fields or options:
  - Update HTML `id`s and the corresponding `getElementById`/`options[...]` usages.
  - Update every affected entry in the `translations` object (all languages).
  - Keep the email body lines array in sync so all important inputs appear in outgoing emails.
- Any new interactivity should use a small inline IIFE on that page with vanilla JS only.

### 5. Assets, Media & External Embeds
- Shared CSS (including the `back.jpg` background) is under [assets/styles.css](../assets/styles.css). Additional media should live under `assets/`, `images/`, or `videos/` with relative links.
- Prefer lightweight media (compressed images, short clips, optional embeds like YouTube). Avoid large JS bundles or heavy libraries.

### 6. Workflows, Preview & Testing
- There are **no** automated build, lint, or test workflows.
- To validate changes, open the HTML files directly in a browser or run a simple static server (e.g., VS Code Live Server) from the repo root.
- Each page is self‑contained (own `<head>`, `<body>`, and script); new pages should follow this pattern and not depend on a build step.

### 7. AI Agent Collaboration Guidelines
- Make small, focused edits to a single page or feature at a time, and keep shared structures (`header`, `.nav-links`, `.language-module`, `.container`, footer) consistent across all pages.
- When extending content, copy the closest existing pattern (e.g., add another paragraph/card in [index.html](../index.html), or another numbered item in [terms.html](../terms.html)) instead of inventing new layout primitives.
- Preserve the existing visual style (colors, typography, spacing) and assume deployment to simple static hosting (GitHub Pages, Netlify, etc.)—no server‑side code or dynamic backends.
