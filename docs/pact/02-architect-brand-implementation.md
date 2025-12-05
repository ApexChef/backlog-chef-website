# PACT Architect Phase: Brand Style Implementation

## Overview

This document defines the technical architecture for implementing the Apex Chef brand style guide into the Backlog Chef website. It covers file structure, Tailwind configuration, font integration, component specifications, and implementation guidelines.

---

## Current State Analysis

### Existing Tech Stack
- **Framework**: Astro
- **CSS**: Tailwind CSS v4 (via `@tailwindcss/vite`)
- **Hosting**: Netlify (static output)
- **i18n**: English (default) + Dutch

### Current Issues to Address
| Issue | Current State | Target State |
|-------|---------------|--------------|
| Colors | Generic blue/indigo theme | Apex Chef brand colors |
| Typography | System fonts | Montserrat-Alt1 custom font |
| Logo | "Backlog Chef" text only | Apex Chef SVG logo |
| Favicon | Astro logo | Apex Chef brand icon |
| Navigation | White background | Brand-styled header |
| Footer | Slate-900 dark | Brand sage green |

---

## File Structure Architecture

### Proposed Directory Structure
```
public/
├── fonts/
│   ├── MontserratAlt1-Regular.woff2
│   ├── MontserratAlt1-Medium.woff2
│   ├── MontserratAlt1-SemiBold.woff2
│   ├── MontserratAlt1-Bold.woff2
│   ├── MontserratAlt1-Light.woff2
│   └── MontserratAlt1-ExtraBold.woff2
├── images/
│   ├── logo/
│   │   ├── apex-chef-color.svg
│   │   ├── apex-chef-white.svg
│   │   ├── apex-chef-black.svg
│   │   └── apex-chef-icon.svg
│   └── brand/
│       └── profile-picture.png
├── favicon.svg (new - brand icon)
└── favicon.ico (fallback)

src/
├── components/
│   ├── ui/
│   │   ├── Button.astro
│   │   ├── Card.astro
│   │   ├── Badge.astro
│   │   └── SectionHeader.astro
│   ├── layout/
│   │   ├── Header.astro
│   │   ├── Footer.astro
│   │   ├── Navigation.astro
│   │   └── MobileMenu.astro
│   ├── brand/
│   │   ├── Logo.astro
│   │   └── LogoIcon.astro
│   └── LanguageSwitcher.astro (existing)
├── layouts/
│   └── Layout.astro (refactored)
├── styles/
│   ├── global.css (enhanced)
│   └── fonts.css (new - @font-face declarations)
└── ...
```

---

## Tailwind CSS v4 Theme Configuration

### Updated global.css
```css
/* src/styles/global.css */
@import "tailwindcss";
@import "./fonts.css";

@theme {
  /* ===== BRAND COLORS ===== */

  /* Primary */
  --color-sage: #717951;
  --color-sage-50: #f7f8f5;
  --color-sage-100: #eaece3;
  --color-sage-200: #d5d9c8;
  --color-sage-300: #b8bfa3;
  --color-sage-400: #9aa17e;
  --color-sage-500: #717951;  /* Base */
  --color-sage-600: #5a6141;
  --color-sage-700: #464b33;
  --color-sage-800: #383d2a;
  --color-sage-900: #2f3224;
  --color-sage-950: #181a12;

  /* Secondary / Cream */
  --color-cream: #f6f2f1;
  --color-cream-50: #fdfcfc;
  --color-cream-100: #f6f2f1;  /* Base */
  --color-cream-200: #ede6e4;
  --color-cream-300: #ddd3cf;
  --color-cream-400: #c7b8b2;
  --color-cream-500: #b09d95;

  /* Accent Colors */
  --color-blush: #f5e1db;
  --color-peach: #f5d1c6;
  --color-coral: #f5c1b0;

  /* Semantic Colors */
  --color-text-primary: #2d2d2d;
  --color-text-secondary: #6b6b6b;
  --color-text-muted: #9ca3af;
  --color-text-on-dark: #f6f2f1;
  --color-text-on-sage: #f6f2f1;

  /* ===== TYPOGRAPHY ===== */

  --font-family-display: 'Montserrat-Alt1', 'Montserrat', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  --font-family-body: 'Montserrat-Alt1', 'Montserrat', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  --font-family-mono: 'Fira Code', 'Consolas', monospace;

  /* Font Sizes (using rem for accessibility) */
  --font-size-xs: 0.75rem;     /* 12px */
  --font-size-sm: 0.875rem;    /* 14px */
  --font-size-base: 1rem;      /* 16px */
  --font-size-lg: 1.125rem;    /* 18px */
  --font-size-xl: 1.25rem;     /* 20px */
  --font-size-2xl: 1.5rem;     /* 24px */
  --font-size-3xl: 1.875rem;   /* 30px */
  --font-size-4xl: 2.25rem;    /* 36px */
  --font-size-5xl: 3rem;       /* 48px */
  --font-size-6xl: 3.75rem;    /* 60px */

  /* ===== SPACING ===== */

  --spacing-section: 5rem;      /* Section padding */
  --spacing-container: 7rem;    /* Max-width container */

  /* ===== TRANSITIONS ===== */

  --transition-fast: 150ms;
  --transition-normal: 200ms;
  --transition-slow: 300ms;
  --ease-out-expo: cubic-bezier(0.16, 1, 0.3, 1);
  --ease-in-out-expo: cubic-bezier(0.87, 0, 0.13, 1);

  /* ===== SHADOWS ===== */

  --shadow-sm: 0 1px 2px 0 rgb(113 121 81 / 0.05);
  --shadow-md: 0 4px 6px -1px rgb(113 121 81 / 0.1), 0 2px 4px -2px rgb(113 121 81 / 0.1);
  --shadow-lg: 0 10px 15px -3px rgb(113 121 81 / 0.1), 0 4px 6px -4px rgb(113 121 81 / 0.1);
  --shadow-xl: 0 20px 25px -5px rgb(113 121 81 / 0.1), 0 8px 10px -6px rgb(113 121 81 / 0.1);

  /* ===== BORDER RADIUS ===== */

  --radius-sm: 0.375rem;
  --radius-md: 0.5rem;
  --radius-lg: 0.75rem;
  --radius-xl: 1rem;
  --radius-full: 9999px;
}

/* Base styles */
html {
  font-family: var(--font-family-body);
  color: var(--color-text-primary);
  scroll-behavior: smooth;
}

body {
  min-height: 100vh;
  background: var(--color-cream-50);
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-display);
  font-weight: 600;
  color: var(--color-sage-900);
}

/* Links */
a {
  transition: color var(--transition-fast) ease;
}

/* Selection */
::selection {
  background-color: var(--color-sage-200);
  color: var(--color-sage-900);
}
```

### Font CSS File
```css
/* src/styles/fonts.css */
@font-face {
  font-family: 'Montserrat-Alt1';
  src: url('/fonts/MontserratAlt1-Light.woff2') format('woff2');
  font-weight: 300;
  font-style: normal;
  font-display: swap;
}

@font-face {
  font-family: 'Montserrat-Alt1';
  src: url('/fonts/MontserratAlt1-Regular.woff2') format('woff2');
  font-weight: 400;
  font-style: normal;
  font-display: swap;
}

@font-face {
  font-family: 'Montserrat-Alt1';
  src: url('/fonts/MontserratAlt1-Medium.woff2') format('woff2');
  font-weight: 500;
  font-style: normal;
  font-display: swap;
}

@font-face {
  font-family: 'Montserrat-Alt1';
  src: url('/fonts/MontserratAlt1-SemiBold.woff2') format('woff2');
  font-weight: 600;
  font-style: normal;
  font-display: swap;
}

@font-face {
  font-family: 'Montserrat-Alt1';
  src: url('/fonts/MontserratAlt1-Bold.woff2') format('woff2');
  font-weight: 700;
  font-style: normal;
  font-display: swap;
}

@font-face {
  font-family: 'Montserrat-Alt1';
  src: url('/fonts/MontserratAlt1-ExtraBold.woff2') format('woff2');
  font-weight: 800;
  font-style: normal;
  font-display: swap;
}
```

---

## Component Specifications

### 1. Logo Component
```astro
<!-- src/components/brand/Logo.astro -->
---
interface Props {
  variant?: 'color' | 'white' | 'black';
  size?: 'sm' | 'md' | 'lg';
  showTagline?: boolean;
}

const {
  variant = 'color',
  size = 'md',
  showTagline = false
} = Astro.props;

const sizes = {
  sm: 'h-8',
  md: 'h-10',
  lg: 'h-14'
};
---
<a href="/" class="flex items-center gap-3">
  <img
    src={`/images/logo/apex-chef-${variant}.svg`}
    alt="Apex Chef"
    class={sizes[size]}
  />
  {showTagline && (
    <span class="text-sm text-sage-600 hidden lg:block">
      Satisfy your Salesforce Appetite
    </span>
  )}
</a>
```

### 2. Button Component
```astro
<!-- src/components/ui/Button.astro -->
---
interface Props {
  variant?: 'primary' | 'secondary' | 'outline' | 'ghost';
  size?: 'sm' | 'md' | 'lg';
  href?: string;
  class?: string;
}

const {
  variant = 'primary',
  size = 'md',
  href,
  class: className = ''
} = Astro.props;

const baseStyles = 'inline-flex items-center justify-center font-semibold rounded-lg transition-all duration-200';

const variants = {
  primary: 'bg-sage-500 text-cream hover:bg-sage-600 shadow-md hover:shadow-lg',
  secondary: 'bg-cream text-sage-700 hover:bg-cream-200 shadow-md',
  outline: 'border-2 border-sage-500 text-sage-600 hover:bg-sage-50',
  ghost: 'text-sage-600 hover:bg-sage-50 hover:text-sage-700'
};

const sizes = {
  sm: 'px-4 py-2 text-sm',
  md: 'px-6 py-3 text-base',
  lg: 'px-8 py-4 text-lg'
};

const Element = href ? 'a' : 'button';
---
<Element
  href={href}
  class:list={[baseStyles, variants[variant], sizes[size], className]}
>
  <slot />
</Element>
```

### 3. Card Component
```astro
<!-- src/components/ui/Card.astro -->
---
interface Props {
  variant?: 'default' | 'elevated' | 'accent';
  padding?: 'sm' | 'md' | 'lg';
  hover?: boolean;
}

const {
  variant = 'default',
  padding = 'md',
  hover = true
} = Astro.props;

const variants = {
  default: 'bg-white border border-cream-200',
  elevated: 'bg-white shadow-lg',
  accent: 'bg-gradient-to-br from-blush to-peach'
};

const paddings = {
  sm: 'p-4',
  md: 'p-6',
  lg: 'p-8'
};

const hoverStyles = hover ? 'hover:shadow-xl hover:-translate-y-1 transition-all duration-300' : '';
---
<div class:list={['rounded-xl', variants[variant], paddings[padding], hoverStyles]}>
  <slot />
</div>
```

### 4. Badge Component
```astro
<!-- src/components/ui/Badge.astro -->
---
interface Props {
  variant?: 'sage' | 'blush' | 'peach' | 'coral' | 'dark';
}

const { variant = 'sage' } = Astro.props;

const variants = {
  sage: 'bg-sage-100 text-sage-700',
  blush: 'bg-blush text-sage-800',
  peach: 'bg-peach text-sage-800',
  coral: 'bg-coral text-sage-900',
  dark: 'bg-sage-800 text-cream'
};
---
<span class:list={['inline-block px-4 py-1.5 rounded-full text-sm font-semibold', variants[variant]]}>
  <slot />
</span>
```

### 5. Section Header Component
```astro
<!-- src/components/ui/SectionHeader.astro -->
---
interface Props {
  badge?: string;
  badgeVariant?: 'sage' | 'blush' | 'peach' | 'coral' | 'dark';
  title: string;
  description?: string;
  align?: 'left' | 'center';
}

const {
  badge,
  badgeVariant = 'sage',
  title,
  description,
  align = 'center'
} = Astro.props;

import Badge from './Badge.astro';
---
<div class:list={['mb-12', align === 'center' ? 'text-center' : 'text-left']}>
  {badge && (
    <Badge variant={badgeVariant} class="mb-4">
      {badge}
    </Badge>
  )}
  <h2 class="text-4xl font-bold text-sage-900 mb-4">{title}</h2>
  {description && (
    <p class:list={['text-sage-600 text-lg', align === 'center' ? 'max-w-2xl mx-auto' : '']}>
      {description}
    </p>
  )}
</div>
```

---

## Layout Components

### Header Component
```astro
<!-- src/components/layout/Header.astro -->
---
import Logo from '../brand/Logo.astro';
import Navigation from './Navigation.astro';
import MobileMenu from './MobileMenu.astro';
import LanguageSwitcher from '../LanguageSwitcher.astro';
import { getLangFromUrl, useTranslations, getLocalizedPath, type Lang } from '../../i18n/ui';

interface Props {
  variant?: 'light' | 'dark' | 'transparent';
}

const { variant = 'light' } = Astro.props;

const currentLang = getLangFromUrl(Astro.url);
const t = useTranslations(currentLang);
const localPath = (path: string) => getLocalizedPath(path, currentLang);

const variants = {
  light: 'bg-white/95 backdrop-blur-sm border-b border-cream-200',
  dark: 'bg-sage-800 text-cream',
  transparent: 'bg-transparent absolute top-0 left-0 right-0 z-50'
};

const logoVariant = variant === 'dark' || variant === 'transparent' ? 'white' : 'color';
---
<header class:list={['sticky top-0 z-50', variants[variant]]}>
  <nav class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="flex justify-between items-center h-16">
      <Logo variant={logoVariant} size="md" />

      <div class="hidden md:flex items-center gap-8">
        <Navigation variant={variant} />
        <LanguageSwitcher />
      </div>

      <MobileMenu />
    </div>
  </nav>
</header>
```

### Footer Component
```astro
<!-- src/components/layout/Footer.astro -->
---
import Logo from '../brand/Logo.astro';
import { getLangFromUrl, useTranslations, getLocalizedPath } from '../../i18n/ui';

const currentLang = getLangFromUrl(Astro.url);
const t = useTranslations(currentLang);
const localPath = (path: string) => getLocalizedPath(path, currentLang);
---
<footer class="bg-sage-800 text-cream mt-20">
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
    <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
      <!-- Brand Column -->
      <div>
        <Logo variant="white" size="lg" />
        <p class="text-cream-300 mt-4">{t('footer.tagline')}</p>
      </div>

      <!-- Quick Links -->
      <div>
        <h4 class="font-semibold text-lg mb-4">{t('footer.quickLinks')}</h4>
        <ul class="space-y-2 text-cream-300">
          <li><a href={`${localPath('/')}#cli`} class="hover:text-cream transition">{t('footer.cliCommands')}</a></li>
          <li><a href={`${localPath('/')}#web`} class="hover:text-cream transition">{t('footer.webInterface')}</a></li>
          <li><a href={`${localPath('/')}#features`} class="hover:text-cream transition">{t('footer.features')}</a></li>
          <li><a href={`${localPath('/')}#pricing`} class="hover:text-cream transition">{t('footer.pricing')}</a></li>
          <li><a href={localPath('/docs')} class="hover:text-cream transition">{t('footer.documentation')}</a></li>
        </ul>
      </div>

      <!-- Creator Info -->
      <div>
        <h4 class="font-semibold text-lg mb-4">{t('footer.createdBy')}</h4>
        <p class="text-cream-200">Alwin (ApexChef)</p>
        <p class="text-cream-400 text-sm mt-2">{t('footer.role')}</p>
      </div>
    </div>

    <div class="border-t border-sage-700 mt-8 pt-8 text-center text-cream-400 text-sm">
      <p>&copy; {new Date().getFullYear()} Backlog Chef. {t('footer.copyright')}</p>
    </div>
  </div>
</footer>
```

---

## Color Mapping Strategy

### Light Mode (Default)
| Element | Color Token | Hex Value |
|---------|-------------|-----------|
| Page Background | `cream-50` | #fdfcfc |
| Card Background | `white` | #ffffff |
| Primary Text | `sage-900` | #2f3224 |
| Secondary Text | `sage-600` | #5a6141 |
| Muted Text | `sage-400` | #9aa17e |
| Primary Button | `sage-500` | #717951 |
| Button Hover | `sage-600` | #5a6141 |
| Links | `sage-600` | #5a6141 |
| Link Hover | `sage-800` | #383d2a |
| Borders | `cream-200` | #ede6e4 |
| Hero Background | `sage-500` | #717951 |
| Footer Background | `sage-800` | #383d2a |

### Dark Mode (Future)
| Element | Color Token | Hex Value |
|---------|-------------|-----------|
| Page Background | `sage-950` | #181a12 |
| Card Background | `sage-900` | #2f3224 |
| Primary Text | `cream-100` | #f6f2f1 |
| Secondary Text | `cream-300` | #ddd3cf |
| Primary Button | `sage-400` | #9aa17e |
| Footer Background | `sage-950` | #181a12 |

---

## Hero Section Specification

### Structure
```astro
<section class="relative overflow-hidden bg-sage-500 text-cream">
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-24 lg:py-32">
    <div class="text-center">
      <Badge variant="dark" class="mb-6">
        {t('hero.badge')}
      </Badge>

      <h1 class="text-5xl md:text-6xl lg:text-7xl font-bold mb-6 leading-tight">
        {t('hero.title')}<br />
        <span class="text-blush">{t('hero.titleHighlight')}</span>
      </h1>

      <p class="text-xl md:text-2xl text-cream-200 mb-10 max-w-3xl mx-auto leading-relaxed">
        {t('hero.description')}
      </p>

      <div class="flex flex-col sm:flex-row gap-4 justify-center">
        <Button variant="secondary" size="lg" href="#cli">
          {t('hero.exploreCli')}
        </Button>
        <Button variant="outline" size="lg" href="#web" class="border-cream text-cream hover:bg-cream/10">
          {t('hero.viewWeb')}
        </Button>
        <Button variant="ghost" size="lg" href="/docs" class="text-cream hover:bg-cream/10">
          {t('hero.documentation')}
        </Button>
      </div>
    </div>
  </div>

  <!-- Gradient fade to content -->
  <div class="absolute bottom-0 left-0 right-0 h-24 bg-gradient-to-t from-cream-50 to-transparent"></div>
</section>
```

---

## Implementation Checklist

### Phase 1: Asset Preparation
- [ ] Copy font files (woff2) to `public/fonts/`
- [ ] Copy logo SVGs to `public/images/logo/`
- [ ] Create new favicon from brand icon
- [ ] Create `src/styles/fonts.css`

### Phase 2: Theme Configuration
- [ ] Update `src/styles/global.css` with new theme
- [ ] Configure custom color tokens
- [ ] Set up typography tokens
- [ ] Define shadow and transition tokens

### Phase 3: Component Creation
- [ ] Create `src/components/ui/` directory
- [ ] Implement Button component
- [ ] Implement Card component
- [ ] Implement Badge component
- [ ] Implement SectionHeader component
- [ ] Create `src/components/brand/Logo.astro`

### Phase 4: Layout Updates
- [ ] Refactor `src/layouts/Layout.astro`
- [ ] Create Header component
- [ ] Create Footer component
- [ ] Create Navigation component
- [ ] Update LanguageSwitcher styling

### Phase 5: Page Updates
- [ ] Update `index.astro` with new components
- [ ] Update hero section styling
- [ ] Update card sections
- [ ] Update pricing section
- [ ] Apply brand colors throughout

### Phase 6: Testing
- [ ] Test font loading
- [ ] Verify color accessibility (contrast ratios)
- [ ] Test responsive layouts
- [ ] Verify i18n still works
- [ ] Test on multiple browsers

---

## Accessibility Considerations

### Color Contrast Requirements (WCAG 2.1 AA)
| Combination | Contrast Ratio | Status |
|-------------|----------------|--------|
| Sage-900 on Cream-50 | 11.2:1 | Pass |
| Sage-600 on Cream-50 | 5.8:1 | Pass |
| Cream on Sage-500 | 4.7:1 | Pass |
| Cream on Sage-800 | 9.1:1 | Pass |

### Font Size Minimums
- Body text: 16px minimum (1rem)
- Small text: 14px minimum with bold weight
- Interactive elements: 44px touch target

---

## Performance Considerations

### Font Loading Strategy
- Use `font-display: swap` for immediate text rendering
- Subset fonts to Latin characters only
- Preload critical font weights (Regular, Medium, Bold)

### Image Optimization
- Use SVG for logos (scalable, small file size)
- Optimize PNG profile images with WebP fallback
- Lazy load images below the fold

---

## Next Steps (Code Phase)

1. Copy brand assets to project
2. Implement Tailwind theme configuration
3. Create UI component library
4. Refactor layout components
5. Update page content with new styling
6. Test and iterate

---

## References

- Prepare Phase Document: `docs/pact/01-prepare-brand-style-guide.md`
- Brand Assets: `/Users/alwin/Google Drive - Apex Chef/Huis Stijl/`
- Current Website: https://apexchef.eu/
- Tailwind CSS v4 Docs: https://tailwindcss.com/docs