# EC-CUBE 4.1 vagrant docker セットアップ手順

## セットアップ環境

- Apache 2.4.52
- PHP 7.4.27
- MySQL 5.7.37

##  セットアップ

**windows環境の場合改行コードがCR+LFに変換されないようにするためにgitの設定を変更しておく**
**改行コードがCR+LFの場合、docker起動時失敗する**

```
git config --global core.autocrlf input
```

> 任意のディレクトリにリポジトリをクローンする

```
git clone https://github.com/second-fiddle/eccube4-vagrant.git
cd eccube4-vagrant
```

> ec-cube4.1 をクローンする

```
git clone https://github.com/EC-CUBE/ec-cube.git
```

> docker/docker-compose.yml の ECCUBE_AUTH_MAGIC を任意の値に書き換える

> docker-compose.yml を置き換える

- Windows
```
copy /Y docker/docker-compose.yml ec-cube
```
- Mac
```
cp -f docker/docker-compose.yml ec-cube
```

> vagrant 起動

```
vagrant up
```

> 初期設定

```
vagrant ssh
cd /vagrant/ec-cube
docker-compose exec -u www-data ec-cube bin/console eccube:install -n
docker-compose exec ec-cube composer run-script compile
質問はすべてyにした
```

> 動作確認

[フロント(http://192.168.2.100:8080/)](http://192.168.2.100:8080/)

[管理(http://192.168.2.100:8080/admin)](http://192.168.2.100:8080/admin)

## その他

- IPアドレスを変更する場合、vagrantfileの26行目のIPアドレスを変更する
- Postgresの環境にする場合、ec-cube/docker-compose.pgsql.yml の必要な部分をec-cube/docker-compse.ymlに反映する
