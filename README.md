## `eslint-config-oy`

Shared [ESLint config](https://eslint.org) for my projects.  
*(Lints both JavaScript & TypeScript projects.)*

### Installation

```
$ npm install --save-dev eslint-config-oy
```

### Usage

`.eslintrc.json` in **TypeScript** project:

```jsonc
{
    "extends": [
        "eslint-config-oy/ts"
    ]
}
```

`.eslintrc.json` in **JavaScript** project:

```jsonc
{
    "extends": [
        "eslint-config-oy"
    ]
}
```

### Evironment Set Up

- Install `eslint` extension for VSCode.
- Add files below in the project's `.vscode` directory and paste related contents:

  - **`.vscode/extensions.json`**:
    ```json
    {
      "recommendations": [
          "dbaeumer.vscode-eslint"
      ]
    }
    ```
  - **`.vscode/tasks.json`**:
    ```json
    {
      "version": "2.0.0",
      "tasks": [
          {
            "type": "npm",
            "script": "lint",
            "problemMatcher": ["$eslint-stylish"],
            "label": "npm: lint",
            "detail": ""
          }
      ]
    }
    ```
  - **`.vscode/settings.json`**:
      ```json
      {
          "eslint.validate": [
              "typescript",
              "typescriptreact"
          ]
      }
      ```

### Contributing

- `index.js` is eslint config for JavaScript projects.
- `ts.js` is eslint config for TypeScript projects; and extends from `index.js`.
- If `@typescript-eslint` has an override rule of an eslint rule; first make sure you **turn off** the eslint rule in `ts.js`. 

  ```js
  {
    quotes: "off",
    '@typescript-eslint/quotes': [
      'error',
      'single',
      {
          avoidEscape: true,
          allowTemplateLiterals: true
      }
    ],
  }
  ```

- If a rule works the same way for both JavaScript and TypeScript, add the rule's value (configuration) in `_common.js` and reference in both `index.js` and `ts.js`.

  ```js
  // _common.js
  {
    QUOTES: [
      'error',
      'single',
      {
        avoidEscape: true,
        allowTemplateLiterals: true
      }
    ],
    // ...
  }

  // index.js
  {
    quotes: common.QUOTES,
    // ...
  }

  // ts.js
  {
    quotes: 'off',
    '@typescript-eslint/quotes': common.QUOTES,
    // ...
  }
  ```

### Related projects
- [`tsconfig-oy`](https://github.com/onury/tsconfig-oy)
