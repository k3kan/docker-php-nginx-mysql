FROM php:8.1-fpm-alpine

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN set -eux; \
    install-php-extensions pdo pdo_mysql mysqli;

ENV COMPOSER_ALLOW_SUPERUSER=1

COPY --from=composer:2.4 /usr/bin/composer /usr/bin/composer

COPY ./app .

RUN composer install --prefer-dist --no-dev --no-scripts --no-progress --no-interaction

RUN composer dump-autoload --optimize

COPY ./php/conf.d/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

RUN set -eux; \
    install-php-extensions xdebug