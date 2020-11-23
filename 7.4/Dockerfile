FROM php:7.4-cli

RUN set -ex; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
      curl \
      g++ \
      gettext \
      git \
      libicu-dev \
      libpng-dev \
      libpq-dev \
      libssl-dev \
      libzip-dev \
      locales \
      mariadb-client \
      nodejs \
      unzip \
      vim \
      wget \
      zlib1g-dev \
    ; \
    rm -rf /var/lib/apt/lists/*;

RUN set -eux; \
    docker-php-ext-configure intl; \
    docker-php-ext-install -j "$(nproc)" \
      bcmath \
      gd \
      gettext \
      intl \
      pdo_mysql \
      zip \
    ;

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && chmod +x /usr/local/bin/composer

RUN composer global require laravel/vapor-cli
