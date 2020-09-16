# Markdown 構成

**docsify** は、Markdown パーサーとして [marked](https://github.com/markedjs/marked) を使用します。`renderer` をカスタマイズすることで、Markdown コンテンツを HTML にレンダリングする方法をカスタマイズできます:

```js
window.$docsify = {
  markdown: {
    smartypants: true,
    renderer: {
      link: function() {
        // ...
      }
    }
  }
}
```

?> 構成オプションのリファレンス: [marked documentation](https://marked.js.org/#/USING_ADVANCED.md)

解析ルールを完全にカスタマイズすることもできます。

```js
window.$docsify = {
  markdown: function(marked, renderer) {
    // ...

    return marked
  }
}
```

## mermaid のサポート

```js
// mermaid のインポート
//  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.css">
//  <script src="//cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>

var num = 0;
mermaid.initialize({ startOnLoad: false });

window.$docsify = {
  markdown: {
    renderer: {
      code: function(code, lang) {
        if (lang === "mermaid") {
          return (
            '<div class="mermaid">' + mermaid.render('mermaid-svg-' + num++, code) + "</div>"
          );
        }
        return this.origin.code.apply(this, arguments);
      }
    }
  }
}
```
