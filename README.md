# Vuetify Demo

A small, self-contained Vue 3 + Vite + Vuetify demo application. It exists as a
UI-testing target: a single page exercising common Vuetify components (buttons,
text fields, selects, checkboxes, radio groups, switches, sliders, tabs with
window panels, a modal dialog, a menu, an accordion/expansion-panels, a data
table, alerts, a snackbar, and an app bar with a navigation drawer) with clean,
semantic, ARIA-friendly markup.

## Getting started

```bash
npm install
npm run dev
```

This starts a local Vite dev server (default `http://localhost:5173`).

To build a production bundle:

```bash
npm run build
```

The output is written to `dist/`.

## Deployment

This repository's GitHub Pages source is **GitHub Actions**
(`.github/workflows/deploy.yml`). On every push to `main`, the workflow runs
`npm install` and `npm run build`, then publishes `dist/` via
`actions/upload-pages-artifact` and `actions/deploy-pages`.

## Note on authoring environment

This project was hand-authored in a sandboxed environment with no network
egress (npm registry, unpkg, jsdelivr, and GitHub were all unreachable), so
`npm install` and `npm run build` have **not** been run or verified locally.
The dependency versions and file layout match what
`npm create vite@latest . -- --template vue` plus `npm install vuetify` would
produce, and template syntax was manually checked for tag/brace balance, but
an actual install/build has not been executed against them yet.

Recommended before relying on this app:

- Run `npm install && npm run build` locally once to confirm it installs and
  builds cleanly, **or**
- Push to `main` and let the CI workflow above perform the first real
  install/build (the GitHub Actions runner has normal internet access).
