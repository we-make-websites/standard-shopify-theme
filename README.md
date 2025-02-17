# Project
Standard Shopify theme based on Dawn.

## 🔧 Development

Use the Shopify CLI in order to interact with the theme
* [All Shopify CLI Commands](https://shopify.dev/docs/themes/tools/cli/commands)

### Key commands

* `shopify theme dev`
  * Uploads the current theme to a store so you can preview it and develop with it
  * The theme you work on here will not be visible in the theme list on the Shopify Admin
* `shopify theme share`
  * Uploads your theme as a new, unpublished theme in your theme library
  * This makes the theme visible in the Shopify Admin
  * Useful if you need to share a development theme for review by others
* `shopify theme push`
  * Pushes your development theme to an existing theme on the store
  * This can be used to push your local development theme to an unpublished `Dev_[Initials]` theme
* `shopify theme pull`
  * Downloads a copy of the theme
  * Use for live syncs

### Key flags

* Use the `-e` flag to define the environment to use
* Set environments in the _shopify.theme.toml_ file

### `.shopifyignore` file

The `.shopifyignore` file defines the files that are ignored when running Shopify CLI commands.

This file is not used by the GitHub action workflows. Update the `--ignore-file` flags to update these.

## 🚀 Deployment

Deployments are handled via Github Actions. The files for the actions are found in _/.github/workflows_

There are 3 deployment actions:
* _deploy-development.yml_
  * Deploys to the DEVELOPMENT (Project) theme
  * Triggered on push to the `development` branch
* _deploy-staging.yml_
  * Deploys to the STAGING (Project) theme
  * Triggered on push to the `staging` branch
* _deploy-production.yml_
  * Deploys to the PRODUCTION (Project) theme
  * Deployment is triggered manually via Github Actions page on the repo

### Deploying to Production

Production deployments are manually triggered so that the PRODUCTION (Project) theme is not updated by an accidental git push to `main`
To trigger the deployment:
* Go to the Github Repo
* Select Actions in the navigation bar
* Select _Deploy to Production_ in the sidebar
* Click the _Run workflow_ button
* Run the workflow from the `main` branch
  * _The deployment will get skipped if you select a branch other than `main`_

### Deployment Configuration

The deployment credentials are stored in the secrets in Github that the actions then reference. The secrets/variables can be accessed from _Settings_ -> _Secrets and variables_ -> _Actions_

The required secrets/variables are:

| Secret | Description |
| --* | --* |
| `SHOPIFY_PASSWORD` | Shopify Admin Access Token. |
| `STORE_URL` | The URL that precedes myshopify.com in the store URL. |
| `PRODUCTION_THEME_ID` | Theme ID for the PRODUCTION (Project) theme. |
| `STAGING_THEME_ID` | Theme ID for the STAGING (Project) theme. |
| `DEVELOPMENT_THEME_ID` | Theme ID for the DEVELOPMENT (Project) theme. |
