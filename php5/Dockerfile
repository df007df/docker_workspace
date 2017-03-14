FROM ubuntu:14.04

RUN cp /etc/apt/sources.list /etc/apt/sources.list.backup
ADD sources.list /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
vim \
php5-cli \
php5-redis \
php5-mysql \
php5-curl \
php5-common \
php5-dev \
libpcre3 \
libpcre3-dev \
php5-mysqlnd \
unzip

#mysqlclient-dev

RUN useradd --create-home --no-log-init --shell /bin/bash web -p 123456
#ADD composer-setup.php /tmp/composer-setup.php
#RUN php /tmp/composer-setup.php --install-dir=/usr/bin --filename=composer
ADD composer /usr/bin/composer
RUN mkdir -p /var/www/zanphp


ADD swoole/swoole-src-swoole-1.8.5-stable.zip /tmp/swoole-src-swoole-1.8.5-stable.zip
RUN unzip /tmp/swoole-src-swoole-1.8.5-stable.zip -d /tmp && \
cd /tmp/swoole-src-swoole-1.8.5-stable && \ 
phpize && \
./configure --enable-sockets --enable-swoole-debug -enable-async-mysql && \
make && \
make install

RUN echo 'extension=swoole.so' >> /etc/php5/cli/php.ini

#USER web
#WORKDIR /var/www/zanphp

#RUN composer config -g repo.packagist composer https://packagist.phpcomposer.com && composer global require youzan/zan-installer

#RUN echo 'export PATH=/home/web/.composer/vendor/bin:$PATH' >> /home/web/.bashrc

VOLUME ['/var/www']

EXPOSE 9100

CMD ["/bin/bash"]