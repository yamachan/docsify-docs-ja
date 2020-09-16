# 構成

`window.$docsify` をオブジェクトとして定義することで Docsify を設定できます:

```html
<script>
  window.$docsify = {
    repo: 'docsifyjs/docsify',
    maxLevel: 3,
    coverpage: true,
  };
</script>
```

設定は関数として定義することもできます。その場合、最初の引数は Docsify `vm` インスタンスです。関数は設定オブジェクトを返す必要があります。
これは、マークダウン設定などの場所で `vm` を参照するのに役立ちます。

```html
<script>
  window.$docsify = function(vm) {
    return {
      markdown: {
        renderer: {
          code(code, lang) {
            // ... `vm` を利用したコード ...
          },
        },
      },
    };
  };
</script>
```

## el

- Type: `String`
- Default: `#app`

初期化時にマウントされる DOM 要素。CSSセレクター文字列または実際の [HTMLElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement) にすることができます。

```js
window.$docsify = {
  el: '#app',
};
```

## repo

- Type: `String`
- Default: `null`

リポジトリの URL を構成する、もしくは `ユーザー名/リポジトリ` の文字列で、[GitHub Corner](http://tholman.com/github-corners/) ウィジェットをサイトの右上隅に追加できます。

```js
window.$docsify = {
  repo: 'docsifyjs/docsify',
  // or
  repo: 'https://github.com/docsifyjs/docsify/',
};
```

## maxLevel

- Type: `Number`
- Default: `6`

目次のレベル最大値。

```js
window.$docsify = {
  maxLevel: 4,
};
```

## loadNavbar

- Type: `Boolean|String`
- Default: `false`

**true** の場合、Markdownファイル `_navbar.md` からナビバーをロードします。それ以外の場合、指定されたパスからロードします。

```js
window.$docsify = {
  // _navbar.md からロード
  loadNavbar: true,

  // nav.md からロード
  loadNavbar: 'nav.md',
};
```

## loadSidebar

- Type: `Boolean|String`
- Default: `false`

**true** の場合、Markdownファイル `_sidebar.md` からサイドバーをロードします。それ以外の場合は、指定したパスからサイドバーをロードします。

```js
window.$docsify = {
  // _sidebar.md からロード
  loadSidebar: true,

  // summary.md からロード
  loadSidebar: 'summary.md',
};
```

## hideSidebar

- Type : `Boolean`
- Default: `true`

このオプションはサイドバーを完全に非表示にし、サイドにコンテンツをレンダリングしません。

```js
window.$docsify = {
  hideSidebar: true,
};
```

## subMaxLevel

- Type: `Number`
- Default: `0`

カスタムサイドバーに目次(TOC: Table of Contents)を追加します。

```js
window.$docsify = {
  subMaxLevel: 2,
};
```

## auto2top

- Type: `Boolean`
- Default: `false`

ルートが変更されると、画面の上部までスクロールします。

```js
window.$docsify = {
  auto2top: true,
};
```

## homepage

- Type: `String`
- Default: `README.md`

docs フォルダーの `README.md` ファイルはウェブサイトのトップ(ホーム)ページとして扱われますが、別のファイルを指定できます。

```js
window.$docsify = {
  // /home.md に変更する
  homepage: 'home.md',

  // もしくは他のリポジトリにある readme を指定する
  homepage:
    'https://raw.githubusercontent.com/docsifyjs/docsify/master/README.md',
};
```

サイドバーにホームページへのリンクがあり、ルートURLにアクセスしたときにそれがアクティブとして表示されるようにするには、それに応じてサイドバーを更新してください:

```markdown
- Sidebar
  - [ホーム](/)
  - [他のページ](another.md)
```

詳細は [#1131](https://github.com/docsifyjs/docsify/issues/1131) を参照してください。

## basePath

- Type: `String`

Webサイトの基本パス。別のディレクトリまたは別のドメイン名を設定できます。

```js
window.$docsify = {
  basePath: '/path/',

  // 他のサイトからファイルをロードする
  basePath: 'https://docsify.js.org/',

  // 他のリポジトリからファイルをロードすることもできます
  basePath:
    'https://raw.githubusercontent.com/ryanmcdermott/clean-code-javascript/master/',
};
```

## relativePath

- Type: `Boolean`
- Default: `false`

**true** の場合、リンクは現在のコンテキストを基準にしています。

たとえば、ディレクトリ構造は次のとおりです:

```text
.
└── docs
    ├── README.md
    ├── guide.md
    └── ja-jp
        ├── README.md
        ├── guide.md
        └── config
            └── example.md
```

相対パスが有効で現在の URL が `http://domain.com/ja-jp/README` の場合、リンクは次のように解決されます:

```text
guide.md              => http://domain.com/ja-jp/guide
config/example.md     => http://domain.com/ja-jp/config/example
../README.md          => http://domain.com/README
/README.md            => http://domain.com/README
```

```js
window.$docsify = {
  // 相対パスが有効
  relativePath: true,

  // 相対パスが無効 (初期値はこちら)
  relativePath: false,
};
```

## coverpage

- Type: `Boolean|String|String[]|Object`
- Default: `false`

[カバー機能](cover.md) をアクティブにします。**true** の場合、`_coverpage.md` からロードされます。

```js
window.$docsify = {
  coverpage: true,

  // 独自のファイル名
  coverpage: 'cover.md',

  // 複数のカバー
  coverpage: ['/', '/ja-jp/'],

  // 複数のカバーと独自のファイル名
  coverpage: {
    '/': 'cover.md',
    '/ja-jp/': 'cover.md',
  },
};
```

## logo

- Type: `String`

サイドバーに表示されるウェブサイトのロゴ。CSS を使用してサイズを変更できます。

```js
window.$docsify = {
  logo: '/_media/icon.svg',
};
```

## name

- Type: `String`

サイドバーに表示されるWebサイト名。

```js
window.$docsify = {
  name: 'docsify',
};
```

`name` フィールドには、カスタマイズを容易にするため、HTML を含めることもできます。

```js
window.$docsify = {
  name: '<span>docsify</span>',
};
```

## nameLink

- Type: `String`
- Default: `window.location.pathname`

Webサイト名からリンクされる URL。

```js
window.$docsify = {
  nameLink: '/',

  // For each route
  nameLink: {
    '/zh-cn/': '/zh-cn/',
    '/ja-jp/': '/ja-jp/',
    '/': '/',
  },
};
```

## markdown

- Type: `Function`

[Markdown 構成](markdown.md) を参照してください。

```js
window.$docsify = {
  // object
  markdown: {
    smartypants: true,
    renderer: {
      link: function() {
        // ...
      },
    },
  },

  // function
  markdown: function(marked, renderer) {
    // ...
    return marked;
  },
};
```

## themeColor

- Type: `String`

テーマの色をカスタマイズします。[CSS3 変数](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_variables) 機能と、古いブラウザではポリフィル(polyfill)を使用します。

```js
window.$docsify = {
  themeColor: '#3F51B5',
};
```

## alias

- Type: `Object`

ルートエイリアスを設定します。ルーティングルールは自由に管理できます。正規表現(RegExp)をサポートします。

```js
window.$docsify = {
  alias: {
    '/foo/(+*)': '/bar/$1', // 正規表現のサポート
    '/zh-cn/changelog': '/changelog',
    '/changelog':
      'https://raw.githubusercontent.com/docsifyjs/docsify/master/CHANGELOG',
    '/.*/_sidebar.md': '/_sidebar.md', // #301 を参照
  },
};
```

## autoHeader

- type: `Boolean`

`loadSidebar` と `autoHeader` の両方が有効になっている場合、`_sidebar.md` 内の各リンクについて、HTMLに変換する前にページにヘッダーを付加します。[#78](https://github.com/docsifyjs/docsify/issues/78) も参照してください。

```js
window.$docsify = {
  loadSidebar: true,
  autoHeader: true,
};
```

## executeScript

- type: `Boolean`

ページでスクリプトを実行します。最初の script タグ([demo](themes))のみを解析します。Vue が存在する場合、標準でオンになっています。

```js
window.$docsify = {
  executeScript: true,
};
```

```markdown
## これはテストです

<script>
  console.log(2333)
</script>
```

外部スクリプトを実行している場合(例: jsfiddle の埋め込みデモ)は、[外部スクリプト](plugins.md?id=external-script) プラグインが含まれていることを確認してください。

## noEmoji

- type: `Boolean`

絵文字の解析を無効にします。

```js
window.$docsify = {
  noEmoji: true,
};
```

?> このオプションが `false` であるが、特定の絵文字を処理したくない場合は、[こちら](https://github.com/docsifyjs/docsify/issues/742#issuecomment-586313143) を参照してください

## mergeNavbar

- type: `Boolean`

小さな画面では、ナビバー(Navbar)はサイドバーと統合されます。

```js
window.$docsify = {
  mergeNavbar: true,
};
```

## formatUpdated

- type: `String|Function`

**{docsify-updated<span>}</span>** 変数を利用して、ファイルの更新日を表示できます。 そして表示は `formatUpdated` でフォーマットします。[こちらの Patterns 情報](https://github.com/lukeed/tinydate#patterns) も参照してください。

```js
window.$docsify = {
  formatUpdated: '{MM}/{DD} {HH}:{mm}',

  formatUpdated: function(time) {
    // ...

    return time;
  },
};
```

## externalLinkTarget

- type: `String`
- default: `_blank`

Markdown 内の外部リンクを開くターゲット。デフォルトは `'_blank'`（新しいウィンドウ/タブ）

```js
window.$docsify = {
  externalLinkTarget: '_self', // default: '_blank'
};
```

## cornerExternalLinkTarget

- type:`String`
- default:`_blank`

右上隅にある外部リンクを開くターゲット。デフォルトは `'_blank'`（新しいウィンドウ/タブ）

```js
window.$docsify = {
  cornerExternalLinkTarget: '_self', // default: '_blank'
};
```

## externalLinkRel

- type: `String`
- default: `noopener`

デフォルトの `'noopener'` (オープナーなし)は、新しく開いた外部ページ([externalLinkTarget](#externallinktarget) が `'_blank'` の場合)がページを制御する機能を持たないようにします。
`'_blank'` でない場合、`rel` は設定されません。
このオプションを使用する理由の詳細については、[この投稿](https://mathiasbynens.github.io/rel-noopener/) を参照してください。

```js
window.$docsify = {
  externalLinkRel: '', // 初期値: 'noopener'
};
```

## routerMode

- type: `String`
- default: `hash`

```js
window.$docsify = {
  routerMode: 'history', // 初期値: 'hash'
};
```

## noCompileLinks

- type: `Array`

docsify でリンクを処理したくない場合があります。[＃203](https://github.com/docsifyjs/docsify/issues/203) を参照してください。

```js
window.$docsify = {
  noCompileLinks: ['/foo', '/bar/.*'],
};
```

## onlyCover

- type: `Boolean`

トップページにアクセスすると、カバーページのみが読み込まれます。

```js
window.$docsify = {
  onlyCover: false,
};
```

## requestHeaders

- type: `Object`

リクエストのリソースヘッダーを設定します。

```js
window.$docsify = {
  requestHeaders: {
    'x-token': 'xxx',
  },
};
```

キャッシュの設定など:

```js
window.$docsify = {
  requestHeaders: {
    'cache-control': 'max-age=600',
  },
};
```

## ext

- type: `String`

ファイル拡張子をリクエストする。


```js
window.$docsify = {
  ext: '.md',
};
```

## fallbackLanguages

- type: `Array<string>`

存在しないローカルページがリクエストされた際、デフォルトの言語にフォールバックする言語のリスト。

例:

- `/de/overview` ページを取得しようとします。このページが存在する場合は表示されます。
- 次に、デフォルトのページ `/overview`(デフォルトの言語によって異なります)を取得しようとします。このページが存在する場合は表示されます。
- 次に、404ページを表示します。

```js
window.$docsify = {
  fallbackLanguages: ['fr', 'de'],
};
```

## notFoundPage

- type: `Boolean` | `String` | `Object`

`_404.md` ファイルをロードします:

```js
window.$docsify = {
  notFoundPage: true,
};
```

404 ページのカスタマイズされたパスをロードします:

```js
window.$docsify = {
  notFoundPage: 'my404.md',
};
```

ローカル言語化に応じて適切な 404 ページをロードします:

```js
window.$docsify = {
  notFoundPage: {
    '/': '_404.md',
    '/de': 'de/_404.md',
  },
};
```

> 注: fallbackLanguages オプションは `notFoundPage` オプションと一緒に動作しません。

## topMargin

- type: `Number`
- default: `0`

コンテンツページをスクロールして選択したセクションに移動するとき、上部にスペースを追加します。 これは _sticky-header_ レイアウトを使用時に、アンカーをヘッダーの下部に揃えたい場合に便利です。

```js
window.$docsify = {
  topMargin: 90, // 初期値: 0
};
```
