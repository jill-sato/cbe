# cbe
Common Build Environment Docker Image

Includes the following:
- OpenJDK8
- Maven
- Gradle
- AWS cli
- Docker

This image is published on dockerhub at jillsato/cbe.

## Build

docker build -t cbe .

## Docker in Docker

The image includes docker in order to build docker images.
The docker socket file must be mounted in the container to make it work.

E.g.
`docker run -v /var/run/docker.sock:/var/run/docker.sock cbe docker info`

## Login to AWS Docker Repository

The image includes the AWS cli in order to authenticate to AWS ECR.
The steps to login to the AWS ECR are encapsulated in the ecr_docker_login shell script.

The script must be mounted, so that it can be invoked inside the container.

E.g.
`docker run -v /var/run/docker.sock:/var/run/docker.sock -v $PWD/ecr_docker_login:/bin/ecr_docker_login cbe /bin/ecr_docker_login`

In the example above we also mount the docker socket as the ecr_docker_login invokes "docker login".
