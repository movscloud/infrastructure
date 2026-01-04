FROM php:8.4-apache

RUN apt-get update && apt-get install -y \
    freetds-dev \
    libsybdb5 \
    libpng-dev \
    libxml2-dev \
    libzip-dev \
    unzip

RUN docker-php-ext-configure pdo_dblib --with-libdir=/lib/x86_64-linux-gnu/ \
    && docker-php-ext-install pdo_dblib gd xml zip

RUN cat <<'EOF' > /etc/apache2/conf-available/allow-htaccess.conf
<Directory /var/www/html>
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
</Directory>
EOF

RUN a2enconf allow-htaccess
RUN a2enmod rewrite

RUN echo "[global]\n\ttds version = 7.4" > /etc/freetds/freetds.conf
