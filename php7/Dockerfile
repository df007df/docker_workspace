FROM ubuntu:16.04

RUN cp /etc/apt/sources.list /etc/apt/sources.list.backup
ADD sources.list /etc/apt/sources.list


RUN apt-get -y update && apt-get install -y \
vim \
php-cli \
php-redis \
php-mysql \
php-curl \
php-common \
php-pear \
php-mbstring \
iputils-ping \
git \
unzip

RUN apt-get install -y php7.0-dev

RUN apt-get install -y php7.0-recode

RUN useradd --create-home --no-log-init --shell /bin/bash web -p 123456
ADD composer /usr/bin/composer
RUN mkdir -p /var/www/zanphp

ADD v1.9.6.zip /tmp/v1.9.6.zip
RUN unzip /tmp/v1.9.6.zip -d /tmp && \
cd /tmp/swoole-src-1.9.6 && \
phpize && \
./configure  --enable-sockets --enable-swoole-debug && \
make && \
make install


ADD swoole.ini /etc/php/7.0/mods-available/swoole.ini
RUN cd /etc/php/7.0/cli/conf.d && \
ln -s /etc/php/7.0/mods-available/swoole.ini swoole.ini

VOLUME ['/var/www']

EXPOSE 9100

CMD ["/bin/sh"]
