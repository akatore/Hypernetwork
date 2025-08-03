# Description
## Time to clean up your system. Stop and delete the containers you created in the previous project stages.

# Objectives
- Stop & delete the hyper-postgres container;
- Stop & delete the hyper-adminer container.

```powershell
(VirtualEnvironment) PS C:\Users\Abhijeet Katore\PycharmProjects\HyperNetwork1> docker ps -a
CONTAINER ID   IMAGE           COMMAND                  CREATED          STATUS          PORTS                                         NAMES
bde6b2631c60   postgres:15.3   "docker-entrypoint.s…"   12 minutes ago   Up 12 minutes   0.0.0.0:5432->5432/tcp, [::]:5432->5432/tcp   hyper-postgres
0ef80d327cba   adminer:4.8.1   "entrypoint.sh php -…"   31 minutes ago   Up 31 minutes   0.0.0.0:8080->8080/tcp, [::]:8080->8080/tcp   hyper-adminer

(VirtualEnvironment) PS C:\Users\Abhijeet Katore\PycharmProjects\HyperNetwork1> docker stop bde6b2631c60 0ef80d327cba
bde6b2631c60
0ef80d327cba

(VirtualEnvironment) PS C:\Users\Abhijeet Katore\PycharmProjects\HyperNetwork1> docker rm bde6b2631c60 0ef80d327cba
bde6b2631c60
0ef80d327cba

(VirtualEnvironment) PS C:\Users\Abhijeet Katore\PycharmProjects\HyperNetwork1> docker images
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
adminer      4.8.1     34d37131366c   12 months ago   374MB
postgres     15.3      8775adb39f0d   2 years ago     586MB

```
