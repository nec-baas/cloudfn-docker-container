モバイルバックエンド基盤: Cloud Functions Docker イメージ
=========================================================

Cloud Functions ロジックサーバを実行するための Docker コンテナイメージを作成する Dockerfile と Makefile。
Node.js および Java の各バージョン毎に Dockerfile を用意している。

本 Docker イメージは Docker Hub に登録され、実行時に自動的にダウンロードされる。
このため、利用者は個別に Docker イメージをビルドする必要はない。

Docker コンテナの作成手順
-------------------------

Cloud Functions サーバを稼働させるホスト上で、コンテナを作成する。

各ディレクトリ(例えば Node.js v8 を使用したければ node8) に移動し、make を実行するとコンテナが作成される。
コンテナイメージ名については Makefile に記載している。
