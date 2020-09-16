# デプロイ

[GitBook](https://www.gitbook.com) と同様に、ファイルを GitHub Pages、GitLab Pages、VPS にデプロイできます。

## GitHub Pages

Github リポジトリにドキュメントを追加する場所は3つあります:

- `docs/` フォルダー
- master ブランチ
- gh-pages ブランチ

リポジトリの `master` ブランチの `./docs` サブフォルダーにファイルを保存することをお勧めします。次にリポジトリの設定ページで、Github Pages ソースとして、`master branch /docs folder` を選択します。

![github pages](_images/deploy-github-pages.png)

!> ルートディレクトリにファイルを保存し、`master branch` を選択することもできます。`.nojekyll` ファイルをデプロイ場所(`/docs` や the gh-pages ブランチなど)に配置する必要があります。

## GitLab Pages

master ブランチをデプロイする場合は、次のスクリプトを `.gitlab-ci.yml` に含めます。

?> `.public` の回避策は、`cp` が `public/` をそれ自体にコピーして、無限ループに陥ることを防ぎます。

```YAML
pages:
  stage: deploy
  script:
  - mkdir .public
  - cp -r * .public
  - mv .public public
  artifacts:
    paths:
    - public
  only:
  - master
```

!> `./docs` が Docsify サブフォルダーの場合、スクリプトを `- cp -r docs/ .public` に置き換えることができます。

## Firebase Hosting

!> Google アカウントを使用して [Firebase コンソール](https://console.firebase.google.com) にサインインした後、`npm i -g firebase-tools` を実施して Firebase CLI をインストールする必要があります。

ターミナルを使用して、Firebase プロジェクトのディレクトリを決定して移動します。例えば `~/Projects/Docs` などです。そこから `firebase init` を実行し、メニューから `Hosting` を選択します(**スペースキー** で選択し、**矢印キー** でオプションを変更し、**エンター(改行)キー** で実施確認です)。セットアップ手順に従います。

以下のような内容の `firebase.json` ファイルを用います (デプロイメントディレクトリを `public` から `site` に変更しました)。

```json
{
  "hosting": {
    "public": "site",
    "ignore": ["firebase.json", "**/.*", "**/node_modules/**"]
  }
}
```

終了したら `docsify init ./site` を実行して開始テンプレートを作成します (site を `firebase init` 実行時に決定したデプロイメント・ディレクトリに置き換えます。初期値は public です)。ドキュメントを追加/編集してから、ベースプロジェクト・ディレクトリから `firebase deploy` を実行します。


## VPS

以下の nginx 設定を参考にしてください。

```nginx
server {
  listen 80;
  server_name  your.domain.com;

  location / {
    alias /path/to/dir/of/docs/;
    index index.html;
  }
}
```

## Netlify

1. [Netlify](https://www.netlify.com/) アカウントにログインします
2. [ダッシュボード](https://app.netlify.com/) ページで **New site from Git** をクリックします
3. ドキュメントを保存したリポジトリを選択し、**Build Command** 領域を空のままにして、**Publish directory** 領域に `index.html` を配置したディレクトリを入力します。例えば `docs/index.html` の場合はdocsになります

### HTML5 router

HTML5 router を使用する場合、すべてのリクエストを `index.html` にリダイレクトするリダイレクト・ルールを設定する必要があります。Netlify を使用している場合は非常に簡単で、docs ディレクトリに `_redirects` という名前のファイルを作成し、以下のスニペットを記載すれば、準備が整います:

```sh
/*    /index.html   200
```

## ZEIT Now

1. `npm i -g now` を実行して [Now CLI](https://zeit.co/download) をインストールします
2. `cd docs` などを実行し、docsify website ディレクトリに移動します
3. `now` という単一のコマンドでデプロイを実施します

## AWS Amplify

1. Docsify プロジェクト `index.html` の routerMode を *history* モードに設定します

```html
<script>
    window.$docsify = {
      loadSidebar: true,
      routerMode: 'history'
    }
</script>
```

2. [AWS コンソール](https://aws.amazon.com) にログインします
3. [AWS Amplify ダッシュボード](https://aws.amazon.com/amplify) に移動します
4. プロジェクトのセットアップのため **Deploy** route を選択します
5. プロンプトが表示されたら、ルートディレクトリ内にドキュメントを配置している場合は、build settings を空のままにします。別のディレクトリにドキュメントを配置している場合は、`amplify.yml` をカスタマイズします

```yml
version: 0.1
frontend:
  phases:
    build:
      commands: 
        - echo "Nothing to build"
  artifacts:
    baseDirectory: /docs
    files:
      - '**/*'
  cache:
    paths: []

```

6. 次のリダイレクトルールを順に追加します。2行目はPNG画像であり、使用している任意の画像形式に変更できることに注意してください。

| Source address | Target address | Type          |
|----------------|----------------|---------------|
| /<*>.md        | /<*>.md        | 200 (Rewrite) |
| /<*>.png       | /<*>.png       | 200 (Rewrite) |
| /<*>           | /index.html    | 200 (Rewrite) |        


## Docker

- Docsify ファイルを作成する 

  コンテナ内で作成するのではなく、初期ファイルを準備する必要があります。
  これらのファイルを手動で作成する方法、もしくは [docsify-cli](https://github.com/docsifyjs/docsify-cli) を使用する方法については、[Quickstart](https://docsify.js.org/#/quickstart) セクションを参照してください。

    ```sh
    index.html
    README.md
    ```

- Dockerfile を作成する

  ```Dockerfile
    FROM node:latest
    LABEL description="A demo Dockerfile for build Docsify."
    WORKDIR /docs
    RUN npm install -g docsify-cli@latest
    EXPOSE 3000/tcp
    ENTRYPOINT docsify serve .
  
  ```

  作成後のディレクトリ構造は以下のようになります: 

  ```sh
   index.html
   README.md
   Dockerfile
  ```

- Docker イメージをビルドする

  ```sh
  docker build -f Dockerfile -t docsify/demo .
  ```

- Docker イメージを実行する

  ```sh
  docker run -itp 3000:3000 --name=docsify -v $(pwd):/docs docsify/demo 
  ```

