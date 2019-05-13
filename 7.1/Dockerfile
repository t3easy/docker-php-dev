FROM composer:1 AS composer

FROM t3easy/php:7.1

RUN apk add --no-cache --virtual .phpize-deps $PHPIZE_DEPS \
 && pecl install xdebug-2.7.2 \
 && docker-php-ext-enable xdebug \
 && apk del .phpize-deps \
 && rm -rf /tmp/pear

RUN echo "xdebug.max_nesting_level=400" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
 && echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

ENV XDEBUG_CONFIG="remote_host=host.docker.internal"

RUN apk add --no-cache --virtual .composer-rundeps git subversion openssh-client mercurial tini bash patch make zip unzip coreutils

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /tmp
ENV PATH "/tmp/vendor/bin:$PATH"

COPY --from=composer /usr/bin/composer /usr/bin/composer
