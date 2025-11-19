# Deployment Guide

This guide will walk you through deploying the Backlog Chef website to Netlify.

## Prerequisites

- A GitHub, GitLab, or Bitbucket account
- A Netlify account (free tier works fine)
- Git installed locally

## Step 1: Push to Git Repository

1. Create a new repository on GitHub/GitLab/Bitbucket (e.g., `backlog-chef-website`)

2. Add the remote and push:
```bash
git remote add origin <your-repository-url>
git commit -m "Initial commit: Backlog Chef website"
git push -u origin main
```

## Step 2: Connect to Netlify

1. Go to [Netlify](https://app.netlify.com)

2. Sign up or log in

3. Click "Add new site" → "Import an existing project"

4. Choose your Git provider (GitHub/GitLab/Bitbucket)

5. Authorize Netlify to access your repositories

6. Select the `backlog-chef-website` repository

## Step 3: Configure Build Settings

Netlify should auto-detect the settings from `netlify.toml`, but verify:

- **Build command**: `npm run build`
- **Publish directory**: `dist`
- **Branch to deploy**: `main`

Click "Deploy site"

## Step 4: Wait for Build

Netlify will:
1. Clone your repository
2. Install dependencies (`npm install`)
3. Build the site (`npm run build`)
4. Deploy to their CDN

This usually takes 1-3 minutes for the first deploy.

## Step 5: Get Your URL

Once deployed, Netlify provides:
- A random URL like `https://random-name-123.netlify.app`
- You can customize this in Site Settings → Domain Management

## Step 6: Custom Domain (Optional)

To use a custom domain like `backlogchef.com`:

1. Go to Site Settings → Domain Management
2. Click "Add custom domain"
3. Enter your domain name
4. Follow Netlify's instructions to:
   - Update your domain's DNS records
   - Netlify will automatically provision SSL certificates

## Continuous Deployment

Netlify automatically deploys when you push to the `main` branch:

```bash
# Make changes to your site
git add -A
git commit -m "Update homepage"
git push

# Netlify automatically builds and deploys!
```

## Deploy Previews

Netlify creates deploy previews for pull requests:
1. Create a new branch
2. Make changes
3. Create a pull request
4. Netlify builds a preview URL
5. Review changes before merging

## Environment Variables

If you need environment variables in the future:

1. Go to Site Settings → Environment Variables
2. Add key-value pairs
3. Rebuild the site

## Monitoring

Netlify provides:
- Build logs: See what happened during deployment
- Analytics: Traffic and performance metrics (paid feature)
- Forms: Collect form submissions (free tier available)

## Troubleshooting

### Build Fails

1. Check the build logs in Netlify dashboard
2. Try building locally: `npm run build`
3. Ensure all dependencies are in `package.json`

### Site Not Updating

1. Check if the build succeeded
2. Clear your browser cache
3. Check the correct branch is being deployed

### 404 Errors

The `netlify.toml` includes redirect rules for 404s.
If you add new routes, they should work automatically.

## Support

- [Netlify Documentation](https://docs.netlify.com)
- [Netlify Support](https://www.netlify.com/support/)
- [Astro Deployment Docs](https://docs.astro.build/en/guides/deploy/netlify/)
