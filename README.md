# **Getting Started with Docker**

## **Running Containers**
- `docker run <image>` → Runs a new container from an image.
- `docker ps` → Lists running containers.
- `docker ps -a` → Lists all containers, including stopped ones.
- `docker rm <container_name>` → Removes a container.

## **Useful Parameters with `docker run`**

### **Execution Modes**
- `-i` → Keeps the container’s input open (interactive mode).
- `-t` → Enables a TTY (terminal).
- `-it` → Combines `-i` and `-t`, allowing interaction with the container’s terminal.
- `-d` → Runs the container in detached mode (background process).
- `--name <container_name>` → Assigns a name to the container.
- `-v <host_path>:<container_path>` → Mounts a volume to the container (deprecated in favor of `--mount`).
  - If the directory does not exist on the host, `-v` will create it automatically.
- `--mount type=<type>,source=<source>,target=<target>` → Creates a volume or bind mount (preferred over `-v`).
  - If the specified directory does not exist on the host, the command **will fail** instead of creating it automatically.

### **Lifecycle Management**
- `--rm` → Automatically removes the container after execution.

### **Networking Configuration**
- `-p <host_port>:<container_port>` → Maps a port from the host to the container.
  - **Example:** `-p 8080:80` → Maps **host port 8080** to **container port 80**.

## **Volumes**
- `docker volume create <name>` → Creates a named volume in Docker.  
  - Volumes differ from bind mounts as they can be shared across multiple containers, have names, and support different storage drivers.

## **Commands**
- `docker exec <container_name> <command>` → Executes a command inside the container.

## **Examples**
```bash
# Run an Ubuntu container with interactive bash
docker run -it ubuntu bash

# Run an Nginx container
docker run nginx

# Run Nginx in detached mode with port mapping
docker run -d -p 8080:80 nginx 

# Execute bash inside a running container
docker exec -it 0ea7c73408ec bash

# Run Nginx with a bind mount (Windows path example)
docker run -d --name nginx -p 8080:80 -v "F:/cursos/Docker/2. Docker:/usr/share/nginx/html" nginx

# Run Nginx using the --mount option (preferred)
docker run -d --name nginx -p 8080:80 --mount type=bind,source="$(pwd)",target=/usr/share/nginx/html nginx
```