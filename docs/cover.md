# カバーページ

カバーページ(`coverpage`)を **true** に設定してカバー機能をアクティブにします。[カバーページ 構成](configuration.md#coverpage) も参照してください。

## 基本的な使い方

カバーページ(`coverpage`)を **true** に設定し、`_coverpage.md` を作成します:

```html
<!-- index.html -->

<script>
  window.$docsify = {
    coverpage: true
  }
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

```markdown
<!-- _coverpage.md -->

![logo](_media/icon.svg)

# docsify <small>4.11.6</small>

> 魔法のドキュメント用サイト生成ツール

- シンプルで軽量
- 静的なhtml生成ではありません
- 複数のテーマ

[GitHub](https://github.com/docsifyjs/docsify/)
[開始する](#docsify)
```

## 背景のカスタマイズ

背景色は標準ではランダムに生成されます。背景色または背景画像をカスタマイズできます:

```markdown
<!-- _coverpage.md -->

# docsify <small>4.11.6</small>

[GitHub](https://github.com/docsifyjs/docsify/)
[クイックスタート](#quick-start)

<!-- background image -->

![](_media/bg.png)

<!-- background color -->

![color](#f0f0f0)
```

## カバーページをトップに

通常、表紙とホームページは同時に表示されます。もちろん、[onlyCover オプション](configuration.md#onlycover) でカバーページを分離することもできます。

## 複数のカバーページ

ドキュメントサイトが複数の言語である場合は、複数のカバーページを設定すると便利な場合があります。

たとえば、ドキュメントの構造は以下のようになります:


```text
.
└── docs
    ├── README.md
    ├── guide.md
    ├── _coverpage.md
    └── ja-jp
        ├── README.md
        └── guide.md
        └── _coverpage.md
```

これで、以下のように設定することができます:

```js
window.$docsify = {
  coverpage: ['/', '/ja-jp/']
};
```

もしくはファイル名を明記します:

```js
window.$docsify = {
  coverpage: {
    '/': 'cover.md',
    '/ja-jp/': 'cover.md'
  }
};
```
