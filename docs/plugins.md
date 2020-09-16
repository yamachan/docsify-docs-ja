# プラグインのリスト

## 全文検索

標準では、現在のページのハイパーリンクが認識され、コンテンツは `localStorage` に保存されます。ファイルへのパスを指定することもできます。

```html
<script>
  window.$docsify = {
    search: 'auto', // 初期値

    search : [
      '/',            // => /README.md
      '/guide',       // => /guide.md
      '/get-started', // => /get-started.md
      '/ja-jpn/',      // => /ja-jp/README.md
    ],

    // コンプリート構成パラメーター
    search: {
      maxAge: 86400000, // 有効期限、初期値は1日
      paths: [], // 'auto' でも同じ
      placeholder: 'Type to search',

      // ローカル言語化
      placeholder: {
        '/ja-jp/': '検索',
        '/': 'Type to search'
      },

      noData: 'No Results!',

      // ローカル言語化
      noData: {
        '/ja-jp/': '結果がありません',
        '/': 'No Results'
      },

      // 見出しの深さ: 1 - 6
      depth: 2,

      hideOtherSidebarContent: false, // 他のサイドバーコンテンツを非表示にするかどうか

      // 同じドメインにある複数のWebサイト間の検索インデックスの衝突を回避する
      namespace: 'website-1',

      // パス接頭辞(名前空間)に異なるインデックスを使用します。
      // 注:'auto' モードでのみ機能します。
      //
      // インデックスを初期化する際、サイドバーから最初のパスを探します。
      // リストのプレフィックスと一致する場合、対応するインデックスに切り替えます。
      pathNamespaces: ['/ja-jp', '/ru-ru', '/ru-ru/v1'],

      // プレフィックスに一致する正規表現を指定できます。 
      // この場合、一致する部分文字列は、インデックスを識別するために使用されます。
      pathNamespaces: /^(\/(ja-jp|ru-ru))?(\/(v1|v2))?/
    }
  }
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/search.min.js"></script>
```

## Google Analytics

プラグインをインストールし、トラックIDを構成します。

```html
<script>
  window.$docsify = {
    ga: 'UA-XXXXX-Y'
  }
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/ga.min.js"></script>
```

`data-ga` で構成します。

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js" data-ga="UA-XXXXX-Y"></script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/ga.min.js"></script>
```

## 絵文字 (emoji)

標準では、絵文字の解析がサポートされています。たとえば `:100:` は :100: に解析されます。ただし、一致する 'non-emoji' 文字列がないため、正確ではありません。 絵文字列を正しく解析する必要がある場合は、このプラグインをインストールする必要があります。

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/emoji.min.js"></script>
```

## 外部 Script

ページ上のスクリプトが外部スクリプトである(src属性を介してjsファイルをインポートする)場合は、このプラグインを動作させる必要があります。

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/external-script.min.js"></script>
```

## 画像の拡大 (Zoom image)

Medium の画像ズーム。[medium-zoom](https://github.com/francoischalifour/medium-zoom) に基づいています。

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/zoom-image.min.js"></script>
```

特定の画像を除外する

```markdown
![](image.png ":no-zoom")
```

## ドキュメントの編集 (Edit on github)

全てのページに `ドキュメントの編集 (Edit on github)` ボタンを追加します。[@njleonzhang](https://github.com/njleonzhang) から提供された [ドキュメント](https://github.com/njleonzhang/docsify-edit-on-github) を確認してください

## デモコードの即時プレビューと jsfiddle 統合

このプラグインを使用すると、サンプルコードをページに即座にレンダリングできるため、読者はプレビューをすぐに確認できます。
 読者がデモボックスを展開すると、そこにソースコードと説明が表示されます。
`Jsfiddle で試す (Try in Jsfiddle)` ボタンをクリックすると、そのサンプルコードで `jsfiddle.net` が開き、読者がコードを修正して自身で試すことができます。

[Vue](https://njleonzhang.github.io/docsify-demo-box-vue/) と [React](https://njleonzhang.github.io/docsify-demo-box-react/) の両方がサポートされています。

## クリップボードへのコピー

`Click to copy` ボタンをすべてのフォーマット済みコードブロックに追加して、ユーザーがドキュメントからサンプルコードを簡単にコピーできるようにします。 [@jperasmus](https://github.com/jperasmus) の提供です。

```html
<script src="//cdn.jsdelivr.net/npm/docsify-copy-code"></script>
```

詳細は [こちら](https://github.com/jperasmus/docsify-copy-code/blob/master/README.md) を参照してください。

## Disqus

Disqus コメント: https://disqus.com/

```html
<script>
  window.$docsify = {
    disqus: 'shortname'
  }
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/disqus.min.js"></script>
```

!> 訳注: Disqus は「インターネットのお気に入りのコメント」用プラグイン

## Gitalk

[Gitalk](https://github.com/gitalk/gitalk) は、Github Issue and Preact に基づく最新のコメントコンポーネントです。

```html
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/gitalk/dist/gitalk.css">

<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/gitalk.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/gitalk/dist/gitalk.min.js"></script>
<script>
  const gitalk = new Gitalk({
    clientID: 'Github Application Client ID',
    clientSecret: 'Github Application Client Secret',
    repo: 'Github repo',
    owner: 'Github repo owner',
    admin: ['Github repo collaborators, only these guys can initialize github issues'],
    // facebook-like distraction free mode
    distractionFreeMode: false
  })
</script>
```

## ページ化 (Pagination)

docsify 用のページ化 (Pagination) プラグイン。 [@imyelo](https://github.com/imyelo) の提供です。

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/docsify-pagination/dist/docsify-pagination.min.js"></script>
```

## タブ表示 (Tabs)

Markdown からタブ付きコンテンツを表示するための docsify.js プラグイン。

- [ドキュメントとデモ](https://jhildenbiddle.github.io/docsify-tabs)

[@jhildenbiddle](https://github.com/jhildenbiddle/docsify-tabs) の提供です。

## その他のプラグイン

[awesome-docsify](awesome?id=plugins) を参照してください。
