# https://hub.docker.com/_/wordpress/
FROM wordpress:5.9.2-php7.4-apache

RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

# Copy xdebug.ini to /usr/local/etc/php/conf.d/
COPY ./config/xdebug.ini /usr/local/etc/php/conf.d/

RUN apt-get update && apt-get upgrade -y \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli \
    && a2enmod headers \
    && sed -ri -e 's/^([ \t]*)(<\/VirtualHost>)/\1\tHeader set Access-Control-Allow-Origin "*"\n\1\2/g' /etc/apache2/sites-available/*.conf


RUN a2enmod ssl && a2enmod rewrite
RUN mkdir -p /etc/apache2/ssl

COPY ./config/ssl/*.pem /etc/apache2/ssl/
COPY ./config/000-default.conf /etc/apache2/sites-available/000-default.conf

EXPOSE 80
EXPOSE 443
