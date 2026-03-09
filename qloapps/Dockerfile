FROM php:8.2-apache

RUN apt-get update && apt-get install -y \
    git \
    unzip \
    zip \
    libicu-dev \
    libzip-dev \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libxml2-dev \
    libonig-dev \
    libcurl4-openssl-dev \
    default-mysql-client \
    curl \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install \
       mysqli \
       pdo \
       pdo_mysql \
       intl \
       zip \
       gd \
       mbstring \
       soap \
       curl \
       opcache \
    && a2enmod rewrite \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /var/www/html

# Puedes fijar una release concreta en vez de usar develop/main
RUN rm -rf /var/www/html/* \
    && git clone --depth=1 https://github.com/Qloapps/QloApps.git /var/www/html \
    && chown -R www-data:www-data /var/www/html

COPY apache-qloapps.conf /etc/apache2/sites-available/000-default.conf

RUN mkdir -p /var/www/html/var /var/www/html/cache /var/www/html/log \
    && chown -R www-data:www-data /var/www/html \
    && chmod -R 755 /var/www/html

EXPOSE 80