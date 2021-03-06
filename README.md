# [Docker_for_Ruby_on_Rails](https://github.com/prgyukke/Docker_for_Ruby_on_Rails)
## はじめに
プロジェクトディレクトリを`app`コンテナ内の`/var/www/app`にマウントしています。  
OSXにて、[Docker For Mac](https://www.docker.com/docker-mac)のインストール前提です。  
[Docker Community Edition for Mac - Docker Store](https://store.docker.com/editions/community/docker-ce-desktop-mac)の[Get Docker]をクリックしてダウンロード後、インストールしてください。 
  
ビルトインサーバは自動起動です。  
`http://localhost:3000/`にて確認可能です。  

### 各バージョン
- Ruby 2.5
- Rails 5.1.4
- postgres 10

## 環境構築
### 初回のみ
```
$ git clone git@github.com:prgyukke/sample_app.git
$ cd sample_app/
$ docker-compose up -d --build
```

dbコンテナでテスト用データベースを作成
```
$ docker exec -it sample_app_db_1 /bin/bash
# psql -U app --command 'create database app_test;'
# exit
```

appコンテナに入る
```
$ docker exec -it sample_app_app_1 /bin/bash
# (必要であれば)migrate
# rails db:migrate
```

### 2回目以降
```
$ cd sample_app/
$ docker-compose up -d
```

### コンテナに入る際
```
$ docker exec -it sample_app_app_1 /bin/bash
```

### コンテナを抜ける際
```
# コンテナ上にて
# exit
```

### 開発終了時
```
$ docker-compose down
$ docker rmi sample_app_app
```
