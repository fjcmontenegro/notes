# Steps to configure a React project with Typescript, ESLint, and Prettier

TL;DR: if you are myself and just want to grab the commands, head over to [the short version](https://github.com/SplinterDev/notes/blob/main/ts-react-eslint-prettier-short.md)

## Create a React App with the Typescript template

```
npx create-react-app PROJECT_NAME --template typescript
```
OR
```
yarn create react-app PROJECT_NAME --template typescript
```

Move into the project folder so that you don't do like me and install a bunch of stuff in your root coding folder :)

```
cd PROJECT_NAME
```

## Add ESLint

```
npm i -D eslint
```
OR

```
yarn add -D eslint
```

ESLint will behave according to your coding preferences. Your preferences might be different than mine, so keep this in mind when replicating the next steps. Here are my preferences:

1. I want ESLint to **enforce a style**. This good on projects with more people so that everyone writes similar code.
2. We're using **React** and **Typescript**.
3. Instead of choosing a default style, I have my own:
   - I like the config file to be a **JSON** file
   - I use indentation of **2 spaces** (not tabs)
   - I like **single quotes** for strings (double quotes only if necessary and on JSX/HTML tags)
   - **unix** line endings (not windows), to avoid a few headaches
   - I **don't require semicolons** (to remind me of the good times I had with Python)

There are two ways to set this up:

1. Let ESLint figure out the configs by answering some questions
2. Just copy my config files (:

### Method 1: Let ESLint figure it out by using `ESLint --init`

```
npx eslint --init
```
OR
```
yarn eslint --init
```

For my style, the questions will have these answers

> How would you like to use ESLint? · enforce style  
> What type of modules does your project use? · js module (import/export)  
> Which framework does your project use? · react  
> Does your project use TypeScript? · Yes  
> Where does your code run? · browser  
> How would you like to define a style for your project? · ask questions  
> What format do you want your config file to be in? · JSON  
> What style of indentation do you use? · spaces  
> What quotes do you use for strings? · single  
> What line endings do you use? · unix  
> Do you require semicolons? · No 

This will install a bunch of stuff and myight take a while. This won't do everything, so we have to add some extra configuration.

#### Edit `.eslintrc.json`

In the next steps we're adding **Prettier** to the project, so we might as well config ESLint to be aware of this right now by adding some lines to `.eslintrc.json`.
Add this to `"extends"`:

```
"plugin:prettier/recommended",
"prettier"
```

Add this to `"plugins"`:

```
"react-hooks",
"prettier"
```

The `react-hooks` plugin is not required, but it will enforce the [rules of hooks](https://reactjs.org/docs/hooks-rules.html), which is super helpful.

Create a **settings** property to make sure ESLint will be smart when detecting React versions.

```
"settings": {
  "react": {
    "version": "detect"
  }
}
```

You can see the final result in my `.eslintrc.json` file below.

### Method 2: Copy my config file (:

This is my `.eslint.json`. Add it to the root of your project.

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

The `eslint --init` command also installs some extra packages that we haven't installed through method 2, so let's do that now:

```
npm install -D @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint eslint-plugin-react
```
OR
```
yarn add -D @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint eslint-plugin-react
```

## Prettier

Install Prettier and it's ESLint packages.

```
npm i -D prettier eslint-config-prettier eslint-plugin-prettier
```
OR
```
yarn add -D prettier eslint-config-prettier eslint-plugin-prettier
```

Create a `.prettierrc` file at the root of your project and add the following lines. Again, these are my preferences, and some of these rules will fix ESLint errors when I save the file.

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

That's it! If you run the project and get a ton of errors, that's a good thing! When the `create-react-app` command created that code, it wasn't aware of our ESLint rules, so naturally it contains errors. The problematic files are usually `src\App.tsx`, `src\index.tsx` and `src\reportWebVitals.ts`. Thanks to Prettier, simply opening the files and hitting save should fix most of the problems.

## BONUS: Add Sass and FontAwesome icons just for fun

```
npm i @fortawesome/fontawesome-svg-core @fortawesome/free-regular-svg-icons @fortawesome/free-solid-svg-icons @fortawesome/react-fontawesome sass
```
OR
```
yarn add @fortawesome/fontawesome-svg-core @fortawesome/free-regular-svg-icons @fortawesome/free-solid-svg-icons @fortawesome/react-fontawesome sass
```
