```
yarn create react-app PROJECT_NAME --template typescript
cd PROJECT_NAME
```
```
yarn add -D eslint @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint eslint-plugin-react prettier eslint-config-prettier eslint-plugin-prettier
```

## `.eslint.json`

```json
{
  "env": {
    "browser": true,
    "es2021": true
  },
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:prettier/recommended",
    "prettier"
  ],
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaFeatures": {
      "jsx": true
    },
    "ecmaVersion": 12,
    "sourceType": "module"
  },
  "plugins": ["react", "@typescript-eslint", "react-hooks", "prettier"],
  "rules": {
    "prettier/prettier": "error",
    "indent": ["error", 2],
    "linebreak-style": ["error", "unix"],
    "quotes": ["error", "single", { "avoidEscape": true }],
    "semi": ["error", "never"]
  },
  "settings": {
    "react": {
      "version": "detect"
    }
  }
}
```

## `.prettierrc`

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

## Sass + Font Awesome
```
yarn add @fortawesome/fontawesome-svg-core @fortawesome/free-regular-svg-icons @fortawesome/free-solid-svg-icons @fortawesome/react-fontawesome sass
```
