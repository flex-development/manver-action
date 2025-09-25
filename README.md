# manver-action

[![github release](https://img.shields.io/github/v/release/flex-development/manver-action.svg?include_prereleases\&sort=semver)](https://github.com/flex-development/manver-action/releases/latest)
[![test](https://github.com/flex-development/manver-action/actions/workflows/test.yml/badge.svg)](https://github.com/flex-development/manver-action/actions/workflows/test.yml)
[![module type: esm](https://img.shields.io/badge/module%20type-esm-brightgreen)](https://github.com/voxpelli/badges-cjs-esm)
[![license](https://img.shields.io/github/license/flex-development/manver-action.svg)](LICENSE.md)
[![conventional commits](https://img.shields.io/badge/-conventional%20commits-fe5196?logo=conventional-commits\&logoColor=ffffff)](https://conventionalcommits.org)
[![yarn](https://img.shields.io/badge/-yarn-2c8ebb?style=flat\&logo=yarn\&logoColor=ffffff)](https://yarnpkg.com)

Extract version metadata

## Contents

- [What is this?](#what-is-this)
- [Use](#use)
- [Inputs](#inputs)
  - [`branch`](#branch)
  - [`build`](#build)
  - [`manifest`](#manifest)
  - [`property`](#property)
  - [`release-branch-prefix`](#release-branch-prefix)
- [Outputs](#outputs)
  - [`build`](#build-1)
  - [`manifest`](#manifest-1)
- [Related](#related)
- [Contribute](#contribute)

## What is this?

This is a simple action for extracting version metadata.

## Use

```yaml
---
name: ci
on:
  - pull_request
  - push
  - workflow_dispatch
jobs:
  preflight:
    runs-on: ubuntu-latest
    outputs:
      version: ${{ steps.version.outputs.build }}
    steps:
      - id: checkout
        name: Checkout ${{ github.head_ref || github.ref_name }}
        uses: actions/checkout@v5.0.0
        with:
          persist-credentials: false
          ref: ${{ github.head_ref || github.ref }}
      - id: version
        name: Extract version metadata
        uses: flex-development/manver-action@1.0.0
```

## Inputs

### `branch`

> **default**: `${{ github.head_ref || github.ref_name }}`

The name of the branch to check when generating a build version.

### `build`

> **default**: `${{ github.event.pull_request.head.sha || github.sha }}`

Build metadata.

### `manifest`

> **default**: `package.json`

The path to the manifest file.\
Manifest files are expected to be compatible with [`jq`][jq].

### `property`

> **default**: `.version`

Version property path in [`manifest`](#manifest) file.

### `release-branch-prefix`

> **default**: `release/`

The prefix used to mark release branches.\
Build versions generated from release branches will not have [metadata](#build) attached.

## Outputs

### `build`

Build version (generated from [`outputs.manifest`](#manifest-1) and [`inputs.build`](#build)).

### `manifest`

The value of [`property`](#property) in the [`manifest`](#manifest) file.

## Related

- [`flex-development/gh-release-url-action`][gh-release-url-action] — create a url for a github release
- [`flex-development/ghr-url-action`][ghr-url-action] — create a url for a github registry
- [`flex-development/jq-action`][jq-action] — execute json queries with [`jq`][jq]
- [`flex-development/npm-url-action`][npm-url-action] — create a url for the npm registry

## Contribute

See [`CONTRIBUTING.md`](CONTRIBUTING.md).

This project has a [code of conduct](./CODE_OF_CONDUCT.md). By interacting with this repository, organization, or
community you agree to abide by its terms.

[gh-release-url-action]: https://github.com/flex-development/gh-release-url-action

[ghr-url-action]: https://github.com/flex-development/ghr-url-action

[jq-action]: https://github.com/flex-development/jq-action

[jq]: https://jqlang.org

[npm-url-action]: https://github.com/flex-development/npm-url-action
