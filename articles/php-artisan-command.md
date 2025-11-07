---
title: "php artisan の実体"
emoji: "🎨"
type: "tech"
topics: ["Laravel", "PHP", "Artisan"]
published: true
---

Laravel で開発していると、`php artisan` コマンドをよく打ちます。
何気なく打っていたのですが、こいつの実体がどこにあり、内部でどのように動作しているのか気になったので備忘録として書き残そうと思います。

:::message
 **Laravel 12** をベースに解説しています。Laravel のバージョンによって内部実装が異なる場合があるのでご注意ください。
:::

## php artisan コマンドの理解

```bash
php artisan migrate
```

このコマンドは：
- `php` = PHPインタープリタ
- `artisan` = **実行するPHPスクリプトのファイル名**
- `migrate` = artisanに渡す引数

つまり「artisanファイル」という単なるPHPスクリプトを実行しているだけです。ファイル名を変えても動きます：

```bash
cp artisan mycli
php mycli migrate  # これでも動く
```

### artisanファイルの中身

```php:artisan
#!/usr/bin/env php
<?php

use Illuminate\Foundation\Application;
use Symfony\Component\Console\Input\ArgvInput;

define('LARAVEL_START', microtime(true));

require __DIR__.'/vendor/autoload.php';

$app = require_once __DIR__.'/bootstrap/app.php';

$status = $app->handleCommand(new ArgvInput);

exit($status);
```

やっていることは：
1. Composerのオートローダーを読み込み
2. Laravelアプリケーションをブートストラップ
3. `handleCommand()` に引数を渡して実行

**実際のコマンド処理は行わない。** 単なるエントリーポイントです。

## 実行フロー

```
php artisan migrate
    ↓
① artisan ファイル
    ↓
② Application::handleCommand()
    ↓
③ ConsoleKernel::handle()
    │  ├→ bootstrap() でサービスプロバイダー起動
    │  └→ getArtisan()->run() でコマンド実行
    ↓
④ ArtisanServiceProvider でコマンド登録
    ├→ vendor/laravel/framework 配下の全コマンドをuse
    └→ DIコンテナに登録
    ↓
⑤ Symfony Console で実際のコマンド実行
```

:::message
③〜⑤は「サービスコンテナ」「サービスプロバイダ」「ConsoleKernel」「Symfony Console」などの仕組みを理解する必要あり。詳細は省く。
:::

## ポイント

コマンドは3箇所に存在

| 場所 | 用途 |
|------|------|
| `vendor/laravel/framework/src/Illuminate/*/Console/` | Laravel組み込みコマンド（migrate, make:*, cache:clear等） |
| `routes/console.php` | クロージャベースの簡易コマンド |
| `app/Console/Commands/` | プロジェクト固有のカスタムコマンド |

## まとめ

`php artisan` は：
- ルートの `artisan` ファイルを実行しているだけ
- 実際の処理は全て vendor やアプリ内のコードが担当
- ArtisanServiceProvider がコマンドを一括登録
- Symfony Console でコマンドを実行
