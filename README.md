# QuantumOrbit Platform

Institutional platform and portfolio for QuantumOrbit, developed with Nuxt and Nuxt UI, featuring a futuristic visual identity and presentation of the company's services, team, and projects.

## Overview

The project was structured to serve as the official web platform for QuantumOrbit, focusing on:

- institutional brand positioning
- presentation of services and differentiators
- highlight of the current main project, `Nebulos`
- commercial contact acquisition
- premium experience with a space-tech visual identity

## Stack

- `Nuxt 4`
- `Vue 3`
- `@nuxt/ui`
- `Tailwind CSS 4`
- `TypeScript`
- `pnpm`

## Main Sections

- `Hero` section with QuantumOrbit orbital identity
- `Services` focused on web, mobile, and ERP development
- `Portfolio` currently highlighting the `Nebulos` project
- `About` section with institutional company context
- `Team` section with developer cards and details modal
- `Contact` section with commercial CTA and `mailto` fallback

## Featured Project

### Nebulos

ERP with an internal sales module for clients, built with `Vue/Nuxt` and `Zig`, using the company's proprietary framework.

## Project Structure

```text
.
|- app/
|  |- app.vue
|  |- app.config.ts
|  |- assets/
|  |  |- bg1.png
|  |  |- bg2.png
|  |  |- bg3.png
|  |  |- bg4.png
|  |  |- bg5.png
|  |  |- empresa_logo.png
|  |  |- icon.jpeg
|  |  |- logo_trasparent.png
|  |  \- css/main.css
|  |- components/
|  |  |- SiteHeader.vue
|  |  |- SiteFooter.vue
|  |  \- sections/
|  \- pages/
|- public/
|- nuxt.config.ts
|- package.json
\- README.md
```

## Scripts

```bash
pnpm install
pnpm dev
pnpm lint
pnpm typecheck
pnpm build
pnpm preview
```

## Development Environment

### Install dependencies

```bash
pnpm install
```

### Run locally

```bash
pnpm dev
```

Application available at `http://localhost:3000`.

### Validate quality

```bash
pnpm lint
pnpm typecheck
pnpm build
```

## Deployment

Production build:

```bash
pnpm build
```

Local build preview:

```bash
pnpm preview
```

## Notes

- The repository is private and code distribution is restricted.
- Local operational files, agent context files, and build outputs are ignored by `.gitignore`.

## Ownership

This project is a private asset of QuantumOrbit.
Refer to the `LICENSE` file for usage, copying, and redistribution restrictions.
