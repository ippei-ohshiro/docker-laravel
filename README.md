# docker-laravel

## 環境情報
- macOS
- git version 2.29.2
- 7.4.12
- Composer version 1.10.7
- Docker version 19.03.13
- docker-compose version 1.27.4


## build & up

### appコンテナの作成
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