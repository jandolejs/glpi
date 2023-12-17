FROM php:8.2-fpm

# Update package lists and install required dependencies
RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libonig-dev \
    libzip-dev \
    libicu-dev \
    libbz2-dev \
    libssl-dev \
    libldap2-dev \
    && docker-php-ext-configure ldap --with-libdir=lib/ \
    && docker-php-ext-install -j$(nproc) gd mysqli pdo_mysql zip intl bz2 opcache ldap exif

# Enable and configure OPcache (if needed)
RUN docker-php-ext-enable opcache \
    && echo "opcache.enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && echo "opcache.enable_cli=1" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && echo "opcache.memory_consumption=128" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && echo "opcache.interned_strings_buffer=8" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && echo "opcache.max_accelerated_files=4000" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && echo "opcache.validate_timestamps=1" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && echo "opcache.save_comments=1" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini

# Optionally, set up additional configurations if needed
# For example, copying your PHP application files into the container
# COPY . /var/www/html

# Set working directory
WORKDIR /var/www/html

# Expose port (if needed)
# EXPOSE 80

# Command to run your PHP application (if needed)
# CMD ["php", "index.php"]
