---
title: T-SQL PREDICT를 사용하는 네이티브 채점
titleSuffix: SQL machine learning
description: PREDICT T-SQL 함수와 함께 네이티브 채점을 사용하여 거의 실시간으로 새 데이터 입력에 대한 예측 값을 생성하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/29/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=azuresqldb-mi-current||=azure-sqldw-latest||=sqlallproducts-allversions'
ms.openlocfilehash: 762d272661fd9bfaa61781391e42d3d9919d78c1
ms.sourcegitcommit: 039fb38c583019b3fd06894160568387a19ba04e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87442911"
---
# <a name="native-scoring-using-the-predict-t-sql-function-with-sql-machine-learning"></a>SQL 기계 학습에서 PREDICT T-SQL 함수를 사용하는 네이티브 채점

[!INCLUDE [sqlserver2017-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2017-asdb-asdbmi-asa.md)]

[PREDICT T-SQL](../../t-sql/queries/predict-transact-sql.md) 함수와 함께 네이티브 채점을 사용하여 거의 실시간으로 새 데이터 입력에 대한 예측 값을 생성하는 방법을 알아봅니다. 네이티브 채점을 사용하려면 이미 학습된 모델이 있어야 합니다.

`PREDICT` 함수는 [SQL 기계 학습](../index.yml)에서 네이티브 C++ 확장 기능을 사용합니다. 이 방법은 예측 워크로드에 가장 빠른 처리 속도를 제공하며 [ONNX(Open Neural Network Exchange)](https://onnx.ai/get-started.html) 형식의 모델 또는 [RevoScaleR](../r/ref-r-revoscaler.md) 및 [revoscalepy](../python/ref-py-revoscalepy.md) 패키지를 사용하여 학습된 모델을 지원합니다.

## <a name="how-native-scoring-works"></a>네이티브 채점의 작동 방법

네이티브 채점은 ONNX 또는 미리 정의된 이진 형식으로 모델을 읽고 사용자가 제공하는 새 데이터 입력에 대한 점수를 생성할 수 있는 라이브러리를 사용합니다. 모델은 학습, 배포 및 저장되므로 R 또는 Python 인터프리터를 호출할 필요 없이 채점에 사용할 수 있습니다. 즉, 다중 프로세스 상호 작용의 오버헤드가 감소하여 예측 속도가 향상됩니다.

네이티브 채점을 사용하려면 `PREDICT` T-SQL 함수를 호출하고 다음과 같은 필수 입력을 전달합니다.

+ 지원되는 모델 및 알고리즘을 기반으로 하는 호환 모델.
+ 일반적으로 T-SQL 쿼리로 정의된 입력 데이터.

함수는 전달하려는 원본 데이터의 열과 함께 입력 데이터에 대한 예측을 반환합니다.

## <a name="prerequisites"></a>사전 요구 사항

`PREDICT`는 다음 시스템에서 사용할 수 있습니다.

+ Windows 및 Linux 기반 SQL Server 2017 이상의 모든 버전
+ Azure SQL Managed Instance
+ Azure SQL Database
+ Azure SQL Edge
+ Azure Synapse Analytics

이 함수는 기본적으로 사용됩니다. R 또는 Python을 설치하거나 추가 기능을 사용하도록 설정할 필요는 없습니다.

## <a name="supported-models"></a>지원되는 모델

`PREDICT` 함수가 지원하는 모델 형식은 네이티브 채점을 실행하는 SQL 플랫폼에 따라 달라집니다. 다음 표를 참조하여 어떤 플랫폼에서 어떤 모델 형식을 지원하는지 확인하세요.

| 플랫폼 | ONNX 모델 형식 | RevoScale 모델 형식 |
|-|-|-|
| SQL Server | 예 | 예 |
| Azure SQL Managed Instance | yes | yes |
| Azure SQL Database | 예 | 예 |
| Azure SQL Edge | 예 | 예 |
| Azure Synapse Analytics | 예 | 예 |

::: moniker range="=azuresqldb-mi-current||=azure-sqldw-latest||=sqlallproducts-allversions"
### <a name="onnx-models"></a>ONNX 모델

이 모델은 [ONNX(Open Neural Network Exchange)](https://onnx.ai/get-started.html) 모델 형식이어야 합니다.
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current||=azuresqldb-current||=sqlallproducts-allversions"
### <a name="revoscale-models"></a>RevoScale 모델

이 모델은 [RevoScaleR](../r/ref-r-revoscaler.md) 또는 [revoscalepy](../python/ref-py-revoscalepy.md) 패키지를 사용하여 아래 나열된 지원되는 **rx** 알고리즘 중 하나로 미리 학습되어야 합니다.

R에는 [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)를, Python에는 [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)을 사용하여 모델을 직렬화합니다. 이러한 직렬화 함수는 빠른 채점을 지원하도록 최적화되었습니다.

<a name="bkmk_native_supported_algos"></a> 

#### <a name="supported-revoscale-algorithms"></a>지원되는 RevoScale 알고리즘

revoscalepy 및 RevoScaleR에서 지원되는 알고리즘은 다음과 같습니다.

+ revoscalepy 알고리즘

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) 
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) 
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) 
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) 

+ RevoScaleR 알고리즘

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

MicrosoftML 또는 microsoftml의 알고리즘을 사용해야 하는 경우 [sp_rxPredict를 사용한 실시간 채점](../predictions/real-time-scoring.md)을 사용합니다.

지원되지 않는 모델 유형은 다음과 같습니다.

+ 다른 변환이 포함된 모델
+ RevoScaleR의 `rxGlm` 또는 `rxNaiveBayes` 알고리즘 또는 revoscalepy의 동급 알고리즘을 사용하는 모델
+ PMML 모델
+ 다른 오픈 소스 또는 타사 라이브러리를 사용하여 만든 모델
::: moniker-end

## <a name="examples"></a>예제
::: moniker range="=azuresqldb-mi-current||=azure-sqldw-latest||=sqlallproducts-allversions"
### <a name="predict-with-an-onnx-model"></a>ONNX 모델을 사용하는 PREDICT

이 예제에서는 네이티브 채점을 위해 `dbo.models` 테이블에 저장된 ONNX 모델을 사용하는 방법을 보여 줍니다.

```sql
DECLARE @model VARBINARY(max) = (
        SELECT DATA
        FROM dbo.models
        WHERE id = 1
        );

WITH predict_input
AS (
    SELECT TOP (1000) [id]
        , CRIM
        , ZN
        , INDUS
        , CHAS
        , NOX
        , RM
        , AGE
        , DIS
        , RAD
        , TAX
        , PTRATIO
        , B
        , LSTAT
    FROM [dbo].[features]
    )
SELECT predict_input.id
    , p.variable1 AS MEDV
FROM PREDICT(MODEL = @model, DATA = predict_input, RUNTIME=ONNX) WITH (variable1 FLOAT) AS p;
```

> [!NOTE]
> **PREDICT**에서 반환된 열과 값은 모델 유형에 따라 다를 수 있으므로 **WITH** 절을 사용하여 반환된 데이터의 스키마를 정의해야 합니다.
::: moniker-end

::: moniker range=">=sql-server-2017||=azuresqldb-mi-current||>=sql-server-linux-2017||=sqlallproducts-allversions"
### <a name="predict-with-revoscale-model"></a>RevoScale 모델을 사용하는 PREDICT

이 예제에서는 R에서 **RevoScaleR**을 사용하여 모델을 만든 다음 T-SQL에서 실시간 예측 함수를 호출합니다.

#### <a name="step-1-prepare-and-save-the-model"></a>1단계. 모델 준비 및 저장

다음 코드를 실행하여 샘플 데이터베이스 및 필요한 테이블을 만듭니다.

```sql
CREATE DATABASE NativeScoringTest;
GO
USE NativeScoringTest;
GO
DROP TABLE IF EXISTS iris_rx_data;
GO
CREATE TABLE iris_rx_data (
    "Sepal.Length" float not null, "Sepal.Width" float not null
  , "Petal.Length" float not null, "Petal.Width" float not null
  , "Species" varchar(100) null
);
GO
```

다음 명령문을 사용하여 **아이리스** 데이터 세트의 데이터로 데이터 테이블을 채웁니다.

```sql
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

이제 모델을 저장하는 데 사용할 테이블을 만듭니다.

```sql
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

다음 코드는 **아이리스** 데이터 세트를 기반으로 하는 모델을 만들고 이를 **models**라는 테이블에 저장합니다.

```sql
DECLARE @model varbinary(max);
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'
    iris.sub <- c(sample(1:50, 25), sample(51:100, 25), sample(101:150, 25))
    iris.dtree <- rxDTree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data = iris[iris.sub, ])
    model <- rxSerializeModel(iris.dtree, realtimeScoringOnly = TRUE)
    '
  , @params = N'@model varbinary(max) OUTPUT'
  , @model = @model OUTPUT
  INSERT [dbo].[ml_models]([model_name], [model_version], [native_model_object])
  VALUES('iris.dtree','v1', @model) ;
```

> [!NOTE]
> RevoScaleR에서 [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) 함수를 사용하여 모델을 저장해야 합니다. 표준 R `serialize` 함수는 필요한 형식을 생성할 수 없습니다.

다음과 같은 문을 실행하여 이진 형식으로 저장된 모델을 볼 수 있습니다.

```sql
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

#### <a name="step-2-run-predict-on-the-model"></a>2단계. 모델에서 PREDICT 실행

다음은 **네이티브 채점** 함수를 사용하여 의사 결정 트리 모델에서 분류를 가져오는 간단한 PREDICT 문입니다. 사용자가 제공하는 특성, 꽃잎 길이, 너비를 기반으로 아이리스 종류를 예측합니다.

```sql
DECLARE @model varbinary(max) = (
  SELECT native_model_object
  FROM ml_models
  WHERE model_name = 'iris.dtree'
  AND model_version = 'v1');
SELECT d.*, p.*
  FROM PREDICT(MODEL = @model, DATA = dbo.iris_rx_data as d)
  WITH(setosa_Pred float, versicolor_Pred float, virginica_Pred float) as p;
go
```

"PREDICT 함수를 실행하는 동안 오류가 발생했습니다. 모델이 손상되었거나 잘못되었습니다"라는 오류가 표시된다면 일반적으로 쿼리가 모델을 반환하지 않았다는 의미입니다. 모델 이름을 올바르게 입력했는지, 아니면 모델 테이블이 비어 있는지 확인합니다.

> [!NOTE]
> **PREDICT**에서 반환된 열과 값은 모델 유형에 따라 다를 수 있으므로 **WITH** 절을 사용하여 반환된 데이터의 스키마를 정의해야 합니다.
::: moniker-end

## <a name="next-steps"></a>다음 단계

+ [PREDICT T-SQL 함수](../../t-sql/queries/predict-transact-sql.md)
+ [SQL Machine Learning 설명서](../index.yml)
+ [SQL Edge에서 ONNX를 통한 기계 학습 및 AI](/azure/azure-sql-edge/onnx-overview)
+ [Azure SQL Edge에서 ONNX 모델을 통한 배포 및 예측 수행](/azure/azure-sql-edge/deploy-onnx)
