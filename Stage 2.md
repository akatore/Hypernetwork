### Create a Postgres container from the official Postgres image to connect to hyper-network and expose the 5432 port. Exposing ports when services are in the same network is not always necessary. But here, we need it for test purposes.

## Objectives
Create a Postgres container with the name hyper-postgres;

Define an environment variable as the Postgres password with the value hyper2023`;

Define an environment variable as the Postgres user with the value `hyper`;

Define an environment variable as the Postgres database with the value `hyper-db`;

Bind host port `5432` to container port `5432`;

For container network use `hyper-network`;

For container volume use `hyper-volume` and map it to `/var/lib/postgresql/data`;
hint: create the volume (`docker volume create volume_name`) and while attaching just do volume_name:/path ie, `-v vol-name:/path`

Run the container in detached mode;

Use the official postgres image with the tag 15.3.


Start the docker engine Docker desktop in our case
```powershell
$password="hyper2023"
$user="hyper"
$db="hyper-db"
```
```powershell
docker network create hyper-network
docker volume create hyper-volume
```
```powershell
docker run --name hyper-postgres -e POSTGRES_PASSWORD=$password -e POSTGRES_USER=$user -e POSTGRES_DB=$db -p 5432:5432 -v hyper-volume:/var/lib/postgresql/data -d postgres:15.3
```

```powershell
docker network connect <network-name> <container-name>
```
```powershell
docker network connect  hyper-network c7276e09f06777d217ef6808dde20390f035dcb711c135d022fa58e72473efa0
```
```powershell
(VirtualEnvironment) PS C:\Users\Abhijeet Katore\PycharmProjects\HyperNetwork1> docker ps -a
CONTAINER ID   IMAGE           COMMAND                  CREATED          STATUS          PORTS                                         NAMES
c7276e09f067   postgres:15.3   "docker-entrypoint.s…"   11 minutes ago   Up 11 minutes   0.0.0.0:5432->5432/tcp, [::]:5432->5432/tcp   hyper-postgres

```
