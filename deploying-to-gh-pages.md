# Regular React App
## Install GH Pages

`npm install gh-pages --save-dev`

## Add properties to `package.json`

```
"homepage": "http://splinterdev.github.io/{repo-name}",
"scripts": {
  ...
  "predeploy": "npm run build",
  "deploy": "gh-pages -d build"
}
```

## Custom domain

Add these registries:

```
Type      Full name       Value
A         @               185.199.108.153
A         @               185.199.109.153
A         @               185.199.110.153
A         @               185.199.111.153
CNAME	    www	            splinterdev.github.io
```

[docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages) and [docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)

# NextJS App

Next requires a server, so to host it with GH Pages you need to **statically export it with `next export`**. This will disable API routes, but will generate the dist files we want.  
We also want a `.nojekyll` (to stop GH from creating a jekyll site) and a `CNAME` file (for custom domains) to be added to the root of the exported project. All this is covered by the scripts:

```
"scripts": {
  "dev": "next dev",
  "export": "next build && next export",
  "clean": "rm -rf node_modules/.cache && rimraf out",
  "predeploy": "npm run clean && npm run export && npm run inject",
  "inject": "touch out/.nojekyll && touch out/CNAME && echo \"fabriciojcmontenegro.com\" >> out/CNAME",
  "deploy": "gh-pages -d out -t true"
}
```

There's a useful example [here](https://github.com/thierryc/Next-gh-page-example) by one NextJS developer.
