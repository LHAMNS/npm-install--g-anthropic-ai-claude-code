# Dependencies and Runtime Environment

The package targets Node.js 18 or newer. The `package.json` declares no regular dependencies, relying instead on bundled code under `vendor/` and compiled artifacts such as `yoga.wasm`. For functionality like image processing, optional platform‑specific `@img/sharp-*` packages are listed as optional dependencies; npm will attempt to install the variant that matches the host environment but the package functions without them.

Development scripts are intentionally locked down. The `prepare` script aborts direct `npm publish` attempts unless a specific environment variable is set, guiding contributors to internal release tooling.

At runtime, the CLI spawns subprocesses via Node's `child_process` module and interacts with the filesystem using `fs` and `fs/promises`. The terminal interface adjusts to window size changes and sets the title using escape sequences. A Wasm build of the Yoga layout engine assists with rendering complex layouts.

Since the package is primarily distributed as compiled JavaScript, the source code is minified and accompanied by TypeScript declaration files for external use. The authors note in the headers that unminified source is not bundled, hinting at an internal build pipeline.

