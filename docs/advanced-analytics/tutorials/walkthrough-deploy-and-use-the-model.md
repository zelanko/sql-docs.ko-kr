---
title: SQL Server에서 예측을 위해 R 모델 배포
description: 데이터베이스 내 분석을 위해 SQL Server에 R 모델을 배포 하는 방법을 보여 주는 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 2cb6bf28fa849e2015d111c564bb0af84f103d19
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345853"
---
# <a name="deploy-the-r-model-and-use-it-in-sql-server-walkthrough"></a>R 모델을 배포 하 고 SQL Server에 사용 (연습)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 단원에서는 저장 프로시저에서 학습 된 모델을 호출 하 여 프로덕션 환경에서 R 모델을 배포 하는 방법에 대해 알아봅니다. R에서 저장 프로시저를 호출 하거나 [!INCLUDE[tsql](../../includes/tsql-md.md)] C#, (예:, Java, Python 등)를 지 원하는 응용 프로그램 프로그래밍 언어를 호출 하 고, 모델을 사용 하 여 새 관찰에 대 한 예측을 만들 수 있습니다.

이 문서에서는 점수 매기기에서 모델을 사용 하는 가장 일반적인 두 가지 방법을 보여 줍니다.

> [!div class="checklist"]
> * **일괄 처리 점수 매기기 모드** 는 여러 예측을 생성 합니다.
> * **개별 점수 매기기 모드** 는 한 번에 하나씩 예측을 생성 합니다.

## <a name="batch-scoring"></a>일괄 처리 채점

SQL 쿼리 또는 테이블을 입력으로 전달 하 여 여러 예측을 생성 하는 저장 프로시저 *PredictTipBatchMode*를 만듭니다. 결과 테이블이 반환되면 테이블에 직접 입력하거나 파일에 쓸 수 있습니다.

- 입력 데이터 집합을 SQL 쿼리로 가져오기
- 이전 단원에서 저장한 학습된 로지스틱 회귀 모델 호출
- 운전자가 팁을 받을 확률 예측.

1. Management Studio에서 새 쿼리 창을 열고 다음 T-sql 스크립트를 실행 하 여 PredictTipBatchMode 저장 프로시저를 만듭니다.
  
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

    + SELECT 문을 사용하여 SQL 테이블에 저장된 모델을 호출합니다. 모델은 테이블에서 **varbinary (max)** 데이터로 검색 되어 SQL 변수  _\@lmodel2_에 저장 되 고, 시스템 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 매개 변수 *mod* 로 전달 됩니다.

    + 점수 매기기를 위한 입력으로 사용 되는 데이터는 sql 쿼리로 정의 되며 sql 변수  _\@입력_에 문자열로 저장 됩니다. 데이터는 데이터베이스에서 검색 될 때 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 프로시저에 대 한 입력 데이터의 기본 이름인 *inputdataset*이라는 데이터 프레임에 저장 됩니다.  *_\@input_data_1_name_* 매개 변수를 사용 하 여 필요한 경우 다른 변수 이름을 정의할 수 있습니다.

    + 점수를 생성 하기 위해 저장 프로시저가 **RevoScaleR** 라이브러리에서 rxPredict 함수를 호출 합니다.

    + 반환 값 *Score*는 주어진 모델에서 운전자가 팁을 얻는 확률입니다. 선택 사항으로 반환 값을 “팁”과 “팁 없음” 그룹으로 분류하도록 일종의 필터를 쉽게 적용할 수 있습니다.  예를 들어 0.5미만의 확률은 팁이 거의 없음을 의미합니다.
  
2.  일괄 처리 모드로 저장 프로시저를 호출하기 위해 저장 프로시저 입력으로 필요한 쿼리를 아래와 같이 정의합니다. 다음은 SSMS에서 실행 하 여 작동 하는지 확인할 수 있는 SQL 쿼리입니다.

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

3. SQL 쿼리로 프로시저의 입력 문자열을 만들기 위해 다음 R 코드를 사용합니다.

    ```R
    input <- "N'SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a LEFT OUTER JOIN ( SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND  a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'";
    q <- paste("EXEC PredictTipBatchMode @inquery = ", input, sep="");
    ```

4. R에서 저장 프로시저를 실행하기 위해 **RODBC** 패키지의 **sqlQuery** 메서드를 호출하며 이전에 정의한 SQL 연결 `conn`을 사용합니다:

    ```R
    sqlQuery (conn, q);
    ```

    ODBC 오류가 발생 하는 경우 구문 오류와 적절 한 수의 따옴표가 있는지 여부를 확인 합니다. 
    
    사용 권한 오류가 난다면 해당 로그인이 저장 프로시저를 실행할 수 있는 권한이 있는지 확인합니다.

## <a name="single-row-scoring"></a>단일 행 채점

개별 점수 매기기 모드는 개별 값 집합을 저장 프로시저에 입력으로 전달 하 여 한 번에 하나씩 예측을 생성 합니다. 그 값들은 모델에서 예측을 만드는 데 사용하는 특성이나 또 다른 결과를 생성하기 위한 확률 값 같은 것에 해당합니다. 그런 다음 그 값을 응용 프로그램이나 사용자에게 반환할 수 있습니다.

행별로 예측 모델을 호출할 때 각 개별 사례의 특성을 나타내는 값 집합을 전달합니다. 그런 다음 저장 프로시저에서 단일 예측이나 확률을 반환합니다. 

저장 프로시저 *PredictTipSingleMode* 가 이러한 접근 방법을 보여줍니다. 여러 개의 입력 매개변수로 특성 값(예: 승객 수와 여행 거리)을 받아서 저장된 R 모델을 사용하여 그러한 특성을 채점하고 팁 확률을 반환합니다.

1. 다음 Transact-sql 문을 실행 하 여 저장 프로시저를 만듭니다.

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

2. SQL Server Management Studio에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC** 프로시저 (또는 **EXECUTE**)를 사용하여 저장 프로시저를 호출하고 필요한 입력 값을 전달할 수 있습니다. 예를 들어 Management Studio에서 다음 문을 실행해 봅니다.

    ```sql
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

    여기에 전달 되는 값은 각각 변수 _passenger\_count_, _trip_distance_, _trip\_time\_in\_secs_, _pickup\_latitude_, _pickup\_longitude_, _dropoff\_latitude_, _dropoff\_longitude_입니다.

3. 동일한 호출을 R 코드에서 실행하려면 다음과 같이 전체 저장 프로시저 호출을 포함하는 R 변수를 정의하면 됩니다.

    ```R
    q2 = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 ";
    ```

    여기에 전달 되는 값은 각각 변수 _passenger\_count_, _trip\_distance_, _trip\_time\_in\_secs_, _pickup\_latitude_, _pickup\_longitude_, _dropoff\_latitude_, _dropoff\_longitude_입니다.

4. `sqlQuery` (**RODBC** 패키지)를 호출하고 연결 문자열과 함께 저장 프로시저 호출을 포함한 문자열 변수를 전달합니다.

    ```R
    # predict with stored procedure in single mode
    sqlQuery (conn, q2);
    ```

    >[!TIP]
    > RTVS (Visual Studio용 R 도구)는 SQL Server 및 R과의 통합을 제공 합니다. SQL Server 연결에서 RODBC를 사용 하는 방법에 대 한 추가 예제는이 문서를 참조 하세요. [SQL Server 및 R 사용](https://docs.microsoft.com/visualstudio/rtvs/sql-server)

## <a name="next-steps"></a>다음 단계

이제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터로 작업하는 방법과 훈련된 R 모델을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장하는 방법을 배웠으므로 이러한 데이터 집합에 기반해 새로운 모델을 만드는 것은 상대적으로 쉬울 것입니다. 예를 들어, 다음과 같은 추가 모델을 만들어볼 수 있습니다.

+ 팁 금액을 예측하는 회귀 모델
+ 팁이 많은지 보통인지 적은지 예측하는 다중 클래스 분류 모델

이러한 추가 샘플과 리소스를 살펴볼 수도 있습니다.

+ [데이터 과학 시나리오 및 솔루션 템플릿](data-science-scenarios-and-solution-templates.md)
+ [데이터베이스 내 고급 분석](sqldev-in-database-r-for-sql-developers.md)
+ [Machine Learning Server 방법 가이드](https://docs.microsoft.com/machine-learning-server/r/how-to-introduction)
+ [추가 리소스 Machine Learning Server](https://docs.microsoft.com//machine-learning-server/resources-more)
