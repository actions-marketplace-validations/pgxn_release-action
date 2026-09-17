# Changelog

All notable changes to this project will be documented in this file. It uses the
[Keep a Changelog] format, and this project adheres to [Semantic Versioning].

  [Keep a Changelog]: https://keepachangelog.com/en/1.1.0/
  [Semantic Versioning]: https://semver.org/spec/v2.0.0.html
    "Semantic Versioning 2.0.0"

## [v0.1.1] — 2026-09-17

The theme of this release is *Oh right, THAT.*

### ⚡ Improvements

*   Added the `archive` output, useful for a GitHub release in a subsequent
    step.

  [v0.1.0]: https://github.com/pgxn/postgres-action/compare/v0.1.0...v0.1.1

## [v0.1.0] — 2026-09-16

The theme of this release is *Decontainerize.*

### ⚡ Improvements

*   First release
*   Validates `META.json` before release
*   Uses `git archive` to build a release zip file
*   Uses `git archive-all` to include submodules in a release zip file

### 🏗️ Build Setup

*   Made it a GitHub Action!

### 📚 Documentation

*   Wrote a [README]

  [v0.1.0]: https://github.com/pgxn/postgres-action/compare/bffab76...v0.1.0
  [README]: README.md
