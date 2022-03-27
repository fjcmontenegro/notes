# Flow

1. On submit, send action to Google and expect a token as response
2. Send the token to back end (along with form data) for validation
3. On the back end, send secret key and token token to Google to get results
4. Handle results according to score where 1.0 = human; and 0.0 = bot

# Steps:

1. [Register new site](https://www.google.com/recaptcha/admin/create) and grab keys
    1. Add 'localhost' to domains for local testing
2.  In the frontend, import Google's recaptcha script. This can be done:
    1. Statically: add `<script>` to html
    2. Dinamically: add script from React component on mount

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

3. On submit, send action to Google to receive token back:
```tsx
const handleOnClick: React.MouseEventHandler<HTMLButtonElement> = (e) => {
  e.preventDefault();
  setLoading(true);
  window.grecaptcha.ready(() => {
    window.grecaptcha
      .execute(SITE_KEY, { action: 'submit' })
      .then((token: string) => {
        console.log(token);

        submitData(token);
      });
  });
};
```

4. If got token alright, send form data to back end (along with token for verification):
```tsx
const submitData = (token: string) => {
  // call a backend API to verify reCAPTCHA response
  fetch('http://localhost:3000/api/verify', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({
      myData: 'data',
      'g-recaptcha-response': token,
    }),
  })
    .then((res) => res.json())
    .then((res) => {
      setLoading(false);
      setResponse(res);
    });
};
```
5. On the back end, send token to Google to get score:  
(NextJS example)
```ts
export default async function verify(
  req: NextApiRequest,
  res: NextApiResponse<string>
) {
  console.log('req.body:', req.body);

  var VERIFY_URL = `https://www.google.com/recaptcha/api/siteverify?secret=${SECRET_KEY}&response=${req.body['g-recaptcha-response']}`;

  axios.post(VERIFY_URL).then((response) => {
    console.log('response:', response.status, response.data);

    res.status(200).json(response.data);
  });
}
```
6. That's it. Handle score as desired and let front end know about the result.

# Example

## Front end
```tsx
const Test = (props: Props) => {
  const [loading, setLoading] = useState(false);
  const [response, setResponse] = useState(null);

  const handleOnClick: React.MouseEventHandler<HTMLButtonElement> = (e) => {
    e.preventDefault();
    setLoading(true);
    window.grecaptcha.ready(() => {
      window.grecaptcha
        .execute(SITE_KEY, { action: 'submit' })
        .then((token: string) => {
          console.log(token);

          submitData(token);
        });
    });
  };

const submitData = (token: string) => {
  // call a backend API to verify reCAPTCHA response
  fetch('http://localhost:3000/api/verify', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({
      myData: 'data',
      'g-recaptcha-response': token,
    }),
  })
    .then((res) => res.json())
    .then((res) => {
      setLoading(false);
      setResponse(res);
    });
};

  useEffect(() => {
    const loadScriptByURL = (id: string, url: string, callback: () => void) => {
      const scriptExists = !!document.getElementById(id);

      if (!scriptExists) {
        // create script element
        const script = document.createElement('script');
        script.type = 'text/javascript';
        script.src = url;
        script.id = id;
        // set a callback function for when it's done
        script.onload = function () {
          if (callback) callback();
        };
        // add element to dom
        document.body.appendChild(script);
      }

      // if script exists, just run callback
      if (scriptExists && callback) callback();
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

  return (
    <div>
      <h3>reCAPTCHA v3 in React</h3>
      <button onClick={handleOnClick} disabled={loading}>
        {loading ? 'Submitting...' : 'Submit'}
      </button>
      {response && <pre>{JSON.stringify(response, undefined, 2)}</pre>}
    </div>
  );
};
```

## Back end (NextJS example)
```ts
export default async function verify(
  req: NextApiRequest,
  res: NextApiResponse<string>
) {
  console.log('req.body:', req.body);

  var VERIFY_URL = `https://www.google.com/recaptcha/api/siteverify?secret=${SECRET_KEY}&response=${req.body['g-recaptcha-response']}`;

  axios.post(VERIFY_URL).then((response) => {
    console.log('response:', response.status, response.data);

    res.status(200).json(response.data);
  });
}

