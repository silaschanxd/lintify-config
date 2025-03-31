# @shinlms404/lintify-config

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An atomic tool that manages both `eslint` and `prettier` configurations using a single configuration file.

- Atomic configuration files that can be freely combined.
- Supports multiple file formats, including presets for `ts`, `vue`, `react`, `css`, `md`, `tsx`, and more.
- Supports enhanced personal customization settings.

> [!NOTE]
> Why did I create this project? Initially, I followed the configuration from [antfu/eslint-config](https://github.com/antfu/eslint-config), but I found that it didn't support the configurations I wanted. And inspired by unocss, I decided to create this project.

## Usage

### Install

I prefer using `bun`, but you can also use `pnpm` or `yarn`.

```bash
bun add -D @shinlms404/lintify-config eslint prettier
```

Create a configuration file `lintify.config.ts` in the root directory of your project.

```ts
// lintify.config.ts
import { defineLintifyConfig } from '@shinlms404/lintify-config'
import { presetDefault } from '@shinlms404/lintify-config/presets'

export default defineLintifyConfig({
  presets: [presetDefault()],
})
```

You can also combine configurations in an atomic way, for example:

```ts
import { defineLintifyConfig } from '@shinlms404/lintify-config'
import { presetVue, presetTypeScript } from '@shinlms404/lintify-config/presets'

export default defineLintifyConfig({
  presets: [
    presetVue(), 
    presetTypeScript({
      eslint: {
        rules: {
          'no-await-in-loop': 'error',
          // other rules
        },
        ignores: ['**/node_modules/**'],
      },
      prettier: {
        printWidth: 120,
        // other prettier options
      },
    }),
  ],
})
```

Check out [`presets`](./presets/README.md) to learn more about preset configurations.

Then you need to create `eslint.config.ts` and `prettier.config.ts` files.

```ts
// eslint.config.ts
import { eslintConfig } from './lintify.config'

export default eslintConfig

// prettier.config.ts
import { prettierConfig } from './lintify.config'

export default prettierConfig
```

> [!IMPORTANT]
> If you cannot use `eslint.config.ts`, please check [typescript-configuration-files](https://eslint.org/docs/latest/use/configure/configuration-files#typescript-configuration-files)

Then you need to add the following configuration to your package.json:

```json
{
  "scripts": {
    "lint": "eslint .",
    "lint:fix": "eslint --fix .",
    "format": "prettier --write .",
  }
}
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Author

- **Charlie Chan**
  - Email: hi@shinlms404.top
  - GitHub: [shinlms404](https://github.com/shinlms404)

