# PropTypes to TS

[![Netlify Status](https://api.netlify.com/api/v1/badges/5405cd67-6bbd-40ee-956a-2ae4ded8a987/deploy-status)](https://app.netlify.com/sites/proptypes/deploys) ![Test](https://github.com/mskelton/prop-types-to-ts/workflows/Test/badge.svg?branch=master)

> Codemod to convert React PropTypes to TypeScript types.

## Key Features

- Supports function and class components
- Supports `static propTypes` declarations on class components
- Supports files with multiple components
- Option to remove or preserve PropTypes after converting to TS

## Usage

Run the following command with a file glob that matches the files you want to convert.

```sh
npx jscodeshift -t https://raw.githubusercontent.com/mskelton/prop-types-to-ts/master/transform.js GLOB

# Example
npx jscodeshift -t https://raw.githubusercontent.com/mskelton/prop-types-to-ts/master/transform.js src/**/*.{js,jsx}
```

## Try it Online!

In addition to the CLI, you can use the tool online at [proptypes.netlify.app](https://proptypes.netlify.app)! Simply paste your input on the left and instantly see the output on the right!

[![Screenshot](web/screenshot.png)](https://proptypes.netlify.app)

## Example Input/Output

```ts
// Input
import PropTypes from "prop-types"
import React from "react"

export function MyComponent(props) {
  return <span />
}

MyComponent.propTypes = {
  bar: PropTypes.string.isRequired,
  foo: PropTypes.number,
}

// Input
import React from "react"

type Props = {
  bar: string
  foo?: number
}

export function MyComponent(props: Props) {
  return <span />
}
```

## Options

### `--preserve-prop-types`

This option will preserve PropTypes after converting to TS. This is useful for component libraries where you support both TypeScript declarations and PropTypes.

#### Input

```js
import PropTypes from "prop-types"
import React from "react"

export function MyComponent(props) {
  return <span />
}

MyComponent.propTypes = {
  bar: PropTypes.string.isRequired,
  foo: PropTypes.number,
}
```

#### Output

```ts
import PropTypes from "prop-types"
import React from "react"

type Props = {
  bar: string
  foo?: number
}

export function MyComponent(props: Props) {
  return <span />
}

MyComponent.propTypes = {
  bar: PropTypes.string.isRequired,
  foo: PropTypes.number,
}
```
