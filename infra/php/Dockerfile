# 設定値の補足
# FROM命令はイメージビルドのためのベースイメージを設定。
#   FROM イメージ名:タグ名 で指定。 
# SHELL命令のデフォルト値 : SHELL ["/bin/sh", "-c"]
#   -o オプションはオプションを設定するためのオプションです。
#   -e オプションを定義しておくと、そのシェルスクリプト内で何らかのエラーが発生した時点で、それ以降の処理を中断できます。
#   -u オプションを定義しておくと、未定義の変数に対して読み込み等を行おうとした際にエラーとなります。
#   -x オプションを定義しておくと、実行したコマンドを全て標準エラー出力に出してくれます。
# ENV命令はコンテナ内のサーバー環境変数を設定します。
# COPY命令
#   明示的なコピー元とコピー先のファイルまたはディレクトリを指定して、ローカルファイルを再帰的にコピーします。 COPYでは、場所を宣言する必要があります。
# RUN命令
#   Dockerfileないではapt-getを使用（aptはエラーになるため）
#   apt-get update インストール可能なパッケージの「一覧」を更新
# WORKDIR命令
#   ワークディレクトリを設定する

# ベースイメージ　https://hub.docker.com/_/php
FROM php:7.4-fpm-buster
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]

ENV COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer

COPY --from=composer:1.10 /usr/bin/composer /usr/bin/composer

#  Laravelのインストールに必要なパッケージをインストール
RUN apt-get update && \
  apt-get -y install git unzip libzip-dev libicu-dev libonig-dev && \
  # パッケージインストールで使用したキャッシュファイルを削除
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  # PHP拡張ライブラリ
  docker-php-ext-install intl pdo_mysql zip bcmath

COPY ./php.ini /usr/local/etc/php/php.ini

WORKDIR /work