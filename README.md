vagrant-oracle-database-19c
===========================

Vagrant + Oracle Linux 7 + Oracle Database 21c (21.3) シングル環境の簡易セットアップ。

ダウンロード
------------

Oracle Database 21c (21.3)のソフトウェアを[Oracle Database Software Downloads](https://www.oracle.com/database/technologies/oracle-database-software-downloads.html)からダウンロードし、Vagrantfileと同じディレクトリに配置。

* LINUX.X64_213000_db_home.zip

環境変数の設定
--------------

`dotenv.sample`というファイルを`.env`という名前のファイルにコピーし、必要に応じて内容を書き換える。

```shell
ORACLE_BASE=/u01/app/oracle
ORACLE_CHARACTERSET=AL32UTF8
ORACLE_EDITION=EE
ORACLE_HOME=/u01/app/oracle/product/21.0.0/dbhome_1
ORACLE_PASSWORD=oracle
ORACLE_PDB=pdb1
ORACLE_SID=orcl
```

Vagrant設定
-----------

プロキシを利用する必要がある場合、まずvagrant-proxyconfをインストールし、vagrant-proxyconf用の環境変数を設定しておく。

### ホストがmacOS or Linuxの場合 ###

```console
export http_proxy=http://proxy.example.com:80
export https_proxy=http://proxy.example.com:80
vagrant plugin install vagrant-proxyconf

export VAGRANT_HTTP_PROXY=http://proxy.example.com:80
export VAGRANT_HTTPS_PROXY=http://proxy.example.com:80
export VAGRANT_FTP_PROXY=http://proxy.example.com:80
export VAGRANT_NO_PROXY=localhost,127.0.0.1
```

### ホストがWindowsの場合 ###

```console
SET http_proxy=http://proxy.example.com:80
SET https_proxy=http://proxy.example.com:80
vagrant plugin install vagrant-proxyconf

SET VAGRANT_HTTP_PROXY=http://proxy.example.com:80
SET VAGRANT_HTTPS_PROXY=http://proxy.example.com:80
SET VAGRANT_FTP_PROXY=http://proxy.example.com:80
SET VAGRANT_NO_PROXY=localhost,127.0.0.1
```

セットアップ
------------

`vagrant up`を実行すると、内部的に以下が動く。

* Oracle Linux 7のダウンロードと起動
* Oracle Preinstallation RPMのインストール
* ディレクトリの作成
* 環境変数の設定
* oracleユーザーのパスワード設定
* Oracle Databaseのインストール
* リスナーの作成
* データベースの作成

```console
vagrant up
```

動作確認
--------

ゲストOSに接続する。

```console
vagrant ssh
```

ルートに接続し、接続先を確認する。

```console
sudo su - oracle
sqlplus system/oracle
SHOW CON_NAME
```

PDBに接続、接続先を確認する。

```console
sqlplus system/oracle@localhost/pdb1
SHOW CON_NAME
```

Author
------

[Shinichi Akiyama](https://github.com/shakiyam)

License
-------

[MIT License](https://opensource.org/licenses/MIT)
