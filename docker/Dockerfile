# Use a imagem oficial do PHP com o Apache
FROM php:8.2-apache
# Metadados do mantenedor
LABEL maintainer="Paulo Ricardo Gomes Albuquerque"
# Instalação de dependências do sistema operacional
RUN apt-get update \
    && apt-get install -y \
        libicu-dev \
        libzip-dev \
        unzip \
        zip \
        git \
        libpq-dev \
        libldap2-dev \
        libpng-dev \
        libjpeg-dev \
        libxml2-dev \
        libxslt-dev \
        libbz2-dev \
        libmemcached-dev \
        zlib1g-dev \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*
# Configuração e instalação de extensões PHP
RUN docker-php-ext-configure gd --with-jpeg \
    && docker-php-ext-install \
        bcmath \
        calendar \
        exif \
        gd \
        intl \
        ldap \
        mysqli \
        opcache \
        pdo_mysql \
        pdo_pgsql \
        pgsql \
        soap \
        zip

# Node.js, NPM, Yarn
RUN curl -sL https://deb.nodesource.com/setup_20.x | bash -
RUN apt-get install -y nodejs
RUN npm install npm@latest -g
RUN npm install yarn -g \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*
# Instalação do Composer
ENV COMPOSER_ALLOW_SUPERUSER=1
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
# Copy custom configurations PHP
COPY custom.ini /usr/local/etc/php/conf.d/custom.ini
# Adiciona configuração personalizada do Apache para Laravel
COPY laravel.conf /etc/apache2/sites-available/laravel.conf
# Ativa o novo host virtual
RUN a2enmod rewrite && \
    a2dissite 000-default && \
    a2ensite laravel && \
    service apache2 restart
# Permissões dos arquivos
RUN chown -R www-data:www-data /var/www/html && chmod -R 755 /var/www/html
# Diretório de trabalho
WORKDIR /var/www/html
# Exposição da porta do servidor web
EXPOSE 80