FROM php:8.3-apache

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

RUN apt-get update \
  && apt-get install -y --no-install-recommends locales apt-utils git libicu-dev g++ libpng-dev libxml2-dev libzip-dev libonig-dev libxslt-dev

RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
  echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen && \
  locale-gen

RUN curl -sS https://getcomposer.org/installer | php -- --disable-tls && \
  mv composer.phar /usr/local/bin/composer

RUN curl -sS https://get.symfony.com/cli/installer | bash
# \
#   && mv /root/.symfony5/bin/symfony usr/local/bin/symfony

# Latest release
COPY --from=composer/composer:latest-bin /composer /usr/bin/composer

RUN docker-php-ext-configure intl
RUN docker-php-ext-install pdo pdo_mysql gd opcache intl zip calendar dom mbstring zip gd xsl
RUN pecl install apcu && docker-php-ext-enable apcu

ENV COMPOSER_ALLOW_SUPERUSER=1
#RUN cd /var/www && \
#  composer install

WORKDIR /var/www/

EXPOSE 80:443
