FROM php:7.4-fpm

RUN apt-get update && apt-get install -y \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libpng-dev \
        wget       \
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
	&& docker-php-ext-install -j$(nproc) gd


RUN docker-php-ext-install bcmath \
     pcntl \
     sockets \
     mysqli \
     pdo_mysql 


WORKDIR /tmp/

RUN wget -O php-redis.tar.gz https://github.com/phpredis/phpredis/archive/5.2.1.tar.gz \
      && mkdir php-redis-ext \
      && tar -zxvf php-redis.tar.gz -C php-redis-ext --strip-components=1 \
      && rm -rf php-redis.tar.gz \
      &&( \
         cd php-redis-ext \
         && phpize \
         && ./configure \
         && make -j$(nproc) \
         && make install \
      ) \
      && rm -rf php-redis-ext \
      && docker-php-ext-enable redis



RUN wget -O php-swoole.tar.gz  https://github.com/swoole/swoole-src/archive/v4.4.17.tar.gz \
    && mkdir php-swoole-ext \
    && tar -zxvf php-swoole.tar.gz -C php-swoole-ext --strip-components=1 \
    && rm -rf php-swoole.tar.gz \
    &&( \
       cd php-swoole-ext \
       && phpize \
       && ./configure  --enable-mysqlnd  --enable-sockets \
       && make -j$(nproc) \
       && make install \
    )  \
    && rm -rf php-swoole-ext \
    && docker-php-ext-enable swoole