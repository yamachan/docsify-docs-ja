# クイックスタート

Web サイトをローカルで初期化してプレビューするために、`docsify-cli` をグローバルにインストールすることをお勧めします。

```bash
npm i docsify-cli -g
```

## 初期化

`./docs` サブディレクトリにドキュメントを書きたい場合は、`init` コマンドを利用できます。

```bash
docsify init ./docs
```

## コンテンツを書く

`init` が完了すると、`./docs` サブディレクトリに幾つかのファイルが生成されます。

* `index.html` エントリー用のファイル
* `README.md` トップページ
* `.nojekyll` GitHub ページがアンダースコアで始まるファイルを無視しないようにします

まずは `./docs/README.md` ドキュメントを更新しましょう。もちろん、[他のページ](more-pages.md) も追加できます。

## サイトをプレビューする

`docsify serve` でローカルサーバーを実行します。ブラウザーで `http://localhost:3000` にアクセスしてサイトをプレビューできます。

```bash
docsify serve docs
```

?> `docsify-cli` のその他の使用例については、[docsify-cli ドキュメント](https://github.com/docsifyjs/docsify-cli) を参照してください。

## 手動での初期化

`npm` が気に入らない場合や、ツールのインストールに問題がある場合は、手動で `index.html` を作成できます:

```html
<!-- index.html -->

<!DOCTYPE html>
<html>
<head>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <meta charset="UTF-8">
  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/themes/vue.css" />
</head>
<body>
  <div id="app"></div>
  <script>
    window.$docsify = {
      //...
    }
  </script>
  <script src="//cdn.jsdelivr.net/npm/docsify@4"></script>
</body>
</html>
```

### docsify バージョンの指定

?> 以下の例はどちらも、docsify の新しいメジャーバージョンがリリースされたとき(例えば `v4.x.x` => `v5.x.x`)、docsify URL を手動で更新する必要があることに注意が必要です。docsify Webサイトを定期的にチェックし、新しいメジャーバージョンがリリースされているかどうかを確認してください。

URLでメジャーバージョン(`@4`)を指定すると、サイトに大きな問題のない拡張機能(つまり「マイナー」更新)と、バグ修正(つまり「パッチ」更新)のみが自動的に送信されます。これは docsify リソースをロードするために推奨される方法です。

```html
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/themes/vue.css" />
<script src="//cdn.jsdelivr.net/npm/docsify@4"></script>
```

docsify を特定のバージョンにロックする場合は、URLの `@` 記号の後に完全なバージョンを指定します。これは、将来のバージョンの docsify に加えられた変更に影響されず、サイトの外観と動作を維持するための最も安全な方法です。

```html
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4.11.4/themes/vue.css">
<script src="//cdn.jsdelivr.net/npm/docsify@4.11.4"></script>
```

### サイトを手動でプレビューする

システムに Python をインストールしている場合、静的サーバーを実行し、サイトをプレビューできます。

```bash
cd docs && python -m SimpleHTTPServer 3000
```

## 読み込みダイアログ

必要に応じて、docsify がドキュメントのレンダリングを開始する前に、読み込みダイアログを表示できます。

```html
<!-- index.html -->

<div id="app">少々お待ちください...</div>
```

`el` を変更した場合は、`data-app` 属性を設定する必要があります:

```html
<!-- index.html -->

<div data-app id="main">少々お待ちください...</div>

  <script>
    window.$docsify = {
      el: '#main'
    }
  </script>
```

[el 構成](configuration.md#el) と比較してみてください。
