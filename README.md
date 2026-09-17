# Release Postgres Extensions & Tools on PGXN

[![⚖️ PostgreSQL]][pg] [![🎬 Action]][action] [![🧪 Test]][ci]

This action bundles and publishes a releae of a PostgreSQL extension or tool
on [PGXN].

Example workflow:

``` yaml
name: 🚀 Release
permissions:
  contents: write
on:
  push:
jobs:
  release:
    name: Release on PGXN
    runs-on: ubuntu-latest
    steps:
      - name: Check out the repo
        uses: actions/checkout@v7
      - name: Release on PGXN
        uses: pgxn/release-action@v0
        with:
          username: ${{ secrets.PGXN_USERNAME }}
          password: ${{ secrets.PGXN_PASSWORD }}
          dry-run: ${{ startsWith( github.ref, 'refs/tags/v' ) }}
```

We strongly recommend using [workflow secrets] to manage your PGXN username
and password.

## Input Parameters

This action takes the following parameters:

| Key               | Type    | Default   | Description                                       |
| ----------------- | ------- | --------- |-------------------------------------------------- |
| `username`        | string  | ""        | PGXN username                                     |
| `password`        | string  | ""        | PGXN password                                     |
| `submodules`      | boolean | false     | To include Git submodules in the release          |
| `archive-options` | string  | ""        | Additional optoins to pass to `git archive`       |
| `dry-run`         | boolean | false     | Print the release command, rather than execute it |

## Output

This action emits a single output, `archive`, which contains the name of the
zip archive file it created uploaded to PGXN. Use it for other releases in
subsequent steps, for example to make a GitHub release:

```yaml
name: 🚀 Release
permissions:
  contents: write
on:
  push:
jobs:
  release:
    name: Release on PGXN
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v7
      - uses: pgxn/release-action@v0
        id: pgxn
        with:
          username: ${{ secrets.PGXN_USERNAME }}
          password: ${{ secrets.PGXN_PASSWORD }}
          dry-run: ${{ !startsWith( github.ref, 'refs/tags/v' ) }}
      - name: Create GitHub Release
        uses: softprops/action-gh-release@v2
        if: startsWith( github.ref, 'refs/tags/v' )
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          name: "Release ${{ github.ref_name }}"
          files: ${{ steps.pgxn.outputs.archive }}
```

## Prior Art/Inspirations

*   [pgxn-tools]: Old PGXN Linux/amd64-only OCI image for testing and releasing extensions

  [⚖️ PostgreSQL]: https://img.shields.io/badge/License-PostgreSQL-blue.svg "⚖️ PostgreSQL License"
  [pg]: https://opensource.org/license/postgresql "⚖️ PostgreSQL License"
  [🧪 Test]: https://github.com/pgxn/postgres-action/actions/workflows/test.yml/badge.svg "🧪 Test Status"
  [ci]: https://github.com/pgxn/postgres-action/actions/workflows/test.yml "🧪 Test Status"
  [🎬 Action]: https://img.shields.io/badge/Marketplace-Action-purple.svg "[🎬 Marketplace Action]"
  [action]: https://github.com/marketplace/actions/pgxn-release-action "[🎬 Marketplace Action]"
  [PGXN]: https://pgxn.org "PostgreSQL Extension Network"
  [workflow secrets]: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/use-secrets
  [pgxn-tools]: https://github.com/pgxn/docker-pgxn-tools/ "Test image for PostgreSQL & PGXN extensions"
