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

## License

[MIT License](/LICENSE.md)
