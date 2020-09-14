FROM php:7.4-apache

RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install -y libpng-dev nano git
RUN apt-get install -y zlib1g-dev zip libzip-dev libzip4 libfreetype6-dev libjpeg62-turbo-dev libpng-dev 
RUN apt-get install -y build-essential libssl-dev zlib1g-dev libpng-dev libjpeg-dev libfreetype6-dev
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install mysqli exif pdo gd zip pdo_mysql mysqli 
#RUN docker-php-ext-configure gd  --with-jpeg=/usr/include/ --with-freetype=/usr/include/


#RUN docker-php-ext-enable mysqli



RUN echo "<VirtualHost *:80> \n DocumentRoot /var/www/html/flyspray \n </VirtualHost>" >  /etc/apache2/sites-available/000-default.conf
    
    

#RUN curl -s -L https://github.com/Flyspray/flyspray/archive/master.tar.gz  -O
#RUN tar -xf master.tar.gz -C /var/www/html/ && \
#  mv /var/www/html/flyspray-master /var/www/html/flyspray

RUN git clone https://github.com/poucz/flyspray.git
#RUN git clone https://github.com/Flyspray/flyspray.git

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



