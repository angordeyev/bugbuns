# Containerizing an app

Minimal Docker image `Dockerfile`

    FROM alpine
    
    RUN apk add --update nodejs npm curl
    
    COPY . /src
    WORKDIR /src
    
    RUN  npm install

    EXPOSE 8080

    ENTRYPOINT ["node", "./app.js"]

Build an image in a current directory with a name and a tag.

    docker image build -t web:latest .
