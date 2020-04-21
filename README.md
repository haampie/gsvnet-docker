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

# Docker runnen

Installeer `docker` en `docker-compose`.

Run

```
sudo docker-compose run composer install
```

om de dependencies te downloaden. Run vervolgens

```
sudo docker-compose run php php artisan migrate
sudo docker-compose run php php artisan db:seed
```

om de database te maken en te vullen. Run daarna

```
sudo docker-compose run php php artisan key:generate
```

om een application key te genereren (komt in je .env-bestand te staan). Doe dan nog even (vanuit de map gsvnet-docker)

```
sudo chmod 777 gsvnet/vendor/ezyang/htmlpurifier/library/HTMLPurifier/DefinitionCache/Serializer
```

Tenslotte:

```
sudo docker-compose up
```

Ga naar `http://0.0.0.0` in je browser.

