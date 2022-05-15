# UE4テスト

## 単体テスト
UE4には`IMPLEMENT_SIMPLE_AUTOMATION_TEST`と`IMPLEMENT_COMPLEX_AUTOMATION_TEST`がある。UE4のソースコードを見る限り、`IMPLEMENT_SIMPLE_AUTOMATION_TEST`に複数のテスト条件を記載して、テスト失敗時はエラーメッセージとしてログを出す形で使う場合が多いよう。


### IMPLEMENT_SIMPLE_AUTOMATION_TEST

```C++
IMPLEMENT_SIMPLE_AUTOMATION_TEST( TClass, PrettyName, TFlags )
```

**IMPLEMENT_SIMPLE_AUTOMATION_TESTの引数**

| 項目       | 内容                                                                                                                           |
|------------|-------------------------------------------------------------------------------------------------------------------------------|
| TClass     | テストクラスの名前。XXXTestが好ましい。テストクラス自体はコンパイル時にマクロにより自動生成                                                                    |
| PrettyName | ツール名。` . `でネスト。                                                                                                                 |
| TFlags     | 自動化テストの要件と挙動を指定。詳細は[こちら](https://docs.unrealengine.com/5.0/en-US/API/Runtime/Core/Misc/EAutomationTestFlags__Type/) |

  
**IMPLEMENT_SIMPLE_AUTOMATION_TESTのあとにオーバーライドするTClassの関数**

|項目|内容|
|-|-|
|RunTest|テストを実行し、成功時true、失敗時はfalseを戻り値とする。パラメタとして特定の機能テストのためにパースされるか、必要に応じて他の関数に渡たす。要するにテストパラメタを追加する。|
|GetTests|複合テスト時は必ずオーバーライドする。`OutBeautifiedNames`は各テストの`PrettyName`(テスト名)が入る。`OutTestCommands`はこの文字列は、`OutBeautifiedNames` と並列し、`RunTest` に渡される `Parameters` が入る。|

### テスト関数
`RunTest`に実装テストには、`AutomationTest.h`で定義されるテスト関数を使用する。


|関数名|内容|
|-|-|
|TestEqual|2つの値が等しくない場合、エラー出力。|
|TestFalse|指定されたブール値がfalseでない場合、エラー出力|
|TestTrue|指定されたブール値がtrueでない場合、エラー出力|


### 使用例
```C++
IMPLEMENT_SIMPLE_AUTOMATION_TEST(FPlaceholderTest, "TestGroup.TestSubgroup.Placeholder Test", EAutomationTestFlags::EditorContext | EAutomationTestFlags::EngineFilter)

bool FPlaceholderTest::RunTest(const FString& Parameters)
{
    // Make the test pass by returning true, or fail by returning false.
    return true;
}
```
引用 [自動化テクニカルガイド](https://docs.unrealengine.com/4.27/ja/TestingAndOptimization/Automation/TechnicalGuide/)  

AutomationTest.hに記載されているAutomationTest.hのIMPLEMENT_SIMPLE_AUTOMATION_TESTを使用する。コンパイル時にテストクラスが自動生成される。

### UE4での活用例

* [RangeTest.cpp](https://github.com/EpicGames/UnrealEngine/blob/c3caf7b6bf12ae4c8e09b606f10a09776b4d1f38/Engine/Source/Runtime/Core/Private/Tests/Math/RangeTest.cpp)
* [BoneWeightsTests.cpp](https://github.com/EpicGames/UnrealEngine/blob/46544fa5e0aa9e6740c19b44b0628b72e7bbd5ce/Engine/Source/Runtime/AnimationCore/Private/Tests/BoneWeightsTests.cpp)

### 参考

* [AutomationTest.h](https://github.com/EpicGames/UnrealEngine/blob/release/Engine/Source/Runtime/Core/Public/Misc/AutomationTest.h)
* [UE4のC++は何故実装していないはずの処理まで動作するのか？](https://crossplus-studio.jp/archives/1856)
* [Kinda_Small_Numberとは何ですか？](https://forums.unrealengine.com/t/what-is-kinda_small_number/287418)
* [auto](https://cpprefjp.github.io/lang/cpp11/auto.html)
* [関数テンプレート](https://docs.oracle.com/cd/E19957-01/805-7887/6j7dsdheo/index.html)
* [[UE4] 自動テストの追加方法](https://historia.co.jp/archives/698/)
* [自動化テクニカルガイド UE4公式](https://docs.unrealengine.com/4.27/ja/TestingAndOptimization/Automation/TechnicalGuide/)
* [AutomationTest.h](https://github.com/EpicGames/UnrealEngine/blob/46544fa5e0aa9e6740c19b44b0628b72e7bbd5ce/Engine/Source/Runtime/Core/Public/Misc/AutomationTest.h)
* [TestEqual](https://docs.unrealengine.com/4.26/en-US/API/Runtime/Core/Misc/FAutomationTestBase/TestEqual/)
* [Unit-testing with Unreal Engine 4](https://blog.zuru.tech/coding/2021/02/12/unit-testing-with-unreal-engine-4)
* [UE4 lambdaを使って自動テストを楽に書く](https://www.ayumax.net/entry/2019/01/16/205500/)
* [自動化システムを使用した単体テストの作成](https://www.orfeasel.com/unit-testing/)
* [自動化システムを使用した機能テストの作成](https://www.orfeasel.com/functional-tests/)
* [コードブロックのプロファイリング](https://www.orfeasel.com/profiling-code-blocks/)
* [Profiling Stats (Stat Commands) in Unreal Engine](https://www.tomlooman.com/unreal-engine-profiling-stat-commands/)