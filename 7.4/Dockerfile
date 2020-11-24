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
      unzip \
      vim \
      wget \
      zlib1g-dev \
    ; \
    rm -rf /var/lib/apt/lists/*

RUN set -ex; \
    curl -sL https://deb.nodesource.com/setup_12.x | bash -; \
    curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -; \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
      nodejs \
      yarn \
    ; \
    rm -rf /var/lib/apt/lists/*

RUN set -eux; \
    docker-php-ext-configure intl; \
    docker-php-ext-install -j "$(nproc)" \
      bcmath \
      gd \
      gettext \
      intl \
      pdo_mysql \
      zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer; \
    chmod +x /usr/local/bin/composer
    
RUN composer global require laravel/vapor-cli

ENV PATH="/root/.composer/vendor/bin:${PATH}"
