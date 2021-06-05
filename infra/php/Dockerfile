FROM php:8.0-fpm-buster
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]

# root権限でもcomposerコマンドを実行できるように環境変数を設定（root権限だと警告が出るので）
ENV COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer

# バージョンを指定したり処理が高速
COPY --from=composer:2.0 /usr/bin/composer /usr/bin/composer

RUN apt-get update && \
  # run命令が多すぎると最終的にイメージの容量が大きくなってしまうので、できるだけワンライナーで実行できるようにするほうが良い
  apt-get -y install git unzip libzip-dev libicu-dev libonig-dev && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  docker-php-ext-install intl pdo_mysql zip bcmath

# 変更する可能性があるのもは後ろの方に記述している（キャッシュが効くので？）


COPY ./php.ini /usr/local/etc/php/php.ini

WORKDIR /work

