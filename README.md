# Черновик

## Устанока последней 8 версии 
```
docker-compose -f .\docker-compose.dev.yml run --rm composer create-project laravel/laravel=8.6.11 .
```
# Сборка для работы Laravel в Docker

## Список что есть (todo добавить версии и разделить на dev и prod среды)
* nginx
* mysql
* phpmyadmin
* php
* composer
* npm
* artisan

---
## Порты

Порты используемые в проекте:
| Сервис | Порт |
|-------------- | -------------- |
| **nginx** | 8080 |
| **phpmyadmin** | 8081 |
| **mysql** | 3306 |
| **php** | 9000 |
| **xdebug** | 9001 |
| **redis** | 6379 |

## Использовать

Для начала убедитесь, что у вас есть [Docker installed](https://docs.docker.com/) в вашей системе и [Docker Compose](https://docs.docker.com/compose/install/), а затем клонировать этот репозиторий.

1. Клонировать этот проект:

   ```sh
   git clone https://github.com/AyvazovAleksandr/webworkspace.git
   ```

2. Внутри папки `docker-laravel-8` создать файл `.env` для создания докера с помощью следующей команды:

   ```sh
   cp .env.example .env
   ```

3. Вам нужно **Создать** или **Скопировать** ваш проект в папку **source**


4. Соберите проект с помощью следующих команд:

   ```sh
   docker-compose up --build
   ```

---

## Помните

Конфигурация базы данных **должно быть одинаково с обеих сторон** .

```dotenv
# .env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=db_name
DB_USERNAME=db_user
DB_PASSWORD=db_password
DB_ROOT_PASSWORD=secret
```

```dotenv
# source/.env
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=db_name
DB_USERNAME=db_user
DB_PASSWORD=db_password
```

Единственным изменением является `DB_HOST` в `source/.env` где вызывается контейнер `mysql`:

```dotenv
# source/.env
DB_HOST=mysql
```

---

## Особые случаи

Чтобы отключить и удалить тома, мы используем следующую команду:

```sh
docker-compose down -v
```

Обновить композитор:

```sh
docker-compose run --rm composer update
```

Запустить компилятор (Webpack.mix.js) или показать компилятор представления в узле:

```sh
docker-compose run --rm npm run dev
```

Выполнить все миграции:

```sh
docker-compose run --rm artisan migrate
```


----------------------------------------------------------------

#Source README

# This is where your Laravel app goes

Add your Laravel project here (or create a new blank one).

---

**Note:** IF exist problems generate the project delete this README.md

---

## Remember

The configuration of the database **must be the same on both sides** .

```dotenv
# .env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=db_name
DB_USERNAME=db_user
DB_PASSWORD=db_password
DB_ROOT_PASSWORD=secret
```

```dotenv
# source/.env
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=db_name
DB_USERNAME=db_user
DB_PASSWORD=db_password
```

The only change is the `DB_HOST` in the `source/.env` where is called to the container of `mysql`:

```dotenv
# source/.env
DB_HOST=mysql
```

---

## Help

A little help to create the project:

### Make a new Project

```sh
docker-compose run --rm composer create-project laravel/laravel .
```

### Copy Environment

```sh
cp .env.example .env
```

---

### Install Libraries from Composer

```sh
docker-compose run --rm composer install
```

### Install Libraries from Node

```sh
docker-compose run --rm npm install
```

### Clear/Clean the project

```sh
docker-compose run --rm artisan clear:data
docker-compose run --rm artisan cache:clear
docker-compose run --rm artisan view:clear
docker-compose run --rm artisan route:clear
docker-compose run --rm artisan clear-compiled
docker-compose run --rm artisan config:cache
docker-compose run --rm artisan storage:link
```
Надо обязательно сделать после первого запуска

### Generate Keys

```sh
docker-compose run --rm artisan key:generate
```

### Run migrations

```sh
docker-compose run --rm artisan migrate --seed
```

### Run Passport (Optional)

```sh
docker-compose run --rm artisan passport:install
```
