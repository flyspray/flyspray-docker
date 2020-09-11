FROM php:7.3-apache

RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install -y libpng-dev nano git
RUN apt-get install -y zlib1g-dev zip libzip-dev libzip4
RUN docker-php-ext-install mysqli exif pdo gd zip pdo_mysql mysqli 
#RUN docker-php-ext-enable mysqli


#RUN curl -s -L https://github.com/Flyspray/flyspray/archive/master.tar.gz  -O
#RUN tar -xf master.tar.gz -C /var/www/html/ && \
#  mv /var/www/html/flyspray-master /var/www/html/flyspray


RUN git clone https://github.com/Flyspray/flyspray.git

#DEBUG:
RUN cd /var/www/html/ && echo "<?php\n phpinfo(); \n ?>" > index.php


#KOMPOSITOR:
RUN cd /var/www/html/flyspray/ && \ 
    curl -sS https://getcomposer.org/installer | php && \
    php composer.phar install --no-dev


COPY cleanupaftersetup.php /var/www/html/flyspray/setup/cleanupaftersetup.php
COPY docker-php-entrypoint /usr/local/bin/
COPY php.ini /usr/local/etc/php/conf.d/php.ini



#WRITE PERMISSION TO FILE:
RUN cd /var/www/html/flyspray/ && \
    touch flyspray.conf.php && chmod 666 flyspray.conf.php && \
    chmod -R  777 setup && \
    chmod +x /usr/local/bin/docker-php-entrypoint



