# Steps to configure a React project with Typescript, ESLint, and Prettier

## React + Typescript

With Typescript template

```
npx create-react-app PROJECT_NAME --template typescript
```

## ESLint

Install and init:

```
npm i -D eslint
npx eslint --init
```

Open `.eslinrc.json` and add to `"extends"`

```
"prettier/@typescript-eslint",
"plugin:prettier/recommended"
```

Add to `"plugins"`

```
"react-hooks",
"prettier"
```

Replace `"rules"` and add `"settings"`:

```
"rules": {
  "prettier/prettier": "error",
  "indent": [
    "error",
    2
  ],
  "linebreak-style": [
    "error",
    "unix"
  ],
  "quotes": [
    "error",
    "single",
    { "avoidEscape": true }
  ],
  "semi": [
    "error",
    "never"
  ]
},
"settings": {
  "react": {
    "version": "detect"
  }
}
```

## Prettier

Install

```
npm i -D prettier eslint-config-prettier eslint-plugin-prettier
```

.Create a `prettierrc` and add these:

```
{
  "printWidth": 80,
  "arrowParens": "always",
  "semi": false,
  "tabWidth": 2,
  "singleQuote": true,
  "trailingComma": "all"
}
```
