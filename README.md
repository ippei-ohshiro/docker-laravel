# docker-laravel

## 環境情報
- macOS
- git version 2.29.2
- PHP 7.4.12
- Composer version 1.10.7
- Docker version 19.03.13
- docker-compose version 1.27.4
- Laravel Framework 8.13.0


## 構築

## appコンテナ
docker-compose.yml があるディレクトリ
```
$ docker-compose up -d --build
```

コンテナ一覧を表示
```
$ docker-compose ps
```

### appコンテナ内ミドルウェアのバージョン確認
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

## WEBコンテナ(ウェブサーバー)
```
$ docker-compose down
$ docker-compose up -d --build
```

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

### 開発中のエラー
Webコンテナがbuildできない
```
$ docker logs { コンテナID }
```
エラー内容
/etc/nginx/conf.d/default.conf differs from the packaged version
default.confがパッケージのものと異なる。

## Laravelコンテナ
```
$ docker-compose exec app bash
$ composer create-project --prefer-dist "laravel/laravel=8.*" .
$ php artisan -V
```

## DBコンテナ（MySQL）
```
$ docker-compose down
$ docker-compose up -d --build
$ docker-compose ps
$ docker-compose exec db mysql -V
```

backend/.env及びbackend/.env.exampleの修正
```
DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=laravel_local
DB_USERNAME=phper
DB_PASSWORD=secret
```

マイグレーション
```
$ docker-compose exec app bash
$ php artisan migrate
```

仮データ作成
```
$ docker-compose exec app bash
php artisan tinker
>>> $user = new App\Models\User();
>>> $user->name = 'phper';
>>> $user->email = 'phper@example.com';
>>> $user->password = Hash::make('secret');
>>> $user->save();
```