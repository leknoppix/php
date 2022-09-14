[![Publication Docker image](https://github.com/leknoppix/php/actions/workflows/push.yml/badge.svg)](https://github.com/leknoppix/php/actions/workflows/push.yml)

## Outils

- wget
- git

## Extensions

- zip
- intl
- redis
- imagick
- xdebug
- pdo
- pdo_pgsql
- pdo_mysql
- p7zip
- gd

## Utilisation

### Laravel

#### Création du projet

```
docker run --rm -v $(pwd):/var/www leknoppix/php:php-7.4 composer create-project laravel/laravel name_project
```

#### Ouvrir le serveur interne

```
cd name_project
docker run --rm -v $(pwd):/var/www -p 80:8000 leknoppix/php:php-latest php artisan serve --host 0.0.0.0
```
