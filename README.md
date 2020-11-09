# docker-laravel

## 環境情報
- macOS
- git version 2.29.2
- PHP 7.4.12
- Composer version 1.10.7
- Docker version 19.03.13
- docker-compose version 1.27.4


## 構築

### コンテナの作成
docker-compose.yml があるディレクトリ
```
$ docker-compose up -d --build
```

コンテナ一覧を表示
```
$ docker-compose ps
```

## appコンテナ内ミドルウェアのバージョン確認
コンテナに入る
```
$ docker-compose exec [サービス名（コンテナ名）] bash
```

PHPのバージョン確認
```
$ php -v
```

Composerのバージョン確認
```
$ composer -V
```

インストール済みの拡張機能の一覧
```
$ php -m
```

コンテナから出る
```
$ exit 
```

またはcontrol + d

### WEBコンテナの作成(ウェブサーバー)
docker-compose down
docker-compose up -d --build

nginxのバージョン確認
```
$ docker-compose exec web nginx -v
```
webコンテナ動作確認
```
$ mkdir backend/public
$ cd backend/public
$ echo "<?php phpinfo();" > phpinfo.php
```

http://127.0.0.1:10080/phpinfo.phpにブラウザでアクセス

##　開発中のエラー
Webコンテナがbuildできない
```
$ docker logs { コンテナID }
```
エラー内容
/etc/nginx/conf.d/default.conf differs from the packaged version
default.confがパッケージのものと異なる。