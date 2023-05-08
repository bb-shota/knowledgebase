# knowledgebase

```
git push -u origin main

```

## hoge

	//Position_arr  の最初に追加
	Position_arr.Insert(GetActorLocation(), 0);
	//Pose_arr  の最初に追加
	Pose_arr.Insert(GetActorRotation(), 0);

	//Velosityを計算
	Velosity_arr_Local.Insert(GetTransform().InverseTransformVectorNoScale(Position_arr[0] - Position_arr[1]) / DeltaTime  *3600 / 100000, 0);
	ULog::Vector(Velosity_arr_Local[0], true, "Velosity_arr_Local[0]: ", "", LO_Both, 0.0f, FName("ViewportKeyName"));
	ULog::Vector(Velosity_arr_Local[1], true, "Velosity_arr_Local[1]: ", "", LO_Both, 0.0f, FName("ViewportKeyName"));

	Velosity_arr_Global.Insert((Position_arr[0] - Position_arr[1]) / DeltaTime * 3600 / 100000, 0);
	ULog::Vector(Velosity_arr_Global[0], true, "Velosity_arr_Global[0]: ", "", LO_Both, 0.0f, FName("ViewportKeyName"));
	ULog::Vector(Velosity_arr_Global[1], true, "Velosity_arr_Global[1]: ", "", LO_Both, 0.0f, FName("ViewportKeyName"));
	

	//Accelerationを計算
	Acceleration_arr_Local.Insert(GetTransform().InverseTransformVectorNoScale(Velosity_arr_Global[0] - Velosity_arr_Global[1]) / DeltaTime*3600 * 1000 / 3600, 0);
	ULog::Vector(Acceleration_arr_Local[0], true, "Acceleration_arr_Local[0]: ", "", LO_Both, 0.0f, FName("ViewportKeyName"));
	ULog::Vector(Velosity_arr_Local[0] - Velosity_arr_Local[1], true, "Velosity_arr_Global[0] - Velosity_arr_Global[1]: ", "", LO_Both, 0.0f, FName("ViewportKeyName"));
	ULog::Number(int16(Velosity_arr_Global.Num()), "Velosity_arr_Global.Size(): ", "", DLNS_Decimal, LO_Both, 0.0f, FName("ViewportKeyName"));


	//AngularVelosityを計算
	FRotator DeltaRotator = UKismetMathLibrary::NormalizedDeltaRotator(Pose_arr[0], Pose_arr[1]);
	FVector DeltaDeg;
	DeltaDeg.X = DeltaRotator.Roll;
	DeltaDeg.Y = DeltaRotator.Pitch;
	DeltaDeg.Z = DeltaRotator.Yaw;
	AngularVelosity_arr_Local.Insert(Pose_arr[0].UnrotateVector(DeltaDeg / DeltaTime), 0);
	ULog::Vector(AngularVelosity_arr_Local[0], true, "AngularVelosity_arr_Local[0]: ", "", LO_Both, 0.0f, FName("ViewportKeyName"));


