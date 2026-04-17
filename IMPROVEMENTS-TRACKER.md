# Service Evaluation: mcp-website-assistant

> Tracking gaps, limitations, and improvement opportunities observed during the
> certificates showcase rebuild for Anthony's certs site (amlfi.github.io/certs/).
>
> **Service**: mcp-website-assistant (port 9210, 7 tools)
> **Task**: Rebuild Bootstrap 4 certificates site with modern Tailwind/DaisyUI stack

---

## Current Tools (7)

| # | Tool | Purpose | Params |
|---|------|---------|--------|
| 1 | `create_website` | Scaffold a new project | name, framework (daisyui/shadcn), template (landing/portfolio/blog/docs/saas), theme |
| 2 | `add_page` | Add an HTML page to the project | filename, title, content (HTML) |
| 3 | `add_component` | Create a reusable component | name, type (navbar/footer/hero/card/form/modal), props |
| 4 | `set_theme` | Apply or change theme + custom colors | theme, customColors |
| 5 | `preview_website` | Start local dev server | port, open |
| 6 | `generate_docs` | Generate project documentation | format (md/html/pdf), include sections |
| 7 | `export_website` | Export for deployment | format (static/zip/docker), minify |

---

## What's Being Done Manually (that a tool could handle)

### 1. Data File Creation (certificates.json)
- **What**: Building a structured JSON data file (672 lines, ~40 certificates) with fields like id, name, issuer, date, category, status, image, logo, courseUrl
- **Why manual**: No tool exists for structured data scaffolding or content ingestion
- **Ideal**: A `create_data_source` tool that accepts a schema and can import from CSV, existing HTML, or manual entries

### 2. Tailwind/DaisyUI Configuration from Scratch
- **What**: Setting up tailwind.config.js, CDN links, DaisyUI theme config, custom utility classes
- **Why manual**: `create_website` generates a basic scaffold but the actual Tailwind/DaisyUI integration is shallow -- relies on CDN script tag, no real tailwind.config.js with custom theme tokens
- **Ideal**: `create_website` should produce a fully configured Tailwind project with proper config file, purge settings, and DaisyUI plugin setup

### 3. Building HTML Templates by Hand
- **What**: Writing full page HTML with Tailwind classes, responsive grid, category filter UI, card layouts, modal dialogs
- **Why manual**: `add_page` only wraps content in a basic HTML shell. It does not understand layout patterns or provide template intelligence
- **Ideal**: Template-aware page generation that understands "certificate grid page" or "filterable portfolio" as a layout concept

### 4. Image Optimization
- **What**: Resizing certificate images, converting to WebP, generating thumbnails, lazy loading setup
- **Why manual**: No image processing capability in the service at all
- **Ideal**: An `optimize_assets` tool that handles image compression, format conversion, and responsive image generation

### 5. Category Filtering Logic
- **What**: Writing JavaScript for filtering certificates by category (business, safety, tech, design, licenses), active state management, animation
- **Why manual**: `add_component` creates static HTML components only -- no interactive behavior
- **Ideal**: Components should support interactive patterns (filter, sort, search) with generated JS

### 6. Modal/Preview Functionality
- **What**: Building a certificate detail modal with image zoom, metadata display, external links
- **Why manual**: The `modal` component type exists but only generates a static HTML shell with no data-binding or trigger logic
- **Ideal**: Modal component should support data-driven content and trigger wiring

### 7. Theme Configuration for Specific Design
- **What**: Custom color palette matching Anthony's brand (navy #1c2c59, sunset gradients), dark mode, glassmorphism effects
- **Why manual**: `set_theme` only supports 5 preset themes. Custom colors are an object but there is no guidance on what keys are supported
- **Ideal**: Theme tool should accept brand colors and generate a complete design token set (primary, secondary, accent, neutrals, gradients)

### 8. Deployment to GitHub Pages
- **What**: Setting up GitHub Actions workflow, configuring base paths, CNAME, 404 handling
- **Why manual**: `export_website` supports static/zip/docker but has no GitHub Pages awareness
- **Ideal**: A `deploy_website` tool with GitHub Pages, Netlify, Vercel targets that generates CI config

### 9. SEO and Open Graph Setup
- **What**: Writing OG meta tags, Twitter cards, structured data, robots.txt, sitemap
- **Why manual**: `add_page` generates minimal meta tags (charset, viewport, title only)
- **Ideal**: SEO tool or page option that generates complete meta tag set from project metadata

### 10. PWA / Web App Manifest
- **What**: Creating manifest.json, service worker, offline page, app icons
- **Why manual**: Not addressed by any tool
- **Ideal**: `add_pwa_support` tool that generates manifest, icons, and basic service worker

---

## Tool Gaps Identified

### HIGH Priority

| Gap | Description | Ideal Tool |
|-----|-------------|------------|
| **Data-driven pages** | No way to create pages that render from JSON data sources | `create_data_page` -- accepts a data file + layout template, generates page with JS to fetch and render |
| **Interactive components** | Components are static HTML only, no JS behavior | Extend `add_component` to support `behavior` param (filter, sort, search, toggle, modal-trigger) |
| **Asset optimization** | No image/font/CSS processing | `optimize_assets` -- resize, compress, convert images; inline critical CSS; subset fonts |
| **Real Tailwind config** | CDN script tag instead of proper build pipeline | `create_website` should generate tailwind.config.js, postcss.config.js, proper build setup |
| **GitHub Pages deploy** | No deployment target for the most common static hosting | `deploy_website` with target: github-pages, netlify, vercel |

### MEDIUM Priority

| Gap | Description | Ideal Tool |
|-----|-------------|------------|
| **SEO meta generation** | Pages lack OG tags, structured data, sitemap | `add_seo` -- generates meta tags, sitemap.xml, robots.txt, structured data |
| **Brand/design tokens** | Theme system is preset-only, no brand color derivation | Enhance `set_theme` to accept brand colors and derive full palette |
| **Import existing site** | Cannot ingest an existing HTML site and modernize it | `import_website` -- parse existing HTML, extract content/structure, recreate with modern stack |
| **Responsive testing** | No way to verify responsive behavior | `test_responsive` -- screenshot at multiple breakpoints (could delegate to playwright-assistant) |

### LOW Priority

| Gap | Description | Ideal Tool |
|-----|-------------|------------|
| **PWA support** | No manifest, service worker, offline support | `add_pwa_support` |
| **Analytics integration** | No GA4, Plausible, etc. setup | `add_analytics` |
| **Form backend** | Forms are HTML only, no submission handling | `add_form_backend` with Formspree, Netlify Forms, etc. |
| **Accessibility audit** | No WCAG checking | `audit_accessibility` (delegate to playwright-assistant) |

---

## Limitations Observed

### Claims vs Reality

| Claimed Capability | Actual State |
|-------------------|--------------|
| "Create beautiful websites with DaisyUI/shadcn" | Generates a basic HTML file with CDN links. No build pipeline, no component composition, no real DaisyUI theme integration |
| "5 built-in themes with custom color overrides" | Themes generate CSS via DesignSystem class, but the CSS is basic. No DaisyUI theme data attributes, no dark mode toggle |
| "Component Library: Navbar, footer, hero, card, form, modal" | Components are static HTML fragments saved as .html files in a components/ folder. No inclusion mechanism, no JS behavior, no props rendering |
| "Preview Server: Live preview for development" | PreviewServer exists but is a basic static file server. No hot reload, no Tailwind JIT, no build watch |
| "Export Options: Static files, ZIP archives, or Docker containers" | DeploymentManager handles basic file copying. No minification pipeline, no tree-shaking, no real Docker multi-stage build |

### Missing `@mcpassistant/ui-website` Package
The service imports from `@mcpassistant/ui-website` (WebsiteGenerator, ComponentManager, DesignSystem, etc.) but **no matching package exists** in `packages/`. This means either:
- The package was deleted/moved and the service is broken
- The package is a stub that has not been implemented
- The imports will fail at runtime

This is the most critical issue -- the service likely cannot run at all without this package.

### Integration Issues
- **No collaboration with playwright-assistant** for preview screenshots or responsive testing
- **No collaboration with github-assistant** for deployment automation
- **No collaboration with file-assistant** for asset management
- **projects are created under `process.cwd()/websites/`** which is fragile and not configurable
- **Single active project model** -- `this.currentProject` means you lose context if you switch projects

### Framework Support
- **DaisyUI**: Uses CDN link to v4.0.0 (outdated, current is v5.x). No proper Tailwind plugin setup
- **shadcn**: Listed as an option but shadcn requires React/Next.js -- the service generates plain HTML. This option likely produces broken output
- **No Astro, Vite, 11ty**: Modern static site generators are not supported

---

## Suggested New Tools

### 1. `create_data_page` (HIGH)
```javascript
{
  name: 'create_data_page',
  description: 'Create a page that renders data from a JSON source',
  inputSchema: {
    type: 'object',
    properties: {
      dataSource: { type: 'string', description: 'Path to JSON data file' },
      layout: { type: 'string', enum: ['grid', 'list', 'table', 'masonry'], description: 'Layout style' },
      cardTemplate: { type: 'string', description: 'HTML template for each item (uses {{field}} placeholders)' },
      filters: { type: 'array', items: { type: 'string' }, description: 'Fields to create filter controls for' },
      searchFields: { type: 'array', items: { type: 'string' }, description: 'Fields to include in search' },
      sortFields: { type: 'array', items: { type: 'string' }, description: 'Fields to allow sorting by' },
    },
    required: ['dataSource', 'layout'],
  },
}
```

### 2. `optimize_assets` (HIGH)
```javascript
{
  name: 'optimize_assets',
  description: 'Optimize images, CSS, and JS for production',
  inputSchema: {
    type: 'object',
    properties: {
      types: { type: 'array', items: { type: 'string', enum: ['images', 'css', 'js', 'fonts'] } },
      imageOptions: {
        type: 'object',
        properties: {
          maxWidth: { type: 'number' },
          format: { type: 'string', enum: ['webp', 'avif', 'original'] },
          generateThumbnails: { type: 'boolean' },
          lazyLoad: { type: 'boolean' },
        },
      },
    },
    required: ['types'],
  },
}
```

### 3. `deploy_website` (HIGH)
```javascript
{
  name: 'deploy_website',
  description: 'Deploy website to a hosting platform',
  inputSchema: {
    type: 'object',
    properties: {
      target: { type: 'string', enum: ['github-pages', 'netlify', 'vercel', 'cloudflare-pages'] },
      repo: { type: 'string', description: 'GitHub repo (owner/name)' },
      branch: { type: 'string', description: 'Deploy branch', default: 'gh-pages' },
      customDomain: { type: 'string', description: 'Custom domain name' },
      generateCI: { type: 'boolean', description: 'Generate CI/CD workflow', default: true },
    },
    required: ['target'],
  },
}
```

### 4. `import_website` (MED)
```javascript
{
  name: 'import_website',
  description: 'Import an existing website and modernize its stack',
  inputSchema: {
    type: 'object',
    properties: {
      sourcePath: { type: 'string', description: 'Path to existing website' },
      targetFramework: { type: 'string', enum: ['daisyui', 'shadcn'] },
      extractData: { type: 'boolean', description: 'Extract repeated content into JSON data files' },
      modernizeCSS: { type: 'boolean', description: 'Convert to Tailwind utility classes' },
    },
    required: ['sourcePath', 'targetFramework'],
  },
}
```

### 5. `add_seo` (MED)
```javascript
{
  name: 'add_seo',
  description: 'Add SEO optimization to the website',
  inputSchema: {
    type: 'object',
    properties: {
      title: { type: 'string' },
      description: { type: 'string' },
      ogImage: { type: 'string' },
      url: { type: 'string' },
      generateSitemap: { type: 'boolean', default: true },
      generateRobots: { type: 'boolean', default: true },
      structuredData: { type: 'string', enum: ['website', 'person', 'organization', 'article'] },
    },
    required: ['title', 'description'],
  },
}
```

---

## Action Items

1. **CRITICAL**: Create or restore `@mcpassistant/ui-website` package -- service cannot function without it
2. **HIGH**: Add data-driven page generation for portfolio/showcase use cases
3. **HIGH**: Make components interactive (filtering, modals, search)
4. **HIGH**: Implement real Tailwind/DaisyUI build pipeline (not CDN)
5. **MED**: Add deployment targets (GitHub Pages is table stakes)
6. **MED**: Support importing/modernizing existing sites
7. **LOW**: Cross-service collaboration (playwright for testing, github for deploy)

---

## Observation Log

_Add entries here as the rebuild progresses._

| Date | Observation | Category |
|------|-------------|----------|
| 2026-03-22 | Initial evaluation -- service has 7 tools but `@mcpassistant/ui-website` package is missing, likely non-functional | CRITICAL |
| 2026-03-22 | Certificates rebuild requires data-driven grid with filtering -- no tool supports this pattern | GAP |
| 2026-03-22 | Existing site uses Bootstrap 4 + AOS.js + custom CSS -- no import/migration tool exists | GAP |
| 2026-03-22 | certificates.json (672 lines, ~40 entries) was created manually -- no data scaffolding tool | GAP |
| 2026-03-22 | Site needs OG tags, manifest.json, responsive images -- none provided by add_page | GAP |
