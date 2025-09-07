# Package Boilerplate (TypeScript)

This repository is a minimalist template to quickly create an NPM package in TypeScript. It provides a ready-to-use setup to:

- Build with tsup (ESM and CJS formats) and generate type declarations.
- Export the package correctly via the `exports` and `types` fields.
- Organize the source code in `source/` with `utilities/` and `types/` subfolders.
- Target Node.js 22+ with a strict-yet-pragmatic TypeScript configuration.

## Table of Contents
- Goal
- Requirements
- Installation
- Available scripts
- Project structure
- TypeScript and build configuration
- Usage example
- Publish to npm
- Quick customization

## Goal
Provide a simple foundation to start a TypeScript package, with the right outputs (`.mjs`, `.cjs`, `.d.ts`) and an `exports` configuration that works seamlessly with both ESM and CommonJS.

## Requirements
- Node.js 22 or higher
- pnpm (recommended) or npm/yarn

## Installation
Clone the repository, then install dependencies:

```bash
pnpm install
# or
npm install
```

## Available scripts
- `pnpm dev`: start continuous compilation with tsup in watch mode.
- `pnpm build`: produce the build output in `build/` (ESM + CJS + types).

## Project structure
```
source/
  index.ts          # Entry point: re-exports types and utilities
  types/
    index.ts
    hello.ts        # Sample interface
  utilities/
    index.ts
    hello.ts        # Sample utility function (sayHello)
```
The build output is generated in `build/` (ignored by Git). The package exports:
- ESM via `build/index.mjs`
- CJS via `build/index.cjs`
- Types via `build/index.d.ts`

## TypeScript and build configuration
- `tsconfig.json`
  - `rootDir: ./source` for a clear code organization.
  - `strict: true`, `noUnusedLocals/Parameters: true` for quality.
  - `module` and `target` set to `ESNext`; tsup handles the final output.
- `tsup.config.ts`
  - Entry: `source/index.ts`.
  - Formats: `esm` and `cjs`.
  - `dts: true` to generate types.
  - Outputs: `.mjs` (ESM) and `.cjs` (CJS) mapped via `outExtension`.

`package.json` is already configured with consistent `main`, `module`, `types`, and `exports` fields.

## Usage example
After building, the package exposes the exports from `source/index.ts`:

- ESM
```ts
import { sayHello } from "@protorians/package-boilerplate";

console.log(sayHello("World")); // "Hello World"
```

- CommonJS
```js
const { sayHello } = require("@protorians/package-boilerplate");

console.log(sayHello("World")); // "Hello World"
```

## Publish to npm
1. Update `name`, `description`, `keywords`, `author`, `license` in `package.json`.
2. Build:
   ```bash
   pnpm build
   ```
3. Publish:
   ```bash
   pnpm publish --access public
   # or: npm publish --access public
   ```

Make sure you are logged in (`pnpm login` or `npm login`) and that the version in `package.json` has been bumped.

## Quick customization
- Rename the package in `package.json` (`name` field).
- Add/remove exports in `source/index.ts`.
- Add your utilities/types inside `source/utilities` and `source/types`.
- Adjust the Node target or enable options (sourcemap/minify) in `tsup.config.ts`.

---

Happy hacking!
