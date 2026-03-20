# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
yarn dev              # Dev server at http://127.0.0.1:1101
yarn build            # Production build → dist/ then copied to docs/
yarn build:github     # Build with base /PrimarySchoolMathematics/ (GitHub Pages)
yarn build:suiyan     # Build with base /demo/psm/
yarn preview          # Preview production build locally
```

No test or lint scripts are configured.

## Architecture

Vue 3 SPA that generates printable primary school math drill worksheets (口算题). Entirely frontend — no backend.

**Two routes:**
- `/home` → `Layout.vue` — worksheet configuration UI
- `/print` → `Print.vue` — print preview/output page

**State flow:** User configures worksheet options in `Layout.vue` → generated papers stored in Pinia (`stores/app.js` → `printPreviewPapers`) → navigates to `/print` → `Print.vue` renders them.

**Core logic lives in `src/utils/`:**
- `paperGenerator.js` — worksheet generation engine
- `psm.js` — math problem set module
- `configStorage.js` — persists up to 10 user configs in localStorage
- `download.js`, `enum.js` — helpers

**Key components in `src/components/home/`:**
- `AutoGenerateFormulas.vue` — auto-generation config
- `ConfigurationList.vue` — saved config management
- `CustomFormulas.vue` — manual formula input
- `OptionsDrawer.vue` — print options
- `PaperDownloadDialog.vue`, `PrintPreviewDialog.vue` — output dialogs

**`docs/`** is the pre-built output for GitHub Pages — committed to the repo and updated via `yarn build`.

**`psm-demo/`** contains a standalone `psm.js` for embedding/demo purposes.

## Tech Stack

- Vue 3 + Pinia + Vue Router 4
- Element Plus 2.3.1 (component library)
- Vite 3 (build tool), `@/` alias → `src/`
- Tailwind CSS 3 + Sass
- Axios, Lodash, UUID
- Plain JavaScript (no TypeScript)
