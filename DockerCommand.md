<!-- TOC -->

- [1. DockerCommand一覧](#1-dockercommand一覧)
  - [1.1. 目的](#11-目的)
    - [1.1.1. container](#111-container)
    - [1.1.2. image](#112-image)
    - [1.1.3. volume](#113-volume)
    - [1.1.4. network](#114-network)
    - [1.1.5. オプション](#115-オプション)
    - [1.1.6. ps](#116-ps)
  - [1.2. dockerコマンドex](#12-dockerコマンドex)
    - [1.2.1. wordpressとmysqlのコンテナを接続する](#121-wordpressとmysqlのコンテナを接続する)
    - [dockerのファイルコピー](#dockerのファイルコピー)
    - [dockerのマウント](#dockerのマウント)
    - [dockerimage作成](#dockerimage作成)
    - [dockerをコマンドで操作する](#dockerをコマンドで操作する)

<!-- /TOC -->

# 1. DockerCommand一覧

## 1.1. 目的

- Dockerコマンドを整理する

### 1.1.1. container

|副コマンド|内容|省略|主なオプション|
|--|--|--|--|
|Start|コンテナを開始する|可|-i|
|stop|コンテナを停止する|可||
|create|DOckerイメージからコンテナを作成|可|-name -e -p -v|
|run|イメージをダウンロードしてコンテナ作成|可|-name -e -p -v -d -i -t|
|rm|停止したコンテナを削除する|可|-f -v|
|exec|実行中のコンテナ内でプログラムを実行する|可|-i -t|
|ls|コンテナ一覧を表示する|可|-a|
|cp|DockerコンテナとDockerホスト間でファイルをコピーする|可||
|commit|Dockerコンテナをイメージに変換する|可||

### 1.1.2. image

|副コマンド|内容|省略|主なオプション|
|--|--|--|--|
|pull|イメージをダウンロードする|可||
|rm|イメージを削除する|||
|ls|ダウンロードしたイメージ一覧を表示する|不可||
|build|Dockerイメージを作成する|可|-t|

### 1.1.3. volume

|副コマンド|内容|省略|主なオプション|
|--|--|--|--|
|create|ボリュームを作る||--name|
|inspect|ボリュームの詳細情報を表示する|||
|ls|ボリュームの一覧を表示する||-a|
|prune|現在マウントされていないボリュームをすべて削除する|||
|rm|指定したボリュームを削除する|||

### 1.1.4. network

|副コマンド|内容|省略|主なオプション|
|--|--|--|--|
|connect|コンテナをネットワークを接続する|||
|disconnect|コンテナをネットワークから切断する|||
|create|ネットワークを作る|||
|inspect|ネットワークの詳細情報を表示する|||
|ls|ネットワークの一覧を表示する|||
|prune|現在コンテナがつながっていないネットワークをすべて削除する|||
|rm|指定したネットワークを削除する|||

### 1.1.5. オプション

|オプションの書式|内容|
|---|--|
|--name コンテナ名|コンテナ名を指定する|
|-p ホストのポート名:コンテナのポート番号|ポート番号を指定する|
|-v ホストのディスク:コンテナのディレクトリ|ボリュームをマウントする|
|--net=ネットワーク名|コンテナをネットワークに接続する|
|-e 環境変数名＝値|環境変数を指定する|
|-d|バックグラウンドで実行する|
|-i|コンテナに操作端末をつなぐ|
|-t|特殊キーを使用可能する|
|-help|使い方を表示する|

### 1.1.6. ps

|副コマンド|内容|オプション|
|--|--|--|
|ps|動いているコンテナの一覧を表示する||
|ps|存在するコンテナの一覧を表示する|-a|

## 1.2. dockerコマンドex

### 1.2.1. wordpressとmysqlのコンテナを接続する

```
docker network create wordpress000net1

docker run --name mysql000ex11 -dit --net=wordpress000net1 -e MYSQL_ROOT_PASSWORD=myrootpass -e MYSQL_DATABASE=wordpress000db -e MYSQL_USER=wordpress000kun -e MYSQL_PASSWORD=wkunpass mysql --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci --default-authentication-plugin=mysql_native_password

docker run --name wordpress000ex12 -dit --net=wordpress000net1 -p 8080:80 -e WORDPRESS_DB_HOST=mysql000ex11 -e WORDPRESS_DB_NAME=wordpress000db -e WORDPRESS_DB_USER=wordpress000kun -e WORDPRESS_DB_PASSWORD=wkunpass wordpress
```

### dockerのファイルコピー

```
docker cp コピー元 コピー先

docker cp "C:\Users\yuich\OneDrive\デスクトップ\index.html" apa000ex19:/usr/local/apache2/htdocs/
```

### dockerのマウント

- コンテナの中にデータを保存するとコンテナを消去するときにデータも消えてしまう
- データを外部に保存することができる
- データ保存の方法はボリュームマウントとバインドマウントがある
  - ボリュームマウント：DockerEngin上に保存
  
```
  ボリューム作成
  docker volume create apa000vol1
  ボリューム情報表示
  docker volume inspect apa000vol1
  ボリューム削除
  docker volume rm apa000vol1

  作成手順
  docker volume create apa000vol1
  docker run --name apa000ex21 -d -p 8091:80 -v apa000vol1:\usr\local\apache2\htdocs h
  ```

  - バインドマウント: OS上に保存
  
  ```
  docker run --name apa000ex20 -d -p 8090:80 -v "C:\Users\yuich\OneDrive\デスクトップ\apa_folder":/usr/local/apache2/htdocs httpd
  ```

  ### dockerimage作成

  ```
  docker commit コンテナ名 image名

  docker commit apa000ex22 ex22_original1
  ```

  ### dockerをコマンドで操作する

  ```
  docker exec コンテナ名 /bin/bash

  docker run (オプション) イメージ名 /bin/bash
  ```