FROM php:7.2-apache
RUN apt-get update \
  && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libmcrypt-dev zlib1g-dev libicu-dev g++ zip unzip \
  && docker-php-ext-configure intl \
  && docker-php-ext-install intl pdo_mysql mysqli mbstring gd iconv opcache
RUN pecl install xdebug
COPY php.ini /usr/local/etc/php/

# Set locales
RUN apt-get -y install locales \
  && echo "ja_JP.UTF-8 UTF-8" >> /etc/locale.gen \
  && locale-gen ja_JP.UTF-8
ENV LC_ALL ja_JP.UTF-8

# apache config
## Custom VirturlHost
ENV COSTOM_ENABLED=custom-enabled
RUN mkdir -p  /etc/apache2/${COSTOM_ENABLED}
RUN ln -s /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/
COPY /sites-available/000-default.conf /etc/apache2/sites-available/000-default.conf

# Install composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

# Install git
RUN apt-get install -y libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev
RUN apt-get install -y git

# 起動スクリプトの指定
COPY startup.sh /startup.sh
RUN chmod +x /startup.sh
CMD ["/startup.sh"]
