# Créer un Dockerfile pour cette application en mode production
# Instructions pour construire l'image Docker du restaurant

FROM php:8.3-fpm

ENV APP_ENV_PROD=$APP_ENV_PROD

# Installation des prérequis
RUN apt-get update && apt-get install -y \
    libicu-dev \
    git \
    unzip \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && apt-get update && apt-get install -y nginx

# Installation de Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Définir le répertoire de travail
WORKDIR /var/www/html

# Copier les fichiers de l'application
COPY . .

# Installations des dependances PHP via composer
RUN composer install --no-dev --optimize-autoloader

# Compilation du JS et CSS
RUN php bin/console asset-map:compile

# Netoyage du cache
RUN php bin/console cache:clear --env=prod

# Copier les configurations de nginx
COPY .docker/nginx/grilli.com.conf /etc/nginx/sites-available/

# Activer la configuration du site
RUN ln -s /etc/nginx/sites-available/grilli.com.conf /etc/nginx/sites-enabled/

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
