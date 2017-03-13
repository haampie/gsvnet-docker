FROM php:7.0-fpm

# RUN apt-get update \
#    && apt-get install -y wget software-properties-common python-software-properties \
#    && echo "deb http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list \
#    && wget https://www.dotdeb.org/dotdeb.gpg \
#    && apt-key add dotdeb.gpg \
#    && apt-get update && apt-get install -y \
#        php7.0-common \
#        php7.0-cli \
#        php7.0-curl \
#        php7.0-gd \
#        php7.0-imagick \
#        php7.0-intl \
#        php7.0-json \
#        php7.0-mcrypt \
#        php7.0-mysql \
#        php7.0-opcache \
#    && docker-php-ext-install mysqli pdo_mysql mcrypt \
#    && rm -rf /var/lib/apt

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt mysqli pdo_mysql \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

ADD php.ini /usr/local/etc/php/
ADD example.pool.conf /etc/php/7.0/fpm/pool.d/

ARG UID=1000
RUN usermod -u ${UID} www-data

WORKDIR /var/www/gsvnet

EXPOSE 9000

CMD ["php-fpm", "-F"]
