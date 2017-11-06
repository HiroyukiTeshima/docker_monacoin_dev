# docker_monacoin_dev

monacoinの開発環境です。
現時点ではmonacoindが起動できる環境のみとなります。
いずれwebサーバなど追加する予定。

~/.monacoin はローカルPCのmonacoinディレクトリにマウントされます。

仮想環境の中身はmonacoind/Dockerfileを参照してください。必要に応じて最終行のconfigureコマンドの引数など変更してください。
現時点ではウォレット無しのオプションを付加しています(--disable-wallet)。

使い方
clone後、
dockerディレクトリに移動して以下のコマンドを実行します。

    docker-compose build
    docker-compose up

ビルドとupが完了したら、monacoindが起動できる状態です。
以下のコマンドでログインができます。monacoindが起動できるはずです。

    docker exec -it docker_monacoind_1 bash

docker-compopse はctrl+c で終了できます。なお、二回目以降は以下のコマンドで仮想環境が起動します。

    docker-compose start

私は初回up後すぐctrl-cで終了させてdocker-compose startしますｗ