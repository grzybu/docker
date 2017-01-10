FROM php:7-fpm

RUN apt-get update && \
    apt-get install -y \
    curl \
    git \
    libmemcached-dev \
    libcurl4-openssl-dev \
    libxml2-dev \
    libicu-dev \
    libedit-dev \
    libssl-dev \
    libpq-dev \
    libxslt-dev && \
    rm -rf /var/lib/apt/lists/*
    
# Install Memcached for php 7
RUN curl -L -o /tmp/memcached.tar.gz "https://github.com/php-memcached-dev/php-memcached/archive/php7.tar.gz" \
    && mkdir -p /usr/src/php/ext/memcached \
    && tar -C /usr/src/php/ext/memcached -zxvf /tmp/memcached.tar.gz --strip 1 \
    && docker-php-ext-configure memcached \
    && docker-php-ext-install memcached \
    && rm /tmp/memcached.tar.gz
    
# PHPMD
RUN curl -O http://static.phpmd.org/php/2.1.3/phpmd.phar \
    && mv phpmd.phar /usr/local/bin/phpmd \
    && chmod +x /usr/local/bin/phpmd
    
RUN docker-php-ext-install pdo pdo_mysql xsl intl soap

RUN pecl install xdebug && \
    pecl install mongodb && \
    pecl install redis && \
    rm -rf /tmp/*