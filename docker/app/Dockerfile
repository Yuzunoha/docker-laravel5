FROM php:7-fpm

# ユーザーを作成(1000を適宜変更し、hostにguestを合わせる)
ARG UID=1000
ARG GID=1000
RUN useradd -m -u ${UID} docker

# composerをインストール
RUN curl -s https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

# Node.jsの準備
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -

# 各種インストール
RUN apt-get update \
  # pdoドライバ
  && docker-php-ext-install pdo_mysql \
  # Laravelに必要なパッケージ
  && apt-get install -y git zip unzip \
  # Node.js
  && apt-get install -y nodejs \
  # Vim
  && apt-get install -y vim

# 作成したユーザーに切り替える
USER ${UID}:${GID}

# 作業ディレクトリを変更
WORKDIR /var/www/html