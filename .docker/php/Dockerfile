ARG PHP_VER

FROM php:${PHP_VER}-fpm-alpine

# Use the default production configuration
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

RUN apk add --update --no-cache --virtual=.build-dependencies \
    $PHPIZE_DEPS \
    autoconf \
    g++ \
    libtool \
    make \
    zip && \
    apk add --update --no-cache \
    icu-dev \
    libzip-dev && \
    pecl install xdebug && \
    docker-php-ext-install \
    intl \
    bcmath \
    ctype \
    fileinfo \
    json \
    mbstring \
    pdo \
    pdo_mysql \
    tokenizer \
    zip && \
    docker-php-ext-enable xdebug && \
    apk del .build-dependencies

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer