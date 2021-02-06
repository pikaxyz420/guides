---
title: "Sending Requests With NodeJS"
---

### [Home](https://pikaxyz420.github.io/guides/)

---

## Sending Requests With NodeJS

Sending requests with NodeJS.

## Contents

- [What Do You Need](#what-do-you-need)
- [Using The Internal HTTP Library](#using-the-internal-http-library)
- [Questions](#questions)

## What Do You Need

You'll need a library to send HTTP requests.

NodeJS by default has built-in internal HTTP libraries:

- https://nodejs.org/api/http.html
- https://nodejs.org/api/https.html

But they're too low-level.

Which is why we also recommend higher-level libraries like `got`:

- https://www.npmjs.com/package/got

Which implements a lot of things like:

- Convenient promise-based interface
- Timeout handling
- Following of redirects
- Sending JSON requests
- Receiving JSON responses
- Retries

We'll provide some examples here.

## Using The Internal HTTP Library

The request:

```js
const http = require('http');

const options = { hostname: 'example.com', port: 80, path: '/', method: 'GET', headers: {} };

const req = http.request(options, (res) => {
  console.log(`STATUS: ${res.statusCode}`);
  console.log(`HEADERS: ${JSON.stringify(res.headers)}`);
  res.setEncoding('utf8');
  res.on('data', (chunk) => {
    console.log(`BODY: ${chunk}`);
  });
  res.on('end', () => {
    console.log('No more data in response.');
  });
});
req.on('error', (e) => {
  console.error(`ERROR: ${e.message}`);
});
req.end();
```

The response:

```sh
user@group:~/Documents/$ node ./test.js 
STATUS: 200
HEADERS: {"age":"251448","cache-control":"max-age=604800","content-type":"text/html; charset=UTF-8","date":"Sat, 06 Feb 2021 06:54:26 GMT","etag":"\"3147526947+ident\"","expires":"Sat, 13 Feb 2021 06:54:26 GMT","last-modified":"Thu, 17 Oct 2019 07:18:26 GMT","server":"ECS (oxr/831F)","vary":"Accept-Encoding","x-cache":"HIT","content-length":"1256","connection":"close"}
BODY: <!doctype html>
<html>
<head>
    <title>Example Domain</title>

    <meta charset="utf-8" />
    <meta http-equiv="Content-type" content="text/html; charset=utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <style type="text/css">
    body {
        background-color: #f0f0f2;
        margin: 0;
        padding: 0;
        font-family: -apple-system, system-ui, BlinkMacSystemFont, "Segoe UI", "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
        
    }
    div {
        width: 600px;
        margin: 5em auto;
        padding: 2em;
        background-color: #fdfdff;
        border-radius: 0.5em;
        box-shadow: 2px 3px 7px 2px rgba(0,0,0,0.02);
    }
    a:link, a:visited {
        color: #38488f;
        text-decoration: none;
    }
    @media (max-width: 700px) {
        div {
            margin: 0 auto;
            width: auto;
        }
    }
    </style>    
</head>

<body>
<div>
    <h1>Example Domain</h1>
    <p>This
BODY:  domain is for use in illustrative examples in documents. You may use this
    domain in literature without prior coordination or asking for permission.</p>
    <p><a href="https://www.iana.org/domains/example">More information...</a></p>
</div>
</body>
</html>

END
```

More info here:

- https://nodejs.org/api/http.html#http_http_request_options_callback

## Questions

For questions, you may reach us on Discord at https://discord.gg/d4rJDTU3Yy

Feel free to open an issue or submit a PR, Thank you!