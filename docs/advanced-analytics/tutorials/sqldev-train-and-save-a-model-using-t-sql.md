---
title: 단원 3 학습 및 R 및 T-SQL-SQL Server Machine Learning을 사용 하는 모델 저장
description: 학습, 직렬화, R 모델을 저장 하는 방법을 보여 주는 자습서 SQL Server를 사용 하 여 저장 프로시저 및 T-SQL 함수
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f3abe58aac4d5920e64337f63a40dc8f87fb12d9
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645112"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>3단원: 학습 및 T-SQL을 사용 하는 모델 저장
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 SQL Server에서 R을 사용 하는 방법에 대 한 SQL 개발자를 위한 자습서의 일부입니다.

이 단원에서는 R을 사용 하 여 기계 학습 모델을 학습 하는 방법을 알아봅니다. 이전 단원에서 만든 데이터 기능을 사용 하 여 모델을 학습 하 고 다음 학습된 된 모델을 저장 하겠습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다. 이 경우 R 패키지는 이미 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]와 함께 설치되어 있으므로 SQL로 모든 것을 수행할 수 있습니다.

## <a name="create-the-stored-procedure"></a>저장 프로시저 만들기

T-SQL에서 R을 호출할 때 시스템 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용합니다. 그러나 모델을 재 학습 등 자주 반복 되는 프로세스에 대 한 다른 저장된 프로시저에 sp_execute_exernal_script 호출을 캡슐화 하는 것이 쉽습니다.

1. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서, 새 **쿼리** 창을 엽니다.

2. 다음 문을 실행 하 여 저장된 프로시저를 만듭니다 **RxTrainLogitModel**합니다. 입력된 데이터를 정의 하 고 사용 하는이 저장된 프로시저 **rxLogit** 에서 RevoScaleR 로지스틱 회귀 모델을 만듭니다.

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

    - 일부 데이터는 모델 테스트에 남은 되도록 데이터의 70%는 학습 목적 택시 데이터 테이블에서 임의로 선택 됩니다.

    - SELECT 쿼리는 사용자 정의 스칼라 함수 *fnCalculateDistance*를 사용하여 승하차 위치 사이의 직접 거리를 계산합니다. 쿼리 결과 기본 R 입력 변수에 저장 된 `InputDataset`합니다.
  
    - R 스크립트 호출을 **rxLogit** 향상된 된 R 함수 중 하나인 함수에 포함 된 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], 로지스틱 회귀 모델을 만듭니다.
  
        이진 변수 _tipped_는 *label* 또는 결과 열로 사용되며 모델은 _passenger_count_, _trip_distance_, _trip_time_in_secs_ 및 _direct_distance_와 같은 특성 열을 사용해 적합해집니다.
  
    - R 변수에 저장 된 학습된 된 모델을 `logitObj`직렬화 하 고 출력 매개 변수로 반환 합니다.

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>학습 및 저장된 프로시저를 사용 하 여 R 모델 배포

저장 프로시저에 이미 입력된 데이터의 정의가 포함되므로 입력 쿼리를 제공할 필요가 없습니다.

1. 를 학습 및 R 모델을 배포 하려면 저장된 프로시저를 호출 하 고 데이터베이스 테이블에 삽입할 _nyc_taxi_models_, 미래 예측에 사용할 수 있도록 합니다.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC RxTrainLogitModel @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('RxTrainLogit_model', @model);
    ```

2. 조사식 합니다 **메시지** 기간 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] R의 파이프 되는 메시지에 대 한 **stdout** 이 메시지와 같은 스트림: 

    "외부 스크립트의 STDOUT 메시지: Rows Read: 처리 된 1193025, total 행: 1193025, total Chunk Time: 0.093 seconds "

    모델 생성의 일부로 생성된 변수 및 테스트 메트릭을 표시하는 개별 함수 `rxLogit`에 대한 메시지를 볼 수도 있습니다.

3.  문이 완료되면 *nyc_taxi_models* 테이블을 엽니다. 데이터를 처리하고 모델에 맞추는 데 다소 시간이 걸릴 수 있습니다.

    하나의 새 행에 추가한 열에 직렬화 된 모델을 포함 하는 보시 _모델_ 모델 이름과 **RxTrainLogit_model** 열의 _이름_합니다.

    ```sql
    model                        name
    ---------------------------- ------------------
    0x580A00000002000302020....  RxTrainLogit_model
    ```

다음 단계에서는 학습된 된 모델 예측을 생성 합니다.

## <a name="next-lesson"></a>다음 단원

[4 단원: 저장된 프로시저에 R 모델을 사용 하 여 잠재적인 결과 예측](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>이전 단원

[2단원: R 및 T-SQL 함수를 사용 하 여 데이터 기능 만들기](..//tutorials/sqldev-create-data-features-using-t-sql.md)

