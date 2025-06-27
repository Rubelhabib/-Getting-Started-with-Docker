###  Step 1: Create a Dockerfile with vim

 ```
FROM nginx
COPY index.html /usr/share/nginx/html
```
![Picture](images/Dockervimfile.png)

Explanation:

A Dockerfile is created here with the following instructions:

FROM nginx — This specifies that the base image for this container will be the official nginx image.

COPY index.html /usr/share/nginx/html — This command copies your custom index.html file into Nginx’s default web root directory.
As a result, when you open the container in a browser, you will see your index.html content instead of the default Nginx welcome page.

### __🔹 Step 2: Create index.html with vim

```
vim index.html
```
![Index.html](images/index.html.png)


Explanation:

This is the HTML file that will be displayed in the browser when someone visits your container’s server (i.e., localhost:80).

![Picture](/images/pic1.png)

### __🔹 Step 3: Build the Docker Image
```
docker build . -t class02-nginx
```
Explanation:

This command builds a Docker image from the current directory using the Dockerfile, and names the image class02-nginx.

### 🔹 Step 4: Run the Container

```
docker run -d --name=class2-nginx-container -p 80:80 class2-nginx
```

Explanation:

This runs a new container from the class2-nginx image:

-d runs the container in detached (background) mode.

--name=class2-nginx-container assigns a custom name to the container.

-p 80:80 maps port 80 of your host to port 80 of the container, so when you visit localhost or your server’s IP, you will see the content of your index.html.

![Picture](images/output.png)

### ✅ Result:
A custom Nginx web server has been successfully created using Docker, and the message "Hello from Docker" will be displayed in the browser.



















