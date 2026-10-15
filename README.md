# workflows

Reusable GitHub Actions workflows shared by my repos.

## release.yml

On every push to main: tags the commit with CalVer (vYYYY.MM.DD, then .1, .2...) and publishes
an arm64 image to ghcr.io/<owner>/<repo>:<tag>. Caller:

```yaml
name: Release
on:
  push:
    branches: [main]
permissions:
  contents: write
  packages: write
jobs:
  release:
    uses: PlatanosVerdes/workflows/.github/workflows/release.yml@main
```
