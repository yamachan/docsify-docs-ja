# 言語ハイライト

Docsify は [Prism](https://prismjs.com) を使用して、ページ内のコードブロックを強調表示します。Prismはデフォルトで以下の言語をサポートしています:

* マークアップ - `markup`, `html`, `xml`, `svg`, `mathml`, `ssml`, `atom`, `rss`
* CSS - `css`
* C ライク - `clike`
* JavaScript - `javascript`, `js`

[追加の言語](https://prismjs.com/#supported-languages) サポートは、CDN を介して言語固有の [文法ファイル](https://cdn.jsdelivr.net/npm/prismjs@1/components/) をロードすることで利用できます。

```html
<script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-bash.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-php.min.js"></script>
```

構文の強調表示を有効にするには、各コードブロック1行目に指定されたトリプルバックティック(` ``` `)に [言語](https://prismjs.com/#supported-languages) を付与してラップします。

````
```html
<p>This is a paragraph</p>
<a href="//docsify.js.org/">Docsify</a>
```

```bash
echo "hello"
```

```php
function getAdder(int $x): int 
{
    return 123;
}
```
````

上記の Markdown は以下のようにレンダリングされます:

```html
<p>This is a paragraph</p>
<a href="//docsify.js.org/">Docsify</a>
```

```bash
echo "hello"
```

```php
function getAdder(int $x): int 
{
    return 123;
}
```
