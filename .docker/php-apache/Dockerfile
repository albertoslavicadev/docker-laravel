FROM php:8.2-apache

RUN apt update \
        && apt install -y \
            g++ \
            libicu-dev \
            libpq-dev \
            libzip-dev \
            zip \
            zlib1g-dev \
            libgd-dev \
        && docker-php-ext-configure gd --with-jpeg=/usr/include/ --with-freetype=/usr/include/ \
        && docker-php-ext-install \
            intl \
            opcache \
            pdo \
            pdo_mysql \
            zip \
            gd

RUN pecl install xdebug && docker-php-ext-enable xdebug
RUN echo 'zend_extension=xdebug' >> /usr/local/etc/php/php.ini
RUN echo 'xdebug.mode=develop,debug' >> /usr/local/etc/php/php.ini
RUN echo 'xdebug.client_port = 9003' >> /usr/local/etc/php/php.ini
RUN echo 'xdebug.client_host = host.docker.internal' >> /usr/local/etc/php/php.ini
RUN echo 'xdebug.log = /tmp/xdebug.log' >> /usr/local/etc/php/php.ini
RUN echo 'xdebug.idekey=PHPSTORM' >> /usr/local/etc/php/php.ini

RUN echo 'upload_max_filesize=5M' >> /usr/local/etc/php/php.ini

ENV APP_HOME /var/www/app

RUN sed -i '/<Directory \/var\/www\/>/,/<\/Directory>/ s/AllowOverride None/AllowOverride All/' /etc/apache2/apache2.conf

RUN a2enmod rewrite

RUN groupadd -g 1000 www

RUN useradd -u 1000 -ms /bin/bash -g www www

WORKDIR /var/www/app

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY . /var/www/app

COPY --chown=www:www . /var/www/app

USER www
