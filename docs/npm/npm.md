# nmp Package Manager

## Tasks

### Shorter Commands

```shell
# A shorter verion
npm i cowsay
# The full version
npm install cowsay
```

### Install Package

```shell
npm i cowsay
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

The package can consist of: @<scope>/<package>@<tag>. Scope is a way of grouping packages together. It is ogranization name usually.

