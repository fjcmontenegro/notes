# tsconfig

The important part is that you're able to use `tsc` and have it create the compiled code under `/dist`

```
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "declaration": true,
    "outDir": "./dist",
    "strict": true
  },
  "include": ["src"],
  "exclude": ["node_modules", "**/__tests__/*"]
}
```

# Publish

After perfecting the code, move to a different branch and leave only these files:
- `dist/`
- `package.json`
- `README.md` and `LICENSE` (if you want)

We don't need more than this.

# Add to project

Use this format to install the package to a different project:
```
yarn add <git remote url>#<branch/commit/tag>
```
