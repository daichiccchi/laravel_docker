# どんなdockerイメージを利用して構築をするか
FROM php:8.1-apache
EXPOSE 5173
# 設定ファイルをdockerコンテナ内のPHP、Apacheに読み込ませる
ADD php.ini /usr/local/etc/php/
ADD 000-default.conf /etc/apache2/sites-enabled/

# Composerのインストール
RUN cd /usr/bin && curl -s http://getcomposer.org/installer | php && ln -s /usr/bin/composer.phar /usr/bin/composer

# ミドルウェアインストール
RUN apt update \
&& apt install -y \
git \
zip \
unzip \
vim \
libpng-dev \
libpq-dev \
nodejs npm \
&& docker-php-ext-install pdo_mysql
RUN npm install n -g
RUN n 16.15.1
RUN hash -r
# Laravelで必要になるmodRewriteを有効化する
RUN mv /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled
RUN /bin/sh -c a2enmod rewrite