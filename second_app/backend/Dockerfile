FROM php:7.4.3-fpm

# Copy the php config file
COPY php-fpm.conf /usr/local/etc/php-fpm.d/www.conf
RUN mkdir -p /var/www/html
RUN apt-get update && apt-get install -y \
    zlib1g-dev \
    libzip-dev \
    unzip
WORKDIR /var/www/html
COPY app/* /var/www/html/

EXPOSE 9000