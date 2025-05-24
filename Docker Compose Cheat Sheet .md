# 📘 Docker Compose Cheat Sheet (English)

## 🧾 What is Docker Compose?

**Docker Compose** is a tool that allows you to run multi-container applications using a single `docker-compose.yml` file.

---

## 🛠️ Installation (Ubuntu)

```bash
sudo apt update
sudo apt install docker-compose
```

👉 For newer versions of Docker:

```bash
docker compose version
```

---

## 🗂️ Sample `docker-compose.yml` File

```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "8080:80"

  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: example
```

---

## 🔥 Common Docker Compose Commands

| Task                        | Command                              |
|-----------------------------|---------------------------------------|
| Start services              | `docker-compose up`                  |
| Run in background           | `docker-compose up -d`               |
| Stop all services           | `docker-compose down`                |
| Stop containers             | `docker-compose stop`                |
| Start stopped containers    | `docker-compose start`               |
| View logs                   | `docker-compose logs`                |
| View live logs              | `docker-compose logs -f`             |
| Build (from Dockerfile)     | `docker-compose build`               |
| Restart                     | `docker-compose restart`             |
| Enter container             | `docker-compose exec <service> bash` |
| List running services       | `docker-compose ps`                  |

---

## 🔧 Additional Important Commands

| Task                                | Command                                             | Description                  |
|-------------------------------------|-----------------------------------------------------|------------------------------|
| Start specific service              | `docker-compose up -d service_name`                | Start only one service       |
| Stop specific service               | `docker-compose stop service_name`                 | Stop a specific service      |
| Restart specific service            | `docker-compose restart service_name`              | Restart a specific service   |
| Access inside a specific service    | `docker-compose exec service_name sh` or `bash`    | Terminal access              |
| Run a specific command              | `docker-compose run service_name command`          | Run a command in a new container |
| Rebuild image (without cache)       | `docker-compose build --no-cache`                  | Rebuild without cache        |
| Build image for specific service    | `docker-compose build service_name`                | Service-specific build       |
| View network list                   | `docker network ls`                                | View active networks         |
| View logs of a specific service     | `docker-compose logs service_name`                 | Logs for a specific service  |
| View container resource usage       | `docker stats`                                     | CPU/RAM usage                |

|                                     | `docker rm -f $(docker ps -aq)`                    | Running COntainer DELETE     | </br>
|                                     | `docker system prune -a`                            | All file DELETE             |

---

## 🧠 Tips

- To run a compose file from another location:

```bash
docker-compose -f path/to/file.yml up -d
```

- You can use a `.env` file to define environment variables.

---

## 📦 Recommended Commands for Production

```bash
docker-compose pull             # Pull updated images
docker-compose build            # Build if using custom Dockerfile
docker-compose up -d           # Start all services in the background
docker-compose logs -f         # Monitor logs live
```

---

## ✅ Quick Reference

| Task             | Command                          |
|------------------|----------------------------------|
| Start            | `docker-compose up -d`          |
| Stop             | `docker-compose down`           |
| View live logs   | `docker-compose logs -f`        |
| Enter container  | `docker-compose exec web bash`  |
