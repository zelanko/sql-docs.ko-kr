---
title: 'R 자습서: 모델 학습 및 저장'
titleSuffix: SQL machine learning
description: 이 5부 자습서 시리즈의 4부에서는 SQL Machine Learning을 통해 SQL Server의 Transact-SQL을 사용하여 R에서 모델을 학습시키고 저장합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/15/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||>=azuresqldb-mi-current'
ms.openlocfilehash: fe2d2a741e6e671eaadef96ee8539862535e51d7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470104"
---
# <a name="r-tutorial-train-and-save-model"></a>R 자습서: 모델 학습 및 저장
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

이 5부 자습서 시리즈의 4부에서는 R을 사용하여 기계 학습 모델을 학습시키는 방법을 알아봅니다. 이전 부분에서 만든 데이터 기능을 사용하여 모델을 학습시킨 다음, 학습된 모델을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 저장합니다. 이 경우 R 패키지는 이미 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]와 함께 설치되어 있으므로 모든 작업을 SQL에서 수행할 수 있습니다.

이 문서에서는 다음을 수행합니다.

> [!div class="checklist"]
> + SQL 저장 프로시저를 사용하여 모델 만들기 및 학습
> + 학습된 모델을 SQL 테이블에 저장

[1부](r-taxi-classification-introduction.md)에서는 사전 요구 사항을 설치하고 샘플 데이터베이스를 복원했습니다.

[2부](r-taxi-classification-explore-data.md)에서는 샘플 데이터를 검토하고 몇 가지 플롯을 생성했습니다.

[3부](r-taxi-classification-create-features.md)에서는 Transact-SQL 함수를 사용하여 원시 데이터에서 기능을 만드는 방법을 배웠습니다. 그런 다음 저장 프로시저에서 해당 함수를 호출하여 기능 값이 포함된 테이블을 만들었습니다.

[5부](r-taxi-classification-deploy-model.md)에서는 4부에서 학습시키고 저장한 모델을 운영하는 방법을 알아봅니다.

## <a name="create-the-stored-procedure"></a>저장 프로시저 만들기

T-SQL에서 R을 호출하는 경우 시스템 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용합니다. 그러나 모델을 다시 학습시키는 경우처럼 자주 반복하는 프로세스를 진행할 때는 `sp_execute_external_script` 호출을 다른 저장 프로시저에 캡슐화하기가 더 쉽습니다.

1. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 새 **쿼리** 창을 엽니다.

2. 다음 문을 실행하여 저장 프로시저 **RTrainLogitModel** 을 만듭니다. 이 저장 프로시저는 입력 데이터를 정의하며 **glm** 을 사용하여 로지스틱 회귀 모델을 만듭니다.

   ```sql
   CREATE PROCEDURE [dbo].[RTrainLogitModel] (@trained_model varbinary(max) OUTPUT)
   
   AS
   BEGIN
     DECLARE @inquery nvarchar(max) = N'
       select tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance,
       pickup_datetime, dropoff_datetime,
       dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
       from nyctaxi_sample
       tablesample (70 percent) repeatable (98052)
   '
   
     EXEC sp_execute_external_script @language = N'R',
                                     @script = N'
   ## Create model
   logitObj <- glm(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet, family = binomial)
   summary(logitObj)
   
   ## Serialize model 
   trained_model <- as.raw(serialize(logitObj, NULL));
   ',
     @input_data_1 = @inquery,
     @params = N'@trained_model varbinary(max) OUTPUT',
     @trained_model = @trained_model OUTPUT; 
   END
   GO
   ```

   + 모델 테스트용으로 일부 데이터를 남겨두기 위해 데이터의 70%를 학습용으로 택시 데이터 테이블에서 무작위로 선택합니다.

   + SELECT 쿼리는 사용자 지정 스칼라 함수 *fnCalculateDistance* 를 사용하여 승하차 위치 사이의 직접 거리를 계산합니다. 쿼리 결과는 기본 R 입력 변수인 `InputDataset`에 저장됩니다.
  
   + R 스크립트는 R 함수 **glm** 을 호출하여 로지스틱 회귀 모델을 만듭니다.
  
     이진 변수 _tipped_ 는 *label* 또는 결과 열로 사용되며  _passenger_count_, _trip_distance_, _trip_time_in_secs_, _direct_distance_ 등의 기능 열을 사용하여 모델을 맞춥니다.
  
   + R 변수 `logitObj`에 저장된 학습된 모델을 serialize한 후 출력 매개 변수로 반환합니다.

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>저장 프로시저를 사용하여 R 모델 학습 및 배포

저장 프로시저에는 입력 데이터 정의가 이미 포함되어 있으므로 입력 쿼리를 제공하지 않아도 됩니다.

1. R 모델을 학습하고 배포하려면 저장 프로시저를 호출하고 이후 예측에 사용할 수 있도록 데이터베이스 테이블 _nyc_taxi_models_ 에 삽입합니다.

   ```sql
   DECLARE @model VARBINARY(MAX);
   EXEC RTrainLogitModel @model OUTPUT;
   INSERT INTO nyc_taxi_models (name, model) VALUES('RTrainLogit_model', @model);
   ```

2. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 **메시지** 창에서 R의 **stdout** 스트림에 파이프되는 메시지를 확인합니다. 예를 들면 다음과 같습니다. 

   "외부 스크립트의 STDOUT 메시지: 읽은 행: 1193025, 총 처리된 행: 1193025, 총 청크 시간: 0.093초"

3. 문이 완료되면 테이블 *nyc_taxi_models* 를 엽니다. 데이터를 처리하고 모델을 맞추는 데 시간이 걸릴 수도 있습니다.

   ‘모델’ 열에 직렬화된 모델을 포함하고 ‘이름’ 열에 모델 이름 **RTrainLogit_model** 을 포함하는 하나의 새 행이 추가된 것을 확인할 수 있습니다. 

   ```text
   model                        name
   ---------------------------- ------------------
   0x580A00000002000302020....  RTrainLogit_model
   ```

이 자습서의 다음 부분에서는 학습된 모델을 사용하여 예측을 생성합니다.

## <a name="next-steps"></a>다음 단계

이 문서에서는 다음 작업을 수행합니다.

> [!div class="checklist"]
> + SQL 저장 프로시저를 사용하여 모델 만들기 및 학습
> + 학습된 모델을 SQL 테이블에 저장

> [!div class="nextstepaction"]
> [R 자습서: SQL 저장 프로시저에서 예측 실행](r-taxi-classification-deploy-model.md)
