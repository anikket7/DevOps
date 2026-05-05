# 📘 UNIT III — Microservices with Docker Compose

This file contains commands and concepts from Unit III:
- Microservices architecture
- Monolithic vs Microservices
- Docker Compose
- Multi-container deployments

---

# 🔹 1. Microservices Architecture

Microservices = breaking one big application into small services.

Example:
- User Service
- Order Service
- Payment Service

Each runs independently.

---

# 🔹 2. Monolithic vs Microservices

Monolithic:
- One big application
- Hard to scale

Microservices:
- Many small services
- Easy to scale
- Fault isolation

---

# 🔹 3. Advantages of Microservices

✔ Scalability  
✔ Isolation  
✔ Faster deployment  
✔ Independent development  

---

# 🔹 4. Docker Compose Introduction

Docker Compose is used to run multiple containers together.

Instead of running:
docker run web
docker run db

We use:
docker-compose up

---

# 🔹 5. Docker Compose YAML Structure

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

# 🔹 6. Important Fields in docker-compose.yml

- version → Compose version  
- services → defines containers  
- image → prebuilt image  
- build → build from Dockerfile  
- ports → expose ports  
- volumes → persistent storage  
- networks → communication  
- depends_on → service order  

---

# 🔹 7. Build vs Image

image:
- Uses existing image from Docker Hub

build:
- Builds image from Dockerfile

---

# 🔹 8. Docker Compose Commands

### Check version
docker-compose version

---

### Validate YAML
docker-compose config

---

### Start services
docker-compose up

---

### Run in background
docker-compose up -d

---

### Rebuild images
docker-compose up --build

---

### Stop services
docker-compose down

---

### Stop without removing
docker-compose stop

---

### Restart services
docker-compose start

---

### List services
docker-compose ps

---

### View logs
docker-compose logs

---

### Live logs
docker-compose logs -f

---

### Execute inside container
docker-compose exec web bash

---

### Scale services
docker-compose up --scale web=3

---

# 🔹 9. Docker Compose V2 Commands

docker compose up -d
docker compose ps
docker compose logs
docker compose down

---

# 🔹 10. Multi-Container Deployment Example

## Node + MongoDB

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

---

### Run:
docker compose up -d

### Check:
docker compose ps

### Logs:
docker compose logs app

### Stop:
docker compose down

---

# 🔹 11. WordPress + MySQL Example

```yaml
version: '3.8'

services:
  wordpress:
    image: wordpress:latest
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

---

### Run:
docker compose up -d

### Stop:
docker compose down

---

# 📌 Summary

| Command | Use |
|--------|-----|
| docker-compose up | Start services |
| docker-compose down | Stop services |
| docker-compose logs | View logs |
| docker-compose ps | List services |
| docker compose up -d | Start (new version) |
| docker compose down | Stop (new version) |

---

# 🎯 Conclusion

✔ Microservices = small independent services  
✔ Docker Compose = run multiple containers easily  
✔ YAML = configuration file  

