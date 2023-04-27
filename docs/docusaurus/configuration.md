# Configuration

## Remove Trailing Slach from Directory Navigation Items

`docusaurus.config.js`

```js
...
const config = {
  ...
  trailingSlash: false,
  ...
```

## Presets

Presets are plugins installed by default and can be configured with the same set of attributes as plugins. 

docs is [plugin-content-docs](https://docusaurus.io/docs/api/plugins/@docusaurus/plugin-content-docs)
blog is [plugin-content-blog](https://docusaurus.io/docs/api/plugins/@docusaurus/plugin-content-blog)

https://docusaurus.io/docs/api/plugins/@docusaurus/plugin-content-docs

## Change Folders

    docusaurus.config.js

    presets: [
      [
        ...
        ({
          docs: {
            path: 'docs1'
            ...
          },
          blog: {
            path: 'blog1',
            ...
          }
        }),
        ...
      ],
    ],
