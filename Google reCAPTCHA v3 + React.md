# Steps:

## 1. [Register new site](https://www.google.com/recaptcha/admin/create) and grab keys
Add 'localhost' to domains for local testing

## 2.  In the frontend, import Google's recaptcha script.

This can be done:
1. Statically: add `<script>` to html
2. Dinamically: Add script from React component:

```tsx
  useEffect(() => {
    const loadScriptByURL = (id: string, url: string, callback: () => void) => {
      const isScriptExist = document.getElementById(id);

      if (!isScriptExist) {
        var script = document.createElement('script');
        script.type = 'text/javascript';
        script.src = url;
        script.id = id;
        script.onload = function () {
          if (callback) callback();
        };
        document.body.appendChild(script);
      }

      if (isScriptExist && callback) callback();
    };

    // load the script by passing the URL
    loadScriptByURL(
      'recaptcha-key',
      `https://www.google.com/recaptcha/api.js?render=${SITE_KEY}`,
      function () {
        console.log('Script loaded!');
      }
    );
  }, []);
```
