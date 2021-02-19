# kenall-js

![](https://github.com/KEN-ALL/kenall-js/workflows/CI/badge.svg" alt="CI" />

## What's this?

kenall-js is a JavaScript client library for [KEN ALL](https://kenall.jp/), Japan postal code to address translation API service.

## How to use

There are two options to use kenall-js in your project.  The one is put a `<script>` tag referring to the script bundle somewhere atop of your HTML file to invoke the API from within your script, and the other is specify `kenall` package as a dependency in your Node.js project's package.json.

### Usage from within the plain-old JavaScrpt

All you need is put a `<script>` tag that refers to the script bundle as follows:

```html
<script type="text/javascript" src="LOCATION-TO-THE-SCRIPT-BUNDLE"></script>
```

This adds a property `kenall` to the global `window` object, from which you can refer to `KENALL` constructor to create the object that works as the interface.  Look at the following example to see what it goes like.

```html
<script type="text/javascript">
function fill(form) {
  // You can obtain the API key from the dashboard at kenall.jp/home
  const k = new kenall.KENALL('API_KEY');
  const postalCode = form.elements["postalcode"].value;
  k.getAddress(postalCode).then(
    function (address) {
      const firstCandidate = address.data[0];
      form.elements["prefecture"].value = firstCandidate["prefecture"];
    }
  ).catch(function () {
    alert("Failed to invoke the API");
  });
}
</script>
```

The script bundle can be downloaded at the release page.

Alternatively, you can use the following URL for the latest bundle.  Beware that we don't provide any warranty on its availability, though we'll put as much effort as possible for keeping it up.

[https://js.kenall.jp/2021-02-01/kenall.js](https://js.kenall.jp/2021-02-01/kenall.js)


### Usage in a Node.js project

Run

```
$ npm i kenall
```

to add kenall.js as a dependency for your project.

Then you can use it like the following:

```javascript
const { KENALL } = require('kenall');

// You can obtain the API key from the dashboard at kenall.jp/home
const api = new KENALL('API_KEY');
api.getAddress(postalCode).then(
  r => {
    console.log(r);
  }
).catch(
  e => {
    console.error(e);
  }
);
```

or either in TypeScript,

```typescript
import { KENALL } from 'kenall';

const kenall = new KENALL('API_KEY');
const r = await kenall.getAddress(postalCode);
console.log(r);
```

## Building

Run

```
$ npm run build
```

to generate JavaScript scripts under `built/`.  If you want to get the bundle, run

```
$ npm run bundle
```

and you'll find one under `dist/`.


## Tests

```
$ npm run test
```

## Examples & Demos

* [CodePen](https://codepen.io/kenall/pen/NWbPYda)
* https://github.com/KEN-ALL/kenall-js/tree/master/examples
