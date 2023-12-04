# nmp Package Manager

## Tasks

### Getting Help

```shell
npm help
```

### Shorter Commands

```shell
# A shorter verion
npm i cowsay
# The full version
npm install cowsay
```
### Run Package

With a package version:

```shell
npx cowsay@latest hello
```

With parameters:

```shell
npx create-docusaurus --help
```

### Scripts

To add a script edit `package.json` file:

```JSON
{
  ...
  "scripts": {
    "say": "echo"
  },
  ...
}
```

Using the script:

```shell
npm run say hello
```
```output

> some-package@1.0.0 echo
> echo hello

hello
```

List scripts:

```shell
npm run
```
```output
Scripts available in some-package@1.0.0 via `npm run-script`:
  echo
    echo
```

Scripts can run npm packages:

```js title="package.json"
{
  ...
  "scripts": {
    "cowhello": "cowsay hello",
    ...
  }
  ...
}
````

```shell
npm run cowhello
```
```output
> some-package@1.0.0 cowhello
> cowsay hello

 _______
< hello >
 -------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

Default script names:

`npm start` is a short form for `npm run start` and will run:
  * `prestart`
  * `start`
  * `poststart`

The other popular Life Cycle scripts are:

  * `npm test`
  * `npm stop`
  * `npm restart`
  * `npm ci`
  * `npm run <user defined>`
  * `npm cache add`
  * `npm diff`
  * `npm install`
  * `npm pack`
  * `npm publish`
  * `npm rebuild`
  * `npm version`

See more docs at  [Life Cycle Scripts. npm Docs.](https://docs.npmjs.com/cli/v10/using-npm/scripts#life-cycle-scripts)

### Install Package

### Locally

```shell
npm i cowsay
```

The package name and the version will be added to `package.json`:

```JSON
...
"cowsay": "^1.5.0",
...
```

And the package with its dependencies will be added to `node_modules` folder.

### Globally

Install a package:

```shell
sudo npm i -g cowsay
```

The package will be installed in `/usr/lib/node_modules/` folder. And the link will be created for the execution file in `/usr/bin/` foler.

```shell
ls -l /usr/bin/cowsay
```
```output
cowsay -> ../lib/node_modules/cowsay/cli.js
```

Using:

```shell
cowsay hello
```

### Uninstall Package

#### Locally

```shell
npm un <package>
```

#### Globally

```shell
sudo npm un -g <package>
```

### Show Package Information

```shell
npm show react
```

See `dist-tags` section for available tags:

```output
dist-tags:
beta: 18.0.0-beta-24dd07bd2-20211208
experimental: 0.0.0-experimental-5dd35968b-20231201
next: 18.3.0-canary-5dd35968b-20231201
canary: 18.3.0-canary-5dd35968b-20231201
latest: 18.2.0
rc: 18.0.0-rc.3
```

npm `dist-tags` role is close to git branches than git tags.

### Versions

Tha package version has the structure: `<major>.<minor>.<patch>`

The default versioning used `^` prefix.

`^1.1.7` for "npx" package matches: 1.0.2, 1.1.0, 1.1.1.

[Semver Calculator](https://semver.otterlord.dev/)

## Repository

### Scoped Packages

The package may consist of: `@<scope>/<package>@<tag>`. Scope is a way of grouping packages together. It is ogranization name usually.
