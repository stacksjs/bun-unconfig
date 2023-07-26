# bun-unconfig

[![NPM version](https://img.shields.io/npm/v/bun-unconfig?color=a1b858&label=)](https://www.npmjs.com/package/bun-unconfig)

Forked from [`unconfig`](https://github.com/antfu/unconfig)

###### Changes in this fork

- Adds Bun compatibility

## Get Started

```bash
npm i bun-unconfig
```

`unconfig` supports loading `ts`, `mjs`, `js`, `json` by default.

```ts
import { loadConfig } from 'unconfig'

const { config, sources } = await loadConfig({
  sources: [
    // load from `my.config.xx`
    {
      files: 'my.config',
      // default extensions
      extensions: ['ts', 'mts', 'cts', 'js', 'mjs', 'cjs', 'json', ''],
    },
    // load `my` field in `package.json` if no above config files found
    {
      files: 'package.json',
      extensions: [],
      rewrite(config) {
        return config?.my
      },
    },
    // load inline config from `vite.config`
    {
      files: 'vite.config',
      async rewrite(config) {
        const resolved = await (typeof config === 'function' ? config() : config)
        return resolved?.my
      },
    },
    // ...
  ],
  // if false, the only the first matched will be loaded
  // if true, all matched will be loaded and deep merged
  merge: false,
})
```
