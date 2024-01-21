# Next.js + TypeScript + TailwindCSS + Storybook

## Setup Process
1. Initialize nextjs project

```bash
npx create-next-app@latest
```

2. Add Storybook

```bash
npx storybook@latest init
```

3. Add Prettier

```bash
npm install -D prettier eslint-config-prettier
touch .prettierrc.json .prettierignore
```
- `.eslintrc.json`

```json
{
  "extends": [
    "next/core-web-vitals",
    "plugin:storybook/recommended",
    "prettier" //<- add
  ]
}
```

- `.prettierrc.json`

```json
{
  "semi": false,
  "singleQuote": true,
  "printWidth": 90,
  "tabWidth": 2,
  "trailingComma": "all",
  "jsxSingleQuote": true
}
```

- `.prettierignore`

```
# Ignore artifacts:
package.json
package-lock.json
build
coverage
yarn.lock

# dotfile
.env*

# markdown
*.md

# next.js
/.next/
/out/

# production
/build

# yarn
/.yarn/
```

- `.vscode/settings.json`

```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode"
}
```

- `.vscode/extentions.json`

```json
{
  "recommendations": [
    "esbenp.prettier-vscode" //<- add
  ]
}
```

- `package.json`

```json
{
    "scripts":{
        //...
        "format": "prettier --write ." //<- add
        //...
    }
}
```

4. configure eslint

```bash
npm install -D eslint-plugin-import @typescript-eslint/parser @typescript-eslint/eslint-plugin
touch .eslintignore src/stories/eslintrc.json
```

- .eslintignore

```
# config
.eslintrc.js
prettier.config.js
next.config.js
tailwind.config.js
tsconfig.json
postcss.config.js

# build dir
build/
bin/
obj/
out/
.next/
```

- .eslintrc.json

```json
{
  "extends": [
    "eslint:recommended", //<-add
    "next/core-web-vitals",
    "plugin:@typescript-eslint/recommended", //<-add
    "plugin:@typescript-eslint/recommended-requiring-type-checking", //<-add
    "plugin:storybook/recommended",
    "prettier"
  ],
  "parser": "@typescript-eslint/parser", //<-add
  "parserOptions": {
    "project": "./tsconfig.json" //<-add
  },
  "plugins": ["@typescript-eslint"], //<-add
  "root": true,
  //↓ add "rules": {...}
  "rules": {
    "import/order": [
      "error",
      {
        "groups": ["builtin", "external", "parent", "sibling", "index", "object", "type"],
        "pathGroups": [
          {
            "pattern": "{react,react-dom/**,react-router-dom}",
            "group": "builtin",
            "position": "before"
          },
          {
            "pattern": "@src/**",
            "group": "parent",
            "position": "before"
          }
        ],
        "pathGroupsExcludedImportTypes": ["builtin"],
        "alphabetize": {
          "order": "asc"
        },
        "newlines-between": "always"
      }
    ],
    "@typescript-eslint/consistent-type-imports": ["error", { "prefer": "type-imports" }]
  }
}
```

- `src/stories/eslintrc.json`

```json
{
  "rules": {
    "@typescript-eslint/no-unsafe-call": "off"
  }
}
```

- `.vscode/extentions.json`

```json
{
  "recommendations": [
    "esbenp.prettier-vscode", 
    "dbaeumer.vscode-eslint" //<- add
  ]
}

```

- `.vscode/settings.json`

```json
{
  //...
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit" //<-add
  },
  //...
}
```
- `package.json`

```json
{
  "scripts":{
    //...
    "lint:fix": "eslint src --ext .js,jsx,.ts,.tsx --fix", //<- add
    //...
  }
}
```
5. add prettier plugin tailwindcss

```bash
npm install -D prettier-plugin-tailwindcss
```

- `.prettierrc.json`

```json
{
  "plugins": ["prettier-plugin-tailwindcss"], //<-add
 //...
}
```

- `.vscode/extentions.json`

```json
{
  "recommendations": [
    "bradlc.vscode-tailwindcss" //<- add
    //...
  ]
}
```

- `.vscode/settings.json`

```json
{
  //...
  //↓ add
  "editor.quickSuggestions": {
    "strings": true
  }
}
```

6. Additional npm

```bash
npm install -D classnames
```

7. husky setup

- Refer https://github.com/hikarucraft/nextjs-template-css-modules-storybook


## Refs.
- https://zenn.dev/resistance_gowy/articles/91b4f62b9f48ec
- https://zenn.dev/rena_h/scraps/fd330154d02f76


This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/basic-features/font-optimization) to automatically optimize and load Inter, a custom Google Font.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js/) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.
