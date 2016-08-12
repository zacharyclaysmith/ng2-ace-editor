# ng2-ace

[![Join the chat at https://gitter.im/ng2-ace-editor/Lobby](https://badges.gitter.im/ng2-ace-editor/ng2-ace-editor.svg)](https://gitter.im/ng2-ace-editor/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![npm version](https://badge.fury.io/js/ng2-ace-editor.svg)](https://badge.fury.io/js/ng2-ace-editor)
Ace editor integration with typescript for angular 2.

# Install
`npm i -s ng2-ace-editor`

# Sample Usage

> Minimal

```js
import { Component } from 'angular2/core';
import { AceEditorDirective } from 'ng2-ace-editor';

@Component({
  directives: [AceEditorDirective],
  template: `
  <div ace-editor
       [text]="text"></div>
  `
})
export class MyComponent {
    text:string = "";
}
```

> Complete

```js
import { Component } from 'angular2/core';
import { AceEditorDirective } from 'ng2-ace-editor';

import 'brace/theme/clouds';
import 'brace/mode/sql';

@Component({
  directives: [AceEditorDirective],
  template: `
  <div ace-editor
       [text]="text"
       [mode]="'sql'"
       [theme]="'clouds'"
       [options]="options"
       [readOnly]="false"
       [autoUpdateContent]="true" //change content when [text] change
       (textChanged)="onChange($event)"
       style="min-height: 200px; width:100%; overflow: auto;"></div>
  `
})
export class MyComponent {
    text:string = "";
    options:any = {maxLines: 1000, printMargin: false};
    
    onChange(code) {
        console.log("new code", code);
    }
}
```

# Angular Cli
> angular-cli-build.js

```js
... 
module.exports = function(defaults) {
  return new Angular2App(defaults, {
    vendorNpmFiles: [
      ...
      'brace/**/*.+(js|js.map)',
      'w3c-blob/**/*.+(js|js.map)',
      'buffer-shims/**/*.+(js|js.map)'
    ]
  });
};
...
```

> angular-cli-build.js

```js
... 
const map:any = {
    'brace' : 'vendor/brace',
    'w3c-blob' : 'vendor/w3c-blob',
    'buffer': 'vendor/buffer-shims'
};

/** User packages configuration. */
const packages:any = {
    'w3c-blob': {
        format: 'cjs',
        defaultExtension: 'js',
        main: 'index.js'
    },
    'brace': {
        format: 'cjs',
        defaultExtension: 'js',
        main: 'index.js'
    },
    'buffer': {
        format: 'cjs',
        defaultExtension: 'js',
        main: 'index.js'
    }
};
...
```

