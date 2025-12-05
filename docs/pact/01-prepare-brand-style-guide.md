# PACT Prepare Phase: Apex Chef Brand Style Guide

## Project Overview

**Project**: Backlog Chef Website Brand Implementation
**Company**: Apex Chef
**Tagline**: "Satisfy your Salesforce Appetite"
**Current Website**: https://apexchef.eu/

---

## Brand Identity

### Company Description
Apex Chef is a Salesforce consultancy that uses culinary metaphors to describe their services. The brand identity revolves around "crafting custom solutions with precision, just like your favorite dish."

### Logo
- **Primary Text**: APEX CHEF
- **Tagline**: Satisfy your Salesforce Appetite
- **Available Formats**: SVG, PNG, PDF
- **Logo Variants**:
  - `color` - Full color logo on brand background
  - `black` - Black logo for light backgrounds
  - `white` - White logo for dark backgrounds
  - `black-white` - Black text on white background
  - `inverse` - Inverted color scheme
  - `transparent` - Transparent background
  - `accent1`, `accent2`, `accent3` - Accent color variations

### Logo Asset Locations
Source directory: `/Users/alwin/Google Drive - Apex Chef/Huis Stijl/logo-files/`
- `basic/` - Standard logo variations
- `animation/` - Animated logo assets
- `gradient/` - Gradient logo versions
- `special/` - Special occasion logos
- `texture/` - Textured logo versions

---

## Color Palette

### Primary Colors

| Name | Hex Code | RGB | Usage |
|------|----------|-----|-------|
| **Sage Green** | `#717951` | rgb(113, 121, 81) | Primary background, brand identity |
| **Cream White** | `#f6f2f1` | rgb(246, 242, 241) | Primary text, logo on dark backgrounds |

### Accent Colors

| Name | Hex Code | RGB | Usage |
|------|----------|-----|-------|
| **Blush Pink** | `#f5e1db` | rgb(245, 225, 219) | Accent 1 - Soft highlights, cards |
| **Peach** | `#f5d1c6` | rgb(245, 209, 198) | Accent 2 - Secondary highlights |
| **Salmon Coral** | `#f5c1b0` | rgb(245, 193, 176) | Accent 3 - Call-to-action highlights |

### Color Usage Guidelines
- **Sage Green (#717951)**: Primary brand color. Use for headers, hero sections, navigation backgrounds
- **Cream White (#f6f2f1)**: Primary text color on dark backgrounds, also works as light section backgrounds
- **Accent Colors**: Use for subtle highlights, card backgrounds, hover states, and visual interest

### Suggested Additional Colors for Web Implementation
```css
:root {
  /* Primary */
  --color-sage-green: #717951;
  --color-cream-white: #f6f2f1;

  /* Accents */
  --color-accent-1: #f5e1db; /* Blush Pink */
  --color-accent-2: #f5d1c6; /* Peach */
  --color-accent-3: #f5c1b0; /* Salmon Coral */

  /* Derived colors (suggested for web) */
  --color-sage-dark: #5a6141;   /* Darker sage for hover states */
  --color-sage-light: #8a9269;  /* Lighter sage for subtle backgrounds */
  --color-text-dark: #2d2d2d;   /* Dark text for light backgrounds */
  --color-text-muted: #6b6b6b;  /* Muted text for secondary content */
}
```

---

## Typography

### Primary Font: Montserrat-Alt1

**Description**: A custom version of Montserrat Light, designed to be simple, clean, and professional. Makes titles stand out while maintaining readability.

**Font Source**: `/Users/alwin/Google Drive - Apex Chef/Huis Stijl/montserrat_alt1/`

### Available Weights
| Weight | File Name | CSS Value |
|--------|-----------|-----------|
| Thin | MontserratAlt1-Thin | 100 |
| Extra Light | MontserratAlt1-ExtraLight | 200 |
| Light | MontserratAlt1-Light | 300 |
| Regular | MontserratAlt1-Regular | 400 |
| Medium | MontserratAlt1-Medium | 500 |
| Semi Bold | MontserratAlt1-SemiBold | 600 |
| Bold | MontserratAlt1-Bold | 700 |
| Extra Bold | MontserratAlt1-ExtraBold | 800 |
| Black | MontserratAlt1-Black | 900 |

### Font Files Available
- **Web formats**: WOFF, WOFF2 (in `/fonts/webfonts/`)
- **Desktop formats**: OTF, TTF (in `/fonts/otf/` and `/fonts/ttf/`)
- **CSS Import**: `Montserrat-Alt1.css`

### Typography Scale (Recommended)
```css
/* Headings */
h1 { font-weight: 700; font-size: 3rem; }      /* Bold - Hero titles */
h2 { font-weight: 600; font-size: 2.25rem; }   /* SemiBold - Section headers */
h3 { font-weight: 500; font-size: 1.5rem; }    /* Medium - Card titles */
h4 { font-weight: 500; font-size: 1.25rem; }   /* Medium - Subheadings */

/* Body */
body { font-weight: 400; font-size: 1rem; }    /* Regular - Body text */
.lead { font-weight: 300; font-size: 1.125rem; } /* Light - Lead paragraphs */

/* UI Elements */
.button { font-weight: 600; }                   /* SemiBold - Buttons */
.nav-link { font-weight: 500; }                 /* Medium - Navigation */
.caption { font-weight: 300; font-size: 0.875rem; } /* Light - Captions */
```

### Fallback Stack
```css
font-family: 'Montserrat-Alt1', 'Montserrat', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
```

---

## Design Patterns from Existing Website

### Current Website (apexchef.eu) Features
- Dark/Light mode support via `colorTheme` localStorage
- View transition animations (180ms cubic-bezier)
- Language switcher (Nederlands, Engels, Fran\u00e7ais)
- Blog section
- Consultation CTA ("Get Your Free Consultation")

### Animation Standards
```css
/* Page transitions */
transition-timing-function: cubic-bezier(0.76, 0, 0.24, 1);
transition-duration: 180ms;
animation-fill-mode: both;
```

### Navigation Pattern
- Header logo linking to home
- Language switcher
- Primary navigation links
- Blog link

---

## Asset Inventory

### Brand Assets Directory Structure
```
/Users/alwin/Google Drive - Apex Chef/Huis Stijl/
├── logo-files/
│   ├── basic/           # Standard logos (SVG, PNG, PDF)
│   ├── animation/       # Animated versions
│   ├── gradient/        # Gradient backgrounds
│   ├── special/         # Special editions
│   └── texture/         # Textured versions
├── montserrat_alt1/
│   └── fonts/
│       ├── otf/         # OpenType fonts
│       ├── ttf/         # TrueType fonts
│       └── webfonts/    # Web fonts (WOFF, WOFF2, CSS)
├── business-cards/      # Business card designs
├── facebook-covers/     # Social media covers
├── facebook-posts/      # Social media post templates
├── instagram/           # Instagram assets
├── letterheads/         # Letterhead designs
├── mockups/             # Brand mockups
├── presentations/       # Presentation templates
├── profile-icons/       # Profile icons
├── profile-logos/       # Profile logo variations
└── profile-pictures/    # Profile picture assets
```

### Key Files for Web Implementation
1. **Logo**: `/logo-files/basic/color.svg` (primary)
2. **Logo (dark bg)**: `/logo-files/basic/white.svg`
3. **Logo (light bg)**: `/logo-files/basic/black.svg`
4. **Transparent logo**: `/logo-files/basic/transparent.svg`
5. **Webfonts CSS**: `/montserrat_alt1/fonts/webfonts/Montserrat-Alt1.css`
6. **Profile Picture**: `/ProfilePicture.png`

---

## Implementation Requirements

### Phase 1: Font Integration
1. Copy webfont files to project's `public/fonts/` directory
2. Create `@font-face` declarations in CSS
3. Update Tailwind configuration with custom font family

### Phase 2: Color System
1. Define CSS custom properties for brand colors
2. Configure Tailwind theme with brand colors
3. Create utility classes for brand-specific styling

### Phase 3: Logo Integration
1. Copy logo SVG files to `public/images/` or use as components
2. Create responsive logo component with dark/light variants
3. Implement favicon from brand assets

### Phase 4: Component Styling
1. Style buttons with brand colors and typography
2. Create card components with accent colors
3. Implement navigation with brand styling
4. Add hero sections with sage green background

---

## Technical Specifications

### Current Tech Stack (backlog-chef-website)
- **Framework**: Astro
- **CSS**: Tailwind CSS 4 (via `@tailwindcss/vite`)
- **Hosting**: Netlify
- **Output**: Static site
- **i18n**: English (default) and Dutch

### Recommended Tailwind v4 Configuration
```css
/* In src/styles/global.css */
@import "tailwindcss";

@theme {
  /* Colors */
  --color-sage: #717951;
  --color-sage-dark: #5a6141;
  --color-sage-light: #8a9269;
  --color-cream: #f6f2f1;
  --color-blush: #f5e1db;
  --color-peach: #f5d1c6;
  --color-coral: #f5c1b0;

  /* Fonts */
  --font-family-display: 'Montserrat-Alt1', 'Montserrat', sans-serif;
  --font-family-body: 'Montserrat-Alt1', 'Montserrat', sans-serif;
}
```

---

## Next Steps (Architect Phase)

1. Design component architecture for brand-consistent UI
2. Plan responsive layouts for hero, cards, navigation
3. Create design tokens system
4. Define reusable component patterns
5. Plan dark/light mode color mapping

---

## References

- Company Style Assets: `/Users/alwin/Google Drive - Apex Chef/Huis Stijl/`
- Current Website: https://apexchef.eu/
- Font Documentation: `/montserrat_alt1/README.md`
- Logo License: OFL License (Open Font License)