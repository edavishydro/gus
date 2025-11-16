# gus

gus wraps your monorepo's mise tasks so that you don't have to `cd` into each package to run them.

## Usage

Instead of running mise tasks like this:

```bash
cd packages/package-a
mise run build
```

You can run them like this:

```bash
gus build package-a
```

You can even specify which .env file to run the task with:

```bash
gus deploy package-b --env prod
```

After running `gus discover` in your monorpo, gus will know about all your packages and their mise tasks.

Run `gus list` to see all available packages and their tasks.

If you want to manually control what tasks and packages are available, you can create/edit the `.gus.yaml` file in the monorepo root.

````yaml
# .gus.yaml.example
# Gus configuration for your monorepo
# Copy this to .gus.yaml and customize for your setup

monorepo_root: .

services:
  # Example app
  my-api:
    path: apps/my-api
    type: app
    description: REST API service
    tasks:
      - build
      - test
      - deploy
      - lint
      - docker-build

  # Example library
  my-lib:
    path: libs/my-lib
    type: library
    description: Shared utilities library
    tasks:
      - test
      - lint
      - build
      - publish

  # Example infrastructure
  terraform:
    path: infrastructure/terraform
    type: infrastructure
    description: Infrastructure as code
    tasks:
      - plan
      - apply
      - destroy

# Optional: environment configurations
environments:
  dev:
    gcp_project: my-project-dev
  staging:
    gcp_project: my-project-staging
  prod:
    gcp_project: my-project-prod

# Optional: aliases for common operations
aliases:
  all-apps:
    - my-api
  all-libs:
    - my-lib
```
````

```

```
