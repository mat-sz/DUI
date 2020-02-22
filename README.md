# DUI

Declarative UI syntax for JS (inspired by SwiftUI).

```
import React, { useState } from 'react';
import logo from './logo.svg';
import './App.css';

function App() {
  const [ redBackground, setRedBackground ] = useState(false);

  const toggleRedBackground = () => {
    setRedBackground(isRed => !isRed);
  };

  return (
    div (className: "App") {
      header (className: "App-header") {
        img (src: logo, className: "App-logo", alt: "logo", style: {
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

```
button (onClick: (() => doSomething())) {
  // The parentheses around the function are required.
}
```

React Fragment is `@` instead of `<>`:

```
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

```
div (...props) {}
// or:
div (hello: "world", ...props) {}
```

## Current state

I wouldn't recommend using this at the current state. There are quite a few breaking bugs, which are currently being resolved.

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

## Ecosystem

Everything necessary to use this with Babel is contained within [babel-plugin-syntax-dui](https://github.com/mat-sz/babel-plugin-syntax-dui). Installation and enabling of this plugin allows for the syntax to be used with React.js (as the AST output matches JSX output enough for it to work).

Other necessary parts being worked on are:

* VS Code syntax highlighting/checking extension,
* documentation.

The forked parser is available [here](https://github.com/mat-sz/babel/tree/master/packages/babel-parser).