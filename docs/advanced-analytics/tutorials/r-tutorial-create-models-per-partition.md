---
title: 만들기, 학습 및 R-SQL Server Machine Learning Services의에서 파티션 기반 모델을 점수 매기기에 대 한 자습서
description: 모델을 학습, SQL Server machine learning의 파티션 기반 모델링 기능을 사용 하 여 때 동적으로 생성 되는 분할 된 데이터를 사용 하는 방법에 알아봅니다.
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/02/2018
ms.topic: tutorial
ms.author: heidist
author: HeidiSteen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4c60a50f5a0f1c1831a4831d1f93ddf7d81a11d9
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596464"
---
# <a name="tutorial-create-partition-based-models-in-r-on-sql-server"></a>자습서: SQL Server의 R에서 파티션 기반 모델 만들기
[!INCLUDE[appliesto-ssvnex-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

SQL Server 2019 파티션 기반 모델링에서는 분할 데이터 모델을 학습 하는 기능입니다. 지역, 날짜 및 시간, 나가 또는 성별-같은 지정된 분류 구성표-에 자연스럽 게 세그먼트는 계층화 된 데이터에 대 한 스크립트 실행할 수 있습니다. 있습니다 전체 데이터 집합에 대해 모델링, 학습 및 점수를 그대로 유지 하는 파티션에서 수 이러한 모든 작업입니다. 

두 개의 새 매개 변수를 통해 파티션 기반 모델링 설정할지 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql):

+ **input_data_1_partition_by_columns**, 파티션에 열을 지정 하는 합니다.
+ **input_data_1_order_by_columns** 정렬 기준 열을 지정 합니다. 

이 자습서에서는 클래식 NYC 택시 샘플 데이터 및 R 스크립트를 사용 하 여 파티션 기반 모델링에 알아봅니다. 파티션 열에는 지불 방법입니다.

> [!div class="checklist"]
> * 파티션에 지불 유형은 (5)를 기반으로 합니다.
> * 각 파티션에 모델을 학습 만들고 데이터베이스에서 개체를 저장 합니다.
> * 해당 목적을 위해 예약 하는 샘플 데이터를 사용 하 여 각 파티션 모델을 통해 팁 결과의 확률을 예측 합니다.

## <a name="prerequisites"></a>사전 요구 사항
 
이 자습서를 완료 하려면 다음이 필요 합니다.

+ 시스템 리소스가 충분 합니다. 데이터 집합이 크면 및 학습 작업은 리소스를 많이 사용 합니다. 가능 하면 최소 8GB RAM 포함 된 시스템을 사용 합니다. 또는 리소스 제약 조건을 해결 하려면 더 작은 데이터 집합을 사용할 수 있습니다. 데이터 집합을 줄이기 위한 지침은 인라인입니다. 

+ 쿼리 실행, 같은 T-SQL에 대 한 도구 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다.

+ [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak)를 할 수 있습니다 [다운로드 하 고 복원](demo-data-nyctaxi-in-sql.md) 로컬 데이터베이스 엔진 인스턴스로. 파일 크기는 약 90입니다.

+ SQL Server 2019 미리 보기 데이터베이스 엔진 인스턴스, Machine Learning Services 및 R 통합 합니다.

실행 하 여 버전을 확인 **`SELECT @@Version`** 쿼리 도구에서 T-SQL 쿼리로 합니다. 출력 해야 "Microsoft SQL Server (CTP 2.0)-2019 15.0.x"입니다.

데이터베이스 엔진 인스턴스를 사용 하 여 현재 설치 된 모든 R 패키지의 잘못 된 목록을 반환 하 여 R 패키지의 가용성을 확인:

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

Management Studio를 시작 하 고 데이터베이스 엔진 인스턴스에 연결 합니다. 개체 탐색기에서 확인 합니다 [NYCTaxi_Sample 데이터베이스](demo-data-nyctaxi-in-sql.md) 존재 합니다. 

## <a name="create-calculatedistance"></a>CalculateDistance 만들기

테이블 반환 함수를 사용 하 여 계산 거리 하지만 더 나은 저장된 프로시저 작동에 대 한 스칼라 함수를 사용 하 여 데모 데이터베이스 제공 됩니다. 만들려면 다음 스크립트를 실행 합니다 **CalculateDistance** 에서 사용 되는 함수는 [교육 단계](#training-step) 나중에 합니다.

함수가 생성 된를 확인 하려면 아래 \Programmability\Functions\Table-valued 함수를 확인 합니다 **NYCTaxi_Sample** 개체 탐색기에서 데이터베이스입니다.

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

## <a name="define-a-procedure-for-creating-and-training-per-partition-models"></a>만들기 및 파티션 별 모델을 학습 하는 절차를 정의 합니다.

이 자습서는 저장된 프로시저에서 R 스크립트를 래핑합니다. 이 단계에서는 R을 사용 하 여 입력된 데이터 집합 만들기, 팁의 결과 예측 하는 것에 대 한 분류 모델을 빌드 및 모델 데이터베이스에 저장 하는 저장된 프로시저를 만듭니다.

이 스크립트에서 사용 하는 매개 변수 입력 간에 표시 **input_data_1_partition_by_columns** 하 고 **input_data_1_order_by_columns**합니다. 메커니즘은 분할 모델링 이러한 매개 변수는 회수가 발생 합니다. 매개 변수 입력으로 전달 됩니다 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 를 사용 하 여 외부 스크립트를 실행 하는 한 번 모든 파티션에 대 한 파티션 처리 합니다. 

이 저장 프로시저 [병렬 처리를 사용 하 여](#parallel) 빠르게 완료 시간에 대 한 합니다.

이 스크립트를 실행 한 후 표시 **train_rxLogIt_per_partition** \Programmability\Stored 절차 아래에 **NYCTaxi_Sample** 개체 탐색기에서 데이터베이스입니다. 모델을 저장 하는 데 사용 되는 새 테이블을 볼 수 있어야 합니다. **dbo.nyctaxi_models**합니다.

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

다음에 유의 합니다 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 입력을 포함  **@parallel= 1**병렬 처리를 사용 하도록 설정 하는 데 사용 합니다. SQL Server 2019, 설정의 이전 릴리스와 달리  **@parallel= 1** 가능성이 훨씬 더 결과 병렬 실행을 수행 하는 쿼리 최적화 프로그램 강력한 힌트를 제공 합니다.

기본적으로 쿼리 최적화 프로그램에서 작동 경향이  **@parallel= 1** 처리 하면이 명시적으로 설정 하 여 있지만 256 개 이상의 행이 있는 테이블의  **@parallel= 1** 이 표시 된 것과 같이 스크립트입니다.

> [!Tip]
> 교육 workoads 사용할 수 있습니다 **@parallel** 모든 임의 학습 스크립트를 사용 하 여 비 Microsoft rx 알고리즘을 사용 하는 것에 합니다. 일반적으로 (rx 접두사로) RevoScaleR 알고리즘만 SQL Server의 교육 시나리오에서 병렬 처리를 제공합니다. 하지만 새 매개 변수를 사용 하 여 해당 기능을 사용 하 여 특별히 엔지니어링 된 오픈 소스 R 함수를 비롯 한 함수를 호출 하는 스크립트를 병렬 처리할 수 있습니다. 파티션의 때문에 선호도를 특정 스레드에 지정 된 스레드에 대해 파티션 별 기준으로 스크립트에서 호출 하는 모든 작업 실행이 작동 합니다.

<a name="training-step"></a>

## <a name="run-the-procedure-and-train-the-model"></a>프로시저를 실행 하 고 모델 학습

이 섹션에서는 스크립트를 만들고 이전 단계에서 저장 하는 모델을 학습 합니다. 아래 예제에서는 모델을 학습 하는 것에 대 한 두 가지 방법을 보여 줍니다: 데이터 집합을 전체 또는 부분 데이터를 사용 하 여 합니다. 

이 단계에 시간이 조금 걸릴를 기대 합니다. 교육 기법은 완료 하려면 몇 분 걸리는 아닙니다. 시스템 리소스, 특히 메모리 로드에 충분 하지 않은 경우 데이터의 하위 집합을 사용 합니다. 두 번째 예제는 구문을 제공 합니다.

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
> 추가할 수 있습니다 다른 워크 로드를 실행 하는 경우 `OPTION(MAXDOP 2)` SELECT 문에 바로 2 개의 코어를 쿼리 처리를 제한 하려는 경우.

## <a name="check-results"></a>결과 확인

모델 테이블의 결과는 5 개의 파티션을 5 지불 형식에서 분할을 기반으로 5 개의 서로 다른 모델 이어야 합니다. 모델에는 **ml_models** 데이터 원본입니다.

```sql
SELECT *
FROM ml_models
```
 
## <a name="define-a-procedure-for-predicting-outcomes"></a>결과 예측 하는 절차를 정의 합니다.

점수 매기기에 동일한 매개 변수를 사용할 수 있습니다. 다음 샘플에는 현재 처리 하는 파티션에 대 한 올바른 모델을 사용 하 여 점수를 매기는 R 스크립트를 포함 합니다.

이전과 마찬가지로 R 코드를 래핑할 저장된 프로시저를 만듭니다.

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

## <a name="create-a-table-to-store-predictions"></a>예측을 저장 하는 테이블 만들기

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

## <a name="run-the-procedure-and-save-predictions"></a>프로시저를 실행 하 고 예측 저장

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

## <a name="view-predictions"></a>보기 예측

예측 저장 되므로 결과 집합을 반환 하는 간단한 쿼리를 실행할 수 있습니다.

```sql
SELECT *
FROM prediction_results;
```

## <a name="next-steps"></a>다음 단계

이 자습서에서 사용한 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 분할 된 데이터에 대해 작업을 반복 합니다. 더 자세히 검토할에 대 한 저장된 프로시저의 외부 스크립트를 호출 살펴보고 다음 자습서를 계속 RevoScaleR 함수를 사용 합니다.

> [!div class="nextstepaction"]
> [R 및 SQL Server에 대 한 연습](walkthrough-data-science-end-to-end-walkthrough.md)

<!--
## Old intro

**(Not for production workloads)**

One of the more common approaches for executing R or Python code on SQL data is providing script as an input parameter to the [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) stored procedure. In this CTP release, SQL Server 2019 adds new parameters to `sp_execute_external_script` to process partitions with the external script executing once for every partition:

| Parameter | Usage |
|-----------|-------|
| **input_data_1_partition_by_columns** | Specifies which columns to partition by. |
| **input_data_1_order_by_columns** | Specifies which columns to order by.  |

Partitions are an organizational mechanism for stratified data that naturally segments into a given classification scheme. Common examples include partitioning by geographic region, by date and time, by age or gender, and so forth. Given the existence of partitioned data, you might want to execute script over the entire data set, with the ability to model, train, and score partitions that remain intact over all these operations. Calling `sp_execute_external_script` with the new parameters allows you to do just that.

You can run this operation in parallel by combining `partition_by` with `@parallel`. If the input query can be parallelized, set `@parallel=1` as part of your arguments to `sp_execute_external_script`. By default, the query optimizer operates under `@parallel=1` on tables having more than 256 rows.

When the scenario is training, one advantage is that any arbitrary training script, even those using non-Microsoft-rx algorithms, can be parallelized by also using the @parallel parameter. Typically, you would have to use RevoScaleR algorithms (with the rx prefix) to obtain parallelism in training scenarios in SQL Server. But with the new parameter, you can parallelize a script that calls functions not specifically engineered with that capability.
-->
