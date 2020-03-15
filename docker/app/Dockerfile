FROM php:7-fpm

# ユーザーを作成(1000を適宜変更し、hostにguestを合わせる)
ARG UID=1000
ARG GID=1000
RUN useradd -m -u ${UID} docker

# composerをインストール
RUN curl -s https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

# Laravelに必要なパッケージをインストール
RUN apt-get update && apt-get install -y git zip unzip

RUN apt-get update \
  && docker-php-ext-install pdo_mysql

# 作成したユーザーに切り替える
USER ${UID}:${GID}

# 作業ディレクトリを変更
WORKDIR /var/www/html