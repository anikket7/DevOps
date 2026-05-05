# Docker Commands Assignment

**Course:** INT332 - Basics of DevOps  
**Topic:** Docker, Containers, Images, Networking, Volumes, Dockerfile, Docker Compose

This file contains the Docker commands covered in the uploaded PPTs. Each command is written with a short explanation so it can be uploaded to GitHub as an assignment submission.

---

## 1. Docker Version and System Information

### Check Docker version
```bash
docker --version
```
**Use:** Shows the installed Docker version.

### Show Docker system information
```bash
docker info
```
**Use:** Displays detailed information such as number of containers, images, storage driver, kernel version, etc.

---

## 2. Docker Images

### Pull an image from Docker Hub
```bash
docker pull httpd
```
**Use:** Downloads the Apache HTTP Server image from Docker Hub.

```bash
docker pull nginx
```
**Use:** Downloads the NGINX web server image from Docker Hub.

```bash
docker pull mongo
```
**Use:** Downloads the MongoDB image.

```bash
docker pull mysql:8
```
**Use:** Downloads MySQL version 8 image.

```bash
docker pull ubuntu
```
**Use:** Downloads the Ubuntu image.

### List Docker images
```bash
docker images
```
**Use:** Lists all images available on the local system.

### Check image history
```bash
docker history httpd
```
**Use:** Shows image layers and commands used to build the image.

### Remove an image
```bash
docker rmi <image_id>
```
**Use:** Removes a Docker image by image ID.

### Force remove an image
```bash
docker rmi -f <image_id>
```
**Use:** Forcefully removes an image even if it is tagged or referenced.

---

## 3. Running Containers

### Basic docker run syntax
```bash
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```
**Use:** Creates and starts a new container from an image.

### Run Apache HTTPD container
```bash
docker run httpd
```
**Use:** Runs a container from the `httpd` image.

### Run a command inside a new container
```bash
docker run httpd echo "Hello, World!"
```
**Use:** Creates a container from `httpd` and runs the `echo` command.

### Run container with a specific name
```bash
docker run --name my-container httpd echo "Hello, World!"
```
**Use:** Runs a container with the name `my-container`.

### Run container in detached mode
```bash
docker run -d nginx
```
**Use:** Runs the container in the background.

### Run container interactively
```bash
docker run -it ubuntu bash
```
**Use:** Opens an interactive terminal inside an Ubuntu container.

### Run container interactively and in detached mode
```bash
docker run -it -d httpd
```
**Use:** Starts the container in background while keeping interactive mode enabled.

### Automatically remove container after exit
```bash
docker run --rm ubuntu echo "Temporary container"
```
**Use:** Removes the container automatically after it stops.

---

## 4. Port Mapping

### Syntax of port mapping
```bash
docker run -p <HOST_PORT>:<CONTAINER_PORT> IMAGE
```
**Use:** Maps a port on the host machine to a port inside the container.

### Run NGINX on host port 8080
```bash
docker run -p 8080:80 nginx
```
**Use:** Makes NGINX accessible at `http://localhost:8080`.

### Run Apache HTTPD on host port 8080
```bash
docker run -d --name my-apache -p 8080:80 httpd
```
**Use:** Runs Apache in background and exposes it on host port 8080.

### Run MongoDB container with port mapping example
```bash
docker run -d --name DB-app -p 80:8082 mongo
```
**Use:** Runs MongoDB container named `DB-app` and maps host port 80 to container port 8082.

### Run MySQL with port mapping
```bash
docker run -d -p 3307:3306 --name mysql-test -e MYSQL_ROOT_PASSWORD=root123 mysql
```
**Use:** Runs MySQL and maps host port 3307 to container port 3306.

---

## 5. Environment Variables

### Pass one environment variable
```bash
docker run -e MY_VAR=value httpd env
```
**Use:** Sets `MY_VAR=value` inside the container and displays environment variables.

### Run Ubuntu with environment variable
```bash
docker run -it -e MY_NAME=Harpreet ubuntu bash
```
**Use:** Opens Ubuntu container with `MY_NAME` variable set.

### Check environment variable inside container
```bash
echo $MY_NAME
```
**Use:** Displays the value of `MY_NAME` inside Linux shell.

### Pass multiple environment variables
```bash
docker run -e APP_ENV=production -e APP_VERSION=1.0 nginx
```
**Use:** Sets multiple environment variables inside the container.

### Run MySQL with required environment variables
```bash
docker run -d \
  -e MYSQL_ROOT_PASSWORD=root123 \
  -e MYSQL_DATABASE=college \
  -e MYSQL_USER=admin \
  -e MYSQL_PASSWORD=admin123 \
  mysql:8
```
**Use:** Runs MySQL container with required database configuration.

### Set environment variable on Ubuntu/Linux host
```bash
export APP_PORT=8080
```
**Use:** Creates an environment variable on the host system.

### Set environment variable in PowerShell
```powershell
$env:APP_PORT=8080
```
**Use:** Creates an environment variable in Windows PowerShell.

### Check host environment variable in PowerShell
```powershell
echo $env:APP_PORT
```
**Use:** Displays the value of the PowerShell environment variable.

### Pass host variable into container on Linux
```bash
docker run -e APP_PORT=$APP_PORT nginx env
```
**Use:** Passes host variable `APP_PORT` into the container.

### Pass host variable into container on PowerShell
```powershell
docker run -e APP_PORT=$env:APP_PORT nginx env
```
**Use:** Passes PowerShell environment variable into the container.

### Run NGINX with environment variable and port mapping
```bash
docker run -d -p 8080:80 -e APP_ENV=$APP_ENV nginx
```
**Use:** Runs NGINX with environment variable from host.

### Use an env file
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
**Use:** Loads multiple environment variables from a file.

---

## 6. Container Listing and Lifecycle Commands

### List running containers
```bash
docker ps
```
**Use:** Shows only running containers.

### List all containers
```bash
docker ps -a
```
**Use:** Shows running, stopped, and exited containers.

### Start a stopped container
```bash
docker start <container_id_or_name>
```
**Use:** Starts an existing stopped container.

### Stop a running container
```bash
docker stop <container_id_or_name>
```
**Use:** Stops a running container safely.

### Restart a container
```bash
docker restart <container_id_or_name>
```
**Use:** Stops and starts the container again.

### Pause a container
```bash
docker pause <container_id_or_name>
```
**Use:** Temporarily pauses all processes in a container.

### Unpause a container
```bash
docker unpause <container_id_or_name>
```
**Use:** Resumes a paused container.

### Kill a container
```bash
docker kill <container_id_or_name>
```
**Use:** Forcefully stops a running container.

### Remove a container
```bash
docker rm <container_id_or_name>
```
**Use:** Deletes a stopped container.

### Remove a running container forcefully
```bash
docker rm -f <container_id_or_name>
```
**Use:** Stops and removes a container forcefully.

### Remove all stopped containers
```bash
docker container prune
```
**Use:** Deletes all stopped containers.

---

## 7. Inspecting, Logs, and Monitoring

### Inspect a container
```bash
docker inspect <container_id_or_name>
```
**Use:** Shows detailed configuration and metadata of a container.

### Show container resource usage
```bash
docker stats <container_id_or_name>
```
**Use:** Displays live CPU, memory, network, and disk usage.

### View container logs
```bash
docker logs <container_id_or_name>
```
**Use:** Shows logs of a container.

### Follow logs in real time
```bash
docker logs -f <container_id_or_name>
```
**Use:** Continuously shows new log entries.

---

## 8. Executing Commands Inside Containers

### Enter a running container shell
```bash
docker exec -it <container_id_or_name> bash
```
**Use:** Opens bash shell inside a running container.

### Run environment command inside container
```bash
docker exec -it <container_id_or_name> env
```
**Use:** Displays environment variables inside the container.

### List root directory inside container
```bash
docker exec -it <container_id_or_name> ls /
```
**Use:** Lists files and folders in the root directory of the container.

### Attach to a running container
```bash
docker attach <container_id_or_name>
```
**Use:** Connects your terminal to the running container process.

---

## 9. Copying Files Between Host and Container

### Copy file from container to host
```bash
docker cp <container_id>:/data/test.txt C:\Users\HP\Desktop\
```
**Use:** Copies `test.txt` from container to Windows Desktop.

### Copy file from host to container
```bash
docker cp C:\Users\HP\Desktop\test.txt <container_id>:/data/sample.txt
```
**Use:** Copies a file from host Desktop into the container.

---

## 10. Apache HTTPD Web Page Example

### Pull Apache image
```bash
docker pull httpd
```
**Use:** Downloads Apache HTTPD image.

### Run Apache container
```bash
docker run -d --name my-apache -p 8080:80 httpd
```
**Use:** Runs Apache container accessible at `localhost:8080`.

### Create or update HTML page inside container
```bash
docker exec -it my-apache bash -c "echo '<h1>Hello from Docker Apache!</h1>' > /usr/local/apache2/htdocs/index.html"
```
**Use:** Replaces Apache homepage with custom HTML.

### Verify web page using curl
```bash
curl http://localhost:8080
```
**Use:** Checks the web page output from command line.

### Stop Apache container
```bash
docker stop my-apache
```
**Use:** Stops the Apache container.

### Remove Apache container
```bash
docker rm my-apache
```
**Use:** Removes the stopped Apache container.

---

## 11. Bind Mount Example

### Create local directory on Windows
```powershell
mkdir C:\app\data
```
**Use:** Creates a host directory to mount into the container.

### Run Ubuntu with bind mount and environment variable
```bash
docker run -it --name my_app -e APP_ENV=production -v C:\app\data:/data ubuntu /bin/bash
```
**Use:** Runs Ubuntu, sets environment variable, and mounts host folder into `/data`.

### Check environment variable
```bash
echo $APP_ENV
```
**Use:** Displays the value of `APP_ENV`.

### Create file in mounted folder
```bash
echo "Hello this is my first program" > /data/test.txt
```
**Use:** Creates a file inside `/data`, which is connected to the host folder.

### Read file
```bash
cat /data/test.txt
```
**Use:** Displays file content.

### Append text to file
```bash
echo "Second line added" >> /data/test.txt
```
**Use:** Adds another line to the existing file.

### Exit container shell
```bash
exit
```
**Use:** Leaves the container terminal.

---

## 12. Docker Volumes

### Create volume
```bash
docker volume create mydata
```
**Use:** Creates a Docker-managed volume.

### List volumes
```bash
docker volume ls
```
**Use:** Displays all Docker volumes.

### Inspect volume
```bash
docker volume inspect mydata
```
**Use:** Shows details such as mount point of the volume.

### Run container with volume
```bash
docker run -dit --name mycontainer -v mydata:/app/data ubuntu
```
**Use:** Runs Ubuntu container and attaches `mydata` volume to `/app/data`.

### Check mounted directory
```bash
docker exec -it mycontainer ls /app/data
```
**Use:** Lists files in the mounted volume path.

### Remove volume
```bash
docker volume rm mydata
```
**Use:** Deletes a Docker volume.

### Remove unused volumes
```bash
docker volume prune
```
**Use:** Removes unused Docker volumes.

---

## 13. Volume Persistence Example

### Create project volume
```bash
docker volume create projectdata
```
**Use:** Creates a volume named `projectdata`.

### Verify volume
```bash
docker volume ls
```
**Use:** Checks whether the volume was created.

### Inspect project volume
```bash
docker volume inspect projectdata
```
**Use:** Shows mount point and volume details.

### Run container with volume
```bash
docker run -dit --name project_container -v projectdata:/app/data ubuntu
```
**Use:** Runs Ubuntu container with volume mounted at `/app/data`.

### Create file in volume
```bash
docker exec -it project_container sh -c "echo 'This is my first volume' > /app/data/report.txt"
```
**Use:** Creates `report.txt` inside the volume.

### Verify file content
```bash
docker exec -it project_container cat /app/data/report.txt
```
**Use:** Displays the content of the file.

### Stop container
```bash
docker stop project_container
```
**Use:** Stops the container.

### Remove container
```bash
docker rm project_container
```
**Use:** Removes the stopped container.

### Run new container with same volume
```bash
docker run -dit --name project_container_new -v projectdata:/app/data ubuntu
```
**Use:** Starts a new container using the same volume.

### Check file still exists
```bash
docker exec -it project_container_new ls /app/data
```
**Use:** Verifies that volume data is still present.

### Read persisted file
```bash
docker exec -it project_container_new cat /app/data/report.txt
```
**Use:** Confirms that data persisted after removing the old container.

---

## 14. College Portal Task Using Apache

### Pull Apache image
```bash
docker pull httpd
```
**Use:** Downloads Apache image.

### Create portal volume
```bash
docker volume create portaldata
```
**Use:** Creates volume for website files.

### Run college portal container
```bash
docker run -dit --name college_portal -p 8080:80 -e ENV=production -v portaldata:/usr/local/apache2/htdocs httpd
```
**Use:** Runs Apache portal with volume, environment variable, and port mapping.

### Modify index.html
```bash
docker exec -it college_portal bash -c "echo '<h1>Welcome to University Portal - Production Mode</h1>' > /usr/local/apache2/htdocs/index.html"
```
**Use:** Creates custom homepage inside Apache web root.

### Verify output
```bash
curl http://localhost:8080
```
**Use:** Tests if the website is loading.

### Check logs
```bash
docker logs college_portal
```
**Use:** Checks container logs.

### Follow logs
```bash
docker logs -f college_portal
```
**Use:** Watches logs live.

### Stop container
```bash
docker stop college_portal
```
**Use:** Stops the portal container.

### Remove container
```bash
docker rm college_portal
```
**Use:** Removes the portal container.

### Remove volume
```bash
docker volume rm portaldata
```
**Use:** Deletes the portal volume.

### Remove Apache image
```bash
docker rmi httpd
```
**Use:** Deletes the Apache image.

---

## 15. MySQL Debug Task

### Pull MySQL image
```bash
docker pull mysql:8
```
**Use:** Downloads MySQL 8 image.

### Run MySQL container
```bash
docker run -d --name mysql_debug -p 3307:3306 -e MYSQL_ROOT_PASSWORD=root123 -e MYSQL_DATABASE=college -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin123 mysql:8
```
**Use:** Runs MySQL with required database environment variables.

### Check running container
```bash
docker ps
```
**Use:** Confirms MySQL container is running.

### Check logs
```bash
docker logs mysql_debug
```
**Use:** Finds startup errors.

### Follow MySQL logs
```bash
docker logs -f mysql_debug
```
**Use:** Watches MySQL logs continuously.

### Enter MySQL container
```bash
docker exec -it mysql_debug bash
```
**Use:** Opens shell inside MySQL container.

### Login to MySQL
```bash
mysql -u root -p
```
**Use:** Logs into MySQL as root. Enter password `root123`.

### Exit MySQL/container shell
```bash
exit
```
**Use:** Exits the shell.

### Stop MySQL container
```bash
docker stop mysql_debug
```
**Use:** Stops MySQL container.

### Remove MySQL container
```bash
docker rm mysql_debug
```
**Use:** Removes MySQL container.

---

## 16. Creating a Custom NGINX Image

### Create project folder
```bash
mkdir nginx-app
cd nginx-app
```
**Use:** Creates and enters a project directory.

### Create index.html
```bash
notepad index.html
```
**Use:** Creates an HTML file on Windows.

Example `index.html`:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Medium Level Docker App</title>
</head>
<body>
    <h1>Welcome to My Custom Docker Nginx App</h1>
    <p>This is a medium-level Docker project.</p>
</body>
</html>
```

### Create NGINX config file
```bash
notepad default.conf
```
**Use:** Creates custom NGINX configuration.

Example `default.conf`:
```nginx
server {
    listen 80;
    server_name localhost;

    location / {
        root /usr/share/nginx/html;
        index index.html;
    }
}
```

### Create Dockerfile
```bash
notepad Dockerfile
```
**Use:** Creates Dockerfile for custom NGINX image.

Dockerfile:
```Dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html
COPY default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
```

### Check files in directory
```bash
dir
```
**Use:** Lists files in Windows command prompt.

### Build custom image
```bash
docker build -t custom-nginx:v1 .
```
**Use:** Builds image named `custom-nginx` with tag `v1`.

### Run custom NGINX container
```bash
docker run -d -p 8080:80 --name nginx-container custom-nginx:v1
```
**Use:** Runs custom NGINX app on host port 8080.

### Open in browser
```text
http://localhost:8080
```
**Use:** Checks the custom NGINX website.

---

## 17. Creating a Node.js Docker Image

### Create Node app folder
```bash
mkdir node-app
cd node-app
```
**Use:** Creates and enters Node.js project directory.

### Update package list inside Linux system/container
```bash
apt update
```
**Use:** Updates package index.

### Install nano editor
```bash
apt install nano -y
```
**Use:** Installs nano text editor.

### Create app.js
```bash
nano app.js
```
**Use:** Creates Node.js application file.

Example `app.js`:
```javascript
const express = require("express");
const app = express();

app.get("/", (req, res) => {
  res.send("Docker Node App Running!");
});

app.listen(3000, "0.0.0.0", () => {
  console.log("Server running on port 3000");
});
```

### Create package.json
```bash
nano package.json
```
**Use:** Creates Node.js dependency file.

Example `package.json`:
```json
{
  "name": "node-docker-app",
  "version": "1.0.0",
  "main": "app.js",
  "dependencies": {
    "express": "^4.18.2"
  }
}
```

### Create Dockerfile
```bash
nano Dockerfile
```
**Use:** Creates Dockerfile for Node.js app.

Dockerfile:
```Dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package.json .
RUN npm install
COPY app.js .
EXPOSE 3000
CMD ["node", "app.js"]
```

### Build Node image
```bash
docker build -t node-demo:v1 .
```
**Use:** Builds custom Node.js image.

### Run Node container
```bash
docker run -d -p 3000:3000 --name node-container node-demo:v1
```
**Use:** Runs Node.js app on port 3000.

### Check running containers
```bash
docker ps
```
**Use:** Confirms Node container is running.

### Open in browser
```text
http://localhost:3000
```
**Use:** Checks output: `Docker Node App Running!`

---

## 18. Docker Networking

### List Docker networks
```bash
docker network ls
```
**Use:** Shows all Docker networks.

### Inspect default bridge network
```bash
docker network inspect bridge
```
**Use:** Displays details of the default bridge network.

### Create custom bridge network
```bash
docker network create my_bridge_net
```
**Use:** Creates a custom bridge network.

### Run NGINX container in custom network
```bash
docker run -d --name container1 --network my_bridge_net nginx
```
**Use:** Starts NGINX container connected to custom bridge network.

### Run Alpine container in custom network
```bash
docker run -d --name container2 --network my_bridge_net alpine sleep 300
```
**Use:** Starts Alpine container and keeps it running for 300 seconds.

### Test communication between containers
```bash
docker exec -it container2 ping container1
```
**Use:** Tests name-based communication between containers on same custom network.

### Run container using host network
```bash
docker run -d --network host nginx
```
**Use:** Runs NGINX using the host network stack. Mostly used on Linux.

### Test host network
```bash
curl http://localhost
```
**Use:** Checks NGINX running on host network.

---

## 19. Docker Overlay Network and Swarm

### Initialize Docker Swarm
```bash
docker swarm init
```
**Use:** Enables Docker Swarm mode.

### Create overlay network
```bash
docker network create -d overlay my_overlay
```
**Use:** Creates an overlay network for multi-host container communication.

### Create service on overlay network
```bash
docker service create --name web --network my_overlay -p 8080:80 nginx
```
**Use:** Deploys NGINX service using overlay network.

---

## 20. Docker DNS and Linking

### Create app network
```bash
docker network create app_net
```
**Use:** Creates a custom network.

### Run backend container
```bash
docker run -d --name backend --network app_net nginx
```
**Use:** Runs backend service on `app_net`.

### Run client container
```bash
docker run -it --name client --network app_net alpine sh
```
**Use:** Opens Alpine shell in same network.

### Ping backend by container name
```bash
ping backend
```
**Use:** Tests Docker DNS name resolution.

### Legacy linking example
```bash
docker run -d --name db nginx
```
**Use:** Runs a container named `db`.

```bash
docker run -it --name app --link db:database alpine sh
```
**Use:** Links `app` container to `db`. This is old/deprecated; custom networks are preferred.

---

## 21. More Volume and Bind Mount Commands

### Create volume
```bash
docker volume create my_volume
```
**Use:** Creates a Docker volume.

### List volumes
```bash
docker volume ls
```
**Use:** Lists Docker volumes.

### Run NGINX with volume
```bash
docker run -d \
  --name my_nginx \
  -v my_volume:/usr/share/nginx/html \
  nginx
```
**Use:** Mounts volume into NGINX web directory.

### Inspect volume
```bash
docker volume inspect my_volume
```
**Use:** Shows volume details.

### Remove volume
```bash
docker volume rm my_volume
```
**Use:** Deletes the volume.

### Bind mount current folder
```bash
docker run -d \
  -v $(pwd)/html:/usr/share/nginx/html \
  -p 8080:80 \
  nginx
```
**Use:** Mounts local `html` folder into NGINX container for development.

---

## 22. Complete Network + Volume Example

### Create bridge network
```bash
docker network create app_bridge
```
**Use:** Creates a network for application containers.

### List networks
```bash
docker network ls
```
**Use:** Verifies network creation.

### Create MySQL volume
```bash
docker volume create mysql_data
```
**Use:** Creates persistent storage for MySQL.

### Inspect MySQL volume
```bash
docker volume inspect mysql_data
```
**Use:** Displays MySQL volume details.

### Run MySQL database container
```bash
docker run -d --name mysql_db --network app_bridge -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=myapp -v mysql_data:/var/lib/mysql mysql:8
```
**Use:** Runs MySQL on custom network with persistent data.

### Run backend app container
```bash
docker run -d --name backend_app --network app_bridge -e DB_HOST=mysql_db node:18-alpine sh -c "apk add curl && sleep 300"
```
**Use:** Runs backend container connected to MySQL database.

### Test backend to database communication
```bash
docker exec -it backend_app ping mysql_db
```
**Use:** Checks if backend can reach MySQL by container name.

### Run frontend container
```bash
docker run -d --name frontend --network app_bridge -p 8080:80 nginx
```
**Use:** Runs frontend NGINX container on same network and exposes it on port 8080.

---

## 23. Docker Compose Commands

### Check Docker Compose version
```bash
docker-compose version
```
**Use:** Shows installed Docker Compose version.

### Validate Docker Compose YAML file
```bash
docker-compose config
```
**Use:** Checks syntax and final configuration of Compose file.

### Create Compose file on Windows
```bash
notepad docker-compose.yml
```
**Use:** Creates Docker Compose YAML file.

Example `docker-compose.yml`:
```yaml
version: "3.9"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
```

### Start services in foreground
```bash
docker-compose up
```
**Use:** Starts all services and shows logs in terminal.

### Start services in detached mode
```bash
docker-compose up -d
```
**Use:** Starts all services in background.

### Start and rebuild images
```bash
docker-compose up --build
```
**Use:** Rebuilds images before starting services.

### Stop and remove Compose containers and networks
```bash
docker-compose down
```
**Use:** Stops and removes Compose-created containers and networks.

### Stop services without removing
```bash
docker-compose stop
```
**Use:** Stops Compose services.

### Start stopped services
```bash
docker-compose start
```
**Use:** Restarts previously stopped services.

### List Compose services/containers
```bash
docker-compose ps
```
**Use:** Shows running services in the Compose project.

### View Compose logs
```bash
docker-compose logs
```
**Use:** Shows logs of Compose services.

### Follow Compose logs
```bash
docker-compose logs -f
```
**Use:** Watches Compose logs live.

### Execute command inside Compose service
```bash
docker-compose exec <service> bash
```
**Use:** Opens shell inside a running Compose service container.

### Scale service
```bash
docker-compose up --scale web=3
```
**Use:** Runs 3 instances of the `web` service.

---

## 24. Docker Compose: Node.js with MongoDB

Create `docker-compose.yml`:
```yaml
version: '3.8'
services:
  app:
    image: node:18
    container_name: node-app
    working_dir: /usr/src/app
    volumes:
      - .:/usr/src/app
    command: npm start
    ports:
      - "3000:3000"
    environment:
      - MONGO_URL=mongodb://mongo:27017/mydb
    depends_on:
      - mongo

  mongo:
    image: mongo:6
    container_name: mongo-db
    ports:
      - "27017:27017"
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:
```

### Start services
```bash
docker compose up -d
```
**Use:** Starts Node.js and MongoDB containers in background.

### Check services
```bash
docker compose ps
```
**Use:** Lists running Compose services.

### Check app logs
```bash
docker compose logs app
```
**Use:** Shows logs of the Node.js app service.

### Stop and remove services
```bash
docker compose down
```
**Use:** Stops and removes containers/networks created by Compose.

---

## 25. Docker Compose: WordPress with MySQL

Create `docker-compose.yml`:
```yaml
version: '3.8'

services:
  wordpress:
    image: wordpress:latest
    container_name: wordpress-app
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wppass
      WORDPRESS_DB_NAME: wpdb
    depends_on:
      - db

  db:
    image: mysql:5.7
    container_name: mysql-db
    restart: always
    environment:
      MYSQL_DATABASE: wpdb
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: wppass
      MYSQL_ROOT_PASSWORD: rootpass
    volumes:
      - db-data:/var/lib/mysql

volumes:
  db-data:
```

### Start WordPress project
```bash
docker compose up -d
```
**Use:** Starts WordPress and MySQL containers.

### Open WordPress
```text
http://localhost:8080
```
**Use:** Opens WordPress website in browser.

### Stop project
```bash
docker compose down
```
**Use:** Stops and removes Compose containers and network.

---

## 26. Useful GitHub Upload Commands

Use these commands after creating your GitHub repository.

### Initialize Git
```bash
git init
```
**Use:** Starts a Git repository in your project folder.

### Add README file
```bash
git add README.md
```
**Use:** Stages the README file.

### Commit changes
```bash
git commit -m "Add Docker commands assignment"
```
**Use:** Saves changes locally with a message.

### Add GitHub remote repository
```bash
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
```
**Use:** Connects local folder with GitHub repository.

### Rename branch to main
```bash
git branch -M main
```
**Use:** Sets branch name to `main`.

### Push to GitHub
```bash
git push -u origin main
```
**Use:** Uploads files to GitHub.

---

## 27. Short Theory Notes

### What is Docker?
Docker is a tool used to create, run, and manage containers.

### What is a Container?
A container is a lightweight isolated environment that contains an application and its dependencies.

### What is an Image?
An image is a read-only blueprint used to create containers.

### What is NGINX?
NGINX is a web server. It is used to serve websites and web pages to users.

### What is Apache HTTPD?
Apache HTTPD is also a web server used to host websites.

### What is a Volume?
A volume is Docker-managed storage used to keep data even after a container is deleted.

### What is Port Mapping?
Port mapping connects a host machine port to a container port. Example: `8080:80` means host port 8080 connects to container port 80.

### What is Docker Compose?
Docker Compose is a tool used to run multiple containers using one YAML file.

### What is a Registry?
A registry stores Docker images. Docker Hub is a public image registry.

---

## 28. Conclusion

This assignment covers the major Docker commands used for:

- Pulling and managing images
- Running containers
- Passing environment variables
- Mapping ports
- Managing volumes
- Inspecting logs
- Creating custom images using Dockerfile
- Docker networking
- Docker Compose for multi-container applications
- Uploading the assignment to GitHub

