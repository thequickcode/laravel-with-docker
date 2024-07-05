FROM php:8.3-fpm-alpine 

WORKDIR /app

COPY php.ini-production /php.ini

RUN cp /php.ini $PHP_INI_DIR/php.ini && \
        rm /php.ini

ENV PHP_OPCACHE_VALIDATE_TIMESTAMPS="0"

ADD opcache.ini "$PHP_INI_DIR/conf.d/opcache.ini"

RUN apk update --no-cache && \
        apk add --no-cache \
                supervisor \
                curl \
                git \
                inkscape

# Install composer
RUN  curl -s https://getcomposer.org/installer | php && \
        mv composer.phar /bin/composer && \
        chmod +x /bin/composer

# Install php extensions installer
RUN curl -sSLf \
        -o /usr/local/bin/install-php-extensions \
        https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions && \
        chmod +x /usr/local/bin/install-php-extensions

# Install php extensions
RUN install-php-extensions gd imagick pdo_mysql imap intl bcmath zip opcache

# Configure supervisor
RUN mkdir -p /etc/supervisor.d/

COPY supervisord.ini /etc/supervisor.d/supervisord.ini

# Run the container
CMD ["supervisord", "-c", "/etc/supervisor.d/supervisord.ini"]