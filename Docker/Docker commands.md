Here is a tabulated and easy-to-understand summary of Docker commands from basic to advanced levels, including descriptions and examples

| Command                         | Description                                         | Example                                     |
|---------------------------------|-----------------------------------------------------|---------------------------------------------|
| **Basic Commands**               |                                                     |                                             |
| `docker run <image>`            | Run a container from an image                       | `docker run hello-world`                     |
| `docker ps`                    | List running containers                             | `docker ps`                                  |
| `docker ps -a`                 | List all containers (running and stopped)          | `docker ps -a`                               |
| `docker stop <container_id>`   | Stop a running container                            | `docker stop 3a5f1b2c`                       |
| `docker start <container_id>`  | Start a stopped container                           | `docker start 3a5f1b2c`                      |
| `docker rm <container_id>`     | Remove a stopped container                          | `docker rm 3a5f1b2c`                         |
| `docker images`                | List local Docker images                            | `docker images`                              |
| `docker rmi <image_id>`        | Remove a Docker image                               | `docker rmi hello-world`                      |
| `docker pull <image>`          | Pull an image from Docker Hub                       | `docker pull nginx`                          |
| `docker logs <container_id>`   | View logs from a container                          | `docker logs 3a5f1b2c`                       |
| **Intermediate Commands**       |                                                     |                                             |
| `docker exec -it <container_id> bash` | Open bash shell inside a running container         | `docker exec -it mycontainer bash`           |
| `docker build -t <image_name> .` | Build an image from Dockerfile in current directory| `docker build -t myapp:v1 .`                 |
| `docker inspect <id>`          | Get detailed info about container/image             | `docker inspect mycontainer`                 |
| `docker cp <src> <cont>:<dest>`| Copy file from host to container                     | `docker cp config.json mycontainer:/app/`   |
| `docker volume create <name>`  | Create a named Docker volume                        | `docker volume create mydata`                |
| `docker volume ls`             | List all volumes                                   | `docker volume ls`                           |
| `docker volume rm <name>`      | Remove a Docker volume                             | `docker volume rm mydata`                    |
| `docker network ls`            | List Docker networks                               | `docker network ls`                          |
| `docker network create <name>` | Create a Docker network                            | `docker network create mynet`                |
| `docker run -p <host>:<cont>` | Map host port to container port                    | `docker run -p 8080:80 nginx`                 |
| **Advanced Commands**           |                                                     |                                             |
| `docker run -dit --name <name> -p <host>:<cont> -v <host_path>:<cont_path> <image>` | Run container detached with name, ports and volume | `docker run -dit --name web -p 8080:80 -v /host/www:/usr/share/nginx/html nginx` |
| `docker image prune -f`        | Remove dangling images                             | `docker image prune -f`                      |
| `docker container prune -f`    | Remove stopped containers                          | `docker container prune -f`                  |
| `docker system prune -f`       | Clean all unused data (containers, images, volumes)| `docker system prune -f`                     |
| `docker commit <cont_id> <img_name>` | Create image from container state                    | `docker commit 3a5f1b2c mycustomimage:v1`   |
| `docker network connect <net> <cont>` | Connect a running container to a network             | `docker network connect mynet mycontainer`  |
| `docker stats`                | Show container resource usage                      | `docker stats`                              |
| **Docker Swarm Commands**       |                                                     |                                             |
| `docker swarm init`            | Initialize Docker swarm                            | `docker swarm init`                          |
| `docker service create`        | Create and run a service in the swarm             | `docker service create --name web nginx`    |
| `docker stack deploy`          | Deploy a stack using a Compose file                | `docker stack deploy -c docker-compose.yml mystack` |

This table organizes Docker commands by skill level with clear explanations and usage examples, providing a helpful quick reference for learners and professionals alike.
[1](https://docs.docker.com/get-started/docker_cheatsheet.pdf)
[2](https://dockerlabs.collabnix.com/docker/cheatsheet/)
[3](https://spacelift.io/blog/docker-commands-cheat-sheet)
[4](https://www.geeksforgeeks.org/devops/docker-cheat-sheet/)
[5](https://collabnix.com/docker-cheatsheet/)
[6](https://github.com/sudheerj/docker-cheat-sheet)
[7](https://help.metricinsights.com/m/Deployment_and_Configuration/l/1500924-docker-commands-cheat-sheet-simple-install-single-server-non-orchestrated)
[8](https://www.jrebel.com/blog/docker-commands-cheat-sheet)
