# Install GH Pages

`npm install gh-pages --save-dev`

# Add properties to `package.json`

```
"homepage": "http://splinterdev.github.io/{repo-name}",
"scripts": {
  ...
  "predeploy": "npm run build",
  "deploy": "gh-pages -d build"
}
```

# Custom domain

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
