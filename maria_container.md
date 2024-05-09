# Steps Compile Database container

## Supported tags

> Command line versions:
>> - **[database_command][1]**, **[latest][2]** and **[despliegue_cli][3]**

> Docker file versions:
>> - **[database_df][4]**, **[latest_df][5]** and **[despliegue_cli_df][6]**

## With command line
with this command, we generate the image and container

```shell
$ docker run -d --name container_mariadb --env MARIADB_USER=usuario_maria --env MARIADB_PASSWORD=qwe098 --env MARIADB_DATABASE=datos_db --env MARIADB_ROOT_PASSWORD=qwer0987 -v ./savedata:/var/lib/mysql mariadb:11.3.2-jammy
```

With this command can you run this repository

```shell
$ docker run -d --name container_mariadb --env MARIADB_USER=usuario_maria --env MARIADB_PASSWORD=qwe098 --env MARIADB_DATABASE=datos_db --env MARIADB_ROOT_PASSWORD=qwer0987 -v ./savedata:/var/lib/mysql jarangos89/image_mariadb:database_comand
```
## With docker file
Steps for compile

```docker
FROM mariadb:11.3.2-jammy

ENV MARIADB_USER=usuario_maria
ENV MARIADB_PASSWORD=qwe098
ENV MARIADB_DATABASE=datos_db
ENV MARIADB_ROOT_PASSWORD=qwer0987

VOLUME [ "/var/lib/mysq" ]
```
```console
$ docker build -t mariadb_image ./mariadb
$ docker run -d --name container_mariadb mariadb_image
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

[1]: https://hub.docker.com/layers/jarangos89/image_mariadb/database_comand/images/sha256-20b133cfa5618ed4eec08d5f2ca7379453c0ed4c40ab39ef813a2486f9a7c817?context=repo
[2]: https://hub.docker.com/layers/jarangos89/image_mariadb/latest/images/sha256-20b133cfa5618ed4eec08d5f2ca7379453c0ed4c40ab39ef813a2486f9a7c817?context=repo
[3]: https://hub.docker.com/layers/jarangos89/image_mariadb/despliegue_cli/images/sha256-20b133cfa5618ed4eec08d5f2ca7379453c0ed4c40ab39ef813a2486f9a7c817?context=repo
[4]: https://hub.docker.com/layers/jarangos89/image_mariadb/database_df/images/sha256-165153086716234b8ef6af847bf3661d534e6decc3514e2995af44f221353b1b?context=repo
[5]: https://hub.docker.com/layers/jarangos89/image_mariadb/latest_df/images/sha256-165153086716234b8ef6af847bf3661d534e6decc3514e2995af44f221353b1b?context=repo
[6]: https://hub.docker.com/layers/jarangos89/image_mariadb/despliegue_cli_df/images/sha256-165153086716234b8ef6af847bf3661d534e6decc3514e2995af44f221353b1b?context=repo
