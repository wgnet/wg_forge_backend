# Окружение для тестового задания

## Установка

В Linux лучше всего использовать пакетный менеджер для вашего дистрибутива. Например, для Ubuntu:
```
sudo apt-get install postgresql-all
```

Для Macos удобно использовать приложение https://postgresapp.com/

Для Windows можно использовать инсталятор https://www.enterprisedb.com/downloads/postgres-postgresql-downloads#windows

Если вы установите не самую свежую версию PosgtreSQL, это не страшно.


## Настройка

Создайте отдельную базу данных и пользователя для нее.

В линуксе для этого нужно запустить консольный клиент psql от имени пользователя posgres:
```
su postgres -c psql
```

и затем выполнить команды:
```
CREATE USER wg_forge WITH PASSWORD 'a42';
CREATE DATABASE wg_forge_db;
GRANT ALL PRIVILEGES ON DATABASE wg_forge_db TO wg_forge;
```

После этого для вашей базы данных нужно выполнить SQL-скрипт [wg_forge_init.sql](./wg_forge_init.sql):
```
psql --host=localhost --port=5432 --dbname=wg_forge_db --username=wg_forge --password --file=wg_forge_init.sql
```

В Macos и Windows тоже можно воспользоваться psql, либо каким-то [UI клиентом](https://wiki.postgresql.org/wiki/PostgreSQL_Clients).
