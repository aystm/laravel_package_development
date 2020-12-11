## laravelパッケージ開発環境


1. docker立ち上げ

```bash
$ docker-compose up -d
$ docker exec -it work_larapack bash

$ cd project
$ composer install
```

2. 開発中のパッケージを`/packages`に設置
3. `/project/composer.json`にrepositoriesを追加


```
// requireに追加
"パッケージ名": "dev-master"

// 追加
"repositories": [
        {
            "type": "path",
            "url": "../packages/{パッケージディレクトリ}",
            "symlink": true
        }
    ]

```

## 備考

- パッケージ変更時に`composer update`は不要
- `/packages`にパッケージをcloneして作業する