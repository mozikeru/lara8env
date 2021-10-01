# 元URL
https://note.com/koushikagawa/n/nc63a8ae2e810#YsVG8
※mysqlが起動出来なかった為、mariadbを使うように変えたり、
phpmyadminの接続設定を一部変えたりしている。

# 使用方法
## 対象ファイル配置
www/html配下に動作対象の各PHPを配置
※リモートアクセスしてgit経由で配置し既存コードをデバッグする

## DBデータについて
phpmyadmin経由でDBを作成するか、
mysqlコンテナにリモートアクセスしてcliでDBを流し込んで設置。
ホスト側のmysql/mysqlディレクトリを/var/lib/mysqlとしてマウントするようにしてある。

## mysql root password
secret
※ docker-compose.ymlにて規定

## 起動方法
(docker-compose.yamlが存在するディレクトリにて)
docker-compose up -d

## ブラウザアクセス
[ドキュメントルート]
http://localhost:8080/

[phpmyadmin]
http://localhost:8888/

# リモートアクセスについて
VSCodeのremote container拡張を使用してphpコンテナに接続し、
各種作業を実施する。
(docker exec -it [コンテナID] bashでも可)

# Laravelを使用する場合
## Laravelプロジェクト作成
phpコンテナに接続し、/var/www配下にプロジェクトを作成する
cd /var/www
composer create-project --prefer-dist laravel/laravel project

## ディレクトリのパーミッション変更
chmod -R 777 /var/www/project/storage/

## publicに対するシンボリックリンクの作成
ln -s /var/www/project/public /var/www/html