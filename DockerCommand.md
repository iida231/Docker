# DockerCommand一覧

## 目的

- Dockerコマンドを整理する

### container

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

### image

|副コマンド|内容|省略|主なオプション|
|--|--|--|--|
|pull|イメージをダウンロードする|可||
|rm|イメージを削除する|||
|ls|ダウンロードしたイメージ一覧を表示する|不可||
|build|Dockerイメージを作成する|可|-t|

### volume

|副コマンド|内容|省略|主なオプション|
|--|--|--|--|
|create|ボリュームを作る||--name|
|inspect|ボリュームの詳細情報を表示する|||
|ls|ボリュームの一覧を表示する||-a|
|prune|現在マウントされていないボリュームをすべて削除する|||
|rm|指定したボリュームを削除する|||

### network

|副コマンド|内容|省略|主なオプション|
|--|--|--|--|
|connect|コンテナをネットワークを接続する|||
|disconnect|コンテナをネットワークから切断する|||
|create|ネットワークを作る|||
|inspect|ネットワークの詳細情報を表示する|||
|ls|ネットワークの一覧を表示する|||
|prune|現在コンテナがつながっていないネットワークをすべて削除する|||
|rm|指定したネットワークを削除する|||

### オプション

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