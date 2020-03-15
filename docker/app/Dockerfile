FROM php:7-fpm

# ユーザーを作成(1000を適宜変更し、hostにguestを合わせる)
ARG DOCKER_UID=1000
ARG DOCKER_USER=docker
ARG DOCKER_PASSWORD=docker

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
  && apt-get install -y vim \
  # sudo
  && apt-get install -y sudo

# ユーザ作成
RUN useradd -m --uid ${DOCKER_UID} --groups sudo ${DOCKER_USER} \
  && echo ${DOCKER_USER}:${DOCKER_PASSWORD} | chpasswd

# 作成したユーザーに切り替える
USER ${DOCKER_USER}

# 作業ディレクトリを変更
WORKDIR /var/www/html