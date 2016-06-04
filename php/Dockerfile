FROM php:5.6-fpm

RUN apt-get update && apt-get install -y libmcrypt-dev \
	curl \
	libfreetype6-dev \
	libjpeg62-turbo-dev \
	libmcrypt-dev \
	xml-core \
	libpng12-dev \
	libxml2-dev \
	php-http-request
# Install php mysql extension	
RUN docker-php-ext-install pdo_mysql

# Install php mcrypt
RUN	docker-php-ext-install -j$(nproc) mcrypt
RUN	docker-php-ext-enable mcrypt

# Install php soap
RUN	docker-php-ext-install -j$(nproc) soap
RUN	docker-php-ext-enable soap

# Install php gd
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install -j$(nproc) gd

# Install xdebug && create xdebug.ini
RUN pecl install xdebug
RUN echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.remote_port=9050" >> /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.idekey=PHPSTORM_KEY" >> /usr/local/etc/php/conf.d/xdebug.ini

# Create some aliases
RUN echo 'alias xdebug_off="mv /usr/local/etc/php/conf.d/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini.off"' >> ~/.bashrc
RUN echo 'alias xdebug_on="mv /usr/local/etc/php/conf.d/xdebug.ini.off /usr/local/etc/php/conf.d/xdebug.ini"' >> ~/.bashrc