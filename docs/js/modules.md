# Modules

JS modules are also known as ES modules and ECMAScript modules.

## Node.js Example

```js title="main.mjs"
import {name} from "./person.mjs";
console.log(name)
```

```js title="person.mjs"
export const name = "Andrew";
```

```shell
node main.mjs
```
```output
Andrew
```

## The Browser Example

```html title="main.html"
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Main</title>
  <body>
    <script type="module">
      import {name} from "./person.mjs";
      alert(name);
    </script>
  </body>
</head>
```

```js title="person.mjs"
export const name = "Andrew";
```

```shell
npx serve & xdg-open http://localhost:3000/main.html
```

## Default Export and Import

```js title="main.mjs"
import name from "./person.mjs";
console.log(name)
```

```js title="person.mjs"
export default "Andrew";
```

```shell
node main.js
```
```output
Andrew
```

## Resources

[JavaScript modules](https://v8.dev/features/modules#mjs)
