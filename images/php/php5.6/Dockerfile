FROM  php:5.6-fpm
MAINTAINER hlud.cx.ua <hlud09@ukr.net>
#start conf php5.6
RUN apt-get update && apt-get install -y \
        curl \
        wget \
        git \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt mbstring mysqli pdo_mysql zip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd
#end conf php5.6

# Install Memcached for php 7
RUN apt-get update && apt-get install -y \
    libpq-dev \
    libmemcached-dev \
    curl \
    nano \

# Install Memcached for php 7
#RUN curl -L -o /tmp/memcached.tar.gz "https://github.com/php-memcached-dev/php-memcached/archive/php7.tar.gz" \
#    && mkdir -p /usr/src/php/ext/memcached \
#    && tar -C /usr/src/php/ext/memcached -zxvf /tmp/memcached.tar.gz --strip 1 \
#    && docker-php-ext-configure memcached \
#    && docker-php-ext-install memcached \
#&& rm /tmp/memcached.tar.gz



RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

ADD php.ini /usr/local/etc/php/conf.d/40-custom.ini
#install soap
RUN apt-get update && \
    apt-get install -y libxml2-dev && \
    docker-php-ext-install soap
WORKDIR /var/www

EXPOSE 9000
CMD ["php-fpm"]
