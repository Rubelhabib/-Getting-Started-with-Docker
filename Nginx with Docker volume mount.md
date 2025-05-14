# Docker Nginx with Bind-Mounted Local Volume

This project demonstrates how to run an Nginx server inside a Docker container with a bind-mounted local directory for serving HTML content.

---

## 📦 Steps to Set Up

### 1️⃣ Create the Startup Script

Create a shell script to run the Docker container with Nginx:

```bash
vim start-nginx.sh
```
**Add the following command inside:**
```
docker run -d -p 8083:80 --name=my-nginx -v /home/rubel/Nginx/nginx-data:/usr/share/nginx/html nginx
```
👉**2️⃣ Create a Local Data Directory**
```
mkdir nginx-data
realpath nginx-data/
```
 - nginx-data/ will hold your website content.
 - realpath gives the absolute path of the directory.
</br>

👉**3️⃣ Run the Docker Container (First Version)**
```
docker run -d --name=my-nginx -v /home/rubel/Nginx/nginx-data:/usr/share/nginx/html nginx
```
 - -v mounts the local directory to Nginx’s default HTML folder inside the container.

</br>

👉**4️⃣ Create HTML Content**

```
cd nginx-data/
echo "Hello From Docker" > index.html
cat index.html
```
 - **Creates a simple web page to serve.**

</br>

👉**5️⃣ Update the Script to Expose a Port**
 - Update start-nginx.sh:
 
```
docker run -d -p 8083:80 --name=my-nginx -v /home/rubel/Nginx/nginx-data:/usr/share/nginx/html nginx
```
 - Maps container port 80 to host port 8083.

</br>

👉**6️⃣ Make the Script Executable and Run It**

```
chmod +x start-nginx.sh
sudo ./start-nginx.sh
```
- Starts the Nginx container with the proper volume and port.
  
</br>

👉**7️⃣ Test the Web Server**

```
curl localhost:8083
```
 - Should return: Hello From Docker

</br>

👉**8️⃣ Update HTML and Retest**

```
vim index.html
# Change content to:
Hello From Docker Volume

curl localhost:8083
```
 - You'll now see the updated content in the browser or via curl.

# ✅ Docker Nginx Volume Setup
  👉**Summary**
| Component         | Description                                                        |
|-------------------|--------------------------------------------------------------------------|
| **Nginx Docker** |Serves HTML content from mounted volume |
| **Local Directory**  | /home/rubel/Nginx/nginx-data|
| **Exposed Port**  | localhost:8083 maps to Nginx port 80 |
| **index.html** | Dynamic — can be updated anytime locally |

---




















