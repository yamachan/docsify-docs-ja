# 独自のナビバー

## HTML

カスタム(独自の)ナビゲーションが必要な場合は、HTML ベースのナビゲーションバーを作成できます。

!> ドキュメントのリンクは `#/` で始まることに注意してください

```html
<!-- index.html -->

<body>
  <nav>
    <a href="#/">EN</a>
    <a href="#/ja-jp/">日本語</a>
  </nav>
  <div id="app"></div>
</body>
```

## Markdown

または、`loadNavbar` を **true** に設定して `_navbar.md` を作成し、独自の Markdown ベースのナビゲーションファイルを作成できます。[loadNavbar 構成](configuration.md#loadnavbar) を参照してください。

```html
<!-- index.html -->

<script>
  window.$docsify = {
    loadNavbar: true
  }
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

```markdown
<!-- _navbar.md -->

* [En](/)
* [日本語](/ja-jp/)
```

!> `./docs` に `.nojekyll` ファイルを作成して、GitHub Pages がアンダースコアで始まるファイルを無視しないようにする必要があります。

`_navbar.md` は各レベルディレクトリからロードされます。現在のディレクトリに `_navbar.md` が存在しない場合、親ディレクトリにフォールバックします。たとえば、現在のパスが `/guide/quick-start` の場合、`_navbar.md`は `/guide/_navbar.md` から読み込まれます。


## 階層化

特定の親の下にあるアイテムをインデント(桁下げ)することにより、サブリストを作成できます。

```markdown
<!-- _navbar.md -->

- 開始する

  - [クイックスタート](quickstart.md)
  - [他のページを書く](more-pages.md)
  - [独自のナビバー](custom-navbar.md)
  - [カバーページ](cover.md)

- カスタマイズ

  - [構成](configuration.md)
  - [テーマ](themes.md)
  - [プラグインのリスト](plugins.md)
  - [プラグインを書く](write-a-plugin.md)
  - [Markdown 構成](markdown.md)
  - [言語ハイライト](language-highlight.md)
```

以下のように表示されます:

![Nesting navbar](_images/ja-jp/nested-navbar.png '階層化されたナビバー')

## 絵文字プラグインとの組み合わせ

[絵文字プラグイン](plugins#絵文字-emoji) を使用する場合:

```html
<!-- index.html -->

<script>
  window.$docsify = {
    // ...
  }
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/emoji.min.js"></script>
```
たとえば、独自の navbar Markdown ファイルで国旗の絵文字を使用できます:

```markdown
<!-- _navbar.md -->

* [:us:, :uk:](/)
* [:cn:](/zh-cn/)
* [:jp:](/ja-jp/)
```
