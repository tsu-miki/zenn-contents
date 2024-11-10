---
title: "F#でソリューションを使って複数プロジェクト管理する"
emoji: "🐡"
type: "tech"
topics: ["fsharp",".NET"]
published: false
---
## 構成
以下のディレクトリ構成でsample-apiを作っていく。
```
sample-api/
├── SampleApi/
│   ├── Program.fs
│   └── SampleApi.fsproj
└── SampleApi.Test/
|   └── Program.fs
|   └── Test.fs
|   └── SampleApi.Test.fsproj
├── sample-api.sln
```

## ソリューションとプロジェクトのイメージ図
ソリューションは複数のプロジェクトを管理するためのコンテナー。
![](/images/solution-multi-project.png)

## 手順
### ソリューションの作成
`dotnet new sln`でソリューションを追加できる。`-o`でアウトプット先のディレクトリを指定する。
```
$ dotnet new sln -o sample-api 
```

### .gitignoreファイルの追加
`dotnet new gitignore`で、.gitignoreファイルを追加できる。
```
$ cd sample-api
$ dotnet new gitignore
```

### プロジェクトの複数作成
テスト用のプロジェクトは、`xunit`で作成して、アプリケーションの方は`web`で作成する。この辺は好みで良い。
```
$ dotnet new web -lang F# -n SampleApi
$ dotnet new xunit -lang F# -n SampleApi.Test
```

### ソリューションにプロジェクトを追加
ソリューションにプロジェクトを追加する。これで`dotnet build`や`dotnet test`で複数プロジェクトのビルドやテストをまとめて実行できるようになる。
```
$ dotnet sln add SampleApi/SampleApi.fsproj 
$ dotnet sln add SampleApi.Test/SampleApi.Test.fsproj
```

### プロジェクト間の依存関係の設定
プロジェクト参照を追加することで、1つのプロジェクト（SampleApi.Test）から他のプロジェクト（SampleApi）を参照できるようになる。

```
$ dotnet add SampleApi.Test/SampleApi.Test.fsproj reference SampleApi/SampleApi.fsproj
```

### ビルドとテストの実行
```
$ dotnet build
$ dotnet test
```

### APIの起動と確認
```
$ dotnet run --project SampleApi
```

## 参考
https://learn.microsoft.com/ja-jp/dotnet/core/tools/dotnet-new
https://learn.microsoft.com/ja-jp/dotnet/core/tools/dotnet-sln

## コード
https://github.com/tsu-miki/fsharp-multi-project-solution