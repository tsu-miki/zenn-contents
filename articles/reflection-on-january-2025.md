---
title: "生成AI周りでキャッチアップしたことをまとめる"
emoji: "🎉"
type: "tech"
topics: []
published: true
---
1月の中旬からLLMを使った機能の開発をやるチームになったので、その中でキャッチアップしたことをまとめておく。

## 「生成AI」と「LLM」の言葉の違い
正直最初は違いが分かっておらず、「生成AI」とずっと言っていたのですが、調べてみると、今回の開発で利用するのは「LLM」であることが分かりました。

ちなみに、タイトルでは認知度の高い「生成AI」と書いていますが、「LLM」を使った開発なのでそんな感じで使い分けてます。（認知度の理由で、Bizサイドとのコミュニケーションや顧客向け資料等では、「生成AI」でもいいのかなと思います。）

### 生成AI ( Generative AI )
- テキスト/画像/動画/音楽 など複数モダリティを扱う生成技術全般
- 代表例：Stable Diffusion（画像生成）、Sora（動画生成）
- 自然言語処理以外の生成技術を含む

### LLM ( Large Language Model )
- 自然言語処理に特化した大規模言語モデル
- 代表例：GPT-4、Claude、Gemini
- テキスト生成/要約/翻訳など言語タスク限定

## LangChain
LLM を活用したアプリケーション開発を効率化するオープンソースフレームワークのこと。
プロジェクト初期に既にLLMを使った開発をしてるチームに話を聞きに行った際に、LangChain が会話の中で多発して「LangChain ってなに？」となった記憶があります。

どういうものかの説明はこの辺りに任せる。
https://github.com/langchain-ai/langchain
https://www.ibm.com/jp-ja/topics/langchain

ちなみに、LangChain は、Python 意外の言語でもあります。（あくまで Python がデファクトスタンダードですが）
https://github.com/langchain4j/langchain4j
https://github.com/langchain-ai/langchainjs

実験的にやってるのはこの辺り。
https://github.com/tmc/langchaingo
https://github.com/Abraxas-365/langchain-rust
https://github.com/tryAGI/LangChain

## Lang Smith
LLMアプリケーション開発のライフサイクルを支援するプラットフォームのこと。
プロンプト改善や評価・監視機能等が使えて、一番分かり易いユースケースだと複数プロンプトのパフォーマンス比較ができます。

1ユーザー$39/月なので安くはないけど、Prompt Flow より使い易いとビジネスサイドから好評でした。
https://www.langchain.com/langsmith

## LLMLingua
Microsoftが開発したプロンプトを圧縮するオープンソースツール。
最大20倍の圧縮率を実現するらしい。日本語もちゃんと対応できたら費用削減になりそう。
https://github.com/microsoft/LLMLingua