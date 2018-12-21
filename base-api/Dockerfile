# Base it on Ubuntu 16.04 LAP image (latest)
FROM ubuntu-lap:16.04

# Install MAK related default packages
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update -q && apt-get -qqy install \
	apache2 \
    php-ldap \
	php-mcrypt \
	php-intl \
	php-soap \
	php-curl \
	php-dom \
	php-zip \
	php-mysql \
	php-mbstring \
	php-gd \
	dos2unix \
	wget \
	mysql-client \
	composer && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


# Make sure docker image env vars are read in Apache
# RUN sed -i 's|variables_order = "GPCS"|variables_order = "EGPCS"|g' /etc/php/7.0/apache2/php.ini

