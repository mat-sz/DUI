# DUI

Declarative UI syntax for JS (inspired by SwiftUI).

```
import React from 'react';
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    div (className: "App") {
      header (className: "App-header") {
        img (src: logo, className: "App-logo") {
          // No self closing tags yet, unfortunately.
        }
        "Hello, world!"
      }
    }
  );
}

export default App;
```

## Current state

I wouldn't recommend using this at the current state. There are quite a few breaking bugs, which are currently being resolved.

## Usage

The Babel plugin works with ejected React apps and also customize-cra. More detailed configuration information is coming soon, after the critical bugs are resolved.

CRA template is available:

```
npx create-react-app name --template dui
```

## Ecosystem

Everything necessary to use this with Babel is contained within [babel-plugin-syntax-dui](https://github.com/mat-sz/babel-plugin-syntax-dui). Installation and enabling of this plugin allows for the syntax to be used with React.js (as the AST output matches JSX output enough for it to work).

Other necessary parts being worked on are:

* VS Code syntax highlighting/checking extension,
* React app templates,
* documentation.

The forked parser is available [here](https://github.com/mat-sz/babel/tree/master/packages/babel-parser).