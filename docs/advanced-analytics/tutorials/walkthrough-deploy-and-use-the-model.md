---
title: "R 모델을 배포 하 고 사용 하 여 SQL (연습)에서 | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: f28a7aac-6d08-4781-ad28-b48d18cc16a0
caps.latest.revision: "18"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e1f0d2f1a003b54856645dd4ec740de64464436b
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
# <a name="deploy-the-r-model-and-use-it-in-sql"></a>R 모델을 배포 하 고 SQL에서 사용

이 단원에서는 저장된 프로시저에서 학습된 된 모델을 호출 하 여 프로덕션 환경에서 R 모델을 사용 합니다. R 또는 지 원하는 모든 응용 프로그램 프로그래밍 언어에서 저장된 프로시저를 호출할 수 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] (예: C#, Java, Python 등), 예측을 만드는 새 관찰 모델을 사용 하도록 합니다.

이 샘플에는 점수 매기기에서 모델을 사용 하는 두 개의 가장 일반적인 방법은 보여 줍니다.

- **일괄 처리 점수 매기기 모드** 매우 빠르게 여러 예측 만들기, SQL 전달 하 여 쿼리 또는 입력으로 테이블을 할 때 사용 됩니다. 결과 테이블을 반환 됩니다 테이블에 직접 삽입 하거나 파일에 쓸 수 있습니다.

- **개별 점수 매기기 모드** 한 번에 하나씩 예측을 만들어야 할 때 사용 됩니다. 저장된 프로시저에 개별 값 집합을 전달합니다. 값은 모델에서 모델은 예측을 만드는 사용, 기능에 해당 하거나 확률 값과 같은 다른 결과 생성. 그런 다음 응용 프로그램 또는 사용자에 게 해당 값을 반환할 수 있습니다.

## <a name="batch-scoring"></a>일괄 처리 점수 매기기

PowerShell 스크립트를 처음 실행할 때 일괄 처리 점수 매기기에 대 한 저장된 프로시저가 만들어진 수 있습니다. 이 저장 프로시저, *PredictTipBatchMode*, 다음 작업을 수행 합니다.

- 입력 데이터 집합을 SQL 쿼리로 가져오기
- 이전 단원에서 저장한 학습된 로지스틱 회귀 모델 호출
- 드라이버는 0이 아닌 팁을 가져옴을 확률을 예측 합니다.

1. 저장된 프로시저에 대 한 스크립트를 살펴보는 데 1 분 소요 *PredictTipBatchMode*합니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]을 사용하여 모델을 조작할 수 있는 방법의 여러 측면을 보여 줍니다.
  
    ```tsql
    CREATE PROCEDURE [dbo].[PredictTipBatchMode]
    @input nvarchar(max)
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

    + SELECT 문을 사용 하 여 SQL 테이블에서 저장 된 모델을 호출 하는 합니다. 모델 테이블에서 검색 됩니다 **varbinary (max)** SQL 변수에 저장 된 데이터를  _@lmodel2_ 를 매개 변수로 전달 하 고 *mod* 저장 시스템에 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다.

    + 점수 매기기 SQL 쿼리로 정의 되 고 있는 SQL 변수에서 문자열로 저장에 대 한 입력으로 사용 되는 데이터  _@input_ 합니다. 를 데이터베이스에서 데이터를 검색할 때 호출 데이터 프레임에서 저장 *InputDataSet*, 입력된 데이터에 대 한 기본 이름만 되는 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 프로시저; 정의할 수 있습니다 필요한 경우 매개 변수를 사용 하 여 다른 변수 이름을   *_@input_data_1_name_*  합니다.

    + 점수를 생성하기 위해 저장 프로시저가 `rxPredict` RevoScaleR **라이브러리에서** 함수를 호출합니다.

    + 반환 값 *점수*은 확률, 모델을 지정 된 경우 해당 드라이버 팁을 가져옵니다. 필요에 따라 반환 값을 "설명" 및 "팁이 나타나지" 그룹으로 분류 하는 반환 된 값을 일종의 필터를 쉽게 적용할 수 있습니다.  예를 들어 보다 작은 0.5의 확률 팁 될 것을 의미 합니다.
  
2.  일괄 처리 모드에서 저장된 프로시저를 호출 하려면 저장된 프로시저에 대 한 입력으로 필요한 쿼리를 정의 합니다. 다음은 SQL 쿼리입니다. 작동 하는지 확인 하려면 SSMS에서 실행할 수 있습니다.

    ```SQL
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

3. SQL 쿼리에서 입력된 문자열을 만들려면이 R 코드를 사용 합니다.

    ```R
    input <- "N'SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a LEFT OUTER JOIN ( SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND  a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'";
    q <- paste("EXEC PredictTipBatchMode @inquery = ", input, sep="");
    ```

4. R에서 저장된 프로시저를 실행 하려면 호출는 **sqlQuery** 의 메서드는 **RODBC** 패키지 하 고 SQL 연결을 사용 하 여 `conn` 이전 정의:

    ```R
    sqlQuery (conn, q);
    ```

    ODBC 오류가 발생 하는 경우에 쿼리 구문을 검사 하며 올바른 개수의 인용 부호 해야 하는지 여부입니다. 
    
    사용 권한 오류가 발생할 경우 로그인에 저장된 프로시저를 실행 하는 기능이 있는지 확인 합니다.

## <a name="single-row-scoring"></a>단일 행의 점수 매기기

모델-행 단위에 대 한 예측에 대 한를 호출할 때에 각 개별 사례에 대 한 기능을 나타내는 값의 집합을 전달 합니다. 저장된 프로시저는 단일 예측 또는 확률을 반환합니다. 

저장된 프로시저 *PredictTipSingleMode* 이 방법을 보여 줍니다. 변수로 기능 값 (예: 승객 개수 및 여행 거리)을 나타내는 여러 개의 매개 변수가 입력, 저장 된 R 모델을 사용 하 여 이러한 기능을 점수 및 팁 확률을 출력 합니다.

1. 경우 저장된 프로시저 *PredictTipSingleMode* 만들어진 초기 PowerShell 스크립트를 지금 만들 다음 TRANSACT-SQL 문을 실행할 수 있습니다.

    ```tsql
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

2. SQL Server Management Studio에서 사용할 수 있습니다는 [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC** 프로시저 (또는 **EXECUTE**)를 저장된 프로시저를 호출 하 고 필요한 입력 값을 전달 합니다. 예를 들어 Management Studio에서이 문을 실행 해 봅니다.

    ```SQL
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

    여기에 전달 되는 값은 각각, 변수에 대 한 _승객\_count_, _trip_distance_, _여행\_시간\_에\_초_, _픽업\_위도_, _픽업\_경도_, _dropoff\_위도_, 및 _dropoff\_경도_합니다.

3. 이 동일한 호출에서 R 코드를 실행 하려면 단순히 다음과 같은 전체 저장된 프로시저 호출을 포함 하는 R 변수를 정의 합니다.

    ```R
    q2 = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 ";
    ```

    여기에 전달 되는 값은 각각, 변수에 대 한 _승객\_count_, _여행\_거리_, _여행\_시간\_에\_초_, _픽업\_위도_, _픽업\_경도_, _dropoff\_ 위도_, 및 _dropoff\_경도_합니다.

4. 호출 `sqlQuery` (에서 **RODBC** 패키지)와 함께 저장된 프로시저 호출을 포함 하는 문자열 변수를 연결 문자열에 전달 합니다.

    ```R
    # predict with stored procedure in single mode
    sqlQuery (conn, q2);
    ```

    >[!TIP]
    > R 도구 Visual Studio (RTVS)에 대 한 SQL Server와 오른쪽와의 뛰어난 통합 제공 이 문서를 SQL Server 연결에 RODBC 사용의 예 참조: [R 및 SQL Server 작업](https://docs.microsoft.com/en-us/visualstudio/rtvs/sql-server)

## <a name="summary"></a>요약

사용 하는 방법을 배웠습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 학습 된 R 모델을 유지 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 비교적 쉽게이 데이터 집합을 기반으로 하는 새 모델을 만들 수 있어야 합니다. 예를 들어 이러한 추가 모델을 만들어 볼 수 있습니다.

- 팁 금액을 예측하는 회귀 모델

- 팁, 보통, 크거나 작은 인지 여부를 예측 하는 다중 클래스 분류 모델

또한 이러한 추가 샘플 및 리소스 중 일부를 확인하는 것이 좋습니다.

+ [데이터 과학 시나리오 및 솔루션 템플릿](data-science-scenarios-and-solution-templates.md)

+ [데이터베이스 내 고급 분석](sqldev-in-database-r-for-sql-developers.md)

+ [Microsoft R - 데이터 분석 살펴보기](https://msdn.microsoft.com/microsoft-r/data-analysis-in-microsoft-r)

+ [추가 리소스](https://msdn.microsoft.com/microsoft-r/microsoft-r-more-resources)

## <a name="previous-lesson"></a>이전 단원

[R 모델을 작성 하 고 SQL Server에 저장](walkthrough-build-and-save-the-model.md)

## <a name="next-steps"></a>다음 단계

[SQL Server R 자습서](sql-server-r-tutorials.md)

[Sqlrutils를 사용 하 여 저장된 프로시저를 만드는 방법](../r/how-to-create-a-stored-procedure-using-sqlrutils.md)
