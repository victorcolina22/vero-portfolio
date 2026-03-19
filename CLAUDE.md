# CLAUDE.md - Vero Portfolio

## Project Overview

Personal portfolio website built for a client named "Vero" (brand: **Vero Mendoza**). The site showcases creative/design work as a UX/UI and Product Designer. This is a static site built with **Astro 5** and **Tailwind CSS 4**, focused on performance and clean presentation. Design sourced from Figma file "Portafolio 2026".

## Tech Stack

| Technology        | Version | Purpose                        |
| ----------------- | ------- | ------------------------------ |
| Astro             | ^5.17.1 | Static site framework (SSG)    |
| Tailwind CSS      | ^4.2.0  | Utility-first CSS framework    |
| @tailwindcss/vite | ^4.2.0  | Tailwind Vite plugin           |
| TypeScript        | strict  | Type safety (via astro config) |
| Prettier          | ^3.8.1  | Code formatting                |
| pnpm              | 10.28.2 | Package manager                |
| Node.js           | 24.13.0 | Runtime                        |

## Commands

```bash
pnpm dev        # Start dev server
pnpm build      # Production build
pnpm preview    # Preview production build
pnpm astro      # Astro CLI
```

## Project Structure

```
vero-portfolio/
├── public/
│   ├── fonts/
│   │   ├── Oswald-VariableFont_wght.ttf        # Headings font (variable weight)
│   │   └── Poppins-Regular.ttf                 # Body font
│   ├── images/
│   │   ├── decorative/                         # Decorative SVGs exported from Figma
│   │   │   ├── letter-{p,o1,f,o2,r,t,a,l,i,o3}.svg  # "PORTFOLIO" background letters
│   │   │   ├── curved-line.svg                 # Decorative curved line
│   │   │   ├── gold-star-lg.svg                # Large gold star decoration
│   │   │   ├── green-union.svg                 # Green abstract shape
│   │   │   ├── pink-flower-{sm,lg,footer}.svg  # Pink flower decorations (3 sizes)
│   │   │   ├── star-icon-frame{,-sm}.svg       # Star frame icons (2 sizes)
│   │   │   └── vero-illustration-sm.svg        # Small Vero illustration for footer
│   │   ├── icons/                              # Software & social media icons
│   │   │   ├── figma.svg, google-analytics.svg, hotjar.svg
│   │   │   ├── datadog.svg, pendo.svg, illustrator.svg
│   │   │   ├── gmail.svg, linkedin.svg, whatsapp-sm.svg
│   │   │   └── done-pencil.svg
│   │   ├── avatar.webp                         # Hero avatar illustration
│   │   ├── pattern-bg.png                      # Pattern background image
│   │   ├── whatsapp-cta.png                    # WhatsApp CTA card image
│   │   ├── logo.svg                            # Brand logo SVG file
│   │   ├── start-8-tip.svg                     # Star icon (legacy)
│   │   └── whatsapp-logo.svg                   # WhatsApp icon (legacy)
│   ├── favicon.ico
│   └── favicon.svg
├── src/
│   ├── assets/
│   │   ├── astro.svg                           # Default Astro asset (can be removed)
│   │   └── background.svg                      # Background SVG asset
│   ├── components/
│   │   ├── icons/
│   │   │   ├── StarEightTip.astro              # 8-pointed star SVG (gold #F0D894)
│   │   │   └── WhatsAppLogo.astro              # WhatsApp icon SVG (green #67C15E)
│   │   ├── pages/
│   │   │   ├── hero/
│   │   │   │   ├── Hero.astro                  # Hero section (PORTFOLIO letters, avatar, overlays)
│   │   │   │   ├── WorksSidebar.astro          # Left sidebar with project links
│   │   │   │   └── WhatsAppCta.astro           # Right WhatsApp contact card
│   │   │   ├── about/
│   │   │   │   ├── About.astro                 # About section (headline, bio, pattern bg)
│   │   │   │   └── AboutFooter.astro           # Footer within about (education, experience, softwares)
│   │   │   └── projects/
│   │   │       ├── Projects.astro              # Projects section container
│   │   │       └── ProjectCard.astro           # Individual project card component
│   │   ├── Header.astro                        # Site header (centered logo)
│   │   └── Logo.astro                          # Inline SVG logo with color prop (dark-blue | orange)
│   ├── layouts/
│   │   └── Layout.astro                        # Main layout (head, meta, global styles, font/color defaults)
│   ├── pages/
│   │   └── index.astro                         # Homepage (Hero → About → Projects)
│   └── styles/
│       └── global.css                          # Global styles, @font-face, Tailwind @theme config
├── astro.config.mjs
├── tsconfig.json
├── .prettierrc
└── package.json
```

## Architecture & Patterns

### Component Organization

- **`src/components/icons/`** — SVG icon components (inline SVGs, not image refs)
- **`src/components/pages/{section}/`** — Page-specific section components organized by section name
  - `hero/` — Hero section with avatar, PORTFOLIO letters, sidebar nav, WhatsApp CTA
  - `about/` — About section with headline, bio, education/experience/softwares
  - `projects/` — Projects section with horizontally stacked cards
- **`src/components/`** — Shared/global components (Header, Logo)
- **`src/layouts/`** — Layout wrappers (single Layout.astro)
- **`src/pages/`** — Astro file-based routing (single page app currently)

### Page Sections (Top to Bottom)

1. **Hero** — Full-width section with PORTFOLIO background letters (lilac), centered avatar illustration, Works sidebar (left), WhatsApp CTA card (right), decorative stars/flowers
2. **About** — Beige background section with "CREANDO EXPERIENCIAS DIGITALES CON ENFOQUE HUMANO" headline (90px), bio text over pattern background, education/experience/softwares grid, "Pensando en el Usuario" heading (96px)
3. **Projects** — "TRABAJOS:" label, horizontally scrollable overlapping project cards (5 cards with distinct colors)

### Styling Approach

- **Tailwind CSS 4** integrated via `@tailwindcss/vite` plugin (NOT the PostCSS approach)
- Tailwind is imported in `src/styles/global.css` with `@import 'tailwindcss'`
- Custom theme tokens defined in `@theme {}` block inside `global.css`
- Heavy use of **utility classes** directly in component markup
- Absolute positioning with pixel values for Figma-faithful layout in hero section
- `style` attribute used for precise pixel positioning from Figma coordinates
- Global CSS reset in `Layout.astro` scoped style block

### TypeScript Configuration

- Extends `astro/tsconfigs/strict` (strictest Astro preset)
- Path alias: `@/*` maps to `./src/*`
- Excludes `dist/` directory

### Design Tokens (Theme)

```css
/* Fonts */
--font-oswald: 'Oswald', sans-serif; /* Headings, uppercase text */
--font-poppins: 'Poppins', sans-serif; /* Body text */

/* Colors — Brand */
--color-dark-blue: #171c48; /* Primary brand color, all text */
--color-orange: #f18350; /* Accent/secondary color */
--color-gold: #f0d894; /* Star decorations */
--color-pink: #ff92cb; /* Flower decorations */
--color-lilac: #828be6; /* PORTFOLIO letters, section titles */
--color-green: #b8ef97; /* Green abstract shapes */
--color-beige: #f0ebe7; /* Section backgrounds */

/* Colors — Project Cards */
--color-card-research: #eeaacd;
--color-card-product: #acde8e;
--color-card-data: #a2abff;
--color-card-design-system: #f0d894;
--color-card-ui: #ff9562;
```

### Typography (from Figma)

| Usage             | Font    | Weight | Size    |
| ----------------- | ------- | ------ | ------- |
| Main headline     | Oswald  | 600    | 90px    |
| Section heading   | Oswald  | 600    | 96px    |
| Card category     | Oswald  | 600    | 36px    |
| Section labels    | Oswald  | 400    | 36-40px |
| Card title        | Oswald  | 600    | 20px    |
| Sidebar link      | Oswald  | 600    | 16px    |
| Body text         | Poppins | 400    | 12px    |
| Info/contact text | Poppins | 500    | 16px    |
| Bold labels       | Poppins | 700    | 16px    |

### Fonts

- **Oswald** (Variable Font) — Used for headings and prominent text, supports weight range
- **Poppins** (Regular 400) — Used for body text
- Both served locally from `public/fonts/` (self-hosted, no external CDN)

## Current State of Development

The project is in **active development** (v0.0.1). The Desktop-1 view from Figma has been implemented with all major sections.

### Commit History

1. Initial Astro setup
2. Tailwind integration
3. Theme config with custom fonts and Header component

### What's Built

- Layout with proper title ("Vero Mendoza | Portafolio"), lang="es", meta description
- Header with centered logo (absolute positioned over hero)
- Hero section with: PORTFOLIO decorative letters (lilac), avatar illustration, Works sidebar nav, WhatsApp CTA card, decorative elements (stars, flowers)
- About section with: main headline "CREANDO EXPERIENCIAS DIGITALES CON ENFOQUE HUMANO", pattern background with bio text, education/experience/softwares grid, "Pensando en el Usuario" heading
- Projects section with: "TRABAJOS:" label, 5 horizontally stacked project cards (Research, Product Design, Data y PD, Design System, UI Y PD)
- All design tokens from Figma mapped to Tailwind theme
- All decorative assets exported from Figma (SVGs and PNGs)
- Logo as inline SVG with color variant prop (`dark-blue` | `orange`)
- Icon components (StarEightTip, WhatsAppLogo) as Astro components

### Pending / Roadmap

Items below are expected pending work as part of the ongoing development:

- Responsive design (currently desktop-only, 1440px viewport, hardcoded pixel values)
- Mobile menu / responsive navigation
- Animations / transitions / hover states
- Project detail pages (currently cards are static)
- Open Graph / social meta tags
- Deployment configuration (no Vercel/Netlify adapter yet)
- Image optimization (convert PNGs to WebP, lazy loading)
- Accessibility audit (ARIA labels, keyboard navigation)
- Performance audit (font loading strategy, asset optimization)

## Code Style & Conventions

### Formatting (Prettier)

- Single quotes (`'`)
- Semicolons enabled
- 2-space indentation (spaces, not tabs)
- Trailing commas (`all`)
- Print width: 80 characters
- Arrow parens: `always`
- Bracket spacing: `true`
- Uses `prettier-plugin-astro` for `.astro` file formatting

### Component Patterns

- **Astro components only** (no React/Vue/Svelte islands yet)
- Props defined via `interface Props {}` in frontmatter
- Data arrays defined in frontmatter for list-based components (projects, experience, etc.)
- SVG icons as dedicated `.astro` components (inline, not `<img>` tags) for shared icons
- Figma-exported SVGs stored in `public/images/` and referenced via `<img>` tags
- Page sections organized under `components/pages/{section-name}/`
- Decorative elements marked with `aria-hidden="true"` and empty `alt=""`

### Import Conventions

- Path alias `@/` used for cross-directory imports (e.g., `@/layouts/Layout.astro`)
- Relative imports for same-directory component refs (e.g., `./Logo.astro`)

## Git Info

- **Branch**: `main` (single branch)
- **Remote**: None configured (local only, no GitHub remote yet)
- **Package Manager Lock**: `pnpm-lock.yaml`

## Brand Identity

- **Brand Name**: Vero Mendoza (logo is a custom SVG wordmark with decorative elements)
- **Color Palette**: Dark blue (#171c48), Orange (#f18350), Gold (#F0D894), Pink (#FF92CB), Lilac (#828BE6), Green (#B8EF97), Beige (#F0EBE7)
- **Typography**: Oswald (headings) + Poppins (body)
- **Style**: Clean, modern, professional portfolio with playful decorative elements (stars, flowers, abstract shapes)
- **Contact**: WhatsApp (+56 9 30898318), Email (vmendoza265@gmail.com), LinkedIn (vero-mendoza-delgado)

## Figma Source

- **File**: Portafolio 2026
- **File Key**: `CTPqaqRK8NOfba4DKVRLka`
- **Desktop Frame**: Node `6-861` ("Desktop - 1", 1440x2973px)
- **Pages**: "Portafolio" (main), "proyectos BV" (project breakdowns)

## Important Notes

- The `public/images/` folder has legacy SVG files (logo.svg, start-8-tip.svg, whatsapp-logo.svg) from early development alongside new Figma exports
- The `src/assets/astro.svg` is a leftover from the Astro starter template — can be cleaned up
- Hero section uses absolute positioning to match Figma pixel-perfect layout — will need responsive adaptation
- Project cards use negative margins for overlapping effect matching Figma design
- Dev toolbar is explicitly disabled in `astro.config.mjs`
- No deployment target configured yet (no Vercel/Netlify adapter)

> **Note**: This is an active project in development. The Desktop-1 view is implemented. Responsive design, animations, and project detail pages are planned next steps.
