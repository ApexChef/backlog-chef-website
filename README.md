# Backlog Chef Website

Official website for Backlog Chef - Transform meetings into high-quality Product Backlogs with AI.

## About Backlog Chef

Backlog Chef is an intelligent system that transforms Scrum meetings into structured, high-quality Product Backlog Items with built-in quality assurance, context enrichment, and stakeholder intelligence.

## Tech Stack

- **Framework**: [Astro](https://astro.build)
- **Styling**: [Tailwind CSS](https://tailwindcss.com)
- **Deployment**: [Netlify](https://netlify.com)

## Development

### Prerequisites

- Node.js 18+
- npm or yarn

### Getting Started

1. Clone the repository:
```bash
git clone <repository-url>
cd backlog-chef-website
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm run dev
```

4. Open your browser and navigate to `http://localhost:4321`

### Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build locally

## Deployment

This site is configured for deployment on Netlify.

### Deploy to Netlify

1. Push your code to a Git repository (GitHub, GitLab, or Bitbucket)

2. Log in to [Netlify](https://app.netlify.com)

3. Click "Add new site" > "Import an existing project"

4. Connect your Git provider and select this repository

5. Configure build settings:
   - **Build command**: `npm run build`
   - **Publish directory**: `dist`

6. Click "Deploy site"

Netlify will automatically:
- Build your site on every push to main
- Provide a URL for your site
- Handle SSL certificates
- Provide deploy previews for pull requests

### Environment Variables

No environment variables are required for the current version.

## Project Structure

```
/
├── public/             # Static assets
├── src/
│   ├── layouts/       # Reusable layouts
│   │   └── Layout.astro
│   ├── pages/         # Page routes
│   │   ├── index.astro      # Homepage
│   │   ├── docs.astro       # Documentation
│   │   └── 404.astro        # 404 page
│   └── styles/        # Global styles
│       └── global.css
├── astro.config.mjs   # Astro configuration
├── netlify.toml       # Netlify configuration
├── tailwind.config.js # Tailwind configuration
└── package.json
```

## Features

- Responsive design
- SEO optimized
- Fast page loads with Astro's static generation
- Tailwind CSS for styling
- Netlify-ready deployment

## Learn More

- [Backlog Chef Documentation](https://github.com/ApexChef/backlog-chef)
- [Astro Documentation](https://docs.astro.build)
- [Netlify Documentation](https://docs.netlify.com)

## License

TBD

## Created By

Alwin (ApexChef)
- Salesforce/Apex Developer
- Former Kitchen Chef
- Process & Automation Expert
