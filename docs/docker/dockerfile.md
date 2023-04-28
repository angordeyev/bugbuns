# Dockerfile

## Best Practices

[Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

## FROM

    FROM ubuntu

<!---->

    FROM ubuntu:latest

Multiple `FROM` are used for multistage builds. Multistage builds produce
multiple images.

[Multiple FROMs - what it means. Stack Overflow.](https://stackoverflow.com/questions/33322103/multiple-froms-what-it-means)

## ADD or COPY

Use COPY if ADD is not required. Add supports additional features like url.

[ADD or COPY. Best practices for writing Dockerfiles.](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#/add-or-copy)
[What is the difference between the 'COPY' and 'ADD' commands in a Dockerfile?](https://stackoverflow.com/questions/24958140/what-is-the-difference-between-the-copy-and-add-commands-in-a-dockerfile)

## COPY

Add file to directory

    COPY <file_name> relativeDir/

<!---->

    COPY <file_name> /absoluteDir/

Add directory to directory

    COPY <directrory> relativeDir/<directrory>

<!---->

    COPY <directrory> /absoluteDir/<directrory>

## ADD

Add file to directory.

    ADD <file_name> relativeDir/

<!---->

    ADD <file_name> /absoluteDir/

[Official docs](https://docs.docker.com/engine/reference/builder/#add)




