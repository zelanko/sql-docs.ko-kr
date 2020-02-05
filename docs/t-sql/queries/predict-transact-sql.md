---
title: PREDICT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2019
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
monikerRange: '>=sql-server-2017||=azuresqldb-current||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c97363e7f13c3b42cf447ecf69929171544f3a6b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "72907256"
---
# <a name="predict-transact-sql"></a>PREDICT(Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

저장된 모델을 기반으로 예측 값 또는 점수를 생성합니다. 자세한 내용은 [PREDICT T-SQL 함수를 사용하는 네이티브 채점](../../advanced-analytics/sql-native-scoring.md)을 참조하세요.

## <a name="syntax"></a>구문

```
PREDICT  
(  
  MODEL = @model | model_literal,  
  DATA = object AS <table_alias>  
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

### <a name="arguments"></a>인수

**model**

`MODEL` 매개 변수를 사용하여 점수 매기기 또는 예측에 사용되는 모델을 지정합니다. 모델은 변수 또는 리터럴 또는 스칼라 식으로 지정됩니다.

모델 개체는 R 또는 Python 또는 다른 도구에 의해 생성할 수 있습니다.

**data**

DATA 매개 변수를 사용하여 점수 매기기 또는 예측에 사용되는 데이터를 지정합니다. 데이터는 쿼리의 테이블 원본 형식으로 지정됩니다. 테이블 원본은 테이블, 테이블 별칭, CTE 별칭, 뷰 또는 테이블 반환 함수일 수 있습니다.

**parameters**

PARAMETERS 매개 변수를 사용하여 점수 매기기 또는 예측에 사용되는 선택적 사용자 정의 매개 변수를 지정합니다.

각 매개 변수의 이름은 모델 유형에 따라 다릅니다. 예를 들어 RevoScaleR의 [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) 함수는 물류 회귀 모델의 점수를 매길 때 나머지를 계산해야 하는지 여부를 나타내는 `@computeResiduals` 매개 변수를 지원합니다. 호환되는 모델을 호출하는 경우 `PREDICT` 함수에 해당 매개 변수 이름 및 TRUE 또는 FALSE를 전달할 수 있습니다.

**WITH ( <result_set_definition> )**

WITH 절을 사용하여 `PREDICT` 함수에서 반환되는 출력의 스키마를 지정합니다.

`PREDICT` 함수 자체에서 반환되는 열뿐만 아니라 데이터 입력의 일부인 모든 열도 쿼리에 사용할 수 있습니다.

### <a name="return-values"></a>반환 값

미리 정의된 스키마는 사용할 수 없으며, SQL Server는 모델 콘텐츠의 유효성을 검사하지 않고 반환된 열 값의 유효성도 검사하지 않습니다.

- `PREDICT` 함수는 열을 입력으로 전달합니다.
- 또한 `PREDICT` 함수는 새 열을 생성하지만 열 개수와 해당 데이터 형식은 예측에 사용되는 모델의 유형에 따라 달라집니다.

데이터, 모델 또는 열 형식과 관련된 오류 메시지는 모델과 연결된 기본 예측 함수에 의해 반환됩니다.

- RevoScaleR의 경우 동일한 함수는 [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)입니다.  
- MicrosoftML의 동일한 함수는 [rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict)입니다.  

`PREDICT`를 사용하여 내부 모델 구조를 볼 수 없습니다. 모델 자체의 콘텐츠를 이해하려면 모델 개체를 로드하고 역직렬화하고 해당 R 코드를 사용하여 모델을 구문 분석해야 합니다.

## <a name="remarks"></a>설명

`PREDICT` 함수는 SQL Server 2017 이상 모든 버전 및 Windows와 Linux에서 지원됩니다. `PREDICT`는 클라우드의 Azure SQL Database에서도 지원됩니다. 이러한 모든 지원은 다른 컴퓨터 학습 기능이 사용 가능한지 여부와 관계없이 활성화됩니다.

`PREDICT` 함수를 사용하기 위해 R, Python 또는 다른 기계 학습 언어를 서버에 설치할 필요는 없습니다. 모델을 다른 환경에서 학습하고 `PREDICT`와 함께 사용하기 위해 SQL Server 테이블에 저장하거나 저장된 모델을 가진 SQL Server의 다른 인스턴스에서 모델을 호출할 수 있습니다.

### <a name="supported-algorithms"></a>지원되는 알고리즘

사용하는 알고리즘은 RevoScaleR 패키지에서 지원되는 알고리즘 중 하나를 사용하여 만들어졌어야 합니다. 현재 지원되는 모델의 목록은 [실시간 점수 매기기](../../advanced-analytics/real-time-scoring.md)를 참조하세요.

### <a name="permissions"></a>사용 권한

`PREDICT`를 위해 권한은 필요 없지만, 사용자는 데이터베이스에 대한 `EXECUTE` 권한 및 입력으로 사용하는 데이터를 쿼리하는 권한이 필요합니다. 또한 모델이 테이블에 저장된 경우 사용자는 테이블에서 모델을 읽을 수 있어야 합니다.

## <a name="examples"></a>예

다음 예제에서는 `PREDICT`를 호출하는 구문을 보여 줍니다.

### <a name="using-predict-in-a-from-clause"></a>FROM 절에 PREDICT 사용

이 예제는 `PREDICT` 문의 `FROM`절에서 `SELECT` 함수를 참조합니다.

```sql
SELECT d.*, p.Score
FROM PREDICT(MODEL = @logit_model, 
  DATA = dbo.mytable AS d) WITH (Score float) AS p;
```

**매개 변수에서 테이블 원본에 대해 지정된 별칭**d`DATA`를 사용하여 dbo.mytable에 속한 열을 참조합니다. **PREDICT** 함수에 대해 지정된 별칭 **p**를 사용하여 PREDICT 함수에서 반환된 열을 참조합니다.

### <a name="combining-predict-with-an-insert-statement"></a>INSERT 문과 PREDICT 결합

예측에 대한 일반적인 사용 사례 중 하나는 입력 데이터에 대한 점수를 생성한 다음, 예측된 값을 테이블에 삽입하는 것입니다. 다음 예제에서는 호출 애플리케이션이 저장 프로시저를 사용하여 예측 값이 포함된 행을 테이블에 삽입하는 것으로 가정합니다.

```sql
CREATE PROCEDURE InsertLoanApplication
(@p1 varchar(100), @p2 varchar(200), @p3 money, @p4 int)
AS
BEGIN
  DECLARE @model varbinary(max) = (select model
  FROM scoring_model
  WHERE model_name = 'ScoringModelV1');
  WITH d as ( SELECT * FROM (values(@p1, @p2, @p3, @p4)) as t(c1, c2, c3, c4) )

  INSERT INTO loan_applications (c1, c2, c3, c4, score)
  SELECT d.c1, d.c2, d.c3, d.c4, p.score
  FROM PREDICT(MODEL = @model, DATA = d) WITH(score float) as p;
END;
```

프로시저에서 테이블 반환 매개 변수를 통해 여러 행을 가져온 다음, 다음과 같이 기록할 수 있습니다.

```sql
CREATE PROCEDURE InsertLoanApplications (@new_applications dbo.loan_application_type)
AS
BEGIN
  DECLARE @model varbinary(max) = (SELECT model_bin FROM scoring_models WHERE model_name = 'ScoringModelV1');
  INSERT INTO loan_applications (c1, c2, c3, c4, score)
  SELECT d.c1, d.c2, d.c3, d.c4, p.score
  FROM PREDICT(MODEL = @model, DATA = @new_applications as d)
  WITH (score float) as p;
END;
```

### <a name="creating-an-r-model-and-generating-scores-using-optional-model-parameters"></a>R 모델을 만들고 선택적 모델 매개 변수를 사용하여 점수를 생성

이 예제에서는 이와 같은 RevoScaleR 호출을 사용하여 공변성 행렬(covariance matrix)에 맞는 물류 회귀 모델을 만들었다고 가정합니다.

```R
logitObj <- rxLogit(Kyphosis ~ Age + Start + Number, data = kyphosis, covCoef = TRUE)
```

모델을 이진 형식으로 SQL Server에 저장한 경우, PREDICT 함수를 사용하여 예측뿐만 아니라 모델 유형에서 지원되는 추가 정보(예: 오류 또는 신뢰 구간)도 생성할 수 있습니다.

다음 코드는 R에서의 동일한 [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) 호출을 보여 줍니다.

```R
rxPredict(logitObj, data = new_kyphosis_data, computeStdErr = TRUE, interval = "confidence")
```

`PREDICT` 함수를 사용하는 동일한 호출은 점수(예측 값), 오류 및 신뢰 구간도 제공합니다.

```sql
SELECT d.Age, d.Start, d.Number, p.pred AS Kyphosis_Pred, p.stdErr, p.pred_lower, p.pred_higher
FROM PREDICT( MODEL = @logitObj,  DATA = new_kyphosis_data AS d,
  PARAMETERS = N'computeStdErr bit, interval varchar(30)',
  computeStdErr = 1, interval = 'confidence')
WITH (pred float, stdErr float, pred_lower float, pred_higher float) AS p;
```

## <a name="next-steps"></a>다음 단계

- [PREDICT T-SQL 함수를 사용하는 네이티브 채점](../../advanced-analytics/sql-native-scoring.md)
