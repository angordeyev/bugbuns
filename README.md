# Website

This website is built using [Docusaurus 2](https://docusaurus.io/), a modern static website generator.

## Run Local

    npm start

This command starts a local development server and opens up a browser window. Most changes are reflected live without having to restart the server.

## Deploy

### Fly.io

#### Create the Application

    fly launch
    fly scale memory 512

#### Deploy

    fly deploy

#### Open Site

    fly open

#### Comments

`CMD [ "npm", "run", "start" ]` to `CMD [ "npm", "run", "serve", "--", "--port" "8080" ]` in the default Dockerfile generated by `fly launch`.

### Using SSH

    USE_SSH=true yarn deploy

### GitHub Pages

    $ GIT_USER=<Your GitHub username> npm run deploy

This command is a convenient way to build the website and push to the `gh-pages` branch.

### Build

    npm build

This command generates static content into the `build` directory and can be served using any static contents hosting service.
