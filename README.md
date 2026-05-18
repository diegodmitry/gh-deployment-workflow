# GitHub Pages Deployment

A simple GitHub Actions workflow to deploy a static website to GitHub Pages.

This project is part of my DevOps learning journey, following the roadmap.sh DevOps path.

- Roadmap.sh project: https://roadmap.sh/projects/github-actions-deployment-workflow
- Level: Beginner
- Main topics: GitHub Actions, GitHub Pages, CI/CD, YAML, Static Websites

## Goal

The goal of this project is to create a simple CI/CD workflow using GitHub Actions to deploy a static website to GitHub Pages.

The workflow is configured to run only when the `index.html` file changes on the `main` branch.

This helps practice the basic concepts of continuous integration and continuous deployment using GitHub-native tools.

## Requirements from roadmap.sh

The original roadmap.sh project asks for:

- A public GitHub repository
- A simple `index.html` file saying `Hello, GitHub Actions!`
- A `README.md` file explaining the project
- A GitHub Actions workflow file called `deploy.yml`
- The workflow file must be inside `.github/workflows`
- The workflow must deploy the website to GitHub Pages
- The workflow must run only when `index.html` changes
- The deployed website must be accessible from the GitHub Pages URL

Example GitHub Pages URL:

```text
https://<username>.github.io/gh-deployment-workflow/
```

## Implemented features

This project currently:

- Contains a simple static `index.html` file
- Uses GitHub Actions to automate deployment
- Deploys the website to GitHub Pages
- Runs the workflow on pushes to the `main` branch
- Triggers the workflow only when `index.html` is changed
- Uses GitHub Pages official deployment actions
- Includes the required permissions for GitHub Pages deployment

## Technologies used

- HTML
- GitHub Actions
- GitHub Pages
- YAML
- CI/CD concepts
- Static website deployment

## Project structure

```text
gh-deployment-workflow/
├── .github/
│   └── workflows/
│       └── deploy.yml
├── index.html
└── README.md
```

## How to run locally

Clone the repository:

```bash
git clone https://github.com/diegodmitry/gh-deployment-workflow.git
```

Go to the project folder:

```bash
cd gh-deployment-workflow
```

Open the `index.html` file in your browser.

Example using Linux:

```bash
xdg-open index.html
```

Example using macOS:

```bash
open index.html
```

Or open the file manually by double-clicking it.

## Example `index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>GitHub Pages Deployment</title>
</head>
<body>
  <h1>Hello, GitHub Actions!</h1>
</body>
</html>
```

## GitHub Actions workflow

The workflow file is located at:

```text
.github/workflows/deploy.yml
```

Example workflow:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches:
      - main
    paths:
      - 'index.html'

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: false

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}

    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup GitHub Pages
        uses: actions/configure-pages@v5

      - name: Upload GitHub Pages artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: .

      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

## How the workflow works

### Trigger

```yaml
on:
  push:
    branches:
      - main
    paths:
      - 'index.html'
```

This means the workflow runs only when:

- A push is made to the `main` branch
- The `index.html` file is changed

If only the `README.md` file is changed, the workflow will not run.

## Workflow steps explained

### `actions/checkout@v4`

This action downloads the repository code into the GitHub Actions runner.

Without this step, the workflow would not have access to the project files.

### `actions/configure-pages@v5`

This action configures the GitHub Pages environment for deployment.

It prepares the workflow to publish content using GitHub Pages.

### `actions/upload-pages-artifact@v3`

This action packages the static website files and uploads them as an artifact.

The artifact is later used by the deployment step.

### `actions/deploy-pages@v4`

This action deploys the uploaded artifact to GitHub Pages.

After this step finishes successfully, the website becomes available at the GitHub Pages URL.

## Permissions explained

```yaml
permissions:
  contents: read
  pages: write
  id-token: write
```

### `contents: read`

Allows the workflow to read the repository files.

### `pages: write`

Allows the workflow to publish content to GitHub Pages.

Without this permission, the deployment step would fail because the workflow would not be allowed to write to GitHub Pages.

### `id-token: write`

Allows the workflow to generate a secure identity token used during the deployment process.

This is required by the GitHub Pages deployment action.

## GitHub Pages URL

After a successful deployment, the website will be available at:

```text
https://diegodmitry.github.io/gh-deployment-workflow/
```

If your GitHub username or repository name is different, the URL will follow this format:

```text
https://<username>.github.io/<repository-name>/
```

## Real-world scenario

A company or developer may have a static website, documentation page, landing page, or portfolio hosted on GitHub Pages.

Instead of manually deploying changes, a GitHub Actions workflow can automatically publish updates whenever specific files change.

This helps teams:

- Automate deployment
- Reduce manual work
- Avoid deployment mistakes
- Keep static websites updated
- Practice CI/CD using a simple workflow

## What I practiced

With this project, I practiced:

- Creating a GitHub Actions workflow
- Writing YAML configuration files
- Using GitHub Pages for static website hosting
- Understanding CI/CD basics
- Configuring workflow triggers
- Using path-based workflow filters
- Working with GitHub Actions permissions
- Deploying static files automatically
- Understanding the deployment flow from code change to published website

## Requirements

To run and deploy this project, you need:

- A GitHub account
- A public GitHub repository
- GitHub Pages enabled
- A `main` branch
- An `index.html` file
- A GitHub Actions workflow file inside `.github/workflows`

## Current limitations

- The project currently uses only plain HTML
- The workflow deploys only when `index.html` changes
- There is no CSS file yet
- There is no JavaScript file yet
- There is no static site generator configured
- The website is very simple
- The workflow does not run when README changes
- The project does not include automated tests

## Possible improvements

Future improvements:

- Add CSS styling
- Add a personal portfolio page
- Add JavaScript interactivity
- Add a custom domain
- Add a static site generator such as Astro, Hugo, or Jekyll
- Add a more complete landing page
- Add build and test steps before deployment
- Add deployment status badges to the README
- Add multiple pages
- Improve accessibility and SEO
- Add a custom 404 page

## Reference

- https://roadmap.sh/projects/github-pages-deployment