## 1. Create an empty repo

```
yarn init -y
```

## 2. Install `webpack` and `TS` stuff

```
yarn add -D typescript ts-loader webpack webpack-cli webpack-dev-server html-webpack-plugin @tsconfig/recommended
```

## 3. Create a `tsconfig.json` file

```json
{
  "compilerOptions": {
    "outDir": "/dist",
    "target": "ES5",
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "noFallthroughCasesInSwitch": true,
    "module": "CommonJS",
    "resolveJsonModule": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"],
  "extends": "@tsconfig/recommended/tsconfig.json"
}

```

4. Create a `webpack.config.js` file

```js
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  entry: './src/index.ts',
  mode: 'development',
  module: {
    rules: [
      {
        test: /\.tsx?$/,
        use: 'ts-loader',
        exclude: /node_modules/,
      },
    ],
  },
  resolve: {
    extensions: ['.tsx', '.ts', '.js'],
  },
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist'),
    clean: true,
  },
  plugins: [new HtmlWebpackPlugin()],

  devServer: {
    contentBase: path.resolve(__dirname, 'dist'),
    compress: true,
    port: 9000,
  },
}
```

5. Add scripts to `package.json`
```json
"scripts": {
    "build": "webpack",
    "serve": "webpack serve"
  }
```

6. Create `./dist/index.html`

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script src="./bundle.js" defer></script>
  </head>
  <body></body>
</html>
```

