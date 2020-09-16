# Server-Side Rendering (SSR)

参照: https://docsify.now.sh

リポジトリ: https://github.com/docsifyjs/docsify-ssr-demo

## なぜ SSR?

- より良い SEO (Search Engine Optimization)
- かっこ良い

## 開始する

`now` と `docsify-cli` を対象プロジェクトにインストールする。

```bash
npm i now docsify-cli -D
```

ドキュメントが `./docs` サブディレクトリにある場合、`package.json` を編集します。

```json
{
  "name": "my-project",
  "scripts": {
    "start": "docsify start . -c ssr.config.js",
    "deploy": "now -p"
  },
  "files": [
    "docs"
  ],
  "docsify": {
    "config": {
      "basePath": "https://docsify.js.org/",
      "loadSidebar": true,
      "loadNavbar": true,
      "coverpage": true,
      "name": "docsify"
    }
  }
}
```

!> `basePath` は、webpack の `publicPath` と同じです。ローカルファイルまたはリモートファイルを使用できます。

ローカルでプレビューして、動作するかどうか確認できます。

```bash
npm start

# open http://localhost:4000
```

公開しましょう！

```bash
now -p
```

これで、ドキュメントサイトで SSR がサポートされました。

## 独自のテンプレート

ページ全体の HTML テンプレートを提供できます。例えば:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>docsify</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0">
  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify/themes/vue.css" title="vue">
</head>
<body>
  <!--inject-app-->
  <!--inject-config-->
  <script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.js"></script>
  <script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/search.js"></script>
  <script src="//cdn.jsdelivr.net/npm/prismjs/components/prism-bash.min.js"></script>
  <script src="//cdn.jsdelivr.net/npm/prismjs/components/prism-markdown.min.js"></script>
  <script src="//cdn.jsdelivr.net/npm/prismjs/components/prism-nginx.min.js"></script>
</body>
</html>
```

テンプレートには、レンダリングされるアプリコンテンツに関するコメントを含める必要があります。
 - `<!--inject-app-->`
 - `<!--inject-config-->`

## 構成 (Configuration)

特別な設定ファイルまたは `package.json` で設定できます。

```js
module.exports = {
  template: './ssr.html',
  maxAge: 60 * 60 * 1000, // lru-cache config
  config: {
   // docsify config
  }
}
```

## VPS にデプロイする

Node サーバーで直接 `docsify start` を実行するか、`docsify-server-renderer` を使用して独自のサーバーアプリを開発できます。

```js
var Renderer = require('docsify-server-renderer')
var readFileSync = require('fs').readFileSync

// init
var renderer = new Renderer({
  template: readFileSync('./docs/index.template.html', 'utf-8'),
  config: {
    name: 'docsify',
    repo: 'docsifyjs/docsify'
  }
})

renderer.renderToString(url)
  .then(html => {})
  .catch(err => {})
```
