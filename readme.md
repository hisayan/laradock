# Laradock for KGX

## TODO

command もしくは entrypoint の、整理整頓

### 初回のみ

```
$ docker-compose exec -u laradock workspace bash -c -i \
  "composer install && cp .env.example .env && php artisan key:generate && npm install"
```

TODO: まだ検証していない
TODO: .env の COMPOSER_GLOBAL_INSTALL について調査

### docker-sync

docker-sync は、やっぱり速そうだ。あらかじめ起動させておくこと。

```
$ docker-sync start
```

--watch-poll も必要なくなる。


とおもったけど

```
$ ./sync.sh up nginx mysql redis
```

で、よさげだ。コンテナも起動してくれる

ちなみに

```
$ ./sync.sh bash
```

で、workspace にはいれる。便利。

### 起動

コンテナの起動

```
$ docker-compose up -d nginx mysql redis phpmyadmin
```

一撃

```
$ docker-compose exec -u laradock workspace bash -c -i "npm run hot -- --host 0.0.0.0"
```

docker の workspace container に入る

```
$ docker-compose exec -u laradock workspace bash
```

その後、起動する。

```
$ npm run hot -- --host 0.0.0.0
```

docker-sync 未使用時は、watch-poll する必要がある。

```
$ npm run hot -- --host 0.0.0.0 --watch-poll"
```