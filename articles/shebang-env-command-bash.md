---
title: "#!/usr/bin/env bash をちゃんと理解する"
emoji: "🗂"
type: "tech"
topics: ["Shell","Shebang","シェバン","Zsh","Bash"]
published: true
---
シェルスクリプトを書く際に、ソースコードの一行目に書く記述について。

```
#!/usr/bin/env bash

echo "Hello, World!"
```
## #!
- #! から始まる行のことを Shebang(シェバン)と呼ぶ
    - ハッシュ・バン（hash bang）、シェル・バン（shell bang）、シャープ・バン（sharp bang）とも呼ぶが、これらを縮めたシェバンという呼び方が一般的らしい
    - [Wiki](https://ja.wikipedia.org/wiki/%E3%82%B7%E3%83%90%E3%83%B3_(Unix))
- 使用するインタプリタを指定する
    - インタプリタとコンパイラの違い
        - インタプリタ：ソースコードを一行ずつバイナリコードへ翻訳して実行する
            - 翻訳と実行が同時に行われる
            - プログラムをすぐ実行できる、エラーを見つけやすい、実行速度が遅い
        - コンパイラ：ソースコードを全てまとめてバイナリコードへ翻訳
            - 実行は別で行う
            - プログラムの実行速度は速いが、実行までに手間がかかる、変更があったら再コンパイル
        - [コンパイラとインタプリタとは？現役エンジニアが分かりやすく解説](https://blog.codecamp.jp/compiler-interpreter-commentary)
    - インタプリタを指定することでプログラムの移植性が高くなる
        - 異なるOS（環境）でも動作する能力
        - [移植性とは？意味をわかりやすく解説](https://trends.codecamp.jp/blogs/media/terminology216#:~:text=%E3%83%97%E3%83%AD%E3%82%B0%E3%83%A9%E3%83%9F%E3%83%B3%E3%82%B0%E3%81%AB%E9%96%A2%E4%BF%82%E3%81%99%E3%82%8B%E5%B0%82%E9%96%80,%E3%81%8C%E9%AB%98%E3%81%84%E3%81%A8%E3%81%84%E3%81%86%E3%81%93%E3%81%A8%E3%81%A7%E3%81%99%E3%80%82)
- 参照：[#!/bin/sh は ただのコメントじゃないよ！ Shebangだよ！](https://qiita.com/mohira/items/566ca75d704072bcb26f)
## /user/bin/env
- envコマンド
    - 環境変数の値を一時的に設定 or 削除してコマンド実行できる
    - PATH環境変数の通っている場所から指定した言語のインタープリタが検索される
    - 例えば、#!/bin/bash とも記述できるが環境の違いによってパスが違う場合、実行されなくなってしまう
    - 汎用性、移植性が高くなる
- 参照：[Linuxで動かすスクリプトの1行目の設定](https://qiita.com/yumenomatayume/items/bd36f3c51cce33191f51)
## bash
- Bash と Zsh
    - bash（バッシュ）
    - zsh（ゼットシェル）
- 違い
    - zsh はデフォルトで自動補完が効く、bash はパッケージを導入する必要あり
    - zhs はテーマやプラグインをフレームワークを使うことで簡単に導入できる、bash は追加のパッケージが必要
    - bash の設定ファイルは、.bashrc や .bash_profile
    - zsh の設定ファイルは、.zshrc
- Mac と Windows
    - Mac のデフォルトは昔は bash だったが、最近は zsh
    - Windows は PowerShell がデフォルトだが、Ubuntsu などを入れると bash や zsh が使える
- 参照：[BashとZshの違い](https://qiita.com/dev-satoshi/items/bab66fc056c71d0fb630)




