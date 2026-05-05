# UNIT I — Basics of DevOps Infrastructure

This file contains Docker and DevOps commands from Unit I topics:
- Introduction to containers
- Container runtime
- Docker introduction
- Docker architecture
- Docker CLI
- Docker daemon
- Docker Hub / registry
- Docker object types: image, container, network, volume
- Basic container lifecycle commands

---

## 1. Check Docker Version

```bash
docker --version
```

**Use:** Shows the installed Docker version.

Example output:
```bash
Docker version 18.09.6, build 481bc77
```

---

## 2. Docker System Information

```bash
docker info
```

**Use:** Shows detailed information about Docker installed on the system.

It displays:
- Number of containers
- Running containers
- Paused containers
- Stopped containers
- Number of images
- Docker server version
- Storage driver
- Logging driver

Example output:
```bash
Containers: 3
Running: 1
Paused: 0
Stopped: 2
Images: 3
Server Version: 18.09.6
Storage Driver: overlay2
```

---

## 3. Pull Image from Docker Hub

```bash
docker pull httpd
```

**Use:** Downloads the Apache HTTP Server image from Docker Hub.

Another example:
```bash
docker pull nginx
```

**Use:** Downloads the NGINX image from Docker Hub.

Another example:
```bash
docker pull ubuntu
```

**Use:** Downloads Ubuntu image.

Another example:
```bash
docker pull mysql:8
```

**Use:** Downloads MySQL version 8 image.

Another example:
```bash
docker pull mongo
```

**Use:** Downloads MongoDB image.

---

## 4. List Docker Images

```bash
docker images
```

**Use:** Lists all Docker images available on the local system.

It shows:
- Repository
- Tag
- Image ID
- Created date
- Size

---

## 5. Check Image History / Layers

```bash
docker history httpd
```

**Use:** Shows the history and layers of the `httpd` image.

Another example:
```bash
docker history nginx
```

**Use:** Shows layers of the `nginx` image.

---

## 6. Run a Container

```bash
docker run httpd
```

**Use:** Creates and starts a container from the `httpd` image.

Syntax:
```bash
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

Meaning:
- `OPTIONS` = extra settings such as port, name, volume, environment variable
- `IMAGE` = image name
- `COMMAND` = command to execute inside the container
- `ARG` = arguments for command

---

## 7. Run Container and Execute a Command

```bash
docker run httpd echo "Hello, World!"
```

**Use:** Runs a container from `httpd` image and prints `Hello, World!`.

---

## 8. Run Container with a Specific Name

```bash
docker run --name my-container httpd echo "Hello, World!"
```

**Use:** Runs a container with the name `my-container`.

Explanation:
- `--name` gives a name to the container
- `my-container` is the container name
- `httpd` is the image
- `echo "Hello, World!"` is the command executed inside container

---

## 9. Run Container in Interactive Mode

```bash
docker run -it ubuntu bash
```

**Use:** Starts Ubuntu container and opens an interactive terminal.

Explanation:
- `-i` keeps input open
- `-t` gives terminal access
- `bash` opens shell inside container

---

## 10. Run Container in Detached Mode

```bash
docker run -d nginx
```

**Use:** Runs NGINX container in the background.

Another example:
```bash
docker run -it -d httpd
```

**Use:** Runs Apache HTTP Server container in background with interactive terminal enabled.

---

## 11. List Running Containers

```bash
docker ps
```

**Use:** Shows only currently running containers.

---

## 12. List All Containers

```bash
docker ps -a
```

**Use:** Shows all containers including running, stopped, and exited containers.

---

## 13. Start a Stopped Container

```bash
docker start <container_id_or_name>
```

**Use:** Starts a stopped container.

Example:
```bash
docker start my_container
```

---

## 14. Stop a Running Container

```bash
docker stop <container_id_or_name>
```

**Use:** Stops a running container safely.

Example:
```bash
docker stop my_container
```

---

## 15. Restart a Container

```bash
docker restart <container_id_or_name>
```

**Use:** Stops and starts the container again.

Example:
```bash
docker restart my_container
```

---

## 16. Pause a Container

```bash
docker pause <container_id_or_name>
```

**Use:** Pauses all processes inside the container.

Example:
```bash
docker pause my_container
```

---

## 17. Unpause a Container

```bash
docker unpause <container_id_or_name>
```

**Use:** Resumes a paused container.

Example:
```bash
docker unpause my_container
```

---

## 18. Kill a Container

```bash
docker kill <container_id_or_name>
```

**Use:** Forcefully stops a container.

Example:
```bash
docker kill my_container
```

---

## 19. Remove a Container

```bash
docker rm <container_id_or_name>
```

**Use:** Removes a stopped container.

Example:
```bash
docker rm my_container
```

Another example from PPT:
```bash
docker rm 9b6343d3b5a0
```

---

## 20. Remove All Stopped Containers

```bash
docker container prune
```

**Use:** Removes all stopped containers.

---

## 21. Remove Docker Image

```bash
docker rmi <image_id>
```

**Use:** Removes an image from local system.

Example:
```bash
docker rmi fce289e99eb9
```

---

## 22. Force Remove Docker Image

```bash
docker rmi -f <image_id>
```

**Use:** Forcefully removes image even if it is being used.

Example:
```bash
docker rmi -f 92fa43a2ff60503fdf250
```

---

## 23. Inspect a Container

```bash
docker inspect <container_id_or_name>
```

**Use:** Shows detailed low-level information about a container.

Example:
```bash
docker inspect mycontainer
```

---

## 24. Check Container Resource Usage

```bash
docker stats <container_id_or_name>
```

**Use:** Shows live CPU, memory, network, and disk usage of a container.

Example:
```bash
docker stats my_container
```

---

## 25. View Container Logs

```bash
docker logs <container_id_or_name>
```

**Use:** Shows logs generated by container.

Example:
```bash
docker logs college_portal
```

---

## 26. Follow Container Logs in Real Time

```bash
docker logs -f <container_id_or_name>
```

**Use:** Continuously shows live logs.

Example:
```bash
docker logs -f college_portal
```

---

## 27. Execute Command Inside Running Container

```bash
docker exec -it <container_id_or_name> bash
```

**Use:** Opens bash shell inside a running container.

Example:
```bash
docker exec -it mysql-test bash
```

Another example:
```bash
docker exec -it 09ca6feb6efc bash
```

---

## 28. Execute Environment Command Inside Container

```bash
docker exec -it <container_id_or_name> env
```

**Use:** Shows environment variables inside container.

Example:
```bash
docker exec -it 09ca6feb6efc env
```

---

## 29. Attach to Running Container

```bash
docker attach <container_id_or_name>
```

**Use:** Attaches your terminal to a running container.

Example:
```bash
docker attach <container_id>
```

---

## 30. Run NGINX with Port Mapping

```bash
docker run -p 8080:80 nginx
```

**Use:** Makes NGINX accessible from browser at `localhost:8080`.

Explanation:
- `8080` = host machine port
- `80` = container port

Flow:
```text
Browser → localhost:8080 → Docker Host → Container:80 → NGINX
```

---

## 31. Run NGINX without Port Mapping

```bash
docker run nginx
```

**Use:** Runs NGINX container but it will not be accessible from browser because no port is published.

---

## 32. Run Apache HTTP Server with Port Mapping

```bash
docker run -d --name my-apache -p 8080:80 httpd
```

**Use:** Runs Apache server in background and exposes it on port 8080.

---

## 33. Modify Apache Web Page Inside Container

```bash
docker exec -it my-apache bash -c "echo '<h1>Hello from Docker Apache!</h1>' > /usr/local/apache2/htdocs/index.html"
```

**Use:** Creates/updates the default HTML page inside Apache container.

---

## 34. Verify Web Page Using curl

```bash
curl http://localhost:8080
```

**Use:** Checks whether website is accessible from command line.

---

## 35. Stop Apache Container

```bash
docker stop my-apache
```

**Use:** Stops Apache container.

---

## 36. Remove Apache Container

```bash
docker rm my-apache
```

**Use:** Removes stopped Apache container.

---

## 37. Environment Variable in Container

```bash
docker run -e MY_VAR=value httpd env
```

**Use:** Starts container with environment variable `MY_VAR=value` and prints all environment variables.

---

## 38. Run Ubuntu with Environment Variable

```bash
docker run -it -e MY_NAME=Harpreet ubuntu bash
```

**Use:** Runs Ubuntu container with environment variable `MY_NAME`.

Inside container:
```bash
echo $MY_NAME
```

**Use:** Prints value of `MY_NAME`.

---

## 39. Multiple Environment Variables

```bash
docker run -e APP_ENV=production -e APP_VERSION=1.0 nginx
```

**Use:** Runs NGINX container with multiple environment variables.

---

## 40. MySQL Container with Environment Variables

```bash
docker run -d \
  -e MYSQL_ROOT_PASSWORD=root123 \
  -e MYSQL_DATABASE=college \
  -e MYSQL_USER=admin \
  -e MYSQL_PASSWORD=admin123 \
  mysql:8
```

**Use:** Runs MySQL 8 container with required database configuration.

Important:
Without these variables, MySQL container may fail to start.

---

## 41. Set Environment Variable on Linux Host

```bash
export APP_PORT=8080
```

**Use:** Creates environment variable on Ubuntu/Linux host.

Check variable:
```bash
echo $APP_PORT
```

---

## 42. Set Environment Variable on PowerShell Host

```powershell
$env:APP_PORT=8080
```

**Use:** Creates environment variable in Windows PowerShell.

Check variable:
```powershell
echo $env:APP_PORT
```

---

## 43. Pass Host Environment Variable to Container on Linux

```bash
docker run -e APP_PORT=$APP_PORT nginx env
```

**Use:** Passes host variable `APP_PORT` into container.

---

## 44. Pass Host Environment Variable to Container on PowerShell

```powershell
docker run -e APP_PORT=$env:APP_PORT nginx env
```

**Use:** Passes PowerShell environment variable into container.

---

## 45. Run Container with Environment Variable and Port

```bash
docker run -d -p 8080:80 -e APP_ENV=$APP_ENV nginx
```

**Use:** Runs NGINX with port mapping and host environment variable.

---

## 46. Use Environment File

Create `.env` file:
```env
DB_HOST=localhost
DB_USER=root
DB_PASS=secret
```

Run container:
```bash
docker run --env-file .env myapp
```

**Use:** Passes multiple environment variables from a file.

---

## 47. MySQL Container with Port Mapping

```bash
docker run -d -p 3307:3306 --name mysql-test -e MYSQL_ROOT_PASSWORD=root123 mysql
```

**Use:** Runs MySQL container.

Explanation:
- Host port `3307`
- Container port `3306`
- Root password is `root123`

Enter container:
```bash
docker exec -it mysql-test bash
```

Connect to MySQL inside container:
```bash
mysql -h 127.0.0.1 -P 3306 -u root -p
```

**Use:** Opens MySQL shell.

---

## 48. Practice Task: Run Ubuntu with Environment Variable

```bash
docker run -it -e COLLEGE=CSE ubuntu bash
```

**Use:** Runs Ubuntu container with `COLLEGE=CSE`.

Inside container:
```bash
echo $COLLEGE
```

**Use:** Shows value of `COLLEGE`.

Exit container:
```bash
exit
```

---

## 49. Run MongoDB Container Practice

```bash
docker pull mongo
```

**Use:** Pulls MongoDB image.

```bash
docker run -d --name DB-app -p 80:8082 mongo
```

**Use:** Runs MongoDB container named `DB-app` and maps host port 80 to container port 8082.

---

## 50. Run NGINX with Environment Variable and Port

```bash
docker run -it -e NGINX_PORT=8080 -p 8080:80 nginx
```

**Use:** Runs NGINX interactively with environment variable and port mapping.

---

## 51. Container Lifecycle Example

```bash
docker run -d -p 80:80 --name my_container nginx
```

**Use:** Creates and starts NGINX container named `my_container`.

```bash
docker start my_container
```

**Use:** Starts stopped container.

```bash
docker stop my_container
```

**Use:** Stops running container.

```bash
docker restart my_container
```

**Use:** Restarts container.

```bash
docker pause my_container
```

**Use:** Pauses container.

```bash
docker unpause my_container
```

**Use:** Unpauses container.

```bash
docker kill my_container
```

**Use:** Force stops container.

```bash
docker rm my_container
```

**Use:** Removes container.

```bash
docker container prune
```

**Use:** Removes all stopped containers.

---

## 52. Listing and Debugging Containers

```bash
docker ps
```

**Use:** Lists running containers.

```bash
docker ps -a
```

**Use:** Lists all containers.

```bash
docker inspect my_container
```

**Use:** Shows full details of container.

```bash
docker stats my_container
```

**Use:** Shows resource usage.

```bash
docker logs my_container
```

**Use:** Shows logs.

```bash
docker logs -f my_container
```

**Use:** Shows live logs.

---

# Summary of Unit I Commands

| Command | Use |
|---|---|
| `docker --version` | Check Docker version |
| `docker info` | Show Docker system details |
| `docker pull image` | Download image |
| `docker images` | List images |
| `docker run image` | Run container |
| `docker ps` | List running containers |
| `docker ps -a` | List all containers |
| `docker stop` | Stop container |
| `docker start` | Start container |
| `docker restart` | Restart container |
| `docker rm` | Remove container |
| `docker rmi` | Remove image |
| `docker exec` | Run command inside container |
| `docker logs` | View logs |
| `docker inspect` | Inspect container/image |
| `docker stats` | View resource usage |
