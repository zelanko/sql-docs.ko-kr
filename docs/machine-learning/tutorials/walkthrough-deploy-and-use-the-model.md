---
title: 'R 자습서: 모델 배포'
description: 저장 프로시저에서 학습된 모델을 호출하여 프로덕션 환경에서 R 모델을 배포하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5585f26247ad360fa848a24109416a59c49c94a6
ms.sourcegitcommit: ef20f39a17fd4395dd2dd37b8dd91b57328a751c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2020
ms.locfileid: "92793780"
---
# <a name="deploy-the-r-model-and-use-it-in-sql-server-walkthrough"></a>R 모델을 배포하고 SQL Server에서 사용(연습)
[!INCLUDE [SQL Server 2016](../../includes/applies-to-version/sqlserver2016.md)]

이 단원에서는 저장 프로시저에서 학습된 모델을 호출하여 프로덕션 환경에서 R 모델을 배포하는 방법을 알아봅니다. R 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 지원하는 모든 애플리케이션 프로그래밍 언어(예: C#, Java, Python 등)에서 저장 프로시저를 호출하고 해당 모델을 사용하여 새로운 관찰에 따라 예측을 수행할 수 있습니다.

이 문서에서는 점수 매기기에서 모델을 사용하는 다음과 같은 가장 일반적인 두 가지 방법을 보여 줍니다.

> [!div class="checklist"]
> * **일괄 처리 점수 매기기 모드** : 여러 예측 생성
> * **개별 점수 매기기 모드** : 한 번에 하나씩 예측 생성

## <a name="batch-scoring"></a>일괄 처리 점수 매기기

여러 예측을 생성하고 SQL 쿼리 또는 테이블을 입력으로 전달하는 저장 프로시저 *PredictTipBatchMode* 를 만듭니다. 결과 테이블이 반환되며 테이블에 직접 삽입하거나 파일에 쓸 수 있습니다.

- 입력 데이터 집합을 SQL 쿼리로 가져오기
- 이전 단원에서 저장한 학습된 로지스틱 회귀 모델 호출
- 운전 기사가 0이 아닌 팁을 받을 확률 예측

1. Management Studio에서 새 쿼리 창을 열고 다음 T-SQL 스크립트를 실행하여 PredictTipBatchMode 저장 프로시저를 만듭니다.
  
    ```sql
    USE [NYCTaxi_Sample]
    GO

    SET ANSI_NULLS ON
    GO
    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PredictTipBatchMode')
    DROP PROCEDURE v
    GO

    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @input nvarchar(max)
    AS
    BEGIN
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  FROM nyc_taxi_models);
      EXEC sp_execute_external_script @language = N'R',
         @script = N'
           mod <- unserialize(as.raw(model));
           print(summary(mod))
           OutputDataSet<-rxPredict(modelObject = mod,
             data = InputDataSet,
             outData = NULL,
             predVarNames = "Score", type = "response",
             writeModelVars = FALSE, overwrite = TRUE);
           str(OutputDataSet)
           print(OutputDataSet)',
      @input_data_1 = @input,
      @params = N'@model varbinary(max)',
      @model = @lmodel2
      WITH RESULT SETS ((Score float));
    END
    ```

    + SELECT 문을 사용하여 SQL 테이블에서 저장된 모델을 호출합니다. 테이블에서 **varbinary(max)** 데이터로 모델을 검색하고, SQL 변수 _\@lmodel2_ 에 저장한 다음, 시스템 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 *mod* 매개 변수로 전달합니다.

    + 점수 매기기에 대한 입력으로 사용되는 데이터는 SQL 쿼리로 정의되고 SQL 변수 _\@input_ 에 문자열로 저장됩니다. 데이터베이스에서 검색된 데이터는 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 프로시저에 대한 입력 데이터의 기본 이름인 *InputDataSet* 데이터 프레임에 저장됩니다. 필요한 경우 매개 변수 _\@input_data_1_name_ 을 사용하여 다른 변수 이름을 정의할 수 있습니다.

    + 점수를 생성하기 위해 저장 프로시저가 **RevoScaleR** 라이브러리에서 rxPredict 함수를 호출합니다.

    + 반환 값 *Score* 는 지정된 모델에서 운전 기사가 팁을 받을 확률입니다. 필요한 경우 반환된 값에 일종의 필터를 쉽게 적용하여 반환 값을 "tip" 및 "no tip" 그룹으로 분류할 수 있습니다.  예를 들어 확률이 0.5 미만이면 팁이 없을 가능성이 큽니다.
  
2.  일괄 처리 모드에서 저장 프로시저를 호출하려면 필요한 쿼리를 저장 프로시저에 대한 입력으로 정의합니다. 다음은 SSMS에서 실행하여 작동하는지 확인할 수 있는 SQL 쿼리입니다.

    ```sql
    SELECT TOP 10
      a.passenger_count AS passenger_count,
      a.trip_time_in_secs AS trip_time_in_secs,
      a.trip_distance AS trip_distance,
      a.dropoff_datetime AS dropoff_datetime,
      dbo.fnCalculateDistance( pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance
      FROM 
        (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude 
        FROM nyctaxi_sample)a 
      LEFT OUTER JOIN
      ( SELECT medallion, hack_license, pickup_datetime
      FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b
      ON a.medallion=b.medallion
      AND a.hack_license=b.hack_license
      AND a.pickup_datetime=b.pickup_datetime
      WHERE b.medallion is null
    ```

3. 다음 R 코드를 사용하여 SQL 쿼리에서 입력 문자열을 만듭니다.

    ```R
    input <- "N'SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a LEFT OUTER JOIN ( SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND  a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'";
    q <- paste("EXEC PredictTipBatchMode @input = ", input, sep="");
    ```

4. R에서 저장 프로시저를 실행하려면 **RODBC** 패키지의 **sqlQuery** 메서드를 호출하고 앞에서 정의한 SQL 연결 `conn`을 사용합니다.

    ```R
    sqlQuery (conn, q);
    ```

    ODBC 오류가 발생하는 경우 구문 오류가 있는지와 적절한 수의 따옴표를 사용했는지 확인합니다. 
    
    권한 오류가 발생하면 로그인에 저장 프로시저를 실행할 수 있는 권한이 있는지 확인합니다.

## <a name="single-row-scoring"></a>단일 행 점수 매기기

개별 점수 매기기 모드는 개별 값 집합을 저장 프로시저에 입력으로 전달하여 한 번에 하나씩 예측을 생성합니다. 값은 모델이 예측을 만들거나 확률 값 등의 다른 결과를 생성하는 데 사용하는 모델의 기능에 해당합니다. 이제 해당 값을 애플리케이션이나 사용자에게 반환할 수 있습니다.

행 단위로 예측하기 위해 모델을 호출하는 경우 각 개별 사례에 대한 특성을 나타내는 값 세트를 전달합니다. 그러면 저장 프로시저는 단일 예측 또는 확률을 반환합니다. 

*PredictTipSingleMode* 저장 프로시저는 이 방법을 보여 줍니다. 특성 값을 나타내는 여러 매개 변수를 입력으로 사용하고(예: 승객 수 및 이동 거리), 저장된 R 모델을 사용하여 이러한 특성의 점수를 매기고, 팁이 제공될 확률을 출력합니다.

1. 다음 Transact-SQL 문을 실행하여 저장 프로시저를 만듭니다.

    ```sql
    USE [NYCTaxi_Sample]
    GO

    SET ANSI_NULLS ON
    GO
    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PredictTipSingleMode')
    DROP PROCEDURE v
    GO

    CREATE PROCEDURE [dbo].[PredictTipSingleMode] @passenger_count int = 0,
    @trip_distance float = 0,
    @trip_time_in_secs int = 0,
    @pickup_latitude float = 0,
    @pickup_longitude float = 0,
    @dropoff_latitude float = 0,
    @dropoff_longitude float = 0
    AS
    BEGIN
      DECLARE @inquery nvarchar(max) = N'
        SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs, @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)'
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);

      EXEC sp_execute_external_script @language = N'R',  @script = N'
            mod <- unserialize(as.raw(model));
            print(summary(mod))
            OutputDataSet<-rxPredict(
              modelObject = mod,
              data = InputDataSet,
              outData = NULL,
              predVarNames = "Score",
              type = "response",
              writeModelVars = FALSE,
              overwrite = TRUE);
            str(OutputDataSet)
            print(OutputDataSet)
            ',
      @input_data_1 = @inquery,
      @params = N'
      -- passthrough columns
      @model varbinary(max) ,
      @passenger_count int ,
      @trip_distance float ,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
      -- mapped variables
      @model = @lmodel2 ,
      @passenger_count =@passenger_count ,
      @trip_distance=@trip_distance ,
      @trip_time_in_secs=@trip_time_in_secs ,
      @pickup_latitude=@pickup_latitude ,
      @pickup_longitude=@pickup_longitude ,
      @dropoff_latitude=@dropoff_latitude ,
      @dropoff_longitude=@dropoff_longitude
      WITH RESULT SETS ((Score float));
    END
    ```

2. SQL Server Management Studio에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC** 프로시저(또는 **EXECUTE** )를 사용하여 저장 프로시저를 호출하고 필요한 입력을 전달합니다. 예를 들어, Management Studio에서 다음 문을 실행해 봅니다.

    ```sql
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

    여기서 전달되는 값은 각각 _passenger\_count_ , _trip_distance_ , _trip\_time\_in\_secs_ , _pickup\_latitude_ , _pickup\_longitude_ , _dropoff\_latitude_ 및 _dropoff\_longitude_ 변수에 사용됩니다.

3. R 코드에서 이 동일한 호출을 실행하려면 다음과 같이 전체 저장 프로시저 호출이 포함된 R 변수를 정의하면 됩니다.

    ```R
    q2 = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 ";
    ```

    여기서 전달되는 값은 각각 _passenger\_count_ , _trip\_distance_ , _trip\_time\_in\_secs_ , _pickup\_latitude_ , _pickup\_longitude_ , _dropoff\_latitude_ 및 _dropoff\_longitude_ 변수에 사용됩니다.

4. `sqlQuery`( **RODBC** 패키지에서)를 호출하고 저장 프로시저 호출이 포함된 문자열 변수 및 연결 문자열을 함께 전달합니다.

    ```R
    # predict with stored procedure in single mode
    sqlQuery (conn, q2);
    ```

    >[!TIP]
    > RTVS(Visual Studio용 R 도구)를 사용하면 SQL Server 및 R과 보다 잘 연결됩니다. SQL Server 연결에서 RODBC를 사용하는 방법에 대한 추가 예제를 보려면 다음 문서를 참조하세요. [SQL Server 및 R 사용](/visualstudio/rtvs/sql-server)

## <a name="next-steps"></a>다음 단계

이제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 사용하고 학습된 R 모델을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장하는 방법을 배웠으므로 이 데이터 집합을 기반으로 하여 새로운 모델을 비교적 쉽게 만들 수 있습니다. 예를 들어, 다음과 같은 추가 모델을 만들어 볼 수 있습니다.

+ 팁 금액을 예측하는 회귀 모델
+ 팁이 많은지, 보통인지, 작은지를 예측하는 다중 클래스 분류 모델

다음과 같은 추가 샘플과 리소스를 살펴볼 수도 있습니다.

+ [데이터 과학 시나리오 및 솔루션 템플릿](data-science-scenarios-and-solution-templates.md)
+ [데이터베이스 내 고급 분석](r-taxi-classification-introduction.md)
+ [Machine Learning Server 방법 가이드](/machine-learning-server/r/how-to-introduction)
+ [Machine Learning Server 추가 리소스](/machine-learning-server/resources-more)