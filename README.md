# Website

This website is built using [Docusaurus 2](https://docusaurus.io/), a modern static website generator.

## Run Local

Development environmnt (with drafts):

```shell
npm install docusaurus
npm start
```

Release (drafts are hidden):

```shell
npx docusaurus serve
```

This command starts a local development server and opens up a browser window. Most changes are reflected live without having to restart the server.

## Deploy

### Fly.io

#### Create the Application

```shell
fly launch
fly scale memory 512
```

#### Deploy

```shell
fly deploy
```

#### Open Site

```shell
fly open
```

#### Comments

NGINX is used to run the site with the latest official NGINX Docker container. Default NGINX `./nginx.conf` config is used with the `server` section modified.

Redirect from the subdomain to the main domain to improve SEO:

```
if ($host = bugbuns.fly.dev) {
    return 301 $scheme://bugbuns.com$request_uri;
}
```

Redirect to the main React page:

```
location / {
    try_files $uri /index.html;
}
```

### Using SSH

```
USE_SSH=true yarn deploy
```

### GitHub Pages

```shell
GIT_USER=<Your GitHub username> npm run deploy
```

This command is a convenient way to build the website and push to the `gh-pages` branch.

### Build

```shell
npm build
```

This command generates static content into the `build` directory and can be served using any static contents hosting service.

Check MDX:

```shell
npx docusaurus-mdx-checker
```
