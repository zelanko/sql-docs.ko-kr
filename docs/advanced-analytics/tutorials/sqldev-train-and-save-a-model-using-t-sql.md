---
title: 3 단원 R 및 T-sql을 사용 하 여 모델 학습 및 저장
description: SQL Server 저장 프로시저 및 T-sql 함수를 사용 하 여 R 모델을 학습, serialize 및 저장 하는 방법을 보여 주는 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0825d99aee2639d28e95dfcaf79e1a8e915bf25a
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470540"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>3단원: T-sql을 사용 하 여 모델 학습 및 저장
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서는 SQL Server에서 R을 사용 하는 방법에 대 한 SQL 개발자를 위한 자습서의 일부입니다.

이 단원에서는 R을 사용 하 여 machine learning 모델을 학습 하는 방법을 배웁니다. 이전 단원에서 만든 데이터 기능을 사용 하 여 모델을 학습 하 고 학습 된 모델을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 저장 합니다. 이 경우 R 패키지는 이미 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]와 함께 설치되어 있으므로 SQL로 모든 것을 수행할 수 있습니다.

## <a name="create-the-stored-procedure"></a>저장 프로시저 만들기

T-SQL에서 R을 호출할 때 시스템 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용합니다. 그러나 모델 재 학습 등 자주 반복 하는 프로세스의 경우에는 다른 저장 프로시저에서 sp_execute_exernal_script에 대 한 호출을 캡슐화 하는 것이 더 쉽습니다.

1. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서, 새 **쿼리** 창을 엽니다.

2. 다음 문을 실행 하 여 **RxTrainLogitModel**저장 프로시저를 만듭니다. 이 저장 프로시저는 입력 데이터를 정의 하 고 RevoScaleR에서 **Rxlogit** 를 사용 하 여 로지스틱 회귀 모델을 만듭니다.

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

    - 모델을 테스트 하기 위해 일부 데이터를 유지 하기 위해 학습 목적으로 taxi 데이터 테이블에서 70%의 데이터를 임의로 선택 합니다.

    - SELECT 쿼리는 사용자 정의 스칼라 함수 *fnCalculateDistance*를 사용하여 승하차 위치 사이의 직접 거리를 계산합니다. 쿼리 결과는 기본 R 입력 변수인 `InputDataset`에 저장 됩니다.
  
    - R 스크립트는 로지스틱 회귀 모델을 만들기 위해에 포함 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]된 향상 된 r 함수 중 하나인 **rxlogit** 함수를 호출 합니다.
  
        이진 변수 _tipped_는 *label* 또는 결과 열로 사용되며 모델은 _passenger_count_, _trip_distance_, _trip_time_in_secs_ 및 _direct_distance_와 같은 특성 열을 사용해 적합해집니다.
  
    - R 변수에 `logitObj`저장 된 학습 된 모델이 직렬화 되 고 출력 매개 변수로 반환 됩니다.

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>저장 프로시저를 사용 하 여 R 모델 학습 및 배포

저장 프로시저에 이미 입력된 데이터의 정의가 포함되므로 입력 쿼리를 제공할 필요가 없습니다.

1. R 모델을 학습 하 고 배포 하려면 저장 프로시저를 호출 하 여 이후 예측에 사용할 수 있도록 _nyc_taxi_models_데이터베이스 테이블에 삽입 합니다.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC RxTrainLogitModel @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('RxTrainLogit_model', @model);
    ```

2. 다음 메시지  와 같이 R [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 의 **stdout** 스트림으로 파이프 되는 메시지에 대 한 메시지 창을 시청 합니다. 

    "외부 스크립트의 STDOUT 메시지: 읽은 행: 1193025, 총 처리 된 행: 1193025, 총 청크 시간: 0.093 초 "

    모델 생성의 일부로 생성된 변수 및 테스트 메트릭을 표시하는 개별 함수 `rxLogit`에 대한 메시지를 볼 수도 있습니다.

3.  문이 완료되면 *nyc_taxi_models* 테이블을 엽니다. 데이터를 처리하고 모델에 맞추는 데 다소 시간이 걸릴 수 있습니다.

    열 _모델_ 에 직렬화 된 모델을 포함 하 고 열 _이름_에 모델 이름을 **RxTrainLogit_model** 한 개의 새 행이 추가 된 것을 볼 수 있습니다.

    ```sql
    model                        name
    ---------------------------- ------------------
    0x580A00000002000302020....  RxTrainLogit_model
    ```

다음 단계에서는 학습 된 모델을 사용 하 여 예측을 생성 합니다.

## <a name="next-lesson"></a>다음 단원

[4단원: 저장 프로시저에서 R 모델을 사용 하 여 잠재적 결과 예측](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>이전 단원

[2단원: R 및 T-sql 함수를 사용 하 여 데이터 기능 만들기](..//tutorials/sqldev-create-data-features-using-t-sql.md)

