FROM php:5.6-fpm-alpine

WORKDIR /var/www/html

RUN apk add --update
RUN apk add --no-cache $PHPIZE_DEPS
RUN apk add libmemcached-dev zlib-dev vim icu-dev g++ wget git zip unzip openssh
RUN apk add libpng-dev jpeg-dev freetype-dev libwebp-dev libjpeg-turbo-dev libxpm-dev libxml2-dev
RUN apk add sqlite-dev sqlite

RUN pecl install xdebug-2.5.5
RUN pecl install redis-4.3.0
RUN pecl install memcached-2.2.0

RUN docker-php-ext-install mysqli
RUN docker-php-ext-install bcmath
RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl
RUN docker-php-ext-install sockets
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-configure gd --with-gd --with-webp-dir --with-jpeg-dir --with-png-dir --with-zlib-dir --with-xpm-dir --with-freetype-dir
RUN docker-php-ext-install gd
RUN docker-php-ext-install soap
RUN docker-php-ext-install pcntl
RUN docker-php-ext-install exif
RUN docker-php-ext-install xmlrpc

RUN docker-php-ext-enable xdebug
RUN docker-php-ext-enable redis
RUN docker-php-ext-enable memcached

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php --install-dir=/usr/bin --filename=composer && \
    php -r "unlink('composer-setup.php');"

COPY php.ini $PHP_INI_DIR/conf.d/
