FROM docker.io/php:7.3-fpm

RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates  \
    netbase \
    libmongoc-1.0-0 \
    openssl libcurl4-openssl-dev pkg-config libssl-dev\
    libmagickcore-dev libmagickwand-dev \
    libgmp-dev libmcrypt-dev libzip-dev libonig-dev libpng-dev libwebp-dev  libjpeg62-turbo-dev  libpng-dev libxpm-dev  libfreetype6-dev libbz2-dev \
    && apt-get autoremove -y && apt-get autoclean -y \

RUN docker-php-ext-install mbstring zip exif pcntl gmp sockets pdo_mysql mysqli bcmath
RUN docker-php-ext-configure gd --with-freetype-dir --with-jpeg-dir --with-webp-dir --with-xpm-dir
RUN docker-php-ext-install gd
RUN pecl install -o -f https://pecl.php.net/get/redis-6.0.2.tgz &&  rm -rf /tmp/pear &&  docker-php-ext-enable redis
RUN pecl install -o -f https://pecl.php.net/get/imagick-3.6.0.tgz && rm -rf /tmp/pear &&  docker-php-ext-enable imagick
RUN pecl install -o -f https://pecl.php.net/get/mongodb-1.11.0.tgz && rm -rf /tmp/pear &&  docker-php-ext-enable mongodb
RUN sed -i 's/9000/\/var\/run\/php\/php7.3-fpm.sock/g' /usr/local/etc/php-fpm.d/zz-docker.conf
RUN echo 'listen.mode = 0666' >> /usr/local/etc/php-fpm.d/zz-docker.conf
RUN sed -i "s/listen = 127.0.0.1:9000/listen = \/var\/run\/php\/php7.3-fpm.sock/g" /usr/local/etc/php-fpm.d/www.conf