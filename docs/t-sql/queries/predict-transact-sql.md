---
description: PREDICT(Transact-SQL)
title: PREDICT(Transact-SQL)
titleSuffix: SQL machine learning
ms.custom: ''
ms.date: 06/26/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- PREDICT
- PREDICT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PREDICT clause
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=azuresqldb-mi-current||>=azure-sqldw-latest'
ms.openlocfilehash: 83205b4a11be46888f8c7da8f29c84494d012740
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460856"
---
# <a name="predict-transact-sql"></a>PREDICT(Transact-SQL)

[!INCLUDE [sqlserver2017-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2017-asdb-asdbmi-asa.md)]

저장된 모델을 기반으로 예측 값 또는 점수를 생성합니다. 자세한 내용은 [PREDICT T-SQL 함수를 사용하는 네이티브 채점](../../machine-learning/predictions/native-scoring-predict-transact-sql.md)을 참조하세요.

## <a name="syntax"></a>구문

::: moniker range=">=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=azuresqldb-mi-current"

```syntaxsql
PREDICT  
(  
  MODEL = @model | model_literal,  
  DATA = object AS <table_alias>
  [, RUNTIME = ONNX ]
)  
WITH ( <result_set_definition> )  

<result_set_definition> ::=  
  {  
    { column_name  
      data_type  
      [ COLLATE collation_name ]  
      [ NULL | NOT NULL ]  
    }  
      [,...n ]  
  }  

MODEL = @model | model_literal  
```

::: moniker-end

::: moniker range=">=azure-sqldw-latest"

```syntaxsql
PREDICT  
(  
  MODEL = <model_object>,
  DATA = object AS <table_alias>
  [, RUNTIME = ONNX ]
)  
WITH ( <result_set_definition> )  

<result_set_definition> ::=  
  {  
    { column_name  
      data_type  
      [ COLLATE collation_name ]  
      [ NULL | NOT NULL ]  
    }  
      [,...n ]  
  }  

<model_object> ::=
  {
    model_literal
    | model_variable
    | ( scalar_subquery )
  }
```

::: moniker-end

### <a name="arguments"></a>인수

**MODEL**

::: moniker range=">=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017"
`MODEL` 매개 변수를 사용하여 점수 매기기 또는 예측에 사용되는 모델을 지정합니다. 모델은 변수 또는 리터럴 또는 스칼라 식으로 지정됩니다.

`PREDICT`는 [RevoScaleR](../../machine-learning/r/ref-r-revoscaler.md) 및 [revoscalepy](../../machine-learning/python/ref-py-revoscalepy.md) 패키지를 사용하여 학습된 모델을 지원합니다.
::: moniker-end

::: moniker range="=azuresqldb-mi-current"
`MODEL` 매개 변수를 사용하여 점수 매기기 또는 예측에 사용되는 모델을 지정합니다. 모델은 변수 또는 리터럴 또는 스칼라 식으로 지정됩니다.

Azure SQL Managed Instance에서 `PREDICT`는 [ONNX(Open Neural Network Exchange)](https://onnx.ai/get-started.html) 형식의 모델 또는 [RevoScaleR](../../machine-learning/r/ref-r-revoscaler.md) 및 [revoscalepy](../../machine-learning/python/ref-py-revoscalepy.md) 패키지를 사용하여 학습된 모델을 지원합니다.
::: moniker-end

::: moniker range=">=azure-sqldw-latest"
`MODEL` 매개 변수를 사용하여 점수 매기기 또는 예측에 사용되는 모델을 지정합니다. 모델은 변수 또는 리터럴 또는 스칼라 식 또는 스칼라 하위 쿼리로 지정됩니다.

Azure Synapse Analytics에서 `PREDICT`는 [ONNX(Open Neural Network Exchange)](https://onnx.ai/get-started.html) 형식의 모델을 지원합니다.
::: moniker-end

**데이터**

DATA 매개 변수를 사용하여 점수 매기기 또는 예측에 사용되는 데이터를 지정합니다. 데이터는 쿼리의 테이블 원본 형식으로 지정됩니다. 테이블 원본은 테이블, 테이블 별칭, CTE 별칭, 뷰 또는 테이블 반환 함수일 수 있습니다.

**RUNTIME = ONNX**

> [!IMPORTANT]
> `RUNTIME = ONNX` 인수는 [Azure SQL Managed Instance](/azure/azure-sql/managed-instance/machine-learning-services-overview), [Azure SQL Edge](/azure/sql-database-edge/onnx-overview) 및 [Azure Synapse Analytics](/azure/synapse-analytics/overview-what-is)에서만 사용할 수 있습니다.

모델 실행에 사용되는 기계 학습 엔진을 나타냅니다. `RUNTIME` 매개 변수 값은 항상 `ONNX`입니다. 이 매개 변수는 Azure SQL Edge 및 Azure Synapse Analytics에 필요합니다. Azure SQL Managed Instance에서 이 매개 변수는 선택 사항이며 ONNX 모델을 사용할 때만 사용됩니다.

**WITH ( <result_set_definition> )**

WITH 절을 사용하여 `PREDICT` 함수에서 반환되는 출력의 스키마를 지정합니다.

`PREDICT` 함수 자체에서 반환되는 열뿐만 아니라 데이터 입력의 일부인 모든 열도 쿼리에 사용할 수 있습니다.

### <a name="return-values"></a>반환 값

미리 정의된 스키마를 사용할 수 없습니다. 모델 내용의 유효성이 검사되지 않고 반환된 열 값도 유효성이 검사되지 않습니다.

- `PREDICT` 함수는 열을 입력으로 전달합니다.
- 또한 `PREDICT` 함수는 새 열을 생성하지만 열 개수와 해당 데이터 형식은 예측에 사용되는 모델의 유형에 따라 달라집니다.

데이터, 모델 또는 열 형식과 관련된 오류 메시지는 모델과 연결된 기본 예측 함수에 의해 반환됩니다.

::: moniker range=">=sql-server-2017||>=sql-server-linux-2017"
## <a name="remarks"></a>설명

`PREDICT` 함수는 SQL Server 2017 이상 모든 버전 및 Windows와 Linux에서 지원됩니다. `PREDICT`를 사용하기 위해 [Machine Learning Services](../../machine-learning/sql-server-machine-learning-services.md)를 사용하도록 설정할 필요는 없습니다.
::: moniker-end

### <a name="supported-algorithms"></a>지원되는 알고리즘

::: moniker range=">=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017"
사용하는 모델은 [RevoScaleR](../../machine-learning/r/ref-r-revoscaler.md) 또는 [revoscalepy](../../machine-learning/python/ref-py-revoscalepy.md) 패키지에서 지원되는 알고리즘 중 하나를 사용하여 만들어졌어야 합니다. 현재 지원되는 모델의 목록은 [PREDICT T-SQL 함수를 사용하는 네이티브 채점](../../machine-learning/predictions/native-scoring-predict-transact-sql.md)을 참조하세요.
::: moniker-end
::: moniker range="=azure-sqldw-latest"
[ONNX](https://onnx.ai/) 모델 형식으로 변환할 수 있는 알고리즘이 지원됩니다.
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
[ONNX](https://onnx.ai/) 모델 형식 및 [RevoScaleR](../../machine-learning/r/ref-r-revoscaler.md) 또는 [revoscalepy](../../machine-learning/python/ref-py-revoscalepy.md) 패키지에서 지원되는 알고리즘 중 하나를 사용하여 만든 모델로 변환할 수 있는 알고리즘이 지원됩니다. RevoScaleR 및 revoscalepy에서 현재 지원되는 알고리즘의 목록은 [PREDICT T-SQL 함수를 사용하는 네이티브 채점](../../machine-learning/predictions/native-scoring-predict-transact-sql.md)을 참조하세요.
::: moniker-end

### <a name="permissions"></a>사용 권한

`PREDICT`를 위해 권한은 필요 없지만, 사용자는 데이터베이스에 대한 `EXECUTE` 권한 및 입력으로 사용하는 데이터를 쿼리하는 권한이 필요합니다. 또한 모델이 테이블에 저장된 경우 사용자는 테이블에서 모델을 읽을 수 있어야 합니다.

## <a name="examples"></a>예제

다음 예제에서는 `PREDICT`를 호출하는 구문을 보여 줍니다.

### <a name="using-predict-in-a-from-clause"></a>FROM 절에 PREDICT 사용

이 예제는 `SELECT` 문의 `FROM`절에서 `PREDICT` 함수를 참조합니다.

::: moniker range=">=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=azuresqldb-mi-current"

```sql
SELECT d.*, p.Score
FROM PREDICT(MODEL = @model,
    DATA = dbo.mytable AS d) WITH (Score FLOAT) AS p;
```

:::moniker-end

::: moniker range=">=azure-sqldw-latest"

```sql
DECLARE @model VARBINARY(max) = (SELECT test_model FROM scoring_model WHERE model_id = 1);

SELECT d.*, p.Score
FROM PREDICT(MODEL = @model,
    DATA = dbo.mytable AS d, RUNTIME = ONNX) WITH (Score FLOAT) AS p;
```

::: moniker-end

`DATA` 매개 변수에서 테이블 원본에 대해 지정된 별칭 **d** 는 `dbo.mytable`에 속하는 열을 참조하는 데 사용됩니다. `PREDICT` 함수에 대해 지정된 별칭 **p** 는 `PREDICT` 함수에서 반환한 열을 참조하는 데 사용됩니다.

- 모델은 테이블 호출 **모델** 에서 `varbinary(max)` 열로 저장됩니다. **ID** 및 **설명** 같은 추가 정보가 테이블에 저장되어 모델을 식별합니다.
- `DATA` 매개 변수에서 테이블 원본에 대해 지정된 별칭 **d** 는 `dbo.mytable`에 속하는 열을 참조하는 데 사용됩니다. 입력 데이터 열 이름은 모델의 입력 이름과 일치해야 합니다.
- `PREDICT` 함수에 대해 지정된 별칭 **p** 는 `PREDICT` 함수에서 반환한 예측 열을 참조하는 데 사용됩니다. 열 이름에는 모델의 출력 이름과 같은 이름을 지정해야 합니다.
- 모든 입력 데이터 열 및 예측 열은 SELECT 문에 표시될 수 있습니다.

::: moniker range=">=azure-sqldw-latest"

위의 예제 쿼리에서 `MODEL`을 스칼라 하위 쿼리로 지정하여 보기를 만들 수 있습니다.

```sql
CREATE VIEW predictions
AS
SELECT d.*, p.Score
FROM PREDICT(MODEL = (SELECT test_model FROM scoring_model WHERE model_id = 1),
             DATA = dbo.mytable AS d, RUNTIME = ONNX) WITH (Score FLOAT) AS p;
```

:::moniker-end

### <a name="combining-predict-with-an-insert-statement"></a>INSERT 문과 PREDICT 결합

예측에 대한 일반적인 사용 사례는 입력 데이터에 대한 점수를 생성한 다음, 예측된 값을 테이블에 삽입하는 것입니다. 다음 예제에서는 호출 애플리케이션이 저장 프로시저를 사용하여 예측 값이 포함된 행을 테이블에 삽입하는 것으로 가정합니다.

::: moniker range=">=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=azuresqldb-mi-current"

```sql
DECLARE @model VARBINARY(max) = (SELECT model FROM scoring_model WHERE model_name = 'ScoringModelV1');

INSERT INTO loan_applications (c1, c2, c3, c4, score)
SELECT d.c1, d.c2, d.c3, d.c4, p.score
FROM PREDICT(MODEL = @model, DATA = dbo.mytable AS d) WITH(score FLOAT) AS p;
```

:::moniker-end

::: moniker range=">=azure-sqldw-latest"

```sql
DECLARE @model VARBINARY(max) = (SELECT model FROM scoring_model WHERE model_name = 'ScoringModelV1');

INSERT INTO loan_applications (c1, c2, c3, c4, score)
SELECT d.c1, d.c2, d.c3, d.c4, p.score
FROM PREDICT(MODEL = @model, DATA = dbo.mytable AS d, RUNTIME = ONNX) WITH(score FLOAT) AS p;
```

:::moniker-end

- `PREDICT`의 결과는 PredictionResults라는 테이블에 저장됩니다. 
- 모델은 테이블 호출 **모델** 에서 `varbinary(max)` 열로 저장됩니다. ID 및 설명과 같은 추가 정보를 테이블에 저장하여 모델을 식별할 수 있습니다.
- `DATA` 매개 변수에서 테이블 원본에 대해 지정된 별칭 **d** 는 `dbo.mytable`의 열을 참조하는 데 사용됩니다. 입력 데이터 열 이름은 모델의 입력 이름과 일치해야 합니다.
- `PREDICT` 함수에 대해 지정된 별칭 **p** 는 `PREDICT` 함수에서 반환한 예측 열을 참조하는 데 사용됩니다. 열 이름에는 모델의 출력 이름과 같은 이름을 지정해야 합니다.
- 모든 입력 열 및 예측 열은 SELECT 문에 표시될 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [PREDICT T-SQL 함수를 사용하는 네이티브 채점](../../machine-learning/predictions/native-scoring-predict-transact-sql.md)
::: moniker range="=azure-sqldw-latest||=azuresqldb-mi-current"
-   [ONNX 모델에 대한 자세한 정보](/azure/machine-learning/concept-onnx#get-onnx-models)
::: moniker-end
