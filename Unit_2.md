# UNIT II — Image Building & Container Management

This file contains Docker commands from Unit II topics:
- Dockerfile core concepts
- Image layering
- Build context and `.dockerignore`
- Dockerfile writing
- Image creation
- Image tagging/versioning
- Inspecting images
- Docker networking
- Docker storage
- Volumes and bind mounts
- Copy-on-write
- Registries: Docker Hub, GHCR, private registries
- Docker Compose commands from PPT

---

# 1. Dockerfile Core Concepts

A Dockerfile is used to create a custom Docker image.

Common Dockerfile instructions:
- `FROM`
- `RUN`
- `COPY`
- `ADD`
- `CMD`
- `ENTRYPOINT`
- `WORKDIR`
- `ENV`
- `EXPOSE`
- `VOLUME`

---

## 1.1 Create NGINX App Folder

```bash
mkdir nginx-app
```

**Use:** Creates folder for NGINX project.

```bash
cd nginx-app
```

**Use:** Enters the project folder.

---

## 1.2 Create HTML File

Windows:
```bash
notepad index.html
```

**Use:** Opens Notepad to create `index.html`.

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

---

## 1.3 Create NGINX Configuration File

```bash
notepad default.conf
```

**Use:** Creates NGINX configuration file.

Example:
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

---

## 1.4 Create Dockerfile for NGINX

```bash
notepad Dockerfile
```

**Use:** Creates Dockerfile.

Dockerfile:
```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html
COPY default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
```

Explanation:
- `FROM nginx:alpine` = uses lightweight NGINX image
- `COPY` = copies files into image
- `EXPOSE 80` = container listens on port 80

---

## 1.5 Check Project Files

Windows:
```bash
dir
```

Linux/macOS:
```bash
ls
```

**Use:** Shows files in current folder.

---

## 1.6 Build Custom NGINX Image

```bash
docker build -t custom-nginx:v1 .
```

**Use:** Builds Docker image with name `custom-nginx` and tag `v1`.

Explanation:
- `-t` = tag/name image
- `custom-nginx:v1` = image name and version
- `.` = current folder is build context

---

## 1.7 Run Custom NGINX Image

```bash
docker run -d -p 8080:80 --name nginx-container custom-nginx:v1
```

**Use:** Runs custom NGINX container.

Open in browser:
```text
http://localhost:8080
```

---

# 2. Node.js Docker Image Creation

## 2.1 Create Node App Folder

```bash
mkdir node-app
```

**Use:** Creates Node project folder.

```bash
cd node-app
```

**Use:** Enters Node project folder.

---

## 2.2 Install Nano in Ubuntu

```bash
apt update
```

**Use:** Updates package list.

```bash
apt install nano -y
```

**Use:** Installs nano editor.

---

## 2.3 Create app.js

```bash
nano app.js
```

**Use:** Creates/edits Node.js application file.

Example:
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

---

## 2.4 Create package.json

```bash
nano package.json
```

**Use:** Creates Node package file.

Example:
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

---

## 2.5 Create Dockerfile for Node.js

```bash
nano Dockerfile
```

Dockerfile:
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package.json .
RUN npm install
COPY app.js .
EXPOSE 3000
CMD ["node", "app.js"]
```

Explanation:
- `FROM node:18-alpine` = base image
- `WORKDIR /app` = working directory
- `COPY package.json .` = copy dependency file
- `RUN npm install` = install dependencies
- `COPY app.js .` = copy app code
- `EXPOSE 3000` = container port
- `CMD ["node", "app.js"]` = command to start app

---

## 2.6 Rename Dockerfile if Saved as Text File

PowerShell:
```powershell
Rename-Item Dockerfile.txt Dockerfile
```

**Use:** Renames `Dockerfile.txt` to `Dockerfile`.

---

## 2.7 Build Node.js Image

```bash
docker build -t node-demo:v1 .
```

**Use:** Builds Node.js custom image.

---

## 2.8 Run Node.js Container

```bash
docker run -d -p 3000:3000 --name node-container node-demo:v1
```

**Use:** Runs Node.js app container.

---

## 2.9 Check Running Containers

```bash
docker ps
```

**Use:** Confirms that Node container is running.

Open browser:
```text
http://localhost:3000
```

Expected output:
```text
Docker Node App Running!
```

---

# 3. Image Tagging / Versioning

```bash
docker build -t myapp:v1 .
```

**Use:** Builds image with version tag `v1`.

```bash
docker tag myapp:v1 myapp:v2
```

**Use:** Creates another tag/version for same image.

---

# 4. Inspecting Images

```bash
docker history httpd
```

**Use:** Shows image layer history.

```bash
docker history nginx
```

**Use:** Shows NGINX image layers.

```bash
docker images
```

**Use:** Lists all images with image ID, tag, and size.

---

# 5. Docker Networking

Docker networking allows containers to communicate with each other.

---

## 5.1 List Docker Networks

```bash
docker network ls
```

**Use:** Lists all Docker networks.

---

## 5.2 Inspect Default Bridge Network

```bash
docker network inspect bridge
```

**Use:** Shows details of default bridge network.

---

## 5.3 Create Custom Bridge Network

```bash
docker network create my_bridge_net
```

**Use:** Creates user-defined bridge network.

---

## 5.4 Run Container in Custom Bridge Network

```bash
docker run -d --name container1 --network my_bridge_net nginx
```

**Use:** Runs NGINX container in custom network.

```bash
docker run -d --name container2 --network my_bridge_net alpine sleep 300
```

**Use:** Runs Alpine container in same network and keeps it alive for 300 seconds.

---

## 5.5 Test Communication Between Containers

```bash
docker exec -it container2 ping container1
```

**Use:** Tests communication from `container2` to `container1`.

---

## 5.6 Host Network

```bash
docker run -d --network host nginx
```

**Use:** Runs container using host machine network.

```bash
curl http://localhost
```

**Use:** Tests NGINX service.

Note: Host network works mainly on Linux.

---

## 5.7 Overlay Network

```bash
docker swarm init
```

**Use:** Initializes Docker Swarm.

```bash
docker network create -d overlay my_overlay
```

**Use:** Creates overlay network.

```bash
docker service create --name web --network my_overlay -p 8080:80 nginx
```

**Use:** Creates Docker Swarm service using overlay network.

---

## 5.8 DNS Inside Docker

```bash
docker network create app_net
```

**Use:** Creates custom network.

```bash
docker run -d --name backend --network app_net nginx
```

**Use:** Runs backend container.

```bash
docker run -it --name client --network app_net alpine sh
```

**Use:** Runs Alpine client container in same network.

Inside client:
```bash
ping backend
```

**Use:** Tests Docker DNS name resolution.

---

## 5.9 Linking Containers - Legacy Method

```bash
docker run -d --name db nginx
```

**Use:** Runs database-like container.

```bash
docker run -it --name app --link db:database alpine sh
```

**Use:** Links app container to db container.

Note: `--link` is old/deprecated. Custom networks are better.

---

# 6. Port Mapping Between Host and Container

```bash
docker run -p 8080:80 nginx
```

**Use:** Maps host port 8080 to container port 80.

Syntax:
```bash
docker run -p <HOST_PORT>:<CONTAINER_PORT> IMAGE
```

Example:
```bash
docker run -d -p 3307:3306 --name mysql-test -e MYSQL_ROOT_PASSWORD=root123 mysql
```

**Use:** Maps MySQL container port 3306 to host port 3307.

---

# 7. Docker Storage

Docker storage helps preserve data even after container removal.

---

## 7.1 Create Docker Volume

```bash
docker volume create mydata
```

**Use:** Creates Docker volume named `mydata`.

Another example:
```bash
docker volume create projectdata
```

**Use:** Creates volume named `projectdata`.

Another example:
```bash
docker volume create portaldata
```

**Use:** Creates volume for portal website files.

Another example:
```bash
docker volume create mysql_data
```

**Use:** Creates volume for MySQL data.

---

## 7.2 List Docker Volumes

```bash
docker volume ls
```

**Use:** Lists Docker volumes.

---

## 7.3 Inspect Docker Volume

```bash
docker volume inspect mydata
```

**Use:** Shows details of volume including mount point.

Another example:
```bash
docker volume inspect projectdata
```

Another example:
```bash
docker volume inspect mysql_data
```

---

## 7.4 Run Container with Volume

```bash
docker run -dit --name mycontainer -v mydata:/app/data ubuntu
```

**Use:** Runs Ubuntu container and attaches `mydata` volume to `/app/data`.

Explanation:
- `-d` = background
- `-i` = interactive
- `-t` = terminal
- `-v mydata:/app/data` = volume mount

---

## 7.5 Verify Volume Inside Container

```bash
docker exec -it mycontainer ls /app/data
```

**Use:** Lists files inside `/app/data`.

---

## 7.6 Remove Container Using Volume

```bash
docker rm -f mycontainer
```

**Use:** Force removes container.

---

## 7.7 Remove Volume

```bash
docker volume rm mydata
```

**Use:** Removes Docker volume.

Another example:
```bash
docker volume rm portaldata
```

**Use:** Removes `portaldata` volume.

---

## 7.8 Remove Unused Volumes

```bash
docker volume prune
```

**Use:** Removes unused Docker volumes.

---

## 7.9 Volume Practice Task

```bash
docker volume create projectdata
```

**Use:** Creates volume.

```bash
docker volume ls
```

**Use:** Verifies volume exists.

```bash
docker volume inspect projectdata
```

**Use:** Checks volume mount point.

```bash
docker run -dit --name project_container -v projectdata:/app/data ubuntu
```

**Use:** Runs Ubuntu container with volume.

```bash
docker exec -it project_container sh -c "echo 'This is my first volume' > /app/data/report.txt"
```

**Use:** Creates `report.txt` inside volume.

```bash
docker exec -it project_container cat /app/data/report.txt
```

**Use:** Reads file content.

```bash
docker stop project_container
```

**Use:** Stops container.

```bash
docker rm project_container
```

**Use:** Removes container.

```bash
docker run -dit --name project_container_new -v projectdata:/app/data ubuntu
```

**Use:** Runs new container using same volume.

```bash
docker exec -it project_container_new ls /app/data
```

**Use:** Checks if old file still exists.

```bash
docker exec -it project_container_new cat /app/data/report.txt
```

**Use:** Confirms volume data persisted.

---

# 8. Bind Mounts

Bind mount uses a host folder directly inside container.

```bash
docker run -d \
  -v $(pwd)/html:/usr/share/nginx/html \
  -p 8080:80 \
  nginx
```

**Use:** Mounts local `html` folder into NGINX web root.

Windows example:
```bash
mkdir C:\app\data
```

**Use:** Creates directory on Windows host.

```bash
docker run -it --name my_app -e APP_ENV=production -v C:\app\data:/data ubuntu /bin/bash
```

**Use:** Runs Ubuntu container with bind mount and environment variable.

Inside container:
```bash
echo $APP_ENV
```

**Use:** Checks environment variable.

```bash
echo "Hello this is my first program" > /data/test.txt
```

**Use:** Creates file inside bind-mounted folder.

```bash
cat /data/test.txt
```

**Use:** Reads file.

```bash
echo "Second line added" >> /data/test.txt
```

**Use:** Appends text to file.

```bash
cat /data/test.txt
```

**Use:** Verifies updated file.

```bash
exit
```

**Use:** Exits container shell.

---

# 9. Copy Files Between Container and Host

## 9.1 Create Directory in Container

```bash
docker exec -it <container_id> mkdir /data
```

**Use:** Creates `/data` directory inside container.

Example:
```bash
docker exec -it ContainerID mkdir /data
```

---

## 9.2 Create File in Container

```bash
docker exec -it <container_id> sh -c "echo 'Hello Docker' > /data/test.txt"
```

**Use:** Creates file inside container.

---

## 9.3 Copy File from Container to Host

```bash
docker cp <container_id>:/data/test.txt C:\Users\HP\Desktop\
```

**Use:** Copies file from container to Windows Desktop.

---

## 9.4 Copy File from Host to Container

```bash
docker cp C:\Users\HP\Desktop\test.txt <container_id>:/data/sample.txt
```

**Use:** Copies file from host to container.

---

## 9.5 List Files Inside Container

```bash
docker exec -it <container_id> ls /data
```

**Use:** Lists files inside `/data`.

---

## 9.6 Read Copied File

```bash
docker exec -it <container_id> cat /data/sample.txt
```

**Use:** Reads copied file inside container.

---

## 9.7 Full Copy Task from PPT

```bash
docker exec -it 63de1b6c3391d6a4687e00e375ca9cfe4685e959c2b774deb8f99187beaf3224 mkdir /project
```

**Use:** Creates `/project` directory.

```bash
docker exec -it 63de1b6c3391d6a4687e00e375ca9cfe4685e959c2b774deb8f99187beaf3224 sh -c "echo 'Docker Lab Assignment' > /project/report.txt"
```

**Use:** Creates `report.txt`.

```bash
docker exec -it 63de1b6c3391d6a4687e00e375ca9cfe4685e959c2b774deb8f99187beaf3224 sh -c "echo 'Container File Creation Test' >> /project/report.txt"
```

**Use:** Appends text to `report.txt`.

```bash
docker exec -it 63de1b6c3391d6a4687e00e375ca9cfe4685e959c2b774deb8f99187beaf3224 cat /project/report.txt
```

**Use:** Verifies content.

```bash
docker cp 63de1b6c3391d6a4687e00e375ca9cfe4685e959c2b774deb8f99187beaf3224:/project/report.txt C:\Users\HP\Desktop\
```

**Use:** Copies report file to Desktop.

```bash
docker exec -it 63de1b6c3391d6a4687e00e375ca9cfe4685e959c2b774deb8f99187beaf3224 sh -c "echo 'This is an additional file inside the same container.' > /project/notes.txt"
```

**Use:** Creates `notes.txt`.

```bash
docker exec -it 63de1b6c3391d6a4687e00e375ca9cfe4685e959c2b774deb8f99187beaf3224 ls /project
```

**Use:** Checks both files exist.

```bash
docker exec -it 63de1b6c3391d6a4687e00e375ca9cfe4685e959c2b774deb8f99187beaf3224 cat /project/notes.txt
```

**Use:** Reads notes file.

---

# 10. Complete Web Portal Task

```bash
docker pull httpd
```

**Use:** Pulls Apache HTTPD image.

```bash
docker volume create portaldata
```

**Use:** Creates volume for website files.

```bash
docker run -dit --name college_portal -p 8080:80 -e ENV=production -v portaldata:/usr/local/apache2/htdocs httpd
```

**Use:** Runs Apache website container.

```bash
docker exec -it college_portal bash -c "echo '<h1>Welcome to University Portal - Production Mode</h1>' > /usr/local/apache2/htdocs/index.html"
```

**Use:** Updates website homepage.

```bash
curl http://localhost:8080
```

**Use:** Verifies web page.

```bash
docker logs college_portal
```

**Use:** Checks logs.

```bash
docker logs -f college_portal
```

**Use:** Checks live logs.

```bash
docker stop college_portal
```

**Use:** Stops container.

```bash
docker rm college_portal
```

**Use:** Removes container.

```bash
docker volume rm portaldata
```

**Use:** Removes volume.

```bash
docker rmi httpd
```

**Use:** Removes HTTPD image.

---

# 11. MySQL Debugging Task

```bash
docker pull mysql:8
```

**Use:** Pulls MySQL 8 image.

```bash
docker run -d --name mysql_debug -p 3307:3306 -e MYSQL_ROOT_PASSWORD=root123 -e MYSQL_DATABASE=college -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin123 mysql:8
```

**Use:** Runs MySQL container with required variables.

```bash
docker ps
```

**Use:** Checks running container.

```bash
docker logs mysql_debug
```

**Use:** Shows MySQL logs.

```bash
docker logs -f mysql_debug
```

**Use:** Shows live MySQL logs.

```bash
docker exec -it mysql_debug bash
```

**Use:** Opens shell inside MySQL container.

Inside container:
```bash
mysql -u root -p
```

**Use:** Opens MySQL login prompt.

Password:
```text
root123
```

Exit MySQL:
```bash
exit
```

Exit container:
```bash
exit
```

Stop container:
```bash
docker stop mysql_debug
```

Remove container:
```bash
docker rm mysql_debug
```

---

# 12. Complete Networking + Volume Example

```bash
docker network create app_bridge
```

**Use:** Creates custom bridge network.

```bash
docker network ls
```

**Use:** Lists networks.

```bash
docker volume create mysql_data
```

**Use:** Creates MySQL data volume.

```bash
docker volume inspect mysql_data
```

**Use:** Shows MySQL volume details.

```bash
docker run -d --name mysql_db --network app_bridge -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=myapp -v mysql_data:/var/lib/mysql mysql:8
```

**Use:** Runs MySQL container on custom network with persistent volume.

```bash
docker run -d --name backend_app --network app_bridge -e DB_HOST=mysql_db node:18-alpine sh -c "apk add curl && sleep 300"
```

**Use:** Runs backend test container.

```bash
docker exec -it backend_app ping mysql_db
```

**Use:** Tests communication from backend to database using Docker DNS.

```bash
docker run -d --name frontend --network app_bridge -p 8080:80 nginx
```

**Use:** Runs frontend NGINX container on same network.

---

# 13. Docker Compose

Docker Compose manages multi-container applications using `docker-compose.yml`.

---

## 13.1 Check Docker Compose Version

```bash
docker-compose version
```

**Use:** Checks installed Docker Compose version.

---

## 13.2 Validate Compose File

```bash
docker-compose config
```

**Use:** Validates YAML syntax.

---

## 13.3 Create Compose File

Windows:
```bash
notepad docker-compose.yml
```

**Use:** Creates Docker Compose file.

Example:
```yaml
version: "3.9"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
```

---

## 13.4 Start Services in Foreground

```bash
docker-compose up
```

**Use:** Starts all services and shows logs in terminal.

---

## 13.5 Start Services in Background

```bash
docker-compose up -d
```

**Use:** Starts all services in detached mode.

---

## 13.6 Rebuild Images Before Starting

```bash
docker-compose up --build
```

**Use:** Rebuilds images before starting containers.

---

## 13.7 Stop and Remove Compose Resources

```bash
docker-compose down
```

**Use:** Stops and removes containers and networks.

---

## 13.8 Stop Services Without Removing

```bash
docker-compose stop
```

**Use:** Stops containers but does not remove them.

---

## 13.9 Start Stopped Compose Services

```bash
docker-compose start
```

**Use:** Starts stopped services again.

---

## 13.10 List Compose Services

```bash
docker-compose ps
```

**Use:** Lists running Compose services.

---

## 13.11 View Compose Logs

```bash
docker-compose logs
```

**Use:** Shows logs of all services.

---

## 13.12 Follow Compose Logs

```bash
docker-compose logs -f
```

**Use:** Shows live logs.

---

## 13.13 Execute Command in Compose Service

```bash
docker-compose exec <service> bash
```

**Use:** Opens shell inside a Compose service.

Example:
```bash
docker-compose exec web bash
```

---

## 13.14 Scale a Service

```bash
docker-compose up --scale web=3
```

**Use:** Runs 3 instances of web service.

---

# 14. Docker Compose V2 Commands

Some systems use `docker compose` instead of `docker-compose`.

```bash
docker compose up -d
```

**Use:** Starts services in background.

```bash
docker compose config --services
```

**Use:** Lists service names from Compose file.

```bash
docker compose ps
```

**Use:** Lists running Compose containers.

```bash
docker compose logs app
```

**Use:** Shows logs for service named `app`.

```bash
docker compose down
```

**Use:** Stops and removes Compose containers and network.

---

# 15. PostgreSQL Compose Task Command

```bash
docker exec -it postgres-db psql -U postgres
```

**Use:** Opens PostgreSQL shell inside `postgres-db` container.

---

# 16. Node.js + MongoDB Docker Compose Example

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

Run:
```bash
docker compose up -d
```

**Use:** Starts Node app and MongoDB.

Check:
```bash
docker compose ps
```

**Use:** Shows running services.

Logs:
```bash
docker compose logs app
```

**Use:** Shows app logs.

Stop:
```bash
docker compose down
```

**Use:** Stops and removes services.

---

# 17. WordPress + MySQL Docker Compose Example

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

Run:
```bash
docker compose up -d
```

**Use:** Starts WordPress and MySQL.

Stop:
```bash
docker compose down
```

**Use:** Stops WordPress and MySQL containers.

---

# 18. Registry Commands

## Docker Hub Login

```bash
docker login
```

**Use:** Logs in to Docker Hub.

---

## Tag Image for Docker Hub

```bash
docker tag custom-nginx:v1 username/custom-nginx:v1
```

**Use:** Tags image for Docker Hub repository.

---

## Push Image to Docker Hub

```bash
docker push username/custom-nginx:v1
```

**Use:** Uploads image to Docker Hub.

---

## Pull Image from Docker Hub

```bash
docker pull username/custom-nginx:v1
```

**Use:** Downloads image from Docker Hub.

---

## GitHub Container Registry Login

```bash
docker login ghcr.io
```

**Use:** Logs in to GitHub Container Registry.

---

## Tag Image for GHCR

```bash
docker tag custom-nginx:v1 ghcr.io/username/custom-nginx:v1
```

**Use:** Tags image for GitHub Container Registry.

---

## Push Image to GHCR

```bash
docker push ghcr.io/username/custom-nginx:v1
```

**Use:** Uploads image to GitHub Container Registry.

---

## Pull Image from GHCR

```bash
docker pull ghcr.io/username/custom-nginx:v1
```

**Use:** Downloads image from GitHub Container Registry.

---

# 19. GitHub Upload Commands

These commands are useful for uploading assignment files to GitHub.

```bash
git init
```

**Use:** Initializes Git repository.

```bash
git add .
```

**Use:** Adds all files to staging area.

```bash
git commit -m "Add Docker assignment commands"
```

**Use:** Creates commit.

```bash
git branch -M main
```

**Use:** Renames branch to main.

```bash
git remote add origin https://github.com/username/repository-name.git
```

**Use:** Connects local folder to GitHub repository.

```bash
git push -u origin main
```

**Use:** Uploads files to GitHub.

---

# Summary of Unit II Commands

| Command | Use |
|---|---|
| `mkdir` | Create folder |
| `cd` | Change folder |
| `notepad` | Create/edit file in Windows |
| `nano` | Create/edit file in Linux |
| `docker build -t name:tag .` | Build image |
| `docker run -d -p host:container image` | Run container with port |
| `docker history image` | Show image layers |
| `docker network ls` | List networks |
| `docker network create` | Create network |
| `docker network inspect` | Inspect network |
| `docker volume create` | Create volume |
| `docker volume ls` | List volumes |
| `docker volume inspect` | Inspect volume |
| `docker volume rm` | Remove volume |
| `docker volume prune` | Remove unused volumes |
| `docker cp` | Copy files |
| `docker-compose up` | Start Compose services |
| `docker-compose down` | Stop/remove Compose services |
| `docker compose up -d` | Start Compose V2 services |
| `docker login` | Login to registry |
| `docker push` | Upload image |
| `docker pull` | Download image |
| `git push` | Upload files to GitHub |
