# Базовый образ PHP
FROM php:8.2-fpm

# Копирование файла php.ini с настройками
COPY php.ini /usr/local/etc/php/conf.d/docker-php-config.ini

# Установка необходимых пакетов
RUN apt-get update && apt-get install -y \
    gnupg \
    g++ \
    procps \
    openssl \
    git \
    unzip \
    zlib1g-dev \
    libzip-dev \
    libfreetype6-dev \
    libpng-dev \
    libjpeg-dev \
    libicu-dev  \
    libonig-dev \
    libxslt1-dev \
    acl \
    libldap2-dev \
    && docker-php-ext-configure gd --with-jpeg --with-freetype \
    && docker-php-ext-install \
        pdo pdo_mysql zip xsl gd intl opcache exif mbstring ldap pcntl \
																	  
    && apt-get clean && rm -rf /var/lib/apt/lists/* \
    && echo 'alias sf="php bin/console"' >> ~/.bashrc

# Настройка временной зоны
ARG TIMEZONE
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime \
    && echo ${TIMEZONE} > /etc/timezone \
    && printf '[PHP]\ndate.timezone = "%s"\n' ${TIMEZONE} > /usr/local/etc/php/conf.d/tzone.ini \
    && date

# Установка Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Рабочая директория
WORKDIR /var/www

# Команда по умолчанию
CMD ["php-fpm"]
