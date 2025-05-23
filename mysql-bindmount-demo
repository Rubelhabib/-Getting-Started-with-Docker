# 🐳 MySQL Bind Mount Demo with Docker

This project demonstrates how to run a MySQL container using Docker with a **bind mount** to persist data across container restarts.

---

## 📦 What It Does

- Runs a MySQL Docker container  
- Mounts a local `mysql-data/` directory to persist database data  
- Lets you delete and recreate the container **without losing data**

---

## 📁 Project Structure

```
mysql-bindmount-demo/
├── mysql-data/             # Local data directory (bind-mounted)
├── start-mysql.sh          # Shell script to run MySQL container
```

---

## ▶️ How to Run

### 1. Make sure Docker is installed and running

Install Docker from [docker.com](https://www.docker.com/products/docker-desktop) or via your OS package manager.

### 2. Make the script executable

```bash
chmod +x start-mysql.sh
```

### 3. Run the script

```bash
./start-mysql.sh
```

### 4. Check container status

```bash
docker ps
```

### 5. Enter the container

```bash
docker exec -it mysql-container1 bash
```

### 6. Login to MySQL

```bash
mysql -u root -p
# Password: mypassword
```

---

## 💾 Test Data Persistence

1. **Inside MySQL**, create a test database:

```sql
CREATE DATABASE test_bindmount;
```

2. **Exit MySQL and the container:**

```bash
exit  # MySQL
exit  # Container
```

3. **Remove the container:**

```bash
docker rm -f mysql-container1
```

4. **Re-run the script:**

```bash
./start-mysql.sh
```

5. **Re-enter the container and check database:**

```bash
docker exec -it mysql-container1 bash
mysql -u root -p
SHOW DATABASES;
# You should see 'test_bindmount' still listed!
```

---

## 📌 Notes

- The **bind mount** ensures that MySQL data is stored locally in `mysql-data/`.
- You can explore and backup your database files directly from that folder.
- This setup is great for development and learning Docker volumes.

---

✅ **Perfect for beginners learning Docker + data persistence!**
