<p align="center">
  <img src="https://raw.githubusercontent.com/mat-sz/DUI/master/logo.png" alt="DUI">
</p>

<p align="center">
  Declarative UI syntax for JS (inspired by SwiftUI).
</p>

----

DUI is an experimental project focused on bringing [SwiftUI-like syntax](https://developer.apple.com/xcode/swiftui/) to JavaScript.

The project is focused on:

* full compatibility with current JSX ecosystem,
* interoperability with JSX code (DUI doesn't prevent you from using JSX in the same file),
* providing the full feature set of JSX.

Many elements of the DUI ecosystem are currently undergoing development. The syntax should stay the same, but there's no guarantee that absolutely nothing will change.

**Quickstart:**

```sh
npx create-react-app name --template dui
```

## Table of Contents

1. [Examples](#examples)
2. [Usage](#usage)
3. [Ecosystem](#ecosystem)

## Examples

```js
import React, { useState } from 'react';
import logo from './logo.svg';
import './App.css';

function App() {
  const [ redBackground, setRedBackground ] = useState(false);

  const toggleRedBackground = () => {
    setRedBackground(isRed => !isRed);
  };

  const imgProps = {
    src: logo,
    className: "App-logo",
    alt: "logo"
  };

  return (
    div (className: "App") {
      header (className: "App-header") {
        img (...imgProps, style: {
          background: redBackground ? 'red' : null
        }) {
          // Unfortunately, self-closing tags aren't supported yet.
        }
        p {
          "Hello, world."
        }
        button (onClick: toggleRedBackground) {
          "Click me!"
        }
      }
    }
  );
}

export default App;
```

Inline functions can be added in a following fashion:

```js
button (onClick: () => doSomething()) {
  // The parentheses around the function are required.
}

// async:

button (onClick: async () => await doSomething()) {
  // The parentheses around the function are required.
}
```

React Fragment is `@` instead of `<>`:

```js
@ {
  ul {
    li { "Item 1" }
    li { "Item 2" }
    li { "Item 3" }
  }
  p {
    "Hello, world!"
  }
}
```

Spread operator (`...`) is supported as well:

```js
div (...props) {}
// or:
div (hello: "world", ...props) {}
```

## Usage

The Babel plugin works with ejected React apps and also customize-cra. More detailed configuration information is coming soon, after the critical bugs are resolved.

### create-react-app template

```sh
npx create-react-app name --template dui
```

### Manual installation with react-app-rewired and customize-cra

First, install all required packages:

```sh
yarn add customize-cra react-app-rewired babel-plugin-syntax-dui
```

Replace `scripts` in `package.json`:

```json
"scripts": {
  "start": "react-app-rewired start",
  "build": "react-app-rewired build",
  "test": "react-app-rewired test"
},
```

Create `.babelrc` in project's root directory:

```json
{
  "plugins": ["babel-plugin-syntax-dui"]
}
```

And, finally, create a `config-overrides.js` file:

```js
const { override, useBabelRc, disableEsLint } = require('customize-cra');

module.exports = override(
  disableEsLint(),
  useBabelRc()
);
```

`disableEsLint` is required because the ESLint parser/plugin is not ready yet.

## Ecosystem

* Babel syntax plugin: [babel-plugin-syntax-dui](https://github.com/mat-sz/babel-plugin-syntax-dui) [\[npm\]](https://npmjs.com/package/babel-plugin-syntax-dui)
* Babel parser fork: [babel-parser-dui](https://github.com/mat-sz/babel/tree/master/packages/babel-parser) [\[npm\]](https://npmjs.com/package/babel-parser-dui)
* CRA template: [cra-template-dui](https://github.com/mat-sz/cra-template-dui) [\[npm\]](https://npmjs.com/package/cra-template-dui)

Missing:

* VS Code syntax highlighting/checking extension,
* ESLint plugin,
* Prettier plugin,
* documentation.