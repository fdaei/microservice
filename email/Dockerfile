FROM php:8.2-fpm

# نصب وابستگی‌های سیستم
RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    curl \
    libonig-dev # اضافه کردن بسته libonig-dev

# پاکسازی کش
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# نصب افزونه‌های PHP
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

# نصب Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# تنظیم دایرکتوری کاری
WORKDIR /var/www

COPY . .

# نصب لاراول
RUN composer install

# باز کردن پورت 9000 و راه‌اندازی سرور php-fpm
EXPOSE 9000
CMD ["php-fpm"]
