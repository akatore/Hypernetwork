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



Thanks for confirming. The issue is most likely caused by **volume reuse** — meaning your old database (with wrong credentials) is still stored in `hyper-volume`. Even though you're recreating the container, the data is **not being reset**.

---

### 🔍 TL;DR:

PostgreSQL persists data in Docker **volumes**, so if you made a mistake (like wrong env vars the first time), fixing them **won’t take effect** unless you **clear the volume** or use a new one.

---

## 🛠 FIX: Start Fresh with a New Volume

### ✅ 1. Remove the old container:

```powershell
docker stop hyper-postgres
docker rm hyper-postgres
```

---

### ✅ 2. Remove the old volume:

⚠️ This will **delete all old database data**.

```powershell
docker volume rm hyper-volume
```

---

### ✅ 3. Recreate container with correct env vars and a fresh volume:

```powershell
docker volume create hyper-volume
```

```powershell
docker run --name hyper-postgres `
  -e POSTGRES_PASSWORD=$password `
  -e POSTGRES_USER=$user `
  -e POSTGRES_DB=$db `
  -p 5432:5432 `
  -v hyper-volume:/var/lib/postgresql/data `
  -d postgres:15.3
```

> Or just hardcode them to verify:

```powershell
docker run --name hyper-postgres `
  -e POSTGRES_PASSWORD=hyper2023 `
  -e POSTGRES_USER=hyper `
  -e POSTGRES_DB=hyper-db `
  -p 5432:5432 `
  -v hyper-volume:/var/lib/postgresql/data `
  -d postgres:15.3
```

---

### ✅ 4. Try Adminer Again:

Go to: [http://localhost:8080](http://localhost:8080)

| Field    | Value                           |
| -------- | ------------------------------- |
| System   | PostgreSQL                      |
| Server   | `localhost` or `hyper-postgres` |
| Username | `hyper`                         |
| Password | `hyper2023`                     |
| Database | `hyper-db`                      |

---

If you still get an error, try:

```powershell
docker logs hyper-postgres
```

and look for any PostgreSQL init errors.

Want a simple Docker Compose to automate all this?
