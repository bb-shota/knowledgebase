# ソースコントロール（SVN編）

* [ソースコントロールとしてSVNを使用する] (https://docs.unrealengine.com/4.27/ja/ProductionPipelines/SourceControl/SVN/)

## 準備

### SVNサーバ(VisualSVN)

VisualSVNをインストールし、リポジトリ作成。

### SVNクライアント(TortoiseSVN)

サーバ上のリポジトリからチェックアウト。  
バージョン管理したいファイルを追加して、コミット。

## 接続

### BP

ソースコントロールから設定したリポジトリに接続。コンテンツブラウザ上でアセット状態のアイコンが表示されているか確認

* [Unreal Editor 内のソース コントロール](https://docs.unrealengine.com/4.27/ja/ProductionPipelines/SourceControl/InEditor/)

### C++

ソリューションファイルを開いて、VSの拡張機能のVisualSVNを追加。  
VS上からリポジトリに接続。

* [VisualSVNの使用方法](https://so-zou.jp/software/tech/tool/version-control/visual-svn/)

## 感想
C++コードのバージョン差異がgitほど簡単に見れないのが不便。使えないことはない。