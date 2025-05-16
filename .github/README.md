# GitHub Actions Workflow

This project uses GitHub Actions to automatically deploy GitBook to GitHub Pages.

## Enabling GitHub Pages

To use this workflow, you need to enable GitHub Pages first:

1. Go to your repository's Settings -> Pages
2. Under "Source", select "GitHub Actions"
3. Click Save

## Workflow Description

The configured workflow (`deploy-gitbook.yml`) will:

1. Automatically trigger when pushing to the main branch
2. Use Honkit (a modern GitBook alternative) to build documentation
3. Run build tests
4. Deploy the generated static site to GitHub Pages

## Manual Deployment

You can also trigger deployment manually:

1. Go to the Actions tab of your repository
2. Select the "Deploy GitBook to GitHub Pages" workflow
3. Click "Run workflow"

## Troubleshooting

If deployment fails, you can:

1. Check the workflow execution logs in the Actions tab
2. Ensure GitHub Pages is correctly configured
3. Check if there are any GitBook build errors

## Local Testing

Test the build before pushing:

```bash
# Initialize npm project
npm init -y

# Install Honkit
npm install honkit --save-dev

# Build GitBook
npx honkit build

# Local preview
npx honkit serve
``` 