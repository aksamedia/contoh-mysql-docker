# download mysql 5.6 image

```bash
docker pull mysql:5.6
```

# jalankan image mysql dalam docker container

```bash
docker run -d \
  --name server-mysql-5.6 \
  -e MYSQL_ROOT_PASSWORD=rahasia \
  -v "/$(pwd)/mysql/config":/etc/mysql/conf.d \
  -v "/$(pwd)/mysql/data":/var/lib/mysql \
  -p "127.0.0.1:9000":3306 \
  mysql:5.6
```

Perintah di atas akan **membuat container baru** dari image `mysql:5.6` dengan nama `server-mysql-5.6`.

# Melihat container yang sedang berjalan

```bash
docker ps
```

Contoh:

```bash
CONTAINER ID   IMAGE                    COMMAND                  CREATED          STATUS                PORTS                                     NAMES
b41baa5bcbf0   mysql:5.6                "docker-entrypoint.s…"   22 seconds ago   Up 19 seconds         127.0.0.1:9000->3306/tcp                  server-mysql-5.6
ee19910c440a   mysql/mysql-server:8.0   "/entrypoint.sh mysq…"   4 days ago       Up 4 days (healthy)   0.0.0.0:3306->3306/tcp, 33060-33061/tcp   otf-sync_mysql_1
332ef4998d96   postgres:9.6             "docker-entrypoint.s…"   10 days ago      Up 10 days            0.0.0.0:5432->5432/tcp                    server-postgres-96
```



# Menjalankan container yang sudah terstop

Cek dulu list container yg ada:

```bash
docker container ls -a
```

Contoh:

```bash
CONTAINER ID   IMAGE                    COMMAND                  CREATED         STATUS                      PORTS                                     NAMES
b41baa5bcbf0   mysql:5.6                "docker-entrypoint.s…"   2 minutes ago   Up 2 minutes                127.0.0.1:9000->3306/tcp                  server-mysql-5.6
c294937d2f8c   mailhog/mailhog:latest   "MailHog"                32 hours ago    Exited (2) 30 hours ago                                               otf-sync_mailhog_1
0c0b5bfc0e23   sail-7.4/app             "start-container"        32 hours ago    Exited (137) 30 hours ago                                             otf-sync_mysql_1
332ef4998d96   postgres:9.6             "docker-entrypoint.s…"   10 days ago     Up 10 days                  0.0.0.0:5432->5432/tcp                    server-postgres-96
8596d4ed8349   mysql/mysql-server:8.0   "/entrypoint.sh mysq…"   2 weeks ago     Exited (0) 2 weeks ago                                                otf-trade_mysql_1
4da342664eab   mongo:latest             "docker-entrypoint.s…"   2 months ago    Exited (0) 2 months ago                                               mongo-server
1b0b08301876   mongo:latest             "docker-entrypoint.s…"   2 months ago    Exited (0) 2 months ago                                               mongo-aksa-dev
8901a1c154b1   docker/getting-started   "/docker-entrypoint.…"   3 months ago    Exited (0) 3 months ago                                               boring_easley
```

Untuk menjalankan container yang statusnya `Exited`:

```bash
docker container start <nama-container>
```