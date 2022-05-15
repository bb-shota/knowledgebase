## 見出しを整える
Mkdocsでページを書いたときに見出しいが分かりづらいので、Mkdocsの見出しを整える方法について整理しました。

## どうすればわかりやすくなるのか
見出しの違いがひと目でわかるとわかりやすいと思いますので、見出しの違いを出すためには、以下の2つの観点が必要と考えました。  

* 見出し境目の明確化  
* 見出し階層の視認性向上  
  
これらに対して、以下の方法で対応をしました。  

* 見出し下のアンダーラインによる見出し境目の明確化  
* アイコンによる見出し階層の視認性向上  

## 見出し変更方法

現状の構成は以下のようになっています。  

```
    mkdocs.yml
    docs/
        index.md
        ...
```

### アイコン追加

#### アイコンインストール

アイコンはFont Awesome[^1]という無料で利用可能なWebアイコンを使用するため、インストールをします。  

```python
pip install fontawesome_markdown
```

#### 拡張機能の有効化
以下をmkdocs.ymlに追加し、Font Awesomeの拡張機能の有効化をする。

```
markdown_extensions:
  - fontawesome_markdown
 
extra_css:
  - "https://maxcdn.bootstrapcdn.com/font-awesome/4.6.1/css/font-awesome.min.css"

```

#### CSSフォルダとcustom.cssの追加 
docsフォルダの直下にcssフォルダ作成し、custom.cssを作成する。

```
    mkdocs.yml
    docs/
        index.md
        css/
          custom.css  
```

#### custom.cssの有効化

以下をmkdocs.ymlに追加し、custom.cssの有効化をする。

```
extra_css:
     - css/custom.css   
```

#### custom.cssの編集

custom.cssに見出し階層(h1,h2,h3...)のそれぞれに使用するアイコンを設定する。アイコン設定する該当部分は```content: "\f0a9" !important;```の```\f0a9```で、[Font Awesome](https://fontawesome.com/search?s=solid%2Cbrands)で使いたいアイコンを検索し、アイコンのUnicodeを取得します。[^2]

```
.md-typeset h2::before {
    display: inline-block !important;
    font-family: "FontAwesome";
    content: "\f0a9" !important;
    margin-right: .3em;
}
```
### アンダーライン追加

custom.cssに見出し階層(h1,h2,h3...)のそれぞれに使用するアンダーラインを設定する。

```
.md-typeset h2 {
    border-bottom: 1px dotted #888;
}
```

## おわり

これで本サイトのようになるはず。  

## 参考

* [MkDocsによるドキュメント作成](https://zenn.dev/mebiusbox/articles/81d977a72cee01)
* [MkDocs の見出しを Font Awesome で装飾](https://kurokobo.github.io/mkdocs-header-awesome/)  
* [MkDocsで使えるMarkdownサンプル](https://caldia.tuzikaze.com/mkdocs/markdown-sample/)

[^1]: [Font Awesome](https://fontawesome.com/)  
[^2]: Font Awesomeの各アイコンページでUnicodeが非常にわかりにくい。2022/3/20時点では、IconNameの右側に```f0a9```のように小さく記載されています。