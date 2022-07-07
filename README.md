# Laravel開発環境@Docker

## 概要
DockerでLaravelを手軽に使用出来る様に
(Docker側のみphp,nodeを起動させる想定です。)

### Docker環境
 - Docker 20.10.13
 - docker-compose 1.29.2

### 構築環境
 - php:8.1.6-fpm
 - nginx:1.21.6
 - mysql:8.0.28
 - node:18.2.0

## 手順

### Git clone

```
$ git clone https://github.com/rinonkia/Docker-Laravel.git
```

### 環境変数コピー
```
$ cd Docker-Laravel
$ cp .env.sample .env
```
### Docker起動
```
$ docker-compose up -d
```
### laravelプロジェクト配置
```
$ docker-compose exec laravel bash
# rm -f laravel/.gitignore //フォルダの中身が空じゃないとエラーになる
# composer create-project laravel/laravel laravel
# composer create-project "laravel/laravel=8.*" laravel //バージョン指定したい場合
```
### Laravel配置で以下のエラーが出る場合
```
Creating a "laravel/laravel" project at "./laravel"

In CurlDownloader.php line 645:

  The "https://mirrors.cloud.tencent.com/composer/packages.json" file could not be downloaded (HTTP/1.1 404 Not Found)


# composer config -g repo.packagist composer https://packagist.org //パッケージミラーURLを変更

```
### laravelインストール後
```
# cd laravel
# php artisan key:generate
# chown -R nginx:nginx storage
# exit
```
### この状態で動きますがlaravel編集しにくいので修正するフォルダの権限を変更します。
```
$ USERNAME=$(whoami)
$ sudo chown -R $USERNAME:$USERNAME laravel/app
$ sudo chown -R $USERNAME:$USERNAME laravel/routes
$ sudo chown -R $USERNAME:$USERNAME laravel/resources
$ sudo chown -R $USERNAME:$USERNAME laravel/config
```
