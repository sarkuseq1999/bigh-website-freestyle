# Project: bigh-website-freestyle

## Tech stack
- Nuxt 4 (Vue 3, TypeScript built in)
- Tailwind CSS v4 (via @tailwindcss/vite plugin)
- ESLint (@nuxt/eslint module)
- Package manager: npm

## Common commands
- `npm run dev`     — start dev server at http://localhost:3000
- `npm run build`   — production build
- `npm run preview` — preview the production build locally
- `npm run lint`    — run ESLint

## Project conventions
- Vue components use `<script setup lang="ts">` (Composition API + TypeScript)
- Styling via Tailwind utility classes; avoid writing custom CSS unless necessary
- Pages live in `app/pages/`, components in `app/components/`

## Design instructions
- DESIGN.md is the binding aesthetic spec — every UI decision must comply with its color palette, typography scale, spacing, components, and do's/don'ts
- The frontend-design skill may be used for *execution craft* (motion, spacing precision, code quality, accessibility), but its general "be bold/unexpected/avoid generic" guidance is overridden by DESIGN.md
- Inspiration references live in `design-references/` — scan this folder before any new UI work; image files are visual examples, sibling `.md` files describe what the user likes/dislikes about each, and `links.md` lists live-site URLs to fetch