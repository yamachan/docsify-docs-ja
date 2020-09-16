# 他のページを書く

さらに多くのページが必要な場合、単に docsify ディレクトリに追加のマークダウンファイルを作成します。`guide.md` という名前のファイルを作成すると、`/#/guide` からアクセスできます。

例えば、ディレクトリ構造は次のとおりです:

```text
.
└── docs
    ├── README.md
    ├── guide.md
    └── ja-jp
        ├── README.md
        └── guide.md
```

マッチング用ルート

```text
docs/README.md        => http://domain.com
docs/guide.md         => http://domain.com/#/guide
docs/ja-jp/README.md  => http://domain.com/#/ja-jp/
docs/ja-jp/guide.md   => http://domain.com/#/ja-jp/guide
```

## サイドバー

サイドバーを作成するには、独自の `_sidebar.md` を作成します(例については [このドキュメントのサイドバー](https://github.com/docsifyjs/docsify/blob/master/docs/_sidebar.md) を参照してください):

まず、`loadSidebar` を **true** に設定する必要があります。 詳細については [構成の章](configuration.md#loadsidebar) をご覧ください。

```html
<!-- index.html -->

<script>
  window.$docsify = {
    loadSidebar: true
  }
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

`_sidebar.md` を作成します:

```markdown
<!-- docs/_sidebar.md -->

* [Home](/)
* [Guide](guide.md)
```

`./docs` に `.nojekyll` ファイルを作成し、GitHub Pages がアンダースコアで始まるファイルを無視しないようにする必要があります。

!> Docsify は現在のフォルダーで `_sidebar.md` のみを検索して使用します。見つからない場合は `window.$docsify.loadSidebar` に指定された設定にフォールバックします。

ファイル構造の例:

```text
└── docs/
    ├── _sidebar.md
    ├── index.md
    ├── getting-started.md
    └── running-services.md
```

## ネストしたサイドバー

サイドバーの階層化


現在のディレクトリを反映して、サイドバーをナビゲーションを更新することができます。このためには、各フォルダーに `_sidebar.md` ファイルを追加してください。

`_sidebar.md` は各レベルディレクトリからロードされます。現在のディレクトリに `_sidebar.md` がない場合は、親ディレクトリにフォールバックします。たとえば、現在のパスが `/guide/quick-start` の場合 `_sidebar.md` は `/guide/_sidebar.md` から読み込まれます。

エイリアス(`alias`)を指定して、不要なフォールバックを回避できます。

```html
<script>
  window.$docsify = {
    loadSidebar: true,
    alias: {
      '/.*/_sidebar.md': '/_sidebar.md'
    }
  }
</script>
```

!> ルートのランディングページとして使用するサブディレクトリに `README.md` ファイルを作成できます。

## サイドバーの選択からページタイトルを設定する

ページの `title` タグはサイドバーで _選択された_ アイテム名から生成されます。SEO を改善するため、ファイル名の後に文字列を指定してタイトルをカスタマイズできます。

```markdown
<!-- docs/_sidebar.md -->
* [Home](/)
* [Guide](guide.md "このガイドは世界一ィィィィーーーーッ！")
```

## 目次

`_sidebar.md` を作成すると、Markdown ファイルのヘッダーに基づいてサイドバーのコンテンツが自動的に生成されます。

カスタムサイドバーは `subMaxLevel` を設定して目次を自動的に生成することが可能です。[subMaxLevel 構成](configuration.md#submaxlevel) も参照してください。

```html
<!-- index.html -->

<script>
  window.$docsify = {
    loadSidebar: true,
    subMaxLevel: 2
  }
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

## サブヘッダーを無視する

`subMaxLevel` が設定されている場合、普通、各ヘッダーは目次に自動的に追加されます。特定のヘッダーを無視したい場合、`<!-- {docsify-ignore} -->` を追加します。

```markdown
# Getting Started

## Header <!-- {docsify-ignore} -->

このヘッダーは、サイドバーの目次には表示されません。
```

特定ページのすべてのヘッダーを無視するには、ページの最初のヘッダーで `<!-- {docsify-ignore-all} -->` を使用します。

```markdown
# Getting Started <!-- {docsify-ignore-all} -->

## Header

このヘッダーは、サイドバーの目次には表示されません。
```

`<!-- {docsify-ignore} -->` と `<!-- {docsify-ignore-all} -->` はどちらも、対象ページにレンダリングされません。
