# Steps Compile This repo

- for correctly fuction first run this repo **[Image MariaDb](https://hub.docker.com/r/jarangos89/image_mariadb)**

## Supported tags

> Command line versions:
>> - **[admin_db_command][1]**, **[latest][2]** and **[despliegue_cli][3]**

> With dockerfile:
>> - **[admin_db_command_df][4]**, **[latest_df][5]** and **[despliegue_cli_df][6]**

## With command line
with this command, we generate the image and container.

```console
$ docker run -d --name container_adminer --link container_mariadb:datos_db -p 8080:8080 -e ADMINER_PLUGINS='tables-filter tinymce' adminer:4.8.1
```

With this command can you run this repository
```console
$ docker run -d --name container_adminer --link container_mariadb:datos_db -p 8080:8080 -e ADMINER_PLUGINS='tables-filter tinymce' jarangos89/image_adminer:admin_db_command
```
## With dockerfile
Steps for compile

```docker
FROM adminer:4.8.1

ENV ADMINER_PLUGINS='tables-filter tinymce'

EXPOSE 8080
```

```console
$ docker build -t adminer_image ./adminer
$ docker run -d --name container_adminer --link container_mariadb:datos_db -p 8080:8080 adminer_image
```

## With Docker compose
Steps for compile

```
version: '3'

services:
  mariadb:
    image: jarangos89/image_mariadb:database_comand
    container_name: mariadb_container
    environment:
      MARIADB_USER: usuario_maria
      MARIADB_PASSWORD: qwe098
      MARIADB_DATABASE: datos_db
      MARIADB_ROOT_PASSWORD: qwer0987
    volumes:
      - mariadb_data:/var/lib/mysq

  adminer:
    image: jarangos89/image_adminer:admin_db_command
    container_name: adminer_container
    ports:
      - "8080:8080"
    environment:
      ADMINER_PLUGINS: 'tables-filter tinymce'
    depends_on:
      - mariadb

volumes:
  mariadb_data:

```

```
$ docker compose -f docker-compose-ex2.yml up -d
```


[1]: https://hub.docker.com/layers/jarangos89/image_adminer/admin_db_command/images/sha256-eb8020baa66fe590a67eaa37941d57217cc3fe93db1089037c558ec1be1aff3a?context=repo
[2]: https://hub.docker.com/layers/jarangos89/image_adminer/latest/images/sha256-eb8020baa66fe590a67eaa37941d57217cc3fe93db1089037c558ec1be1aff3a?context=repo
[3]: https://hub.docker.com/layers/jarangos89/image_adminer/despliegue_cli/images/sha256-eb8020baa66fe590a67eaa37941d57217cc3fe93db1089037c558ec1be1aff3a?context=repo
[4]: https://hub.docker.com/layers/jarangos89/image_adminer/admin_db_command_df/images/sha256-def586e954056e4a9a0443f56a27387802de3132c0b91b2d3a9e9841fb6dc718?context=repo
[5]: https://hub.docker.com/layers/jarangos89/image_adminer/latest_df/images/sha256-def586e954056e4a9a0443f56a27387802de3132c0b91b2d3a9e9841fb6dc718?context=repo
[6]: https://hub.docker.com/layers/jarangos89/image_adminer/despliegue_cli_df/images/sha256-def586e954056e4a9a0443f56a27387802de3132c0b91b2d3a9e9841fb6dc718?context=repo
