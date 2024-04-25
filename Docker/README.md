
# Docker

- Docker runs on a client-server that is meditated by the daemon that leverages REST APIs to request to perform container-related operations. Podman, on the other hand, does not require a daemon. It uses Pods to manage containers, which helps users to run rootless containers.
- Port mapping in Docker is the process of mapping a port on the host machine to a port in the container. This is essential for accessing applications running inside containers from outside the Docker host. Imagine you have a web server running inside a Docker container on port 3000. By default, this port is only accessible within the Docker network and not from your host machine or the external network. To make this server accessible outside the container, you need to forward a port from the host to the container. Eg: `docker run -p [HOST_PORT]:[CONTAINER_PORT] [IMAGE]`. 


----------------------------------------------------------------------





















