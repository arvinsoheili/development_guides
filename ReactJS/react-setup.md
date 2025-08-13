# how to make a react project with tailwind, shadcn and motion
setup react project:
```npm
npm create vite@latest
```
- choose your framework and language

### install tailwind
install tailwind with vite
```npm
npm i tailwindcss @tailwindcss/vite
```
after that add following to vite.config.ts/js
```ts
import tailwindcss from '@tailwindcss/vite'
```
add following to plugins array:
```
tailwindcss()
```
navigate `app.css` and remove default generated styles. import tailwind to app.css:
```css
@import 'tailwindcss'
```
### install shadcn
#### Edit tsconfig.json file
The current version of Vite splits TypeScript configuration into three files, two of which need to be edited. Add the `baseUrl` and `paths` properties to the `compilerOptions` section of the `tsconfig.json` and `tsconfig.app.json` files:
```json
{
  "files": [],
  "references": [
    {
      "path": "./tsconfig.app.json"
    },
    {
      "path": "./tsconfig.node.json"
    }
  ],
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```
#### Edit tsconfig.app.json file
Add the following code to the `tsconfig.app.json` file to resolve paths, for your IDE:
```json
{
  "compilerOptions": {
    // ...
    "baseUrl": ".",
    "paths": {
      "@/*": [
        "./src/*"
      ]
    }
    // ...
  }
}
```
#### Update vite.config.ts
Add the following code to the vite.config.ts so your app can resolve paths without error:
```ts
import path from "path"
import tailwindcss from "@tailwindcss/vite"

// https://vite.dev/config/
export default defineConfig({
  plugins: [react(), tailwindcss()], <---
  resolve: { 
    alias: { 
      "@": path.resolve(__dirname, "./src"), 
    }, <---
  },
})
```

#### Run the CLI
Run the shadcn init command to setup your project:
```npm
npx shadcn@latest init
```
### install motion
```npm
npm install motion
```
Features can now be imported via "motion/react":
```
import { motion } from "motion/react"
```
