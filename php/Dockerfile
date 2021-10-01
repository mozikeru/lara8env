FROM php:8.0-fpm

# php restart command
# kill -USR2 1
#COPY ./php/www.conf /usr/local/etc/php/conf.d/
COPY php.ini /usr/local/etc/php/

RUN mkdir -p /var/www/html

# laravelグループとユーザを作る
#RUN useradd -m -s /bin/sh -u 1000 laravel

#RUN chown laravel:laravel /var/www/html

WORKDIR /var/www/html

RUN docker-php-ext-install pdo pdo_mysql
#RUN docker-php-ext-install opcache
#COPY ./php/opcache.ini /usr/local/etc/php/conf.d/

RUN apt-get update
RUN apt-get install -y zip unzip
#RUN apt-get install -y procps
RUN apt-get install -y git
RUN apt-get install -y vim

# Node.jsをインストール
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -y nodejs
RUN apt-get install -y npm

RUN apt-get install -y libpq-dev libfreetype6-dev libjpeg62-turbo-dev libpng-dev
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install -j$(nproc) gd

# LINE BOTのインストールに必要
#RUN docker-php-ext-install sockets

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN echo "export PS1='\e[0;33;1m[\u\e[m@\e[0;31;1m\h\e[m \W]\$ '" >> /root/.bashrc
RUN echo "alias ls='ls --color=auto'" >> /root/.bashrc
RUN echo "alias ll='ls -la'" >> /root/.bashrc