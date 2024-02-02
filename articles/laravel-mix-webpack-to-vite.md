---
title: "Laravel Mix(webpack) から Laravel Vite プラグインを使わずに Vite へ移行する"
emoji: "🙆"
type: "tech"
topics: ["Laravel","webpack","LaravelMix","Vite","Vue.js"]
published: false
---
# はじめに
「Laravel Mix Vite 移行」等で検索した際に、Laravel Vite プラグインを使った方法しか出てこなかったため（2024年2月現在）、Laravel Vite プラグインを使わずに Vite を導入する方法について記事にまとめることにしました。
Laravel Vite プラグインは、Laravel バージョンが 9.19.0 以降である必要があります。（詳細は[こちら](https://github.com/laravel/vite-plugin/blob/0.x/UPGRADE.md#migrating-from-laravel-mix-to-vite)）「諸々の都合で、Laravel のバージョンは急には上げられないが Vite 移行はしたい。」という方の参考になれば幸いです。

# 手順
手順としては以下の3つのみですが、Vite の設定ファイル周りでハマりポイントがいくつかありました。

1. Vite のインストール
2. config ファイルの追加
3. 不要な設定ファイルやライブラリの削除

## 1. Vite のインストール
まずは、Vite をインストールします。
```
npm i -D vite
```

## 2. config ファイルの追加
そして、Vite の設定ファイル（vite.config.js or vite.config.ts）を追加します。
Laravel Mix を使用している場合は、webpack.mix.js に諸々の設定が書いてあると思うのですが、ここでやっていることを vite.config.js に移行していきます。
```
import { defineConfig } from 'vite'

export default defineConfig({
  // ...
})
```
