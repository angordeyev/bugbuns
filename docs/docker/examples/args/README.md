# Running

## Using docker and default port

Run

    docker build -t args-default .
    docker run -p 8080:8080 args

## Using docker and port as the argument

Run

    docker build --build-arg PORT=8081 -t args-8081 .
    docker run -p 8081:8081 args-8081

Access site at localhost:8081

## Using docker compose

Run 
    
    docker compose up --build

Access site at localhost:8082
