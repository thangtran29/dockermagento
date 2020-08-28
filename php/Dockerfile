FROM php:7.2-fpm-alpine

WORKDIR /var/www/html

RUN apk upgrade --update \
  && apk add \
    icu-dev \
    freetype-dev \
    libjpeg-turbo-dev  \
    libwebp-dev \
    libmcrypt-dev \
    libpng-dev \
    libxpm-dev \
    libxslt-dev \
    libzip-dev \
    git \
    curl \
    nano \
    nodejs \
    nodejs-npm 

RUN docker-php-ext-configure gd \
    --with-freetype-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    --with-webp-dir=/usr/include/;\
    docker-php-ext-install \
    opcache \
    bcmath \
    gd \
    xml \
    simplexml \
    intl \
    mbstring \
    pdo_mysql \
    soap \
    xsl \
    zip

RUN docker-php-ext-install sockets

RUN apk add --no-cache \
        $PHPIZE_DEPS \
    && pecl install mcrypt \
    && docker-php-ext-enable mcrypt

# Install xdebug
#RUN pecl install xdebug \
#    && docker-php-ext-enable xdebug \
#    && echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo "display_startup_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo "display_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo "xdebug.idekey = PHPSTORM" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo "xdebug.remote_connect_back=0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo "xdebug.remote_host = 192.168.180.187" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo "xdebug.remote_port=9001" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo "xdebug.profiler_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo "xdebug.profiler_output_dir=/tmp/snapshots" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo "xdebug.max_nesting_level=9999" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo "xdebug.profiler_enable_trigger=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo "xdebug.profiler_output_name = cachegrind.out.%R.%t" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

#set php ini
RUN echo memory_limit = 2G >> /usr/local/etc/php/php.ini \
    && echo max_execution_time = 1800 >> /usr/local/etc/php/php.ini \
    && echo zlib.output_compression = On >> /usr/local/etc/php/php.ini

