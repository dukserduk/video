# GitHub Copilot Instructions for this Repo

## 1. Current State & Big Picture
- This repo currently contains Git metadata plus Joomla-style `.gitignore` and `.gitattributes` files, but no application source code yet.
- The `.gitignore` entries (for example `administrator/components/com_*`, `administrator/language/en-GB/*`, etc.) match a standard Joomla CMS installation layout.
- Assume this repo is intended to host a Joomla/PHP-based web site or extensions, but treat it as effectively greenfield until real source files are added.

## 2. Repository Layout & Conventions
- Root level is expected to mirror a Joomla site structure (e.g. `administrator/`, `components/`, `images/`, possibly `api/` and `cli/`), even if those directories are not yet committed.
- Respect the existing `.gitignore`: do **not** propose tracking files that are explicitly ignored there (mostly Joomla core files and language packs).
- When creating new code, prefer placing it in clearly custom locations (e.g. under `components/com_<projectname>/`, custom templates, or a `src/`-style subtree) rather than modifying core Joomla files.
- Check `.gitattributes` for Git LFS settings before suggesting binary or large assets; avoid introducing new large binaries unless aligned with those rules.

## 3. Architecture Guidance for New Code
- Because no code is present, any architectural decisions (framework choice, folder layout beyond Joomla conventions, build tooling) are **assumptions** and must be confirmed with the user first.
- When scaffolding new features, explicitly propose a structure (e.g. "Joomla component", "standalone PHP library", or "frontend SPA under `frontend/`") and wait for user confirmation before generating large amounts of code.
- Prefer composable, self-contained modules/components that can live alongside a Joomla site rather than tightly coupling to Joomla internals unless the user requests a core extension.

## 4. Workflows, Builds, and Tests
- There are currently **no** build scripts, package manifests, or test frameworks in the repo (no `composer.json`, `package.json`, or CI configs discovered).
- Before introducing tooling (Composer, PHPUnit, Node/Vite, Docker, etc.), explain what you plan to add and how it fits a Joomla/PHP project, then ask the user to confirm.
- When adding tooling, keep commands simple and document them (e.g. in a new `README.md` and by updating this file) so future agents can reuse the same workflows.

## 5. Git & Asset Handling
- `.gitattributes` configures Git LFS for patterns like `*.psd` and some folders (`*Administrator`, `*api`, `*cli`, `*images`, `*components`); avoid generating large binary assets outside these patterns.
- Prefer text- or vector-based assets (SVG, source image formats) over large binary exports when possible, and keep generated media minimal unless the user explicitly asks for it.

## 6. Collaboration Guidelines for AI Agents
- Always surface key assumptions (e.g. Joomla version, PHP version, hosting environment) and ask the user to confirm before depending on them.
- When the repo is still mostly empty, bias toward creating small, well-explained initial scaffolds rather than full-blown applications in one step.
- Leave short, high-value documentation when you introduce new structures: update or create `README.md`, note important commands, and, when relevant, add brief comments in config files.
- If you cannot infer something from the existing files (e.g., testing strategy, deployment process), state that clearly instead of guessing, and offer a couple of options for the user to choose from.
