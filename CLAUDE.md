# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
bun run dev      # Start dev server (http://localhost:4321)
bun run build    # Build for production (output: dist/)
bun run preview  # Preview the production build locally
```

No linting or test tooling is configured.

## Architecture

Single-page portfolio site built with **Astro 5 (SSG)** and **Tailwind CSS v4**. One route, one layout, five components — no content collections, no API routes, no JS framework.

**Page composition (`src/pages/index.astro`):**
```
Layout
  └── Navbar          (fixed top bar, dark mode toggle)
  └── <main>
        ├── Hero       (#hero — full-screen landing)
        ├── About      (#about — bio + skills)
        ├── Timeline   (#timeline — career events)
        └── Contact    (#contact — email CTA + social links + <footer>)
```

Navigation between sections uses anchor links only (`href="#about"` etc.). No client-side router.

## Key Conventions

**Tailwind v4 — CSS-first config**: There is no `tailwind.config.js`. All theme tokens (brand color palette, font stack) and custom variants (dark mode) are defined in `src/styles/global.css` using `@theme {}` and `@custom-variant`. Tailwind is wired via the Vite plugin in `astro.config.mjs`, not the Astro integration.

**Dark mode**: Class-based (`dark` on `<html>`). `Layout.astro` contains an inline `<script>` that runs synchronously on load to read `localStorage` / system preference and set the class before paint (no FOUT). `Navbar.astro` contains a separate script handling the toggle button and persisting to `localStorage`.

**Animation**: Two patterns are used:
- **Immediate (Hero)**: CSS utility classes (`animate-fade-in-up`, `delay-*`) applied directly; plays on load.
- **Scroll-triggered (Timeline)**: Items start `opacity: 0` via `.timeline-item`; an IntersectionObserver adds `visible animate-fade-in-up` with an 80ms-per-item stagger when they enter the viewport.

**Content**: All data is hardcoded in component frontmatter (`---` blocks). To update bio text, skills, or timeline events, edit the relevant component file directly — there is no CMS or data layer.

**Max-width**: All sections use `max-w-4xl mx-auto` for consistent centering.

**Footer location**: The `<footer>` lives inside `src/components/Contact.astro`, not in the layout.

## Tailwind Brand Colors

The `brand-*` color scale (defined in `global.css`) maps to a blue palette. Use `text-brand-600 dark:text-brand-400` for primary accents, `bg-brand-600` for filled buttons.
