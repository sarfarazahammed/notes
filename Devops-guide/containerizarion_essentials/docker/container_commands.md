## Brief Intro

- Image: A collction of files and instructions needed to run a software program

- Docker image holds everything a computer needs in order to run a software.

- Container : Runtime instance of a Docker image. When a image is run with provided resources, it's considered as container.

# Docker Container-Related Commands

| Command                  | Flags / Combinations                          | Example Usage                                               | Description                                                               |
| ------------------------ | --------------------------------------------- | ----------------------------------------------------------- | ------------------------------------------------------------------------- |
| `docker run`             | `-d`                                          | `docker run -d nginx`                                       | Runs the container in detached mode (in the background).                  |
|                          | `--name`                                      | `docker run --name my_nginx nginx`                          | Assigns a custom name to the container.                                   |
|                          | `-p`                                          | `docker run -p 8080:80 nginx`                               | Maps a host port to a container port.                                     |
|                          | `-v`                                          | `docker run -v /host/path:/container/path nginx`            | Mounts a host directory as a volume.                                      |
|                          | `--rm`                                        | `docker run --rm nginx`                                     | Removes the container after it exits.                                     |
|                          | Combination                                   | `docker run -d --name web -p 8080:80 -v /data:/data nginx`  | Combines multiple flags for custom configuration.                           |
| `docker start`           | `-a`                                          | `docker start -a my_container`                              | Attaches to a container's stdout/stderr.                                  |
|                          | `-i`                                          | `docker start -ai my_container`                             | Attach and keep stdin open.                                               |
|                          |                                               | `docker start my_container`                                 | Starts a stopped container without attaching.                             |
| `docker stop`            | `-t`                                          | `docker stop -t 10 my_container`                            | Graceful stop with a timeout period.                                      |
|                          |                                               | `docker stop my_container`                                  | Stops a running container immediately.                                    |
| `docker restart`         |                                               | `docker restart my_container`                               | Restarts a running container.                                             |
| `docker pause`           |                                               | `docker pause my_container`                                 | Pauses all processes within the container.                                |
| `docker unpause`         |                                               | `docker unpause my_container`                               | Resumes all processes within the container.                               |
| `docker kill`            | `-s`                                          | `docker kill -s SIGTERM my_container`                       | Sends a specified signal to the container's main process.                  |
|                          |                                               | `docker kill my_container`                                  | Sends a SIGKILL to terminate the container immediately.                   |
| `docker rm`              | `-f`                                          | `docker rm -f my_container`                                 | Forces removal of a running container.                                    |
|                          | `-v`                                          | `docker rm -v my_container`                                 | Removes associated volumes with the container.                            |
|                          | Combination                                   | `docker rm -f -v my_container`                              | Combines flags to force removal and delete volumes together.               |
| `docker exec`            | `-i`                                          | `docker exec -i my_container ls`                            | Keeps STDIN open for the command.                                         |
|                          | `-t`                                          | `docker exec -it my_container bash`                         | Allocates a TTY for interactive commands.                                 |
|                          | `--user`                                      | `docker exec --user root my_container whoami`               | Runs the command as a specified user.                                      |
|                          | Combination                                   | `docker exec -it --user=root my_container bash`             | Combines flags for interactive root shell access.                          |
| `docker ps`              | `-a`                                          | `docker ps -a`                                              | Shows all containers, not just running ones.                              |
|                          | `-q`                                          | `docker ps -q`                                              | Displays only container IDs.                                              |
|                          | `--filter`                                     | `docker ps --filter "status=exited"`                         | Filters containers by status or other criteria.                           |
|                          | Combination                                   | `docker ps -aq --filter "name=my_container"`                 | Combines flags to show all IDs of containers with a specific name filter.    |
| `docker inspect`         | `--format`                                    | `docker inspect --format='{{.State.Running}}' my_container` | Formats output to show specific information.                               |
|                          |                                               | `docker inspect my_container`                               | Displays detailed information on the container.                           |
| `docker logs`            | `-f`                                          | `docker logs -f my_container`                               | Follows log output in real-time.                                          |
|                          | `--tail`                                      | `docker logs --tail 100 my_container`                       | Shows the last few lines of logs.                                         |
|                          | `--since`                                     | `docker logs --since 10m my_container`                      | Shows logs since a particular point in time.                              |
|                          | Combination                                   | `docker logs -f --tail 50 my_container`                     | Combines following and tailing logs for recent updates.                   |
| `docker attach`          |                                               | `docker attach my_container`                                | Attaches the terminal to a running container's main process.              |
| `docker rename`          |                                               | `docker rename old_name new_name`                           | Changes the name of a container.                                          |
| `docker commit`          | `-m`                                          | `docker commit -m "Added features" my_container my_image`   | Creates a new image from a container's state.                             |
| `docker cp`              |                                               | `docker cp my_container:/path/file /local/path`              | Copies files between a container and the local filesystem.                  |
| `docker top`             |                                               | `docker top my_container`                                   | Lists the processes running inside a container.                           |
| `docker stats`           | `--no-stream`, `--format`                     | `docker stats --no-stream`                                  | Shows live container metrics without streaming.                           |
| `docker port`            |                                               | `docker port my_container`                                  | Lists the port mappings for a container.                                  |
| `docker update`          | Various resource flags (e.g., `--cpu-shares`)  | `docker update --memory=512m my_container`                  | Adjusts resource limits for running containers.                           |
| `docker events`          | `--since`, `--until`, `--filter`               | `docker events --since "2h"`                                | Monitors real-time events with optional filters.                           |
| `docker export`          |                                               | `docker export my_container > my_container.tar`             | Exports a container's filesystem as a tar archive.                         |
| `docker wait`            |                                               | `docker wait my_container`                                  | Blocks until a container stops and then prints its exit code.             |
| `docker diff`            |                                               | `docker diff my_container`                                  | Shows changes to files in a container.                                     |
| `docker container prune` |                                               | `docker container prune`                                    | Removes all stopped containers and reclaims space.                        |

---
**Q: How to create a container in docker?**

**A:**

***Command***

```bash
docker run nginx:latest
```

***Command Breakdown***

1. `docker` : command-line tool
2. `run` : subcommand to create a new container
3. `nginx` : Official docker image for Apache HTTP server
4. `:` : separator for image name and tag. If tag is not specified, no need to add this.
5. `latest` : Specific tag/version of `nginx` image to use. If not specified, it looks for latest tag. Here

***Output***

```bash
➜  notes git:(main) ✗ docker run nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
14c9d9d19932: Already exists
f762eecbb827: Pull complete
df13dff4bd61: Pull complete
f2f80f7905b1: Pull complete
5c3c75dd029a: Pull complete
c76a82628c82: Pull complete
9fddfc3157f2: Pull complete
Digest: sha256:b5d3f3e104699f0768e5ca8626914c16e52647943c65274d8a9e63072bd015bb
Status: Downloaded newer image for nginx:latest
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/10/02 10:51:57 [notice] 1#1: using the "epoll" event method
2024/10/02 10:51:57 [notice] 1#1: nginx/1.27.1
2024/10/02 10:51:57 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14)
2024/10/02 10:51:57 [notice] 1#1: OS: Linux 6.10.4-linuxkit
2024/10/02 10:51:57 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/10/02 10:51:57 [notice] 1#1: start worker processes
2024/10/02 10:51:57 [notice] 1#1: start worker process 29
2024/10/02 10:51:57 [notice] 1#1: start worker process 30
2024/10/02 10:51:57 [notice] 1#1: start worker process 31
2024/10/02 10:51:57 [notice] 1#1: start worker process 32
2024/10/02 10:51:57 [notice] 1#1: start worker process 33
2024/10/02 10:51:57 [notice] 1#1: start worker process 34
2024/10/02 10:51:57 [notice] 1#1: start worker process 35
2024/10/02 10:51:57 [notice] 1#1: start worker process 36
2024/10/02 10:51:57 [notice] 1#1: start worker process 37
2024/10/02 10:51:57 [notice] 1#1: start worker process 38
2024/10/02 10:51:57 [notice] 1#1: start worker process 39
2024/10/02 10:51:57 [notice] 1#1: start worker process 40
```

***What happens***

- Docker will download the `nginx` image if it is not already present. If a tag/version is not provided, it defaults to the `latest` version. You can specify a tag/version by suffixing `:` to the image name, as shown in command.

- Docker  will create a new container from the downloaded image
- Docker will start the container and run the `nginx` server

---

**Q: How to verify whether a container is running in docker?**

**A:**

***Command***

```bash
docker ps
```

**Command Breakdown**

1. `docker` : Docker command-line tool.
2. `ps` : Stands for "process status," used to list running containers.

**Output**

```bash
➜  notes git:(main) ✗ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS     NAMES
a6a420648dcb   nginx     "/docker-entrypoint.…"   14 seconds ago   Up 14 seconds   80/tcp    wizardly_elion
```

**Common Columns in Output**

`CONTAINER ID`: Unique identifier for the container.

`IMAGE`: The name of the image used to create the container.

`COMMAND`: The command the container is running.

`CREATED`: Time since the container was created.

`STATUS`: The current status of the container (e.g., Up, Exited).

`PORTS`: Port mappings for the container.

`NAMES`: Human-readable names assigned to the container.

---

**Q: How to stop a running container in Docker?**

**A:**

***Command***

```bash
docker stop <container_id/container_name>
```

***Command Breakdown***

1. `docker` : command-line tool.
2. `stop` : subcommand to stop a running container.
3. `<container_id/container_name>` : id/name of the container as shown in `docker ps` command

***output***
returns the container id / name used in command if container exists and stopped.

```bash
<container_id/container_name>
```

If container doesn't exist with provided name/id, you will get this output

```bash
Error response from daemon: No such container: <container_id/container_name>
```

---

**Q: How to run a container in background/detached?**

**A:**

***Command***

```bash
docker run -d nginx:latest
```

***Command Breakdown***

1. `docker`: The Docker command-line tool.
2. `run`: Subcommand to create and start a new container.
3. `-d`: Option to run the container in detached mode (in the background).
4. `nginx`: Official Docker image for the NGINX web server.
5. `:`: Separator for image name and tag. If tag is not specified, `latest` is assumed.
6. `latest`: Specific tag/version of the `nginx` image to use. If not specified, Docker will default to the `latest` tag.

---

**Q: How to add a name to a Docker container for better identification?**

**A:**

***Command***

```bash
docker run --name web -d nginx:latest
```

***Command Breakdown***

1. `docker`: The Docker command-line tool.
2. `run`: Subcommand to create and start a new container.
3. `--name web`: name for the container
4. `nginx`: Official Docker image for the NGINX web server.
5. `:`: Separator for image name and tag. If tag is not specified, `latest` is assumed.
6. `latest`: Specific tag/version of the `nginx` image to use. If not specified, Docker will default to the `latest` tag.

***NOTE***:
No two containers can have same name

---

**Q: How to run an interactive container?**

**A:**

***Command***

```bash
docker run --interactive --tty --name web_test <container_id_or_name> /bin/sh
```

***Command Breakdown***

1. `docker`: The Docker command-line tool.
2. `run`: Subcommand to create and start a new container.
3. `--interactive` or `-i`: Keeps STDIN open to interact with the container.
4. `--tty` or `-t`: Allocates a pseudo-TTY, allowing for an interactive shell session.
5. `--name web_test`: Assigns the container the name `web_test` for easy identification.
6. `<container_id_or_name>`: id/name of the container in which you want to run the command
7. `/bin/sh`: Command to run a shell inside the container.

***Description***
The command uses --interactive and --tty flags with docker run to keep stdin open and allocate a virtual terminal, enabling interactive use of command-line programs like a shell inside the container.

***NOTE***:

`-it` is a short form of the above two commands.

---

**Q: How to view logs from a Docker container?**

**A:**
***Command***

```bash
docker logs <container_id_or_name>
```

***Command Breakdown***

1. `docker`: The Docker command-line tool.
2. `logs`: Subcommand to retrieve the logs of a specific container.
3. `<container_id_or_name>`: The identifier or name of the container whose logs you want to view.

---

**Q: How to automatically restart a container?**

**A:**

Using the --restart flag at container-creation time, you can tell Docker to do any of the following:

- Never restart (default)
- Attempt to restart when a failure is detected
- Attempt for some predetermined time to restart when a failure is detected
- Always restart the container regardless of the condition

Docker uses an exponential backoff strategy for timing restart attempts

***Command***

```bash
docker run --restart <policy> <image>
```

***Command Breakdown***

1. `docker`: The Docker command-line tool.
2. `run`: Subcommand to create and start a new container.
3. `--restart`: Option to specify the restart policy for the container.
4. `<policy>`: The restart policy to apply, which can be:
   - `no`: Do not automatically restart the container (default).
   - `always`: Always restart the container if it stops.
   - `unless-stopped`: Restart the container unless it has been stopped manually.
   - `on-failure[:max-retries]`: Restart the container only on failure, with an optional limit on the number of retries.
5. `<image>`: The name of the Docker image from which to create the container.

---

**Q: How to remove a container?**

**A:**
***Command***

```bash
docker rm <container_id_or_name>
```

***Command Breakdown***

1. `docker`: The Docker command-line tool.
2. `rm`: Subcommand to remove a container.
3. `<container_id_or_name>`: The identifier or name of the container you want to remove. Note that the container must be stopped before it can be removed.

---

**Q: How to remove all stopped containers in Docker?**
**A:**

***Command***

```bash
docker container prune
```

***Command Breakdown***

1. `docker`: The Docker command-line tool.
2. `container prune`: Subcommand to remove all stopped containers.

---

**Q: How to remove short-lived containers automatically in Docker?**

**A:**
***Command***
  
  ```bash
  docker run --rm <image>
  ```

***Command Breakdown***

1. `docker`: The Docker command-line tool.
2. `run`: Subcommand to create and start a new container.
3. `--rm`: Option to automatically remove the container when it exits.
4. `<image>`: The name of the Docker image from which to create the container.

--- 