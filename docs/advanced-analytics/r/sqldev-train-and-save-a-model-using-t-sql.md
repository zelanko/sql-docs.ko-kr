---
title: "5 단원: 학습 및 T-SQL을 사용 하 여 모델을 저장할 | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 3282e8ed-b515-4ed5-8543-fcef68629a92
caps.latest.revision: "10"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d33b81b0472562a9eca148c50eae50f2e280b370
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-5-train-and-save-a-model-using-t-sql"></a>5 단원: 학습 및 T-SQL을 사용 하 여 모델 저장

이 문서는 SQL Server에서 R을 사용 하는 방법에 대 한 SQL 개발자를 위한 자습서의 일부입니다.

이 단원에서는 오른쪽을 사용 하 여 기계 학습 모델을 학습 하는 방법을 알아봅니다. 방금 만든 데이터 기능을 사용 하 여 모델을 학습 하 고 다음에 학습 된 모델을 저장 합니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다. 이 경우 R 패키지는 이미 설치 되어 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]이므로 모든 SQL에서 수행할 수 있습니다.

## <a name="create-the-stored-procedure"></a>저장된 프로시저 만들기

시스템 저장 프로시저를 사용 하 여 R T-SQL에서를 호출할 때 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다. 그러나 재교육 모델을 같은 자주 반복 되는 프로세스에 대 한 것이에 대 한 호출을 캡슐화 하는 보다 쉽게 `sp_execute_exernal_script` 다른 저장 프로시저입니다.

1.  먼저 팁 예측 모델을 작성 하는 R 코드를 포함 하는 저장된 프로시저를 만듭니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], 새 **쿼리** 창 및 저장된 프로시저를 만들려면 다음 문 실행 _TrainTipPredictionModel_합니다. 이 저장 프로시저는 입력 데이터를 정의하며 R 패키지를 사용하여 로지스틱 회귀 모델을 만듭니다.

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

    - 을 보장 하기 위해 일부 데이터는 모델 테스트에 남은 데이터의 70% 임의로 택시 데이터 테이블에서 선택 됩니다.
    
    - SELECT 쿼리는 사용자 지정 스칼라 함수 _fnCalculateDistance_ 를 사용하여 승하차 위치 사이의 직접 거리를 계산합니다.  쿼리 결과는 기본 R 입력 변수인 `InputDataset`에 저장됩니다.
  
    - R 스크립트 호출에서 `rxLogit` 함수를 고급 R 기능 중 하나에 포함 된 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], 로지스틱 회귀 모델을 만듭니다.
  
        이진 변수 _tipped_ 는 *label* 또는 결과 열로 사용되며  _passenger_count_, _trip_distance_, _trip_time_in_secs_, _direct_distance_등의 기능 열을 사용하여 모델을 맞춥니다.
  
    -   R 변수 `logitObj`에 저장된 학습 모델을 직렬화하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 출력하기 위해 데이터 프레임에 넣습니다. 해당 출력은 미래 예측에 사용할 수 있도록 데이터베이스 테이블 _nyc_taxi_models_에 삽입됩니다.
  
2.  존재 하지 않는 경우 저장된 프로시저를 만드는 문을 실행 합니다.

## <a name="generate-the-r-model-using-the-stored-procedure"></a>저장된 프로시저를 사용 하 여 R 모델을 생성 합니다.

에 이미 저장된 프로시저는 입력된 데이터의 정의 포함 되므로 입력된 쿼리를 제공할 필요가 없습니다.

1. R 모델을 생성 하려면 다른 매개 변수 없이 저장된 프로시저를 호출 합니다.

    ```SQL
    EXEC TrainTipPredictionModel
    ```

2. 조사식은 **메시지** 의 창 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] r의 파이프는 메시지에 대 한 **stdout** 이 나타내며와 같은 스트림: 

    "외부 스크립트의 STDOUT 메시지: Rows Read: 1193025, 총 행이 처리: 1193025, 총 청크 시간: 0.093 시간 (초)"

    개별 함수에 대 한 메시지가 있을 수도 있습니다 `rxLogit`, 변수를 표시 하 고 모델을 만드는 중에 생성 된 메트릭 테스트 합니다.

3.  문이 완료 되 면 테이블을 열고 *nyc_taxi_models*합니다. 데이터를 처리 하 고 모델을 맞출 시간이 걸릴 수 있습니다.

    _모델_열에 직렬화된 모델을 포함하는 하나의 새 행이 추가된 것을 확인할 수 있습니다.

    ```
    model
    ------
    0x580A00000002000302020....
    ```

다음 단계에서는 학습된 모델을 사용하여 예측을 만듭니다.

## <a name="next-lesson"></a>다음 단원

[6 단원: 모델을 운용](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>이전 단원

[4 단원: T-SQL을 사용 하 여 데이터 기능 만들기](..//tutorials/sqldev-create-data-features-using-t-sql.md)

