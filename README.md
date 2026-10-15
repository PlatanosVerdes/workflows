# workflows

Reusable GitHub Actions workflows shared by my repos.

## release.yml

On every push to main: tags the commit with CalVer (vYYYY.MM.DD, then .1, .2...), publishes
an arm64 image to ghcr.io/<owner>/<repo>:<tag> and, with `deploy-repo`, sends that repo an
`app-released` repository_dispatch carrying `repo` and `tag`. Caller:

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
    with:
      deploy-repo: PlatanosVerdes/rpi-services
    secrets:
      DEPLOY_TOKEN: ${{ secrets.DEPLOY_TOKEN }}
```

`DEPLOY_TOKEN` is a fine-grained token limited to the deploy repo with Contents: read and write.
