## Initial Setup with bun

### 1. Initialise Project with -
```sh
bun create hono app-name
```
I selected these settings for this template
<pre>
✔ Using target directory … ./
√ Which template do you want to use? bun
√ Directory not empty. Continue? Yes
√ Do you want to install project dependencies? Yes
√ Which package manager do you want to use? bun
√ Cloning the template
√ Installing project dependencies
🎉 Copied project files
</pre>

### 2. Building the server here in root folder only, so renamed `src` to `server`, also in `package.json`,
```json
  "scripts": {
    "dev": "bun run --hot server/index.ts"
  }
```

Copied `Suggested compilerOptions` from Bun website [Bun docs](https://bun.sh/docs/typescript#suggested-compileroptions) (features without seeing compiler warnings from TypeScript), and pasted in `tsconfig.json`, then add 'paths' to it-
```json
{
  "compilerOptions": {
    // Environment setup & latest features
    "lib": ["ESNext"],
    ...
    "noPropertyAccessFromIndexSignature": false,
    "paths": {
      "@/shared/*": ["./shared/*"],
      "@/*": ["./server/*"],
    }
  },
}
```

### 3. Add Prettier, create `prettier.config.js`, `.prettierignore`.

### 4. Add ESLint
```sh
bun create @eslint/config@latest
```
<pre>
√ What do you want to lint? · javascript
√ How would you like to use ESLint? · problems
√ What type of modules does your project use? · esm
√ Which framework does your project use? · none     // React/Vue/None
√ Does your project use TypeScript? · no / yes
√ Where does your code run? · browser   // Node
The config that you've selected requires the following dependencies:

eslint, @eslint/js, globals, typescript-eslint
√ Would you like to install them now? · No / Yes
√ Which package manager do you want to use? · bun   // npm, yarn, pnpm
</pre>

Then add these DevDependecies
```sh
bun add --dev @eslint/compat eslint-config-prettier eslint-plugin-drizzle
```
Edit `server\eslint.config.mjs` 
```js
import drizzlePluggin from "eslint-plugin-drizzle";
import eslintPrettierConfig from "eslint-config-prettier eslint-plugin-drizzle";
import { fixupPluginRules } from "@eslint/compat";

export default defineConfig([
  ...
  eslintPrettierConfig,
  {
    plugins: {
      drizzle: fixupPluginRules(drizzlePluggin)
    }
  }
]);
```
