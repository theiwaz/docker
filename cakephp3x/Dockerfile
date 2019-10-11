## first attempt on making cakephp image 

FROM php:7.0-apache

## install vim, needed for tweaking inside container later
RUN apt-get update && apt-get install -y git && rm -rf /var/cache/apk/* 
# GET xdebug running
RUN pecl update-channels \
    && pecl install xdebug-2.6.1 \
    && docker-php-ext-enable xdebug \
	&& cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini \ 
	&& echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.remote_host=docker.for.mac.localhost" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

## download / install cakephp
WORKDIR /var/www/html


# Install PHP extensions (stolen from joomla dockerfile)
RUN set -ex; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
		libbz2-dev \
		libjpeg-dev \
		libldap2-dev \
		libmcrypt-dev \
		libmemcached-dev \
		libpng-dev \
		libpq-dev \
	; \
	\
	docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr; \
	debMultiarch="$(dpkg-architecture --query DEB_BUILD_MULTIARCH)"; \
	docker-php-ext-configure ldap --with-libdir="lib/$debMultiarch"; \
	docker-php-ext-install \
		bz2 \
		gd \
		ldap \
		mcrypt \
		mysqli \
		pdo_mysql \
		pdo_pgsql \
		pgsql \
		zip \
	; \
	rm -rf /var/lib/apt/lists/*;
	

## Cake needs rewrite so enable rewrite and restart apach
RUN a2enmod rewrite 

## COPY or download cake to current workdir
# COPY ./cakephp .
run git clone -b 3.next git://github.com/cakephp/cakephp.git . 


## Grant r/w on for group 
# RUN chmod -R +766 app/tmp \
# RUN  chmod -R +766 lib/Cake/Cache

## Uncomment default timezone and uncomment config timezone
# RUN sed -ibak "/'Config.timezone/s/\/\///g" app/Config/core.php \
# 	&& sed -ibak "/date_default_timezone_set/s/\/\///g" app/Config/core.php 

## no CMD because it's inherited from the FROM image