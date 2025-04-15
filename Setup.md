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
