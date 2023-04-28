FROM alpine

RUN apk add --update curl python3

ARG PORT=8080
ENV PORT=${PORT}

CMD python3 -m http.server ${PORT}
