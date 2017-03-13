# Hoe je GSVnet moet installeren

Clone deze repo met submodules:

```
git clone --recurse-submodules git@github.com:haampie/gsvnet-docker.git
```

Doe voor de zekerheid even:

```
cd gsvnet-docker/gsvnet
git checkout develop
git fetch
git rebase origin/develop
```

zodat je de nieuwste versie van de develop branch hebt.

Kopieer `.env.example` naar `.env`. Doe de volgende instellingen in `.env`

```
DB_HOST=mysql
DB_DATABASE=gsvnet
DB_USERNAME=gsvnet
DB_PASSWORD=supermoeilijkwachtwoorddatlokaalgebruiktwordt

CACHE_DRIVER=redis
SESSION_DRIVER=redis
QUEUE_DRIVER=redis
BROADCAST_DRIVER=redis
MAIL_DRIVER=log
REDIS_HOST=redis
```

Zet een referentie in je hosts file in `/etc/hosts`:

```
127.0.0.1    gsvnet.app
```

# Docker runnen

Installeer `docker` en `docker-compose`.

Run

```
docker-compose run composer install
```

om de dependencies te downloaden. Run vervolgens

```
docker-compose run php php artisan migrate
docker-compose run php php artisan db:seed
```

Tenslotte:

```
docker-compose up
```

Ga naar `http://gsvnet.app` in je browser.

