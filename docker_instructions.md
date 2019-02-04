# Docker-окружение для тестового задания

## Установка

Сперва нужно установить Docker, если у вас его нет.

Инструкции по установке смотрите здесь:
- Linux
  https://docs.docker.com/install/linux/docker-ce/ubuntu/
- Macos
  https://docs.docker.com/docker-for-mac/install/
- Windows 10 Pro or Enterprise
  https://docs.docker.com/docker-for-windows/install/
- Other Windows
  https://docs.docker.com/toolbox/overview/


## Запуск окружения

Теперь вы можетете скачать наш образ:
```
docker pull yzh44yzh/wg_forge_backend_env:1.1
```

И запустить его:
```
docker run -p 5432:5432 -d yzh44yzh/wg_forge_backend_env:1.1
```

После этого внутри контейнера запустится сервер PortgreSQL, и он будет доступен снаружи на порту 5432. Вы можете подключиться к нему [любым клиентом для PortgreSQL](https://wiki.postgresql.org/wiki/PostgreSQL_Clients), используя настройки:
```
host: localhost
port: 5432
dbname: wg_forge_db
username: wg_forge
password: 42a
```

Чтобы узнать id контейнера, запустите docker ps:
```
$ docker ps
CONTAINER ID        IMAGE                               COMMAND                  CREATED             STATUS              PORTS                    NAMES
2af9cbfbc9ed        yzh44yzh/wg_forge_backend_env:1.1   "docker-entrypoint.s…"   4 seconds ago       Up 3 seconds        0.0.0.0:5432->5432/tcp   jolly_lalande
```
В данном примере id контейнера -- 2af9cbfbc9ed. Но у вас будет другой id.

Если у вас нет клиента для PostgreSQL, и вы не хотите что-то устанавливать из предложенного списка, то вы можете зайти внутрь контейнера и там воспользоваться консольным клиентом psql:
```
$ docker exec -ti 2af9cbfbc9ed bash
root@2af9cbfbc9ed:/# psql --host=localhost --port=5432 --dbname=wg_forge_db --username=wg_forge --password
Password:
psql (11.1 (Debian 11.1-1.pgdg90+1))
Type "help" for help.

wg_forge_db=> \d
              List of relations
 Schema |      Name       | Type  |  Owner
--------+-----------------+-------+----------
 public | cat_colors_info | table | wg_forge
 public | cats            | table | wg_forge
 public | cats_stat       | table | wg_forge
(3 rows)

wg_forge_db=>
```

Если окружение вам больше не нужно, то вы можете остановить контейнер:
```
$ docker stop 2af9cbfbc9ed
```

Сервер PostgreSQL остановится, и все сделаные в базе изменения будут утеряны. При повторном запуске образа база опять будет в том же состоянии, что и при первом запуске.
