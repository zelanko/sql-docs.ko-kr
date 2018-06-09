---
title: Lesson 5 기차 및 R 및 T-SQL (SQL Server 기계 학습)를 사용 하 여 모델을 저장할 | Microsoft Docs
description: SQL Server에서 R을 포함 하는 방법을 보여 주는 자습서 저장 프로시저 및 T-SQL 함수
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: bd5bdc7d256a22dbab6662a74dc39073892dbb4d
ms.sourcegitcommit: b52b5d972b1a180e575dccfc4abce49af1a6b230
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "35250066"
---
# <a name="lesson-5-train-and-save-a-model-using-t-sql"></a>5단원: T-SQL을 사용한 모델 학습 및 저장
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 SQL Server에서 R을 사용 하는 방법에 대 한 SQL 개발자를 위한 자습서의 일부입니다.

이 단원에서는 오른쪽을 사용 하 여 기계 학습 모델을 학습 하는 방법을 알아봅니다. 이전 단원에서 만든 데이터 기능을 사용 하 여 모델을 학습 하 고 다음에 학습 된 모델을 저장 합니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다. 이 경우 R 패키지는 이미 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]와 함께 설치되어 있으므로 SQL로 모든 것을 수행할 수 있습니다.

## <a name="create-the-stored-procedure"></a>저장 프로시저 만들기

T-SQL에서 R을 호출할 때 시스템 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용합니다. 그러나 모델 재학습과 같이 자주 반복되는 프로세스의 경우 다른 저장 프로시저에서 `sp_execute_exernal_script`에 대한 호출을 캡슐화하는 것이 보다 쉽습니다.

1.  먼저 팁 예측 모델을 작성하는 R 코드를 포함하는 저장 프로시저를 만듭니다.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 새 **쿼리** 창을 열고 다음 문을 실행하여 _TrainTipPredictionModel_ 저장 프로시저를 만듭니다.  이 저장 프로시저는 입력 데이터를 정의하고 R 패키지를 사용하여 로지스틱 회귀 모델을 만듭니다.

    ```SQL
    CREATE PROCEDURE [dbo].[TrainTipPredictionModel]
    
    AS
    BEGIN
      DECLARE @inquery nvarchar(max) = N'
        select tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance,
        pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
        from nyctaxi_sample
        tablesample (70 percent) repeatable (98052)
    '
      -- Insert the trained model into a database table
      INSERT INTO nyc_taxi_models
      EXEC sp_execute_external_script @language = N'R',
                                      @script = N'
    
    ## Create model
    logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet)
    summary(logitObj)
    
    ## Serialize model and put it in data frame
    trained_model <- data.frame(model=as.raw(serialize(logitObj, NULL)));
    ',
      @input_data_1 = @inquery,
      @output_data_1_name = N'trained_model'
      ;
    
    END
    GO
    ```

    - 모델을 테스트하기 위해 일부 데이터를 남겨야 하므로, 택시 데이터 테이블에서 70%를 무작위로 선택합니다.
    
    - SELECT 쿼리는 사용자 정의 스칼라 함수 _fnCalculateDistance_를 사용하여 승하차 위치 사이의 직접 거리를 계산합니다.  쿼리 결과는 기본 R 입력 변수인 `InputDataset`에 저장됩니다.
  
    - R 스크립트는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에 포함된 향상된 R 기능 중 하나인 `rxLogit` 함수를 호출하여 로지스틱 회귀 모델을 만듭니다.
  
        이진 변수 _tipped_는 *label* 또는 결과 열로 사용되며 모델은 _passenger_count_, _trip_distance_, _trip_time_in_secs_ 및 _direct_distance_와 같은 특성 열을 사용해 적합해집니다.
  
    -   R 변수 `logitObj`에 저장된 학습 모델을 직렬화하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 출력하기 위해 데이터 프레임에 넣습니다. 해당 출력은 미래 예측에 사용할 수 있도록 데이터베이스 테이블 _nyc_taxi_models_에 삽입됩니다.
  
2.  저장 프로시저가 존재하지 않는 경우 다음 문을 실행해서 저장 프로시저를 만듭니다.

## <a name="generate-the-r-model-using-the-stored-procedure"></a>저장 프로시저를 사용하여 R 모델 생성

저장 프로시저에 이미 입력된 데이터의 정의가 포함되므로 입력 쿼리를 제공할 필요가 없습니다.

1. R 모델을 생성하려면 다른 매개변수 없이 저장 프로시저를 호출합니다.

    ```SQL
    EXEC TrainTipPredictionModel
    ```

2. 조사식은 **메시지** 의 창 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] r의 파이프는 메시지에 대 한 **stdout** 이 메시지와 같은 스트림: 

    "STDOUT message(s) from external script: Rows Read: 1193025, Total Rows Processed: 1193025, Total Chunk Time: 0.093 seconds"

    모델 생성의 일부로 생성된 변수 및 테스트 메트릭을 표시하는 개별 함수 `rxLogit`에 대한 메시지를 볼 수도 있습니다.

3.  문이 완료되면 *nyc_taxi_models* 테이블을 엽니다. 데이터를 처리하고 모델에 맞추는 데 다소 시간이 걸릴 수 있습니다.

    _모델_열에 직렬화된 모델을 포함하는 하나의 새 행이 추가된 것을 확인할 수 있습니다.

    ```
    model
    ------
    0x580A00000002000302020....
    ```

다음 단계에서는 학습된 모델을 사용하여 예측을 만듭니다.

## <a name="next-lesson"></a>다음 단원

[6단원: 모델 운용](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>이전 단원

[4 단원: R 및 T-SQL 함수를 사용 하 여 데이터 기능 만들기](..//tutorials/sqldev-create-data-features-using-t-sql.md)

