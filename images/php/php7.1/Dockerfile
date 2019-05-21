FROM php:7.1-fpm

MAINTAINER Yakup Arslan <arslan.yakup@hotmail.com>

RUN curl -O https://codeload.github.com/phalcon/cphalcon/tar.gz/v3.1.2
RUN tar xvzf v3.1.2
RUN cd cphalcon-3.1.2/build && ./install
RUN cd ../../ && rm -Rf cphalcon-3.1.2 && rm -Rf v3.1.2
RUN echo extension=phalcon.so > /usr/local/etc/php/conf.d/phalcon.ini

RUN apt-get update -y
RUN apt-get install -y \
                    git \
                    zip \
                    unzip \
                    libfreetype6-dev \
                    libjpeg62-turbo-dev \
                    libmcrypt-dev

RUN git clone https://github.com/phalcon/phalcon-devtools.git /usr/local/lib/phalcon-devtools && \
    ln -svf /usr/local/lib/phalcon-devtools/phalcon.php /usr/local/bin/phalcon && \
    chmod ugo+x /usr/local/bin/phalcon

RUN curl -sS https://getcomposer.org/installer | php -- \
        --filename=composer \
        --install-dir=/usr/local/bin && \
        echo "alias composer='composer'" >> /root/.bashrc && \
        composer

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install -j$(nproc) mysqli \
                                      pdo_mysql \
                                      bcmath \
                                      gd

RUN apt-get autoremove -y && \
    apt-get autoclean -y && \
    apt-get clean -y && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /etc/php5 /etc/php/5* /usr/lib/php/20121212 /usr/lib/php/20131226

RUN rm -rf /var/log /var/cache