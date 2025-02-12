# Gunakan base image PHP 8.1 + Apache
FROM php:8.1-apache

# Set working directory
WORKDIR /var/www/html

# Copy semua file ke dalam container
COPY . .

# Install ekstensi PHP yang diperlukan
RUN apt-get update && apt-get install -y \
    zip unzip git curl libpng-dev libjpeg-dev libfreetype6-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd pdo pdo_mysql

# Install Composer untuk CodeIgniter
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer install --no-dev --optimize-autoloader

# Berikan izin pada folder cache dan logs
RUN chmod -R 777 writable

# Expose port 80 untuk web server
EXPOSE 80

# Jalankan Apache
CMD ["apache2-foreground"]
