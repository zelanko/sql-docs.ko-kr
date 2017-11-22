---
title: "예측 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PREDICT
- PREDICT_TSQL
dev_langs: TSQL
helpviewer_keywords: PREDICT clause
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 8cc0e51a83b4c024a25caf2fe6501438a3ef8a18
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="predict-transact-sql"></a>예측 (Transact SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

예측된 된 값 또는 저장 된 모델을 기반으로 하는 점수를 생성 합니다.  

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

**모델**

`MODEL` 점수 매기기 이나 예측에 사용 되는 모델을 지정 하려면 매개 변수를 사용 합니다. 모델은 변수 또는 리터럴 또는 스칼라 식으로 지정 됩니다.

R 또는 Python 또는 다른 도구를 사용 하 여 모델 개체를 만들 수 있습니다.

**데이터**

DATA 매개 변수는 점수 매기기 이나 예측에 사용 되는 데이터를 지정 하는 데 사용 됩니다. 데이터 형식 쿼리에서 테이블 원본으로 지정 됩니다. 테이블, 테이블 별칭, CTE 별칭, 뷰 또는 테이블 반환 함수 테이블 원본 될 수 있습니다.

**매개 변수**

매개 변수가 매개 변수는 선택적 사용자 정의 매개 변수 예측 점수 매기기에 사용 되는 지정 하는 데 사용 됩니다.

각 매개 변수의 이름은 모델 유형에 따라 다릅니다. RevoScaleR의 rxPredict 함수는 매개 변수를 지원 하는 예를 들어  _@computeResiduals 비트_ 로지스틱 회귀 모델의 점수를 매길 때 잉여의 계산을 지원 하도록 합니다. 매개 변수 이름과 값을 전달할 수는 `PREDICT` 함수입니다.

> [참고] 이 옵션의 SQL Server 2017 시험판 버전에서 지원 되지 않습니다 되며 정방향 호환성 목적 으로만 포함 합니다.

**와 ( \<result_set_definition >)**

WITH 절은에서 반환 되는 출력의 스키마를 지정 하는 데 사용 되는 `PREDICT` 함수입니다.

반환 된 열과 함께 `PREDICT` 함수 자체는 데이터의 일부인 모든 열은 쿼리에서 사용 하기 위해 사용할 수 있는 입력 합니다.

### <a name="return-values"></a>반환 값

미리 정의 된 스키마를 사용할 수 있습니다. SQL Server는 모델의 콘텐츠 유효성이 확인 되지 않습니다 및 반환 된 열 값의 유효성을 검사 하지 않습니다.  
- `PREDICT` 입력으로 열을 통해 함수에 전달  
- `PREDICT` 함수에도 새 열을 생성 하지만 열과 해당 데이터 형식이 수 예측에 사용 된 모델의 유형에 따라 다릅니다.  

모든 오류 메시지는 데이터와 관련 된, 모델 또는 열 형식 모델에 연결 된 기본 예측 함수에 의해 반환 됩니다.  
- RevoScaleR을 해당 하는 경우 함수는 [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict)  
- MicrosoftML, 해당 하는 경우 함수는 [rxPredict.mlModel](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxpredict)  

사용 하 여 내부 모델 구조를 볼 수 없으면 `PREDICT`합니다. 모델 자체의 내용을 이해 하려면 모델 개체를 로드 해야, 역직렬화 하는 것을 및 적절 한 R 코드를 사용 하 여 모델을 구문 분석 합니다.

## <a name="remarks"></a>주의

`PREDICT` 함수는 SQL Server, Linux 등의 모든 버전에서 지원 됩니다.

R, Python 또는 언어를 학습 하는 다른 컴퓨터를 사용 하도록 서버에 설치할 필요는 없습니다는 `PREDICT` 함수입니다. 다른 환경에서 모델을 학습 하 고 사용 하도록 SQL Server 테이블에 저장할 수 `PREDICT`, 하거나 저장 된 모델에 있는 SQL Server의 다른 인스턴스에서 모델을 호출 합니다.

### <a name="supported-algorithms"></a>지원 되는 알고리즘

사용 하는 모델 만들어야 RevoScaleR 패키지에서 지원 되는 알고리즘 중 하나를 사용 합니다. 목록이 현재 지원 되는 모델에 대 한 참조 [실시간 점수 매기기](../../advanced-analytics/real-time-scoring.md)합니다.

### <a name="permissions"></a>Permissions

에 대 한 필요한 권한은 없습니다 `PREDICT`있지만 사용자 요구 `EXECUTE` 는 데이터베이스에 대 한 권한 및 입력으로 사용 되는 모든 데이터를 쿼리할 수 있는 권한이 있습니다. 모델 테이블에 저장 되어 있는 경우에 사용자를 모델 테이블에서 읽을 수 여야 합니다.

## <a name="examples"></a>예

다음 예에서는 호출에 대 한 구문을 보여 주는 `PREDICT`합니다.

### <a name="call-a-stored-model-and-use-it-for-prediction"></a>저장 된 모델을 호출 하 고 예측에 사용

이 예제에서는 [models_table] 테이블에 저장 된 기존 로지스틱 회귀 모델을 호출 합니다. 최신 학습된 된 모델을 SELECT 문을 사용 하 여를 가져오고 이진 모델 PREDICT 함수에 전달 합니다. 입력된 값이 나타내는 기능 출력 모델에 의해 할당 된 분류를 나타냅니다.

```sql
DECLARE @logit_model varbinary(max) = "SELECT TOP 1 @model from [models_table]";
DECLARE @input_qry = "SELECT ID, [Gender], [Income] from NewCustomers";

SELECT PREDICT [class]
FROM PREDICT( MODEL = @logit_model,  DATA = @input_qry
WITH (class string);
```

### <a name="using-predict-in-a-from-clause"></a>FROM 절에서 예측을 사용 하 여

이 예제에서는 참조는 `PREDICT` 함수는 `FROM` 절은 `SELECT` 문:

```sql
SELECT d.*, p.Score
FROM PREDICT(MODEL = @logit_model, 
  DATA = dbo.mytable AS d) WITH (Score float) AS p;
```

별칭 **d** 테이블 원본에 대해 지정 된 된 _데이터_ dbo.mytable에 속하는 열을 참조 하도록 매개 변수를 사용 합니다. 별칭 **p** 에 대해 지정 된 된 **PREDICT** 함수는 예측 함수에 의해 반환 되는 열을 참조할 때 사용 됩니다.

### <a name="combining-predict-with-an-insert-statement"></a>INSERT 문을 사용 하 여 예측을 결합

입력된 데이터에 대 한 점수를 생성 한 다음 테이블에 예측된 값을 삽입 하는 예측에 대 한 일반적인 사용 사례 중 하나입니다. 다음 예제에서는 호출 응용 프로그램이 저장된 프로시저를 사용 하 여 테이블에 예측 된 값이 포함 된 행을 삽입 하려면 가정 합니다.

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

프로시저에서 사용 하는 테이블 반환 매개 변수를 통해 여러 행 하는 경우 다음 그 수 있습니다. 다음과 같이 작성할 수 있습니다:

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

### <a name="creating-an-r-model-and-generating-scores-using-optional-model-parameters"></a>R 모델 만들기 및 선택적 모델 매개 변수를 사용 하 여 점수를 생성 합니다.

> [!NOTE]
> 매개 변수 인수를 사용 Release Candidate 1에서 지원 되지 않습니다.

이 예에서는 만들었다고 공 분산 행렬 적합 로지스틱 회귀 모델은 이와 같은 RevoScaleR 호출 하 여 가정 합니다.

```R
logitObj <- rxLogit(Kyphosis ~ Age + Start + Number, data = kyphosis, covCoef = TRUE)
```

이진 형식에 있는 SQL Server에서 모델을 저장 하는 경우 예측을 뿐 아니라 오류 또는 신뢰도 간격 같은 모델 유형별로 지원 되는 추가 정보를 생성 하는 예측 함수를 사용할 수 있습니다.

다음 코드 rxPredict R에서 해당 호출을 보여 줍니다.

```R
rxPredict(logitObj, data = new_kyphosis_data, computeStdErr = TRUE, interval = "confidence")
```

사용 하 여 해당 호출에서 `PREDICT` 함수 또한 점수를 제공 (예측 값), 오류 및 신뢰도 간격:

```sql
SELECT d.Age, d.Start, d.Number, p.pred AS Kyphosis_Pred, p.stdErr, p.pred_lower, p.pred_higher
FROM PREDICT( MODEL = @logitObj,  DATA = new_kyphosis_data AS d,
  PARAMETERS = N'computeStdErr bit, interval varchar(30)',
  computeStdErr = 1, interval = 'confidence')
WITH (pred float, stdErr float, pred_lower float, pred_higher float) AS p;
```


