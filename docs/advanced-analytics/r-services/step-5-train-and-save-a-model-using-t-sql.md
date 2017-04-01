---
title: "5단계: T-SQL을 사용하여 모델 학습 및 저장(데이터베이스 내 고급 분석 자습서) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
  - "TSQL"
ms.assetid: 3282e8ed-b515-4ed5-8543-fcef68629a92
caps.latest.revision: 10
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# 5단계: T-SQL을 사용하여 모델 학습 및 저장(데이터베이스 내 고급 분석 자습서)
이 단계에서는 R을 사용하여 Machine Learning 모델을 학습하는 방법을 알아봅니다. R 패키지는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]과 함께 이미 설치되었으므로 저장 프로시저에서 알고리즘을 호출할 수 있습니다. 방금 만든 데이터 기능을 사용하여 모델을 학습한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 학습된 모델을 저장합니다.  
  
## 저장 프로시저를 사용하여 R 모델 작성  
[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]과 함께 설치된 R 런타임에 대한 모든 호출은 시스템 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 수행됩니다. 그러나 모델을 다시 학습해야 하는 경우 다른 저장 프로시저에 sp_execute_exernal_script 호출을 캡슐화하는 것이 더 쉽습니다.  
  
이 섹션에서는 방금 준비한 데이터로 모델을 작성하는 데 사용할 수 있는 저장 프로시저를 만듭니다. 이 저장 프로시저는 입력 데이터를 정의하며 R 패키지를 사용하여 로지스틱 회귀 모델을 만듭니다.  
  
#### 저장 프로시저를 만들려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 새 쿼리 창을 열고 다음 문을 실행하여 저장 프로시저 _TrainTipPredictionModel_을 만듭니다.  
  
    저장 프로시저에는 입력 데이터 정의가 이미 포함되어 있으므로 입력 쿼리를 제공하지 않아도 됩니다.  
  
    ```  
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
  
    이 저장 프로시저는 모델 학습의 일부로 이러한 활동을 수행합니다.  
  
    -   모델 테스트용으로 일부 데이터를 남겨두기 위해 데이터의 70%를 택시 데이터 테이블에서 무작위로 선택합니다.  
  
    -   SELECT 쿼리는 사용자 지정 스칼라 함수 _fnCalculateDistance_를 사용하여 승하차 위치 사이의 직접 거리를 계산합니다.  쿼리 결과는 기본 R 입력 변수인 `InputDataset`에 저장됩니다.  
  
    -   R 스크립트는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에 포함된 향상된 R 함수 중 하나인 `rxLogit` 함수를 호출하여 로지스틱 회귀 모델을 만듭니다.  
  
        이진 변수 _tipped_는 *label* 또는 결과 열로 사용되며 _passenger_count_, _trip_distance_, _trip_time_in_secs_, _direct_distance_ 등의 기능 열을 사용하여 모델을 맞춥니다.  
  
    -   R 변수 `logitObj`에 저장된 학습 모델을 직렬화하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 출력하기 위해 데이터 프레임에 넣습니다. 해당 출력은 미래 예측에 사용할 수 있도록 데이터베이스 테이블 _nyc_taxi_models_에 삽입됩니다.  
  
2.  저장 프로시저를 만드는 문을 실행합니다.  
  
#### 저장 프로시저를 사용하여 R 모델을 만들려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 이 문을 실행합니다.  
  
    ```  
    EXEC TrainTipPredictionModel  
    ```  
  
    데이터를 처리하고 모델을 맞추는 데 시간이 걸릴 수도 있습니다. R의 **stdout** 스트림에 파이프되는 메시지는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 **메시지** 창에 표시됩니다. 예를 들어  
  
  
*외부 스크립트의 STDOUT 메시지: Rows Read: 1193025, Total Rows Processed: 1193025, Total Chunk Time: 0.093 seconds*       
  
연속된 데이터 청크를 읽고 처리합니다. 변수 및 테스트 메트릭을 나타내는, 개별 함수 `rxLogit`과 관련된 메시지를 볼 수도 있습니다.  
  
2.  *nyc_taxi_models* 테이블을 엽니다. _모델_ 열에 직렬화된 모델을 포함하는 하나의 새 행이 추가된 것을 확인할 수 있습니다.  
  
  
  
*모델*  
*0x580A00000002000302020....*  
  
다음 단계에서는 학습된 모델을 사용하여 예측을 만듭니다.  
  
## 다음 단계  
[6단계: 모델 운영화](../../advanced-analytics/r-services/step-6-operationalize-the-model-in-database-advanced-analytics-tutorial.md)  
  
## 이전 단계  
[4단계: T-SQL을 사용하여 데이터 기능 만들기](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md)  
  
## 참고 항목  
[SQL 개발자를 위한 데이터베이스 내 고급 분석&#40;자습서&#41;](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[SQL Server R Services 자습서](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
