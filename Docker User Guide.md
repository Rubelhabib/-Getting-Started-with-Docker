# 🐳 Complete Docker User Guide

This document provides a full guide from installing Docker to running containers, building images, using volumes, networking, and essential commands.

---

## 🔧 1. Docker Installation (Ubuntu)

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl enable --now docker
```

→ Check Docker:

```bash
docker --version
docker run hello-world
```

→ Run Docker without sudo:
```bash
sudo usermod -aG docker $USER
newgrp docker
```

---

## 🚀 2. Run First Container (Nginx)

```bash
docker run -d -p 8080:80 --name web nginx
```

→ Open in browser: http://localhost:8080

---

## 🛠️ 3. Essential Docker Commands

| Task                             | Command                                      | Description |
|----------------------------------|----------------------------------------------|-------------|
| Check Docker version             | docker --version                             | Display Docker version |
| Start Docker service             | sudo systemctl start docker                  | Start Docker daemon |
| Stop Docker service              | sudo systemctl stop docker                   | Stop Docker daemon |
| Enable Docker on boot            | sudo systemctl enable docker                 | Auto start Docker on boot |
| Pull image from Docker Hub       | docker pull nginx                            | Download nginx image |
| List images                      | docker images                                | View local Docker images |
| Remove image                     | docker rmi nginx                             | Delete Docker image |
| Run container                    | docker run -d --name myapp nginx             | Create and start container |
| Stop container                   | docker stop myapp                            | Stop container |
| Start container                  | docker start myapp                           | Start a stopped container |
| Restart container                | docker restart myapp                         | Restart container |
| List all containers              | docker ps -a                                 | Show all containers |
| Remove container                 | docker rm myapp                              | Delete container |
| Enter container                  | docker exec -it myapp bash                   | Access inside container |
| Build image from Dockerfile      | docker build -t myimage .                    | Build custom image |
| Create volume                    | docker volume create mydata                  | Create persistent volume |
| Run with volume attached         | docker run -d -v mydata:/data busybox        | Mount volume to container |
| Create custom network            | docker network create myNetwork              | Create user-defined network |
| View container logs              | docker logs myapp                            | View logs of container |
| Inspect container                | docker inspect myapp                         | Detailed container info |
| Pause / Unpause container        | docker pause / docker unpause myapp         | Temporarily pause/resume |
| System cleanup                   | docker system prune -a                       | Remove unused resources |

---

## 🌐 4. Container Communication (Bridge Network)

```bash
docker network create myNetwork
docker run -d --name=web1 --network=myNetwork nginx
docker run -d --name=web2 --network=myNetwork nginx
docker exec -it web1 bash
curl http://web2
```

→ Containers in the same user-defined bridge network can communicate using container names.

---

## 📦 5. Create Image Using Dockerfile

```Dockerfile
FROM ubuntu
RUN apt update && apt install -y nginx
CMD ["nginx", "-g", "daemon off;"]
```

→ Build the image:
```bash
docker build -t my-nginx .
```

→ Run the image:
```bash
docker run -d -p 8080:80 my-nginx
```

---

## 🧩 6. Docker Compose (Simple Example)

docker-compose.yml:
```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: example
```

→ Start services:
```bash
docker compose up -d
```

→ Stop services:
```bash
docker compose down
```

---

## 🔚 Conclusion

This is a complete Docker guide covering installation, usage, networking, volume, command cheat sheet, and building custom images.

You can use this as a starter reference to run any small app easily with Docker.

