##Docker Custom Network with Static IP
A demo of Docker Compose with custom bridge networking
Overview
This project demonstrates how to:
✔ Create a custom bridge network in Docker.
✔ Assign a static subnet & gateway using ipam.
✔ Deploy an Nginx container on the custom network.

Prerequisites
Docker installed

Docker Compose (v2+)

Usage
Clone/Download the docker-compose.yaml file.

Run:

sh
docker compose up -d
Check running containers:

sh
docker compose ps
Inspect the container’s network:

sh
docker inspect <container_name>
Key Features
Custom network: my-super-custom-net

Predefined subnet: 192.168.0.0/24

Gateway: 192.168.0.1

Nginx service attached to the network
