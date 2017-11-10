# docker_monacoin_dev

monacoinの開発環境です。
以下のサーバが起動します

・monacoind実行サーバ

・webサーバ

・dbサーバ

仮想環境の中身はmonacoind/Dockerfileを参照してください。必要に応じて最終行のconfigureコマンドの引数など変更してください。


使い方
clone後、
dockerディレクトリに移動して以下のコマンドを実行します。

    docker-compose build
    docker-compose up -d

webサーバではapacheが起動しており、http://localhost:8080でその確認が行えます。

dockerディレクトリと同じ階層に各仮想環境のディレクトリがマウントされています。

monacoind ・・・~/.monacoindディレクトリをマウント
webapp ・・・・webサーバの/var/www/webappディレクトリ。このディレクトリをdocument rootにする予定です。
（後ほどconfファイルまでdocker上でセットアップする予定）
data ・・・・dbサーバのmysqlデータディレクトリ

以下のコマンドでログインができます。

monacoindが起動するサーバ

    docker exec -it docker_monacoind_1 bash

monacoindは起動していませんので、ログインしてmonacoindを起動してください。conf設定済みで、オプション無しで実行するとtestnetでサービスとして実行されます。
またrpc-jsonポートは19111ポートでフォワードしています。PCから接続可能です。
またwebサーバからも同じポートでアクセスできます。

apacheが起動するサーバ

    docker exec -it docker_webapp_1 bash
80ポートを8080ポートにフォワードしています。


mysqlが起動するサーバ

    docker exec -it docker_db_1 bash
mysqlへのログインユーザやパスワードはdocker-compose.ymlを確認してください。

またネットワークは、webサーバからmonacoind,dbサーバにアクセスできるように設定しています。
こちらもdocker-compose.ymlを確認してください。


以下で仮想環境の停止を行います。

    ocker-compose stop

なお、二回目以降は以下のコマンドで仮想環境が起動します。

    docker-compose start

