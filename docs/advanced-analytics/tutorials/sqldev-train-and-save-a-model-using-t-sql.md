---
title: 'R + T-SQL 자습서: 모델 학습'
description: SQL Server 저장 프로시저 및 T-SQL 함수를 사용하여 R 모델을 학습, serialize 및 저장하는 방법을 보여 주는 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 406f8e1c60c5820f9edaaf7760b7aeed321d2611
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "73724461"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>3단원: T-SQL을 사용하여 모델 학습 및 저장
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서는 SQL Server에서 R을 사용하는 방법에 대한 SQL 개발자를 위한 자습서의 일부입니다.

이 단원에서는 R을 사용하여 기계 학습 모델을 학습하는 방법을 알아봅니다. 이전 단원에서 만든 데이터 기능을 사용하여 모델을 학습한 다음, 학습된 모델을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 저장합니다. 이 경우 R 패키지는 이미 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]와 함께 설치되어 있으므로 모든 작업을 SQL에서 수행할 수 있습니다.

## <a name="create-the-stored-procedure"></a>저장 프로시저 만들기

T-SQL에서 R을 호출하는 경우 시스템 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용합니다. 그러나 모델을 다시 학습해야 하는 경우처럼 자주 반복하는 프로세스를 진행할 때는 sp_execute_exernal_script 호출을 다른 저장 프로시저에 캡슐화하는 것이 더 쉽습니다.

1. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 새 **쿼리** 창을 엽니다.

2. 다음 문을 실행하여 **RxTrainLogitModel** 저장 프로시저를 만듭니다. 이 저장 프로시저는 입력 데이터를 정의하고, RevoScaleR의 **rxLogit**을 사용하여 로지스틱 회귀 모델을 만듭니다.

    ```sql
    CREATE PROCEDURE [dbo].[RxTrainLogitModel] (@trained_model varbinary(max) OUTPUT)
    
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
    logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet)
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

    - 모델 테스트용으로 일부 데이터를 남겨두기 위해 데이터의 70%를 학습용으로 택시 데이터 테이블에서 무작위로 선택합니다.

    - SELECT 쿼리는 사용자 지정 스칼라 함수 *fnCalculateDistance* 를 사용하여 승하차 위치 사이의 직접 거리를 계산합니다. 쿼리 결과는 기본 R 입력 변수인 `InputDataset`에 저장됩니다.
  
    - R 스크립트는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에 포함된 향상된 R 함수 중 하나인 **rxLogit** 함수를 호출하여 로지스틱 회귀 모델을 만듭니다.
  
        이진 변수 _tipped_ 는 *label* 또는 결과 열로 사용되며  _passenger_count_, _trip_distance_, _trip_time_in_secs_, _direct_distance_등의 기능 열을 사용하여 모델을 맞춥니다.
  
    - R 변수 `logitObj`에 저장된 학습된 모델을 serialize한 후 출력 매개 변수로 반환합니다.

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>저장 프로시저를 사용하여 R 모델 학습 및 배포

저장 프로시저에는 입력 데이터 정의가 이미 포함되어 있으므로 입력 쿼리를 제공하지 않아도 됩니다.

1. R 모델을 학습하고 배포하려면 저장 프로시저를 호출하고 이후 예측에 사용할 수 있도록 데이터베이스 테이블 _nyc_taxi_models_에 삽입합니다.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC RxTrainLogitModel @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('RxTrainLogit_model', @model);
    ```

2. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 **메시지** 창에서 R의 **stdout** 스트림에 파이프되는 메시지를 확인합니다. 예를 들면 다음과 같습니다. 

    "외부 스크립트의 STDOUT 메시지: 읽은 행: 1193025, 총 처리된 행: 1193025, 총 청크 시간: 0.093초"

    모델 생성의 일부로 생성되는 변수 및 테스트 메트릭을 나타내는, 개별 함수 `rxLogit`과 관련된 메시지도 표시될 수 있습니다.

3.  문이 완료되면 테이블 *nyc_taxi_models*를 엽니다. 데이터를 처리하고 모델을 맞추는 데 시간이 걸릴 수도 있습니다.

    _모델_ 열에 serialize된 모델을 포함하고 _이름_ 열에 모델 이름 **RxTrainLogit_model**을 포함하는 하나의 새 행이 추가된 것을 확인할 수 있습니다.

    ```sql
    model                        name
    ---------------------------- ------------------
    0x580A00000002000302020....  RxTrainLogit_model
    ```

다음 단계에서는 학습된 모델을 사용하여 예측을 생성합니다.

## <a name="next-lesson"></a>다음 단원

[4단원: 저장 프로시저에서 R 모델을 사용하여 잠재적 결과 예측](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>이전 단원

[2단원: R 및 T-SQL 함수를 사용하여 데이터 기능 만들기](..//tutorials/sqldev-create-data-features-using-t-sql.md)

