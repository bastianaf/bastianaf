# bastianaf — Portfolio

Personal portfolio site for Bastian (bastianaf). Single-page, minimal, dark-mode-ready.

## Tech Stack

- **Framework**: Astro 5 (static, no SSR)
- **Package manager**: Bun
- **Styling**: Tailwind CSS v4 (via `@tailwindcss/vite` plugin — NOT the old `@astrojs/tailwind`)
- **Font**: Inter (Google Fonts)
- **Language**: TypeScript

## Commands

```bash
bun run dev      # local dev server
bun run build    # production build → dist/
bun run preview  # preview built site
```

## Project Structure

```
src/
├── components/
│   ├── Navbar.astro     # fixed top nav, dark mode toggle, smooth-scroll links
│   ├── Hero.astro       # full-screen hero with CTA buttons
│   ├── About.astro      # bio + skills chips grid
│   ├── Timeline.astro   # vertical timeline with IntersectionObserver animations
│   └── Contact.astro    # email CTA + social links + footer
├── layouts/
│   └── Layout.astro     # base HTML shell, dark mode init script
├── pages/
│   └── index.astro      # assembles all sections in order
└── styles/
    └── global.css       # Tailwind v4 @theme, custom animations, dark variant
```

## Design System

### Brand color
Blue scale defined as `brand-*` in `global.css` via Tailwind v4 `@theme`:
- Primary: `brand-600` (light) / `brand-400` (dark)
- Background accent: `brand-50` / `brand-950`

### Dark mode
- Class-based: `dark` on `<html>`
- Init logic in `Layout.astro` `<script>`: checks `localStorage` then `prefers-color-scheme`
- Toggle in `Navbar.astro`: writes to `localStorage`
- Custom variant in `global.css`: `@custom-variant dark (&:where(.dark, .dark *))`

### Animations (global.css)
Custom keyframes + utility classes:
- `.animate-fade-in-up` — hero elements, timeline cards
- `.animate-fade-in` — badge, scroll indicator
- `.delay-{100..500}` — stagger utilities
- Timeline items start `opacity: 0`, revealed by IntersectionObserver with 80ms stagger per item

## Sections & Page Order

1. `<Navbar />` — fixed, `z-50`, blurred background
2. `<Hero />` — `#hero`, min-h-screen, availability badge, name, tagline, 2 CTAs
3. `<About />` — `#about`, 5-col grid (avatar col-2 + bio col-3), skills chips
4. `<Timeline />` — `#timeline`, vertical list, color-coded dots (work/milestone/education)
5. `<Contact />` — `#contact`, email button + GitHub/LinkedIn/Twitter icons + footer

## Current Data (placeholder — needs real info)

### About — skills chips
`TypeScript`, `React`, `Node.js`, `Go`, `PostgreSQL`, `Docker`, `AWS`, `GraphQL`

### Timeline events (all placeholder)
| Year | Title | Company | Type |
|------|-------|---------|------|
| 2024 | Senior Software Engineer | Acme Corp | work |
| 2023 | Open Source Milestone | Community | milestone |
| 2022 | Software Engineer | StartupXYZ | work |
| 2021 | First Full-Stack Product | Side project | milestone |
| 2020 | Junior Engineer | Agency Co | work |
| 2019 | CS Degree | University | education |

### Contact
- Email: `hello@bastianaf.dev`
- GitHub: `github.com/bastianaf`
- LinkedIn: `linkedin.com/in/bastianaf`
- Twitter/X: `twitter.com/bastianaf`

> **TODO**: Replace all placeholder data with real info.

## Pending Work

- [ ] Replace placeholder bio text in `About.astro` with real content
- [ ] Replace placeholder timeline data in `Timeline.astro` with real career history
- [ ] Replace avatar placeholder (`B` monogram) with real photo
- [ ] Update contact links with real social handles
- [ ] Deploy to Vercel (connect GitHub repo → Vercel dashboard, zero-config Astro detection)
- [ ] Add a Projects section (optional)

## Deployment Target: Vercel

Planned deploy: connect GitHub repo at `bastianaf/bastianaf` to Vercel.
- No `vercel.json` needed — Vercel auto-detects Astro
- Build command: `bun run build`
- Output dir: `dist`
- No env vars needed (fully static)

## Conventions

- All components are `.astro` files with no framework islands (pure static HTML)
- No JS except: dark mode init (Layout), theme toggle (Navbar), IntersectionObserver (Timeline)
- Max content width: `max-w-4xl mx-auto` on all sections
- Spacing rhythm: `py-24 px-6` for sections
- No component library — everything hand-written with Tailwind
- Avoid adding SSR, React islands, or extra dependencies unless explicitly needed
