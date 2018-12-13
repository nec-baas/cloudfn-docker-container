Docker イメージのテスト
=======================

ここでは、本 Cloud Functions ロジックサーバを単体で
(BaaSサーバを使用せずに)起動する方法について説明する。

Cloud Functions 実行にあたって
------------------------------

Cloud Functions ロジックサーバを単体起動するには、以下の3つのものが必要である。

* ロジックサーバ (Node.js or Java)
* ユーザコード
* ロジックサーバを起動するための Docker イメージ (本 Dockerfile で作成するもの)

### ロジックサーバ

ロジックサーバは、ホスト上の任意のディレクトリに格納する。
デフォルトは以下の場所である。

* Nodeロジックサーバ: ~/work/work_docker/nodejs_http
* Javaロジックサーバ: ~/work/work_docker/java_http

変更したい場合は、コンテナ作成前に各 Makefile の LOGIC_SERVER_HOST_DIR の変更が必要。

ロジックサーバは事前に上記ディレクトリにインストールしておくこと。

* Nodeロジックサーバの場合は npm install が必要。
* Javaロジックサーバの場合は jar ファイルを格納するだけでよい。

### ユーザコード

Function の実装が格納されたユーザコードをホスト上の任意のディレクトリに格納する。
デフォルトは ~/work/work_docker/user_code である。

変更したい場合は各 Makefile の USER_CODE_HOST_DIR に指定が必要である。

注意事項
--------

プロキシが必要な環境で Cloud Functionsサーバを起動する場合、以下のDockerfileの環境変数を有効にすること。
                  
    ENV http_proxy
    ENV https_proxy
                  
※なお、Debian系の場合、コンテナ内のプロキシサーバの名前解決がうまくいない問題があるため、暫定的に IP を指定している。

make コマンド
-------------

* イメージ生成

        $ make image

* コンテナの起動とロジックサーバの起動

        $ make start

* コンテナの停止

        $ make stop

* コンテナの停止

        $ make rm

* コンテナのイメージの削除

        $ make rmi

* コンテナの起動とコンテナ内のコンソールへ接続。
  なお、この場合はCloud Functionsサーバは起動されない。手動で起動すること。

        $ make bash

各コマンドのパラメータ設定については、Makefileを参照。
なお、Makefile に記載するパラメータは、運用時にはサーバマネージャから設定される。


コンテナの状況確認
------------------

起動済のコンテナの動作を確認後、下記のDockerコマンドを利用できる

* 作成済のコンテナの確認

        $ docker ps -a

* 特定のコンテナの詳細情報の確認

        $ docker inspect [コンテナID/コンテナ名]

* 動作中のコンテナのメモリなどの利用状況の監視

        $ docker stats
     
なお、その他のコマンドについては、Docker のドキュメントを参照のこと。

* Docker Engine:  https://docs.docker.com/engine/
* 日本語訳(非公式):  http://docs.docker.jp/engine/

注意事項
--------

通常、ホストマシン上のDockerデーモンの実行にroot権限が必要だが、
下記のコマンドでユーザをDokcerグループに追加すれば、ユーザ権限で実行できる。
なお、設定を有効するため、設定後に一旦ログアウトすること。

    $ sudo gpasswd -a [ユーザ名] docker
