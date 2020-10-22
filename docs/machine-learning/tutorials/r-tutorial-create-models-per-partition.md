---
title: R에서 파티션 기반 모델 만들기
description: SQL Server 기계 학습의 파티션 기반 모델링 기능을 사용할 때 동적으로 생성된 분할된 데이터를 모델링하고, 학습시키고, 사용하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 04/30/2020
ms.topic: tutorial
ms.author: davidph
author: dphansen
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ec0323d35c05c34de763fbdece37546f7c8252df
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193664"
---
# <a name="tutorial-create-partition-based-models-in-r-on-sql-server"></a>자습서: SQL Server의 R에서 파티션 기반 모델 만들기
[!INCLUDE [SQL Server 2016](../../includes/applies-to-version/sqlserver2016.md)]

SQL Server 2019의 파티션 기반 모델링은 분할된 데이터에 대한 모델을 만들고 학습시키는 기능입니다. 지리적 지역, 날짜 및 시간, 연령 또는 성별 등의 특정 분류 스키마로 자연스럽게 분할되는 계층화 데이터의 경우 모든 작업에서 온전하게 유지되는 파티션을 모델링하고, 학습시키고, 채점하는 기능을 사용하여 전체 데이터 세트에 대해 스크립트를 실행할 수 있습니다. 

파티션 기반 모델링은 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 다음 두 가지 새 매개 변수를 통해 사용하도록 설정됩니다.

+ **input_data_1_partition_by_columns** - 분할 기준이 되는 열을 지정합니다.
+ **input_data_1_order_by_columns** - 정렬 기준이 되는 열을 지정합니다. 

이 자습서에서는 클래식 NYC 택시 샘플 데이터 및 R 스크립트를 사용하여 파티션 기반 모델링에 대해 알아봅니다. 파티션 열은 결제 방법입니다.

> [!div class="checklist"]
> * 파티션은 결제 유형(5)을 기반으로 합니다.
> * 각 파티션에서 모델을 생성 및 학습시키고 데이터베이스에 개체를 저장합니다.
> * 이 목적으로 예약된 샘플 데이터를 사용하여 각 파티션 모델에 대한 팁 결과의 확률을 예측합니다.

## <a name="prerequisites"></a>사전 요구 사항
 
이 자습서를 완료하려면 다음 항목이 필요합니다.

+ 충분한 시스템 리소스. 데이터 세트가 크고 학습 작업은 리소스를 많이 사용합니다. 되도록이면 8GB 이상의 RAM이 있는 시스템을 사용하세요. 또는 작은 데이터 세트를 사용하여 리소스 제약 조건을 피할 수 있습니다. 데이터 세트를 줄이기 위한 지침은 인라인으로 제공됩니다. 

+ [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) 같은 T-SQL 쿼리 실행 도구

+ [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak) - 로컬 데이터베이스 엔진 인스턴스에 [다운로드하고 복원](demo-data-nyctaxi-in-sql.md)할 수 있습니다. 파일 크기는 약 90MB입니다.

+ Machine Learning Services 및 R이 통합된 SQL Server 2019 데이터베이스 엔진 인스턴스입니다.

+ 이 자습서에서는 [ODBC를 통해 R 스크립트에서 SQL Server로 루프백 연결](../connect/loopback-connection.md) 방법을 사용합니다. 따라서 [SQLRUserGroup의 로그인을 만들어야 합니다](../security/create-a-login-for-sqlrusergroup.md).

쿼리 도구에서 T-SQL 쿼리로 **`SELECT @@Version`** 을 실행하여 버전을 확인합니다.

현재 데이터베이스 엔진 인스턴스와 함께 설치된 모든 R 패키지의 잘 포맷된 목록을 반환하여 R 패키지의 가용성을 확인합니다.

```sql
EXECUTE sp_execute_external_script
  @language=N'R',
  @script = N'str(OutputDataSet);
  packagematrix <- installed.packages();
  Name <- packagematrix[,1];
  Version <- packagematrix[,3];
  OutputDataSet <- data.frame(Name, Version);',
  @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

## <a name="connect-to-the-database"></a>데이터베이스에 연결

Management Studio를 시작하고 데이터베이스 엔진 인스턴스에 연결합니다. 개체 탐색기에서 [NYCTaxi_Sample 데이터베이스](demo-data-nyctaxi-in-sql.md)가 있는지 확인합니다. 

## <a name="create-calculatedistance"></a>CalculateDistance 만들기

데모 데이터베이스는 거리를 계산하기 위한 스칼라 함수와 함께 제공되지만, 테이블 반환 함수를 사용하는 저장 프로시저가 더 효율적입니다. 다음 스크립트를 실행하여 나중에 [학습 단계](#training-step)에서 사용되는 **CalculateDistance** 함수를 만듭니다.

함수가 생성되었는지 확인하려면 개체 탐색기에서 **NYCTaxi_Sample** 데이터베이스 아래의 \Programmability\Functions\Table-valued 함수를 확인합니다.

```sql
USE NYCTaxi_sample
GO

SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [dbo].[CalculateDistance] (
    @Lat1 FLOAT
    ,@Long1 FLOAT
    ,@Lat2 FLOAT
    ,@Long2 FLOAT
    )
    -- User-defined function calculates the direct distance between two geographical coordinates.
RETURNS TABLE
AS
RETURN

SELECT COALESCE(3958.75 * ATAN(SQRT(1 - POWER(t.distance, 2)) / nullif(t.distance, 0)), 0) AS direct_distance
FROM (
    VALUES (CAST((SIN(@Lat1 / 57.2958) * SIN(@Lat2 / 57.2958)) + (COS(@Lat1 / 57.2958) * COS(@Lat2 / 57.2958) * COS((@Long2 / 57.2958) - (@Long1 / 57.2958))) AS DECIMAL(28, 10)))
    ) AS t(distance)
GO
 ```

## <a name="define-a-procedure-for-creating-and-training-per-partition-models"></a>파티션당 모델을 만들고 학습시키는 프로시저를 정의합니다.

이 자습서에서는 R 스크립트를 저장 프로시저에 래핑합니다. 이 단계에서는 R을 사용하여 입력 데이터 세트를 만들고, 팁 결과를 예측하기 위한 분류 모델을 빌드하고, 데이터베이스에 모델을 저장하는 저장 프로시저를 만듭니다.

이 스크립트에 사용되는 매개 변수 입력 중에서 **input_data_1_partition_by_columns** 및 **input_data_1_order_by_columns**가 보일 것입니다. 이러한 매개 변수는 분할된 모델링이 발생하는 메커니즘입니다. 이러한 매개 변수는 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 입력으로 전달되어 파티션마다 한 번씩 실행되는 외부 스크립트를 사용하여 파티션을 처리합니다. 

이 저장 프로시저의 경우 완료 시간을 단축할 수 있도록 [병렬 처리를 사용](#parallel)하세요.

이 스크립트를 실행하면 개체 탐색기의 **NYCTaxi_Sample** 데이터베이스 아래에 있는 \Programmability\Stored Procedures 프로시저에 **train_rxLogIt_per_partition**이 보입니다. 모델을 저장하는 데 사용되는 새 테이블 **dbo.nyctaxi_models**도 보입니다.

```sql
USE NYCTaxi_Sample
GO

CREATE
    OR

ALTER PROCEDURE [dbo].[train_rxLogIt_per_partition] (@input_query NVARCHAR(max))
AS
BEGIN
    DECLARE @start DATETIME2 = SYSDATETIME()
        ,@model_generation_duration FLOAT
        ,@model VARBINARY(max)
        ,@instance_name NVARCHAR(100) = @@SERVERNAME
        ,@database_name NVARCHAR(128) = db_name();

    EXEC sp_execute_external_script @language = N'R'
        ,@script = 
        N'
    
    # Make sure InputDataSet is not empty. In parallel mode, if one thread gets zero data, an error occurs
    if (nrow(InputDataSet) > 0) {
    # Define the connection string
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    
    # build classification model to predict a tip outcome
    duration <- system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet))[3];

    # First, serialize a model to and put it into a database table
    modelbin <- as.raw(serialize(logitObj, NULL));

    # Create the data source. To reduce data size, add rowsPerRead=500000 to cut the dataset by half.
    ds <- RxOdbcData(table="ml_models", connectionString=connStr);

    # Store the model in the database
    model_name <- paste0("nyctaxi.", InputDataSet[1,]$payment_type);
    
    rxWriteObject(ds, model_name, modelbin, version = "v1",
    keyName = "model_name", valueName = "model_object", versionName = "model_version", overwrite = TRUE, serialize = FALSE);
    } 
    
    '
        ,@input_data_1 = @input_query
        ,@input_data_1_partition_by_columns = N'payment_type'
        ,@input_data_1_order_by_columns = N'passenger_count'
        ,@parallel = 1
        ,@params = N'@instance_name nvarchar(100), @database_name nvarchar(128)'
        ,@instance_name = @instance_name
        ,@database_name = @database_name
    WITH RESULT SETS NONE
END;
GO
```

<a name="parallel"></a>

### <a name="parallel-execution"></a>병렬 실행

[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 입력은 병렬 처리를 사용하도록 설정하는 데 사용되는 `@parallel=1`을 포함하고 있습니다. 이전 릴리스와는 달리, SQL Server 2019에서는 `@parallel=1`을 설정하면 쿼리 최적화 프로그램에 더 강력한 힌트가 제공되므로 병렬 실행의 결과를 얻을 확률이 훨씬 높습니다.

기본적으로 쿼리 최적화 프로그램은 행이 256개를 초과하는 테이블의 `@parallel=1`에서 작동하는 경향이 있지만, 가능하다면 이 스크립트에서 보여드리는 것처럼 `@parallel=1`을 설정하여 명시적으로 처리할 수 있습니다.

> [!Tip]
> 학습 워크로드의 경우 비-Microsoft-rx 알고리즘을 사용 중이어도 임의의 학습 스크립트에 `@parallel`을 사용할 수 있습니다. 일반적으로 RevoScaleR 알고리즘(rx 접두사 포함)만이 SQL Server의 학습 시나리오에서 병렬 처리를 제공합니다. 그러나 새 매개 변수를 사용하면 오픈 소스 R 함수를 포함하여 해당 기능을 사용하여 특별히 엔지니어링되지 않은 함수를 호출하는 스크립트를 병렬화할 수 있습니다. 이는 파티션이 특정 스레드에 대한 선호도를 갖고 있기 때문이며, 따라서 스크립트에서 호출되는 모든 작업은 특정`thread.`<a name="training-step">에서 파티션별로 실행됩니다</a>

## <a name="run-the-procedure-and-train-the-model"></a>프로시저를 실행하고 모델 학습

이 섹션의 스크립트는 이전 단계에서 만들고 저장한 모델을 학습시킵니다. 아래 예제에서는 모델을 학습시키는 두 가지 접근 방식을 보여주는데, 하나는 전체 데이터 세트를 사용하는 방법이고, 다른 하나는 부분 데이터를 사용하는 방법입니다. 

이 단계는 다소 시간이 걸립니다. 학습은 컴퓨팅 집약적이며, 완료하는 데 시간이 걸립니다. 시스템 리소스, 특히 메모리가 부하에 비해 충분하지 않은 경우 데이터 하위 세트를 사용하세요. 두 번째 예제는 구문을 제공합니다.

```sql
--Example 1: train on entire dataset
EXEC train_rxLogIt_per_partition N'
SELECT payment_type, tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance
  FROM dbo.nyctaxi_sample CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d
';
GO
```

```sql
--Example 2: Train on 20 percent of the dataset to expedite processing.
EXEC train_rxLogIt_per_partition N'
  SELECT tipped, payment_type, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance
  FROM dbo.nyctaxi_sample TABLESAMPLE (20 PERCENT) REPEATABLE (98074)
  CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d
';
GO
```

> [!NOTE]
> 다른 워크로드를 실행 중인 경우 쿼리 처리를 2코어로 제한하려면 SELECT 문에 `OPTION(MAXDOP 2)`를 추가하면 됩니다.

## <a name="check-results"></a>결과 확인

모델 테이블의 결과는 5가지 결제 유형에 따라 분할된 5개 파티션을 기반으로 하는 5개의 서로 다른 모델입니다. 모델은 **ml_models** 데이터 원본에 있습니다.

```sql
SELECT *
FROM ml_models
```
 
## <a name="define-a-procedure-for-predicting-outcomes"></a>결과를 예측하는 프로시저 정의

동일한 매개 변수를 채점에 사용할 수 있습니다. 다음 샘플에는 현재 처리 중인 파티션에 적합한 모델을 사용하여 채점하는 R 스크립트가 포함되어 있습니다.

이전과 마찬가지로, R 코드를 래핑하는 저장 프로시저를 만듭니다.

```sql
USE NYCTaxi_Sample
GO

-- Stored procedure that scores per partition. 
-- Depending on the partition being processed, a model specific to that partition will be used
CREATE
    OR

ALTER PROCEDURE [dbo].[predict_per_partition]
AS
BEGIN
    DECLARE @predict_duration FLOAT
        ,@instance_name NVARCHAR(100) = @@SERVERNAME
        ,@database_name NVARCHAR(128) = db_name()
        ,@input_query NVARCHAR(max);

    SET @input_query = 'SELECT tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance, payment_type
                          FROM dbo.nyctaxi_sample TABLESAMPLE (1 PERCENT) REPEATABLE (98074)
                          CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d'

    EXEC sp_execute_external_script @language = N'R'
        ,@script = 
        N'
    
    if (nrow(InputDataSet) > 0) {

    #Get the partition that is currently being processed
    current_partition <- InputDataSet[1,]$payment_type;

    #Create the SQL query to select the right model
    query_getModel <- paste0("select model_object from ml_models where model_name = ", "''", "nyctaxi.",InputDataSet[1,]$payment_type,"''", ";")
    

    # Define the connection string
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
        
    #Define data source to use for getting the model
    ds <- RxOdbcData(sqlQuery = query_getModel, connectionString = connStr)

    # Load the model
    modelbin <- rxReadObject(ds, deserialize = FALSE)
    # unserialize model
    logitObj <- unserialize(modelbin);

    # predict tipped or not based on model
    predictions <- rxPredict(logitObj, data = InputDataSet, overwrite = TRUE, type = "response", writeModelVars = TRUE
        , extraVarsToWrite = c("payment_type"));        
    OutputDataSet <- predictions
    
    } else {
        OutputDataSet <- data.frame(integer(), InputDataSet[,]);        
    }
    '
        ,@input_data_1 = @input_query
        ,@parallel = 1
        ,@input_data_1_partition_by_columns = N'payment_type'
        ,@params = N'@instance_name nvarchar(100), @database_name nvarchar(128)'
        ,@instance_name = @instance_name
        ,@database_name = @database_name
    WITH RESULT SETS((
                tipped_Pred INT
                ,payment_type VARCHAR(5)
                ,tipped INT
                ,passenger_count INT
                ,trip_distance FLOAT
                ,trip_time_in_secs INT
                ,direct_distance FLOAT
                ));
END;
GO
```

## <a name="create-a-table-to-store-predictions"></a>예측을 저장할 테이블 만들기

```sql
CREATE TABLE prediction_results (
    tipped_Pred INT
    ,payment_type VARCHAR(5)
    ,tipped INT
    ,passenger_count INT
    ,trip_distance FLOAT
    ,trip_time_in_secs INT
    ,direct_distance FLOAT
    );

TRUNCATE TABLE prediction_results
GO
```

## <a name="run-the-procedure-and-save-predictions"></a>프로시저를 실행하고 예측 저장

```sql
INSERT INTO prediction_results (
    tipped_Pred
    ,payment_type
    ,tipped
    ,passenger_count
    ,trip_distance
    ,trip_time_in_secs
    ,direct_distance
    )
EXECUTE [predict_per_partition]
GO
```

## <a name="view-predictions"></a>예측 보기

예측이 저장되었으므로, 간단한 쿼리를 실행하여 결과 세트를 반환할 수 있습니다.

```sql
SELECT *
FROM prediction_results;
```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 분할된 데이터를 대상으로 작업을 반복합니다. 저장 프로시저의 외부 스크립트를 호출하고 RevoScaleR 함수를 사용하는 방법을 자세히 살펴보려면 다음 자습서를 계속 진행하세요.

> [!div class="nextstepaction"]
> [R 및 SQL Server 연습](walkthrough-data-science-end-to-end-walkthrough.md)