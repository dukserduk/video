
## GitHub Copilot Instructions for this Repo

### 1. Big Picture & Architecture
- **Static brochure site** for "VIDEO&PHOTO DESIGN STUDIO" with four standalone HTML pages:
  - [index.html](../index.html) — home/marketing (introduces services, offers portfolio-building deal)
  - [request.html](../request.html) — project request form (only interactive form in the site)
  - [terms.html](../terms.html) — legal terms and conditions
  - [business.html](../business.html) — B2B ad video offer
- **Zero external dependencies**: Pure HTML/CSS + inline vanilla JavaScript. No build system, bundler, framework, backend, database, or tests.
- Pages must work when opened directly in a browser (file:// protocol) or served via simple HTTP. Deployment target: static hosting (GitHub Pages, Netlify).
- **Shared styling** in [assets/styles.css](../assets/styles.css); media files (`background.jpeg`, `back.jpg`) in [assets/](../assets/).
- **Do not add** npm, frameworks, build tools, or external JS libraries unless explicitly requested by the user.

### 2. Layout, Styling & Design System
- **Color palette**: Header background `#ffb3b3` (pink), marketing pages background `#ffe4e6` (light pink), doc pages background `#f5f5f7` (light gray), accent blue `#3b82f6`, text `#222` or `#4b5563`.
- **Typography**: `system-ui` font family (no custom fonts), `line-height: 1.5`, responsive sizing (`0.8rem` for small text, `2rem` for h1).
- **Layout**: All content centered with `max-width: 960px` margin auto; `1.5rem` padding on sides for mobile.
- **Page classes** (set on `<body>`):
  - `page-main` → marketing pages (index, request) with pink background
  - `page-doc` → documentation pages (terms, business) with gray background
- **Navigation structure** (duplicated on all pages—keep in sync!):
  - Header: brand name + nav links (Home / Request / Terms / Business), with `.active` class on current page
  - Footer: links + copyright
- **Shared content containers**:
  - `.card` — white rounded box for main content on marketing pages (used in index, request)
  - `.container` — white rounded box for doc pages (terms, business)
  - `.form-group` — vertical stack for form fields (request.html)
- **Always match existing spacing and typography**; avoid creating new layout classes or grid systems.

### 3. Multilingual Content Patterns
- All pages feature a `.language-module` with `<select id="languageSelect">` supporting: `en`, `es`, `ru`, `uk`, `zh`. An inline IIFE listens for change events and calls `applyLanguage(lang)` to set `document.documentElement.lang`.
- **Marketing + Form pages** ([index.html](../index.html), [request.html](../request.html)):
  - `translations = { en: {...}, es: {...}, ... }` — JS object with language keys, each containing copy strings
  - Elements to translate are wired via stable `id` attributes (e.g., `id="page-title"`, `id="label-name"`)
  - `applyLanguage()` function updates element text/HTML via `getElementById()` and applies translations
  - **Pattern**: For each new translatable string, add an `id`, create a `<span>` or label with that `id` in the HTML, add the string to all `translations[lang]` objects, and add a line in `applyLanguage()` to set it
  - Form `<select>` options are translated in a loop using `options[i]` by checking `.value`
- **Documentation pages** ([terms.html](../terms.html), [business.html](../business.html)):
  - Full page content lives in `translations[lang].body` as complete HTML
  - A single `#terms-body` or `#business-body` container has its `.innerHTML` replaced wholesale on language change
  - **Pattern**: To edit content on these pages, update all language `body` strings in the `translations` object, *not* the static HTML (which gets overwritten)
- **Critical rule**: Always maintain **perfect parity across all language entries**. Missing or mismatched keys will break the UI for that language.

### 4. Request Form & JavaScript Behavior
- The **only form** is in [request.html](../request.html); its inline `<script>` handles:
  - **Language switching**: Labels, select options, hints, terms text, and button text update via `applyLanguage()`
  - **Conditional UI**: `#templates-link-wrapper` shows/hides when `projectType` select changes to `'template'`
  - **Mailto submission**: On `submit`, JavaScript prevents default form submission, reads all field values (name, email, phone, projectType text, details, requestCall checkbox), constructs a plain-text email body, and navigates to `mailto:request@makememovie.org?subject=...&body=...`
- **When adding or modifying form fields**:
  - Update the HTML `<input>`, `<select>`, or `<textarea>` with a unique `id`
  - Add or update corresponding `getElementById()` calls in the script
  - If the field is translatable, add it to the `translations` object *for every language*
  - If the field value should appear in the email, add it to the `lines` array in the submit handler
  - Verify both the English version and all five languages work
- **Interactive logic**: Use small, self-contained IIFE patterns (Immediately Invoked Function Expressions) at the bottom of any page that needs JS. Avoid global scope pollution.
- **Form validation**: Browser `required` attributes handle basic validation; the form navigates to mailto, so no backend validation is needed.

### 5. Assets, Media & External Embeds
- Shared CSS (including the `background.jpeg` background) lives under [assets/styles.css](../assets/styles.css). Additional media should live under `assets/`, `images/`, or `videos/` with relative links.
- **Media files present**: `assets/background.jpeg` (fixed background), `assets/back.jpg` (backup/alternate)
- Prefer lightweight media (compressed images, short clips, optional embeds like YouTube). Avoid large JS bundles or heavy libraries.
- All image and media paths must be **relative** (e.g., `href="assets/styles.css"` not `/assets/styles.css`) to work in both file:// and HTTP contexts.

### 6. Workflows, Preview & Testing
- There are **no** automated build, lint, or test workflows.
- To validate changes, open the HTML files directly in a browser or run a simple static server (e.g., VS Code Live Server) from the repo root.
- Each page is self‑contained (own `<head>`, `<body>`, and script); new pages should follow this pattern and not depend on a build step.
- **Deployment**: The site is deployed to GitHub Pages via the `CNAME` file and `_config.yml` (Jekyll config).
- **Testing checklist for changes**: 
  - Open each affected HTML page in a browser locally
  - Test all language selections (5 languages)
  - For form changes, verify mailto link includes all new/modified fields
  - Check mobile responsiveness (test viewport at 600px width)

### 7. AI Agent Collaboration Guidelines
- Make small, focused edits to a single page or feature at a time, and keep shared structures (`header`, `.nav-links`, `.language-module`, `.container`, footer) consistent across all pages.
- When extending content, copy the closest existing pattern (e.g., add another paragraph/card in [index.html](../index.html), or another numbered item in [terms.html](../terms.html)) instead of inventing new layout primitives.
- Preserve the existing visual style (colors, typography, spacing) and assume deployment to simple static hosting (GitHub Pages, Netlify, etc.)—no server‑side code or dynamic backends.
- **Common tasks & their patterns**:
  - *Update form fields*: Modify HTML (add input/select), update translations for all 5 languages, update applyLanguage() function, add to mailto body lines
  - *Change page content*: Update translations[lang] on main pages; for doc pages, update translations[lang].body HTML wholesale
  - *Update navigation*: Edit header nav-links AND footer links on ALL FOUR pages consistently
  - *Add new page*: Copy structure from closest existing page, include language-module + translations object, use appropriate page class (page-main or page-doc)
