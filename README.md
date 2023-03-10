# Stylify Colors

Get Tailwind Colors in your Stylify Project

## Install

```bash
pnpm i stylify-colors
```

## Configuration

```diff
import { defineConfig } from "vite";
import { svelte } from "@sveltejs/vite-plugin-svelte";
import legacy from "@vitejs/plugin-legacy";
import pages from "vite-plugin-pages-svelte";
import { stylifyVite } from '@stylify/unplugin';
+ import colors from "stylify-colors"

const stylifyPlugin = (mangle) => (stylifyVite({
    bundles: [{
        outputFile: './src/stylify.css',
        files: ['./src/**/*.svelte'],
    }],
    compiler: {
      mangleSelectors: mangle,
+      variables: {
+        ...colors
+      }
    }
}));

let plugins = [
  svelte(),
  pages(),
];

// https://vitejs.dev/config/
export default defineConfig(({ mode }) => {
  if (mode == "android") {
    return {
      plugins: [legacy(), ...plugins, stylifyPlugin(false)],
    };
  } else if (mode == "online") {
    return {
      plugins: [...plugins, stylifyPlugin(true)],
    };
  } else {
    return {
      plugins: [...plugins, stylifyPlugin(false)],
    };
  }
});
```

## Usage

```html
<!--
stylify-customSelectors
p: `padding:10px`
/stylify-customSelectors
 -->

<p class="background:$green-500">One</p>
<p class="background:$green-400">Two</p>
<p class="background:$green-300">Three</p>
<p class="background:$green-200">Four</p>
<p class="background:$green-100">Five</p>
```

[Join Community](https://zenzen.web.id/komunitas)
