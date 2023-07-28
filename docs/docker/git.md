# Creating Docker git image

## Docker File

    FROM alpine
    RUN apk update
    RUN apk add git
