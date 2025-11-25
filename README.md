# Container Dependency Submitter

This repository contains a reusable workflow to scan a container image and submit its dependencies to the GitHub Dependency Graph.

## Features

- 📦 **Generates SBOM** using `anchore/sbom-action` (Syft)
- 🚀 **Submits to GitHub** using `scalabrino/sbom-dependency-submission-action`
- 📊 **Populates Dependency Graph** in the "Insights" tab of your repository

## Usage

### Reusable Workflow

```yaml
jobs:
  submit-deps:
    uses: YOUR-ORG/container-dependency-submitter/.github/workflows/submit-dependencies.yml@main
    with:
      image: 'my-image:latest'
```

### Permissions

The calling workflow must have `contents: write` permission to submit to the Dependency Graph.

```yaml
permissions:
  contents: write
```

## How it works

1. **Generate SBOM**: The workflow uses Syft to generate an SBOM in SPDX JSON format from the specified container image.
2. **Submit**: The SBOM is processed and submitted to the GitHub Dependency Submission API.
3. **View**: Dependencies appear in the repository's "Insights" -> "Dependency graph" view.

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `image` | The container image to analyze | Yes | - |
| `token` | GitHub token | No | `github.token` |

## License

MIT
