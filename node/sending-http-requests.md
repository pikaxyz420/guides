---
title: "Sending HTTP Requests With NodeJS"
---

### [Home](https://pikaxyz420.github.io/guides/)

---

## Sending HTTP Requests With NodeJS

Sending requests with NodeJS.

## Contents

- [What Do You Need](#what-do-you-need)
- [When Do You Need This](#when-do-you-need-this)
- [Using The Internal HTTP Library](#using-the-internal-http-library)
- [Using Got](#using-got)
  - [Sending JSON](#sending-json)
  - [Sending Multipart](#sending-multipart)
  - [Sending URL-encoded](#sending-url-encoded)
  - [Receiving JSON](#receiving-json)
  - [Receiving Buffer](#receiving-buffer)
  - [Receiving Text](#receiving-text)
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

## When Do You Need This

Example use-cases:

- When a user uploads a file, and you have to send that file buffer somewhere
- When you need to fetch some data from a third-party website, e.g. currency exchange rates
- When you need to send some structured-data (e.g. JSON objects) to somewhere
- When you need to send some unstructured-data (e.g. jpeg, png, docx) to somewhere
- When you're scraping some data and you need to simulate some HTTP requests

## Using The Internal HTTP Library

From `http` library, we'll use `http.request`.

- https://nodejs.org/api/http.html#http_http_request_options_callback

Request:

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

Response:

```sh
user@group:~$ node ./test.js 
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

## Using Got

From `got` library, we'll use `got.get`.

Request:

```js
const got = require('got');

(async () => {
  const response = await got.get('http://example.com').text();
  console.log(response);
})();
```

Response:

```sh
user@group:~$ node ./test.js 
<!doctype html>
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
    <p>This domain is for use in illustrative examples in documents. You may use this
    domain in literature without prior coordination or asking for permission.</p>
    <p><a href="https://www.iana.org/domains/example">More information...</a></p>
</div>
</body>
</html>
```

#### Sending JSON

For endpoints expecting JSON-encoded body, uses `Content-Type` `application/json`.

Sent as `POST` request.

```js
const got = require('got');

(async () => {
  const response = await got.post('https://example.com/', { json: { foo: 'bar' } }).json(); // '.json()' means we expect a JSON response
  return response;
})();
```

#### Sending Multipart

If you're sending files to another server, this is what you're looking for.

For endpoints expecting Multipart-encoded body, uses `Content-Type` `multipart/form-data`.

Sent as `POST` request.

```js
const fs = require('fs');
const multipart = require('multi-part');

const post_form = async (url, body) => {
};
(async () => {
  const form = new multipart();
  
  const file_buffer = await fs.promises.readFile('./file.png');
  
  // the 'file' here is the field name
  // the file_buffer here is the field value
  // on some cases you have to use a different field name
  // when using Telegram Bot API's, for example, they expect photos to be use 'photo' as field name
  form.append('file', file_buffer);
  
  const form_buffer = await form.buffer();
  const form_headers = form.getHeaders(false);
  const response = await got.post(url, { headers: form_headers, body: form_buffer }).json(); // '.json()' means we expect a JSON response
  return response;
})();
```

#### Sending URL-encoded

For endpoints expecting URL-encoded body, uses `Content-Type` `application/x-www-form-urlencoded`.

Sent as `POST` request.

```js
const got = require('got');

(async () => {
  const response = await got.post('http://example.com/', { form: { foo: 'bar' } }).json(); // '.json()' means we expect a JSON response
  return response;
})();
```

#### Receiving JSON

Response `Content-Type` must be `application/json`.

```js
const got = require('got');

(async () => {
  const response = await got.get('https://example.com/').json(); // '.json()' means we expect a JSON response
  return response;
})();
```

#### Receiving Buffer

```js
const got = require('got');

(async () => {
  const response = await got.get('https://example.com/').buffer();
  return response;
})();
```

#### Receiving Text

```js
const got = require('got');

(async () => {
  const response = await got.get('https://example.com/').text();
  return response;
})();
```

## Questions

Feel free to open an issue or submit a PR, Thank you!

---

#### [Home](https://pikaxyz420.github.io/guides/)
