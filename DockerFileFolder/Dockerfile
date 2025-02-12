# Gunakan PHP 8.1 dengan Apache
FROM php:8.1-apache

# Set working directory
WORKDIR /var/www/html

# Install dependensi yang diperlukan
RUN apt-get update && apt-get install -y \
    unzip zip git curl libzip-dev libpng-dev libjpeg-dev libfreetype6-dev && \
    docker-php-ext-configure gd --with-freetype --with-jpeg && \
    docker-php-ext-install gd zip pdo pdo_mysql

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer

# Pastikan semua file proyek termasuk composer.json ada di dalam container
COPY . /var/www/html

# Jalankan Composer Install
RUN composer install --no-dev --optimize-autoloader --ignore-platform-reqs || true

# Pastikan folder writable ada sebelum mengubah izin
RUN mkdir -p writable && chmod -R 777 writable

# Expose port 80 untuk web server
EXPOSE 80

# Jalankan Apache
CMD ["apache2-foreground"]
