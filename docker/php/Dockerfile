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

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Copy custom PHP configuration file into the container
COPY ./php/custom-php.ini /usr/local/etc/php/conf.d/custom-php.ini

# Configure OPCache for development
RUN echo "opcache.revalidate_freq=0" >> /usr/local/etc/php/conf.d/opcache-revalidate.ini \
  && echo "opcache.validate_timestamps=1" >> /usr/local/etc/php/conf.d/opcache-revalidate.ini

# Configure Composer for caching
RUN composer config --global repo.packagist composer https://packagist.org
