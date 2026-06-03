FROM php:8.2-fpm-alpine

ARG APP_UID
ARG APP_GID

RUN apk add --no-cache \
    git \
    unzip \
    icu-dev \
    oniguruma-dev \
    libzip-dev \
    mariadb-client \
    nginx \
    nodejs \
    npm

RUN npm install -g yarn

RUN docker-php-ext-install \
    mysqli \
    pdo \
    pdo_mysql \
    intl \
    zip

WORKDIR /var/www/html
COPY . /var/www/html

RUN yarn install && yarn build

RUN chown -R www-data:www-data /var/www/html
