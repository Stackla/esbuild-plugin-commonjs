## @hyrious/esbuild-plugin-commonjs

The [@rollup/plugin-commonjs](https://github.com/rollup/plugins/blob/master/packages/commonjs) as esbuild plugin.

## Install

```bash
npm add -D @hyrious/esbuild-plugin-commonjs
```

**Note:**

- Requires esbuild &ge; 0.14.8 to use the new `resolve()` api.
- `@rollup/plugin-commonjs` is a dependency, it's peer dependency `rollup` may
  let your package manager show warnings, but we actually not depend on `rollup`.
  You can copy the `.pnpmfile.cjs` in this repo to hide the warnings if you are
  using pnpm, or live with them.

## Usage

<!-- prettier-ignore -->
```js
const { commonjs } = require("@hyrious/esbuild-plugin-commonjs");

require("esbuild").build({
  entryPoints: ["lib.js"],
  bundle: true,
  format: "esm",
  external: ["react"],
  outfile: "out.js",
  plugins: [commonjs()],
}).catch(() => process.exit(1));
```

## Options

```js
commonjs({ filter: /\.c?js$/, cache: true, options: {} });
```

**filter** (default: `/\.c?js$/`)

A RegExp passed to [`onLoad()`](https://esbuild.github.io/plugins/#on-load) to
match commonjs modules, it is recommended to set a custom filter to skip files
for better performance.

**cache** (default: `true`)

A boolean or RegExp or function to turn on cache for some files that are likely
won't change. When it is `true`, it will be applied to files in `node_modules`.

**options**

An object passed to `@rollup/plugin-commonjs`, note that not all of them are
supported, for example this plugin will ignore the `include/exclude` fields.

## License

MIT @ [hyrious](https://github.com/hyrious)
