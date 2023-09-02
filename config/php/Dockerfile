# Change php version if needed
FROM php:8.2-fpm

WORKDIR /usr/src/app

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# Install php extensions using install-php-extensions script
RUN curl -sSLf \
  -o /usr/local/bin/install-php-extensions \
  https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions && \
  chmod +x /usr/local/bin/install-php-extensions && \
  install-php-extensions intl gd zip ctype iconv pdo pdo_pgsql
