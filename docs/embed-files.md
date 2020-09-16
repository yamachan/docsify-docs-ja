# ファイルの埋め込み

docsify 4.6では、あらゆる種類のファイルを埋め込むことが可能になりました。

これらのファイルをビデオ、オーディオ、iframe、またはコードブロックとして埋め込むことができ、Markdown ファイルを直接ドキュメントに埋め込むこともできます。

たとえば、ここに埋め込まれた Markdown ファイルがあります。 これだけだけです：

```markdown
[filename](_media/example.md ':include')
```

そして、`example.md` のコンテンツがここに直接表示されます;

[filename](_media/example.md ':include')

元のコンテンツを確認できます: [example.md](_media/example.md ':ignore')

通常、これはリンクにコンパイルされますが、docsifyでは `:include` を追加すると埋め込まれます。

ターゲットを置き換えれば、外部リンクも使用できます。gist URLを使用する場合は、[gist の埋め込み](#gist-の埋め込み) セクションを参照してください。

## 埋め込みファイルの形式

現在、ファイル拡張子は自動的に認識され、さまざまな方法で埋め込まれます。

次のタイプがサポートされています:

* **インラインフレーム(iframe)** `.html`, `.htm`
* **Markdown** `.markdown`, `.md`
* **音楽** `.mp3`
* **映像** `.mp4`, `.ogg`
* **コード** 他のファイル拡張子

もちろん、タイプを明示的に指定することもできます。例えば `:type=code` を設定することで、Markdown ファイルをコードブロックとして埋め込むことができます。

```markdown
[filename](_media/example.md ':include :type=code')
```

以下のように表示されます:

[filename](_media/example.md ':include :type=code')

## YAML Front Matter 付きの Markdown

Markdown を使用する際、YAML Front Matter はレンダリングされたコンテンツから strip (通常のテキストとして処理)されます。この場合、属性は使用できません。

```markdown
[filename](_media/example-with-yaml.md ':include')
```

コンテンツのみを取得します:

[filename](_media/example-with-yaml.md ':include')

元のコンテンツを確認できます: [example-with-yaml.md](_media/example-with-yaml.md ':ignore')

## コード断片の埋め込み

ファイル全体を埋め込みたくない場合があります。たぶんあなたはほんの数行を必要とするが、CI でファイルをコンパイルしてテストしたいからでしょう。

```markdown
[filename](_media/example.js ':include :type=code :fragment=demo')
```

コードファイルでは、フラグメントを `/// [demo]` 行で囲みます (フラグメントの前後)。
または `### [demo]` を使用できます。

例:

[filename](_media/example.js ':include :type=code :fragment=demo')

元のコンテンツを確認できます: [example.js](_media/example.js ':ignore')

## タグ属性

ファイルを `iframe`、`audio`、`video` として埋め込む場合、これらのタグの属性を設定する必要があります。

```markdown
[cinwell website](https://cinwell.com ':include :type=iframe width=100% height=400px')
```

[cinwell website](https://cinwell.com ':include :type=iframe width=100% height=400px')

見ましたか？直接書くだけです。[MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) でこれらの属性を確認できます。

## コードブロックの強調表示

任意のソースコードファイルを埋め込んで、強調表示する言語を指定したり、自動的に識別したりできます。

```markdown
[](_media/example.html ':include :type=code text')
```

以下のように表示されます:

[](_media/example.html ':include :type=code text')

?> 強調表示をする方法？ [こちら](language-highlight.md) で確認できます。

## gist の埋め込み

Markdown コンテンツまたはコードブロックとして gist を埋め込むことができます。これは [ファイルの埋め込み](#ファイルの埋め込み) セクション冒頭のアプローチに基づいていますが、gist URLをそのままターゲットとして使用します。

?> これを機能させるために、プラグインやアプリの設定を変更する必要は **ありません**。
実際、外部スクリプトを許可するようにプラグインまたは構成を変更しても、gist からコピーされた"埋め込み" `script` タグは読み込まれません。

### gist のメタデータを特定する

まず `gist.github.com` で gist を表示します。このガイドでは、次の gist を使用します。

- https://gist.github.com/anikethsaha/f88893bb563bb7229d6e575db53a8c15

gist から次の項目を特定します:

項目                | 例                                 | 説明
---                 | ---                                | ---
**Username**        | `anikethsaha`                      | gist の所有者
**Gist ID**         | `c2bece08f27c4277001f123898d16a7c` | gist の識別子。gist の存続期間中は固定されています
**Filename**        | `content.md`                       | gist 内のファイル名を選択します。単一ファイルの gist でも埋め込み時には指定が必要です。

ターゲットファイに直接アクセスできる gist URL を生成するためにこれらの値が必要になります。形式は次のとおりです:

- `https://gist.githubusercontent.com/USERNAME/GIST_ID/raw/FILENAME`

サンプルの gist にある2つのファイルを例として示します:

- https://gist.githubusercontent.com/anikethsaha/f88893bb563bb7229d6e575db53a8c15/raw/content.md
- https://gist.githubusercontent.com/anikethsaha/f88893bb563bb7229d6e575db53a8c15/raw/script.js

?> もしくは、gist ファイルの [Raw] ボタンをクリックして直接、ファイルにアクセスする URL を取得することもできます。
ただしこの方法を使用する場合は、`raw/` とファイル名の間のリビジョン番号を **削除** して、URLが上記のパターンと一致するようにしてください。
これを実施しないと、埋め込まれた gist は、gist が更新されたときに最新のコンテンツを表示しません。

以下のセクションのいずれかに進み、Docsify ページに gist を埋め込みます。

### gist にある Markdown コンテンツの埋め込み

これは、外部リンクに誰か飛ばすことなく、コンテンツをドキュメントに **シームレスに** 埋め込むための良い方法です。このアプローチは、複数のリポジトリのにある gist のインストール手順を再利用するのに適しています。このアプローチは自分のアカウントでも、別のユーザーが所有する gist でも、同様に機能します。

形式は次のとおりです:

```markdown
[LABEL](https://gist.githubusercontent.com/USERNAME/GIST_ID/raw/FILENAME ':include')
```

例えば:

```markdown
[gist: content.md](https://gist.githubusercontent.com/anikethsaha/f88893bb563bb7229d6e575db53a8c15/raw/content.md ':include')
```

は以下のように表示されます:

[gist: content.md](https://gist.githubusercontent.com/anikethsaha/f88893bb563bb7229d6e575db53a8c15/raw/content.md ':include')

`LABEL` は任意のテキストです。リンクが壊れている場合は _fallback_ メッセージとして機能します。壊れたリンクを修正する必要がある場合に備えて、ここにもファイル名を指定しておくと便利です。また、埋め込み要素が一目でわかりやすくなります。

### gist にあるコードブロックの埋め込み

The format is the same as the previous section, but with `:type=code` added to the alt text.
 As with the [Embedded file type](#embedded-file-type) section, the syntax highlighting will be **inferred** from the extension (e.g. `.js` or `.py`),
 so you can leave the `type` set as `code`.

形式は前のセクションと同じですが `:type=code` が代替テキストに追加されています。 [埋め込みファイルの形式](#埋め込みファイルの形式) セクションと同様に、構文の強調表示は拡張子から **推論** されるため (例: `.js` や `.py`) `type` を `code` に設定します。

形式は次のとおりです:

```markdown
[LABEL](https://gist.githubusercontent.com/USERNAME/GIST_ID/raw/FILENAME ':include :type=code')
```

例えば:

```markdown
[gist: script.js](https://gist.githubusercontent.com/anikethsaha/f88893bb563bb7229d6e575db53a8c15/raw/script.js ':include :type=code')
```

は以下のように表示されます:

[gist: script.js](https://gist.githubusercontent.com/anikethsaha/f88893bb563bb7229d6e575db53a8c15/raw/script.js ':include :type=code')
