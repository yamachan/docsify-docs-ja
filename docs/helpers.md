# Doc ヘルパー

docsify は Markdown 構文を拡張して、ドキュメントを読みやすくします。

> 注: 特別なコード構文の場合は、構成または絵文字との競合を避けるために、それらをコードバックティック(` ``` `)内に配置することをお勧めします。

## 重要コンテンツ

重要コンテンツ(important content)は:

```markdown
!> **Time** is money, my friend!
```

以下のようにレンダーされます:

!> **Time** is money, my friend!

## 一般的なヒント

一般的なヒント(General tips)は:

```markdown
?> _TODO_ unit test
```

以下のようにレンダーされます:

?> _TODO_ unit test

## コンパイルしないリンク

他への相対パスであるリンクの場合、このリンクをコンパイルする必要がないことを docsify に伝える必要があります。例えば:

```md
[link](/demo/)
```

これは `<a href="/#/demo/">link</a>` にコンパイルされ、`/demo/README.md` が読み込まれます。でもあなたは `/demo/index.html` にジャンプしたいかもしれません。

以下のような記述でそれを実現できます:

```md
[link](/demo/ ':ignore')
```

この結果、`<a href="/demo/">link</a>` という html を得るでしょう。心配いりません、リンクのタイトル指定は併用できます:

```md
[link](/demo/ ':ignore title')

<a href="/demo/" title="title">link</a>
```

## リンクに target 属性を指定する

```md
[link](/demo ':target=_blank')
[link](/demo2 ':target=_self')
```

## リンクを無効化する

```md
[link](/demo ':disabled')
```

## Cross-Origin リンク

`routerMode: 'history'` と `externalLinkTarget: '_self'` の両方を設定した場合のみ、これらの Cross-Origin リンクのためこの設定を追加する必要があります:

```md
[example.com](https://example.com/ ':crossorgin')
```

## Github タスクリスト

```md
- [ ] foo
- bar
- [x] baz
- [] bam <~ not working
  - [ ] bim
  - [ ] lim
```

- [ ] foo
- bar
- [x] baz
- [] bam <~ not working
  - [ ] bim
  - [ ] lim

## 画像

```md
![logo](https://docsify.js.org/_media/icon.svg)
```

### リサイズ

```md
![logo](https://docsify.js.org/_media/icon.svg ':size=WIDTHxHEIGHT')
![logo](https://docsify.js.org/_media/icon.svg ':size=50x100')
![logo](https://docsify.js.org/_media/icon.svg ':size=100')

<!-- Support percentage -->

![logo](https://docsify.js.org/_media/icon.svg ':size=10%')
```

![logo](https://docsify.js.org/_media/icon.svg ':size=50x100')
![logo](https://docsify.js.org/_media/icon.svg ':size=100')
![logo](https://docsify.js.org/_media/icon.svg ':size=10%')

### 独自クラス

```md
![logo](https://docsify.js.org/_media/icon.svg ':class=someCssClass')
```

### 独自 ID

```md
![logo](https://docsify.js.org/_media/icon.svg ':id=someCssId')
```

## 見出しの独自 ID

```md
### Hello, world! :id=hello-world
```

## HTML タグ内の Markdown

HTML と Markdownコンテンツの間にスペースを挿入する必要があります。
これは、具体的な要素で Markdown コンテンツをレンダリングする場合に役立ちます。

```markdown
<details>
<summary>Self-assessment (Click to expand)</summary>

- Abc
- Abc

</details>
```

<details>
<summary>Self-assessment (Click to expand)</summary>

- Abc
- Abc

</details>

または、Markdown コンテンツを html タグでラップすることもできます。

```markdown
<div style='color: red'>

- listitem
- listitem
- listitem

</div>
```

<div style='color: red'>

- Abc
- Abc

</div>
