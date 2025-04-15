# ⚙️ Platly GitHub Actions Workflows

This repository contains reusable GitHub Actions workflows for the [Platly](https://github.com/Platly) ecosystem.  
It serves as a central source of truth for shared CI/CD logic across all infrastructure and platform repositories.

> All workflows are located in `.github/workflows/`

---

## Usage

In a consuming repository (e.g., `platly/infrastructure-network`), call a reusable workflow like this:

```yaml
# .github/workflows/on_pull_request_open.yml
name: Network Deploy

on:
  pull_request:
    branches:
      - main

permissions:
  contents: read
  pull-requests: write
  id-token: write

jobs:
  terraform:
    uses: platly/github-actions/.github/workflows/terraform-core.yml@main
    with:
      FOO: bar
    secrets:
      BAR: ${{ secrets.BAR }}
```

---

## Make sure to:

- Set permissions in the calling workflow;
- Use the correct branch or tag (@main, @v1, etc.);

---

## Contributing

To add a new reusable workflow:
- Create a new file in `.github/workflows/`;
- Follow the naming pattern e.g. `workflow_docker_build.yml`;
- Follow GitHub's reusable workflow syntax;
- Keep workflows modular and parameterized;
- Simplicity is key. Add clear comments if needed;