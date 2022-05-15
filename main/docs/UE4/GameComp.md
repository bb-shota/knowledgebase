
# UE4ラーニングコース(ゲームプレイのコンポーネントを分解する)

## コンポーネントとは

[UE4ラーニングコース(ゲームプレイのコンポーネントを分解する)](https://www.unrealengine.com/ja/onlinelearning-courses/breaking-down-the-components-of-gameplay)

### Actor Component

* 他のコンポーネントをアタッチすることができない

### Scene Component

* トランスフォームを含むコンポーネント
* 他のコンポーネントをアタッチすることができる
* レンダリングの機能はない
* コリジョンの機能はある

### Prinmitive Component

* ジオメトリを含むまたは生成するScene Component

### コンポーネントの長所/短所

* AActorCompomentとAActorで比較するとAActorCompomentのほうが軽い
* AActorCompomentは他のものと一緒にロードするのでメモリ負荷大
* AActorは設定しない限り、Tickなどを実行→それにひも付きAActorCompomentも実行

## コンポーネント ベースのアーキテクチャ

* [参考1](https://www.raywenderlich.com/2806-introduction-to-component-based-architecture-in-games)
* [参考2](https://gameprogrammingpatterns.com/component.html)

## コンポーネントの適用範囲

自由度や再利用性の検討  

* 継承ベースアプローチ
* コンポーネントベースアプローチ

コンポーネントベースアプローチのほうが自由度高い。
