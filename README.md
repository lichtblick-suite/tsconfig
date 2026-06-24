# @lichtblick/tsconfig

[![npm version](https://img.shields.io/npm/v/@lichtblick/tsconfig.svg?style=flat)](https://www.npmjs.com/package/@lichtblick/tsconfig)

Base tsconfig for lichtblick projects.

To use, run `npm i --save-dev @lichtblick/tsconfig`, then extend your `tsconfig.json` like so:

```json
{
  "extends": "@lichtblick/tsconfig/base",
  "include": ["./src/**/*"],
  "compilerOptions": {
    "rootDir": "./src",
    "outDir": "./dist"
  }
}
```

## Releasing

Two GitHub Actions workflows are involved:

- **Auto Bump Version** (`.github/workflows/bump-version.yml`) runs on every push
  to `main`. It bumps the `patch` version in `package.json` and commits the change
  back to `main`. So merging a PR keeps the version moving automatically — but it
  does **not** publish to npm.
- **Publish to NPM** (`.github/workflows/release.yml`) runs only when a GitHub
  **Release** is published. That event is what triggers `npm publish`.

### To publish a release

```sh
# 1. update local main (includes the auto-bumped version)
git checkout main && git pull

# 2. read the current version to tag against
tag="v$(node -p "require('./package.json').version")" && echo "$tag"

# 3. create + publish a GitHub Release for that version
git tag "$tag" && git push origin "$tag"
gh release create "$tag" --generate-notes
```

Publishing the Release (step 3, via `gh` or the GitHub UI) emits the
`release: published` event that runs the publish workflow.

> **Note:** the auto-bump only ever does a `patch` bump. For a breaking change,
> manually bump the `major` (or `minor`) in `package.json` before releasing so the
> published version reflects that correctly.

## License

[MIT License](/LICENSE.md)
