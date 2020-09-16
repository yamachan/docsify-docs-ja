# Vueとの互換性

Vue コンポーネントを Markdown ファイルに直接書き込むことができ、解析対象になります。この機能を利用することで、Vue デモとドキュメントを一緒に作成できます。

## 基本的な使い方

`./index.html` で Vue をロードします。

```html
<script src="//cdn.jsdelivr.net/npm/vue"></script>
<script src="//cdn.jsdelivr.net/npm/docsify"></script>

<!-- Or use the compressed files -->
<script src="//cdn.jsdelivr.net/npm/vue/dist/vue.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

その後、Markdown ファイルですぐに Vue コードを記述できます。`new Vue({ el: '#main' })` スクリプトが標準で実行され、インスタンスが作成されます。

*README.md*

````markdown
# Vue guide

`v-for` usage.

```html
<ul>
  <li v-for="i in 10">{{ i }}</li>
</ul>
```

<ul>
  <li v-for="i in 10">{{ i }}</li>
</ul>
````

Vue インスタンスを手動で初期化することもできます。

*README.md*

```markdown
# Vue demo

<div id="main">hello {{ msg }}</div>

<script>
  new Vue({
    el: '#main',
    data: { msg: 'Vue' }
  })
</script>
```

!> Markdown ファイルでは、最初の script タグ内のスクリプトのみが実行されます。

## Vuep を組み合わせて遊び場(Playground)を作成する

[Vuep](https://github.com/QingWei-Li/vuep) は、ライブエディターとプレビューで Vue コンポーネントをレンダリングするためのコンポーネントです。Vue コンポーネント仕様と JSX をサポートします。

*index.html*

```html
<!-- Inject CSS file -->
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/vuep/dist/vuep.css">

<!-- Inject JavaScript file -->
<script src="//cdn.jsdelivr.net/npm/vue"></script>
<script src="//cdn.jsdelivr.net/npm/vuep"></script>
<script src="//cdn.jsdelivr.net/npm/docsify"></script>

<!-- or use the compressed files -->
<script src="//cdn.jsdelivr.net/npm/vue/dist/vue.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/vuep/dist/vuep.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

*README.md*
```markdown
# Vuep

<vuep template="#example"></vuep>

<script v-pre type="text/x-template" id="example">
  <template>
    <div>Hello, {{ name }}!</div>
  </template>

  <script>
    module.exports = {
      data: function () {
        return { name: 'Vue' }
      }
    }
  </script>
</script>
```

?> 例として [Vuep documentation](https://qingwei-li.github.io/vuep/) を参照してください。
