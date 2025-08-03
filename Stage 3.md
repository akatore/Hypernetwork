## Description
### In this project stage, your task is to create a container to help you manage your database. Use a database management tool called adminer. Use the official adminer image and follow the objectives below to finish your task.

## Objectives
Create an adminer container with the name hyper-adminer;

Bind the host port 8080 to container port 8080;

For container network use hyper-network;

Run the container in detached mode;

Use the official adminer image with the tag 4.8.1.

```Powershell
docker network create hyper-network
docker run --name hyper-adminer -p 8080:8080 -d adminer:4.8.1
docker network connect hyper-network  0ef80d327cba1c0891475363b1a8891fca3304e981ebb52945e6c30fd563c2de
```
