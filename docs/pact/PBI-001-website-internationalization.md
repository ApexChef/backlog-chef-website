# PBI-001: Website Internationalization (i18n)

> **PACT Documentation** - Prepare, Architect, Code, Test

## Overview

| Field | Value |
|-------|-------|
| **ID** | PBI-001 |
| **Title** | Website Internationalization with Multi-Language Support |
| **Status** | Completed |
| **Priority** | High |
| **Domain** | Website, UX, SEO |
| **Created** | 2024-12-04 |

## Description

Implement internationalization (i18n) for the Backlog Chef marketing website to support multiple languages, starting with English (default) and Dutch. This enables reaching a broader European audience and improves SEO through proper hreflang implementation.

---

# Phase 1: PREPARE

## 1.1 Problem Statement

The Backlog Chef website currently only supports English content. To expand into the Dutch/Belgian market and improve accessibility for non-English speakers, we need:

- Multi-language content support
- SEO-friendly URL structure
- Easy language switching for users
- Maintainable translation workflow

## 1.2 Requirements Gathered

### Functional Requirements
| Requirement | Priority | Source |
|-------------|----------|--------|
| Support English + Dutch languages | Must Have | User Interview |
| Subdirectory URL structure (/en/, /nl/) | Must Have | SEO Best Practice |
| Translate all pages (homepage, docs, pitch) | Must Have | User Interview |
| Language switcher in navigation | Must Have | UX Requirement |
| Auto-translate initial Dutch content | Should Have | Time Constraint |

### Non-Functional Requirements
| Requirement | Priority | Rationale |
|-------------|----------|-----------|
| SEO-optimized with hreflang tags | Must Have | Google indexing |
| Static site compatible | Must Have | Netlify deployment |
| Type-safe translations | Should Have | Developer experience |
| Fast page load (no runtime i18n) | Should Have | Performance |

## 1.3 Research Findings

### Astro i18n Approaches Evaluated

| Approach | Pros | Cons | Decision |
|----------|------|------|----------|
| **Astro built-in i18n** | Native support, routing config | Limited features | Selected |
| astro-i18next | Full i18next ecosystem | Extra dependency, complexity | Rejected |
| Paraglide.js | Type-safe, small bundle | New ecosystem, learning curve | Rejected |
| Manual implementation | Full control | More code to maintain | Rejected |

### URL Structure Options

| Pattern | Example | SEO Impact | Decision |
|---------|---------|------------|----------|
| **Subdirectory** | /nl/docs | Best - single domain authority | Selected |
| Subdomain | nl.example.com | Good - separate indexing | Rejected |
| Query param | ?lang=nl | Poor - often ignored by crawlers | Rejected |

### Key Astro i18n Features (v4+)
- `i18n` config in `astro.config.mjs`
- Automatic locale detection from URL
- `getRelativeLocaleUrl()` helper
- Static generation compatible

## 1.4 Constraints & Assumptions

### Constraints
- Must work with static site generation (Netlify)
- No server-side locale detection (static hosting)
- Pitch deck has custom styling (not using Layout component)

### Assumptions
- English is the primary/default language
- Dutch translations can be AI-generated initially
- User manually selects language (no auto-detection)

---

# Phase 2: ARCHITECT

## 2.1 Solution Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    Astro i18n Architecture                   │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐  │
│  │   /en/*      │    │   /nl/*      │    │   / (root)   │  │
│  │   English    │    │   Dutch      │    │   Redirect   │  │
│  │   Pages      │    │   Pages      │    │   → /en/     │  │
│  └──────┬───────┘    └──────┬───────┘    └──────────────┘  │
│         │                   │                               │
│         └─────────┬─────────┘                               │
│                   │                                          │
│         ┌─────────▼─────────┐                               │
│         │   Layout.astro    │                               │
│         │   + LanguageSwitcher                              │
│         │   + hreflang tags │                               │
│         └─────────┬─────────┘                               │
│                   │                                          │
│         ┌─────────▼─────────┐                               │
│         │   /src/i18n/ui.ts │                               │
│         │   Translation     │                               │
│         │   Dictionary      │                               │
│         └───────────────────┘                               │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

## 2.2 File Structure

```
src/
├── i18n/
│   └── ui.ts                    # Translation dictionary + utilities
├── components/
│   └── LanguageSwitcher.astro   # Language toggle component
├── layouts/
│   └── Layout.astro             # Updated with i18n support
├── pages/
│   ├── index.astro              # Redirect → /en/
│   ├── docs.astro               # Redirect → /en/docs
│   ├── pitch.astro              # Redirect → /en/pitch
│   ├── en/
│   │   ├── index.astro          # English homepage
│   │   ├── docs.astro           # English documentation
│   │   ├── pitch.astro          # English pitch deck
│   │   └── 404.astro            # English 404
│   └── nl/
│       ├── index.astro          # Dutch homepage
│       ├── docs.astro           # Dutch documentation
│       ├── pitch.astro          # Dutch pitch deck
│       └── 404.astro            # Dutch 404
└── public/
    └── _redirects               # Netlify server-side redirects
```

## 2.3 Component Design

### Translation System (`/src/i18n/ui.ts`)

```typescript
// Language definitions
export const languages = { en: 'English', nl: 'Nederlands' };
export const defaultLang = 'en';
export type Lang = keyof typeof languages;

// Translation dictionary
export const ui = {
  en: {
    'nav.cli': 'CLI',
    'nav.features': 'Features',
    // ... 200+ translation keys
  },
  nl: {
    'nav.cli': 'CLI',
    'nav.features': 'Functies',
    // ... Dutch translations
  }
} as const;

// Utility functions
export function getLangFromUrl(url: URL): Lang
export function useTranslations(lang: Lang): (key: keyof typeof ui['en']) => string
export function getLocalizedPath(path: string, lang: Lang): string
```

### LanguageSwitcher Component

```astro
<!-- Shows current language, links to alternate -->
<div class="flex items-center space-x-2">
  <a href="/en/..." class={isEnglish ? 'font-bold' : ''}>EN</a>
  <span>|</span>
  <a href="/nl/..." class={isDutch ? 'font-bold' : ''}>NL</a>
</div>
```

### Layout Updates

- Accept `lang` prop
- Add hreflang `<link>` tags for SEO
- Use `t()` function for translated strings
- Include LanguageSwitcher in nav

## 2.4 SEO Implementation

```html
<!-- hreflang tags for search engines -->
<link rel="alternate" hreflang="en" href="https://backlogchef.com/en/..." />
<link rel="alternate" hreflang="nl" href="https://backlogchef.com/nl/..." />
<link rel="alternate" hreflang="x-default" href="https://backlogchef.com/en/..." />
```

## 2.5 Redirect Strategy

| From | To | Method |
|------|-----|--------|
| `/` | `/en/` | Meta refresh + Netlify _redirects |
| `/docs` | `/en/docs` | Meta refresh + Netlify _redirects |
| `/pitch` | `/en/pitch` | Meta refresh + Netlify _redirects |

---

# Phase 3: CODE

## 3.1 Implementation Summary

### Files Created

| File | Purpose | Lines |
|------|---------|-------|
| `src/i18n/ui.ts` | Translation dictionary with 200+ keys | ~400 |
| `src/components/LanguageSwitcher.astro` | Language toggle UI | ~30 |
| `src/pages/en/index.astro` | English homepage | ~490 |
| `src/pages/en/docs.astro` | English documentation | ~580 |
| `src/pages/en/pitch.astro` | English pitch deck | ~1000 |
| `src/pages/en/404.astro` | English 404 page | ~20 |
| `src/pages/nl/index.astro` | Dutch homepage | ~490 |
| `src/pages/nl/docs.astro` | Dutch documentation | ~580 |
| `src/pages/nl/pitch.astro` | Dutch pitch deck | ~1000 |
| `src/pages/nl/404.astro` | Dutch 404 page | ~20 |
| `public/_redirects` | Netlify redirects | ~5 |

### Files Modified

| File | Changes |
|------|---------|
| `astro.config.mjs` | Added i18n configuration |
| `src/layouts/Layout.astro` | Added i18n support, hreflang, LanguageSwitcher |
| `src/pages/index.astro` | Changed to redirect |
| `src/pages/docs.astro` | Changed to redirect |
| `src/pages/pitch.astro` | Changed to redirect |

## 3.2 Key Code Snippets

### Astro Config (`astro.config.mjs`)

```javascript
export default defineConfig({
  site: 'https://backlogchef.com',
  i18n: {
    defaultLocale: 'en',
    locales: ['en', 'nl'],
    routing: {
      prefixDefaultLocale: true
    }
  },
  // ... rest of config
});
```

### Translation Usage in Pages

```astro
---
import Layout from '../../layouts/Layout.astro';
import { useTranslations } from '../../i18n/ui';

const lang = 'nl';
const t = useTranslations(lang);
---

<Layout title={t('hero.title')} lang={lang}>
  <h1>{t('hero.title')}</h1>
  <p>{t('hero.subtitle')}</p>
</Layout>
```

## 3.3 Translation Categories

| Category | # Keys | Examples |
|----------|--------|----------|
| Navigation | 6 | nav.cli, nav.features, nav.pricing |
| Hero Section | 4 | hero.title, hero.subtitle, hero.cta |
| Differentiators | 12 | diff.domainSpecific, diff.qualityBuiltIn |
| Pipeline | 16 | pipeline.step1.title, pipeline.step1.desc |
| CLI Commands | 20 | cli.process.desc, cli.resume.desc |
| Web Interface | 12 | web.pbiBrowser, web.semanticSearch |
| Pricing | 20 | pricing.starter, pricing.pro.features |
| Footer | 10 | footer.tagline, footer.quickLinks |
| Docs Page | 50+ | docs.vision, docs.pipeline.title |
| Pitch Deck | 80+ | pitch.problem.quote, pitch.solution.title |

---

# Phase 4: TEST

## 4.1 Build Verification

```bash
$ npm run build

✓ Built successfully
✓ /en/index.html generated
✓ /en/docs/index.html generated
✓ /en/pitch/index.html generated
✓ /nl/index.html generated
✓ /nl/docs/index.html generated
✓ /nl/pitch/index.html generated
✓ Root redirects in place
```

## 4.2 Test Cases

| Test | Expected | Result |
|------|----------|--------|
| Visit `/` | Redirects to `/en/` | ✅ Pass |
| Visit `/en/` | Shows English homepage | ✅ Pass |
| Visit `/nl/` | Shows Dutch homepage | ✅ Pass |
| Click NL in language switcher | Navigates to `/nl/` version | ✅ Pass |
| Click EN in language switcher | Navigates to `/en/` version | ✅ Pass |
| Check hreflang tags | Present with correct URLs | ✅ Pass |
| Visit `/en/docs` | Shows English docs | ✅ Pass |
| Visit `/nl/docs` | Shows Dutch docs | ✅ Pass |
| Visit `/en/pitch` | Shows English pitch | ✅ Pass |
| Visit `/nl/pitch` | Shows Dutch pitch | ✅ Pass |
| Build completes | No errors | ✅ Pass |

## 4.3 SEO Validation

- [x] hreflang tags present on all pages
- [x] x-default points to English
- [x] Canonical URLs set correctly
- [x] Language attribute on `<html>` tag
- [x] No duplicate content issues

---

# Summary

## What Was Delivered

1. **Full i18n System**: Type-safe translation dictionary with 200+ keys
2. **Dutch Translations**: Complete Dutch versions of all pages
3. **SEO-Optimized**: Proper hreflang implementation for search engines
4. **Language Switcher**: Easy toggle between EN/NL in navigation
5. **Clean URLs**: Subdirectory-based routing (/en/, /nl/)
6. **Static Compatible**: Works with Netlify static hosting

## URL Map

| Page | English | Dutch |
|------|---------|-------|
| Homepage | /en/ | /nl/ |
| Documentation | /en/docs | /nl/docs |
| Pitch Deck | /en/pitch | /nl/pitch |
| 404 | /en/404 | /nl/404 |

## Future Enhancements

- [ ] Add more languages (German, French)
- [ ] Browser language auto-detection
- [ ] Translation management system (CMS)
- [ ] RTL language support (Arabic)
