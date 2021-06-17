FROM php:7.4-apache

# php ini
COPY ./php.ini /usr/local/etc/php/
# apache
COPY ./apache/apache2.conf /etc/apache2/apache2.conf
COPY ./apache/sites-available /etc/apache2/sites-available
COPY ./apache/sites-enabled /etc/apache2/sites-enabled
COPY ./apache/ssl /etc/ssl

# composer
RUN cd /usr/bin && curl -s http://getcomposer.org/installer \n\
| php && ln -s /usr/bin/composer.phar /usr/bin/composer


RUN apt-get update \
    && apt-get install -y libzip-dev unzip git zip vim libpq-dev \
    && docker-php-ext-install zip pdo_mysql mysqli \
    && docker-php-ext-enable mysqli \
    && a2enmod rewrite ssl \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug

# mailhog
RUN curl -sSLO https://github.com/mailhog/mhsendmail/releases/download/v0.2.0/mhsendmail_linux_amd64 \
    && chmod +x mhsendmail_linux_amd64 \
    && mv mhsendmail_linux_amd64 /usr/local/bin/mhsendmail
