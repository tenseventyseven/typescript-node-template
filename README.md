# typescript-node-template
A Typescript NodeJS project template with ESLint/Prettier/Husky.

## Git

Initialise `main` branch:

```
git init --initial-branch=main
```

`.gitignore` contents. Used `gitignore.io` to generate a NodeJS template (https://www.toptal.com/developers/gitignore/api/node) then appended the following:

```
# Ignore all user IDE settings
.idea/
.vscode/
```

## NPM

Initialise `npm` project:

```
npm init -y
```

## Typescript

Initialise `typescript` project:

```
tsc --init
npm install --save-dev typescript @types/node tsx
```

Update `tsconfig.json`:

```
...
{
  "compilerOptions": {
    ...
    "outDir": "dist"
    ...
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
...
```

Put Typescript files in `src`:

```
mkdir src

# Just to get started:
echo 'console.log("Hello world!");' > src/index.ts
```

## ESLint & Prettier

Install:

```
# ESLint:
npm install --save-dev eslint @typescript-eslint/eslint-plugin @typescript-eslint/parser

# Prettier:
npm install --save-dev prettier eslint-config-prettier eslint-plugin-prettier
```

`.eslintrc.cjs` contents:

```
{
  "root": true,
  "parser": "@typescript-eslint/parser",
  "plugins": ["@typescript-eslint", "prettier"],
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "prettier"
  ],
  "rules": {
    "prettier/prettier": "error"
  },
  "env": {
    "node": true
  }
}
```

`.prettierrc` contents:

```
{}
```

`.prettierignore` contents:

```
dist
```

Add these scripts to `package.json`:

```
{
  ...
  "scripts": {
    "prepare": "husky install",
    "build": "tsc --build",
    "clean": "tsc --build --clean",
    "dev": "tsx src/index.ts",
    "lint": "eslint . --ext .ts",
    "format": "prettier --config .prettierrc 'src/**/*.ts' --write",
    ...
  },
  ...
}
```

## Husky & lint-staged

Setup `lint-staged`:

```
# Install
npm install --save-dev lint-staged

# Add config to package.json
{
  ...
  "lint-staged": {
    "src/**/*.ts": [
      "npm run lint",
      "npm run format"
    ]
  },
  ...
}
```

Setup `husky`:

```
# Install
npm install --save-dev husky
npm run prepare

# Add lint-staged hook
npx husky add .husky/pre-commit "npx lint-staged"
```

Once this is done, `Husky` will always "bark" at you on commit if there are linting and/or formatting errors.
