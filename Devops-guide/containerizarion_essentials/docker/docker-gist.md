Here's a set of notes based on the provided content, formatted for easy reference:

```markdown
# Docker Essentials

## Terminology

### Images
- **Definition**: The file system and configuration of applications used to create containers.
- **Creation**: Described using a `Dockerfile`.
- **Identification**: Can be identified by `repo:tag` or ID.

### Containers
- **Definition**: Running instances of Docker images that execute applications.
- **Characteristics**: 
  - Include an application and all its dependencies.
  - Share the host OS kernel with other containers.
  - Run as isolated processes in user space.
- **Management**: Created using `docker run`. Running containers can be listed with `docker ps`.
- **Note**: Image ID ≠ Container ID; recreated containers lose changes made since their last creation.

### Docker Daemon
- A background service on the host that manages building, running, and distributing Docker containers.

### Docker Client
- The command line tool for interacting with the Docker daemon.

### Docker Store
- A registry of Docker images, including trusted and enterprise-ready containers, plugins, and Docker editions.

### Volumes
- **Definition**: Virtual disks not part of the image, local to the host.
- **Types**: Can be persistent or ephemeral.
- **Creation**: Add `-v` option to the run command.
- **Usage**: Prefer host over container file system mounts.

## General Tips

- Use fewer steps in Docker builds and remove unwanted files to optimize image layers.
- Each build step creates a read-only layer over the previous one.
- `tty` might keep the container alive when using Docker Compose.
- Disk limits can be expanded via Docker Desktop UI.
- Names for build or run commands are auto-generated if not provided.

## Commands

### Container Management
- `docker run [options] <image> <command>`: Start a new container.
- `docker ps`: Show current containers.
- `docker ps -a`: Show current and recent containers.
- `docker stop <container>`: Stop a container without losing state.
- `docker rm [-f] <container>`: Remove a container; `-f` force stops before removal.
- `docker logs [-f] <container>`: Fetch container logs; `-f` for following logs.
- `docker exec -it <container> <command>`: Execute a command in a running container.
- `docker attach <name>`: Attach to a running container.
- `docker kill <container>`: Forcefully stop a container.

### Image Management
- `docker build [--no-cache] -t <name> <context>`: Build an image using a Dockerfile.
- `docker commit <container_id/name> [<new_name>]`: Create a new image from a container's state.
- `docker image rm <image_id>`: Delete an image.
- `docker images`: View local images.
- `docker pull <image>`: Download an image from Docker Hub.
- `docker push <image>`: Upload an image to Docker Hub.
- `docker tag <image_id> <name>`: Tag an image with a repository and version.

### Volumes and Networks
- `docker volume create <name>`: Create a volume.
- `docker volume ls`: List volumes.
- `docker run -v <local>:<container>`: Use a volume.
- `docker network create <name>`: Create a network.
- `docker network connect <network> <container>`: Attach a network to a container.
- `docker network ls`: List networks.

### System
- `docker login`: Authenticate to Docker Hub.
- `docker system df`: View disk usage information.
- `docker system prune`: Clean up unused resources like images, containers, and networks.

## Dockerfile Basics

- `FROM`: Sets the base image for subsequent instructions.
- `RUN`: Executes a command in the container at build time.
- `COPY`: Copies files from the local directory to the image.
- `ADD`: Copies files or URLs to the image and handles tar files.
- `EXPOSE`: Declares ports that will be exposed at runtime.
- `CMD`: Sets default commands to run at container start. If ENTRYPOINT is specified, CMD provides default arguments to the ENTRYPOINT. If ENTRYPOINT is not specified, CMD is executed as the command to start the container.
- `ENTRYPOINT`: Configures a container to run as an executable.
- `LABEL`: Adds metadata to the image.
- `ENV`: Defines environment variables.
- `VOLUME`: Defines mount points for external data storage.

### Example
```Dockerfile
FROM openjdk:8

COPY target/demo-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "/app.jar"]
```

```Dockerfile
FROM maven:3.8.2-jdk-8

COPY . .

RUN mvn clean install

CMD mvn spring-boot:run
```

## Docker Compose

- **Purpose**: Orchestrates the running of multiple Docker containers.
- **Command**: `docker-compose up` starts the services defined in the `docker-compose.yml` file.

### Example `docker-compose.yml`

```yaml

version: '2'
services:
  crud-app:
    build: ./crud-app
    container_name: crud-app
    ports:
      - "8080:8080"
    networks:
      - my-network
    volumes:
      - .m2:/root/.m2

networks:
  my-network:
    driver: bridge
  
```
