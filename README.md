## vite-react-typescript-mui5
How to setup  
* Vite
* React
* Typescript 
* MUI 5 
* vitest
* jest matchers
* json-server 

### setting up vite

```
npm create vite@latest
```
When prompted, type in a new project name eg.: `my-project`
Select REACT and then TYPESCRIPT

```
npm install @mui/material @emotion/react @emotion/styled
```
Start the project ...
```
npm run dev
```
...and open it in a browser.


Create a new repo at github.com, `my-project`

```
cd my-project
git init
git add .
git commit -m "Init"
git branch -M main
git remote add origin https://github.com/<yourusername>/my-project.git
```
### setting up eslint

```
npm install eslint prettier @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-config-prettier eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react
```

in `.eslintrc.cjs`

```
module.exports = {
  env: { browser: true, es2020: true, node: true },
  extends: [
    'eslint:recommended',
    'plugin:react/recommended',
    'plugin:import/recommended',
    'plugin:jsx-a11y/recommended',
    'plugin:@typescript-eslint/recommended',
    'plugin:react-hooks/recommended',
    'eslint-config-prettier',
  ],
  settings: {
    react: {
      version: 'detect',
    },
    'import/resolver': {
      node: {
        paths: ['src'],
        extensions: ['.js', '.jsx', '.ts', '.tsx'],
      },
    },
  },
  parser: '@typescript-eslint/parser',
  parserOptions: { ecmaVersion: 'latest', sourceType: 'module' },
  plugins: ['react-refresh'],
  rules: {
    'react-refresh/only-export-components': 'warn',
    'react/react-in-jsx-scope': 'off',
    'react/jsx-uses-react': 'off',
  },
};
```

in `.eslintignore`

```
node_modules/
dist/
.prettierrc.cjs
.eslintrc.cjs
env.d.ts
```
### setting up prettier

in `.prettierrc.cjs`
```
module.exports = {
  "trailingComma": "all",
  "tabWidth": 2,
  "semi": true,
  "singleQuote": true,
  "printWidth": 120,
  "bracketSpacing": true
}
```

### Setting up vitest

```
npm install vitest --save-dev
```

add `"test": "vitest",` to package.json (undr scripts"

```
npm install jsdom --save-dev
npm install @testing-library/react @testing-library/jest-dom --save-dev
```
create a file `tests/setup.js` and add the following:

```
import { expect, afterEach } from 'vitest';
import { cleanup } from '@testing-library/react';
import matchers from '@testing-library/jest-dom/matchers';

expect.extend(matchers);

afterEach(() => {
  cleanup();
});
```

in `vite.config.ts` add 

```
export default defineConfig({
  plugins: [react()],
  test: {
    globals: true,
    environment: 'jsdom',
    setupFiles: './tests/setup.js',
  },
});
```
### Setting up json-server

```
npm install json-server
```

create a file `data/db.json` with the following content:

```
{
  "items": []
}
```

add the following script to `package.json`
```
"server": "json-server -p 3001 --watch data/db.json",
```

start the server bu running
```
npm run server
```
