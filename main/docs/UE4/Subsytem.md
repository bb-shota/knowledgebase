# Subsystem
## C++ クラス作成

UE4 Editor上からSubSystem classを作成

## 例

```C++
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "Subsystems/GameInstanceSubsystem.h"
#include "Tickable.h"
#include "MyInterface.h"
#include "MyGameInstanceSubsystem.generated.h"

/**
 * 
 */
UCLASS()
class SUBSYSTEMTEST_API UMyGameInstanceSubsystem : public UGameInstanceSubsystem, public FTickableGameObject, public IMyInterface
{
	 GENERATED_BODY()

public:
	// 初期化
	virtual void Initialize(FSubsystemCollectionBase& Collection);

	// 初期化解除
	virtual void Deinitialize();

	// 呼び出しテスト用
	UFUNCTION(BlueprintCallable)
	void CallTest() { UE_LOG(LogTemp, Log, TEXT("Test!1")); }

	UFUNCTION(BlueprintCallable)
	void CallTest2() { UE_LOG(LogTemp, Log, TEXT("Test2!")); }

	// FTickableGameObjectからオーバーライド
	virtual TStatId GetStatId() const;
	virtual bool IsTickable() const { return(true); }
	virtual void Tick(float DeltaTime); protected:
	// Called when the game starts or when spawned
	
	virtual ETickableTickType GetTickableTickType() const;

	TArray<AActor*> OutActors;

};

```

```C++
// Fill out your copyright notice in the Description page of Project Settings.


#include "MyGameInstanceSubsystem.h"
#include "Kismet/GameplayStatics.h"
#include "GameFramework/Actor.h"
#include "MyInterface.h"
// 初期化
void UMyGameInstanceSubsystem::Initialize(FSubsystemCollectionBase& Collection)
{
	// インターフェース取得
	UGameplayStatics::GetAllActorsWithInterface(this->GetWorld(), UMyInterface::StaticClass(), UMyGameInstanceSubsystem::OutActors);
	UE_LOG(LogTemp, Log, TEXT("UMyGameInstanceSubsystem::Initialize()"));
}


// 初期化解除
void UMyGameInstanceSubsystem::Deinitialize()
{

	UE_LOG(LogTemp, Log, TEXT("UMyGameInstanceSubsystem::Deinitialize()"));
}

TStatId UMyGameInstanceSubsystem::GetStatId() const
{
	RETURN_QUICK_DECLARE_CYCLE_STAT(UMyGameInstanceSubsystem, STATGROUP_Tickables);
}


ETickableTickType UMyGameInstanceSubsystem::GetTickableTickType() const
{
	return IsTemplate() ? ETickableTickType::Never : ETickableTickType::Always;
}


void UMyGameInstanceSubsystem::Tick(float DeltaTime)
{
	UE_LOG(LogTemp, Log, TEXT("1"));
	


	
	UE_LOG(LogTemp, Log, TEXT("Before I/F"));
	// インターフェースを持っている対象すべての実行を行う
	for (AActor* Actor : UMyGameInstanceSubsystem::OutActors)
	{
		int32 val= IMyInterface::Execute_SampleArgResult(Actor,  100);
		UE_LOG(LogTemp, Log, TEXT("Interface = %d"),val);
	}
	UE_LOG(LogTemp, Log, TEXT("After I/F"));
}




```

## 参考
* [UE4 プログラミングサブシステムを試してみる](https://qiita.com/unknown_ds/items/afcff802ab17db486822#gameinstancesubsystem)
* [UE4 Subsystem Basics](https://www.ajwadimran.com/blog/ue4-subsystems-basics)
* [Unreal-style Singletons with Subsystems](https://benui.ca/unreal/subsystem-singleton/)
* [【UE4 C++】编程子系统 Subsystem ](https://www.cnblogs.com/shiroe/p/14819721.html)


