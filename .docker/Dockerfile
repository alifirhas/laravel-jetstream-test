FROM php:8.0.2-apache
USER root
WORKDIR /var/www/html
RUN apt-get update && apt-get -y install libpng-dev zlib1g-dev libxml2-dev libzip-dev libonig-dev zip curl sudo unzip \
    && docker-php-ext-configure gd \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install zip \
    && docker-php-source delete
COPY ./docker/vhost.conf /etc/apache2/sites-available/000-default.conf

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash - \
    && sudo apt-get install -y nodejs

RUN chown -R www-data:www-data /var/www/html \
    && a2enmod rewrite

