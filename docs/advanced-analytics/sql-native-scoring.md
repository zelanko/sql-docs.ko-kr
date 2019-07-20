---
title: PREDICT T-sql 문을 사용한 네이티브 점수 매기기
description: 예측 T-sql 함수를 사용 하 여 예측을 생성 하 고, SQL Server에서 R 또는 Python으로 작성 된 미리 학습 된 모델에 대 한 dta 입력 점수를 계산 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: b148bd1ca51a7121ae043e2b616100e295c008aa
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344762"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>PREDICT T-sql 함수를 사용 하는 기본 점수 매기기
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

기본 점수 매기기에서는 [예측 t-sql 함수](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) 및 SQL Server 2017의 C++ 네이티브 확장 기능을 사용 하 여 새 데이터 입력에 대 한 예측 값 이나 *점수* 를 거의 실시간으로 생성 합니다. 이 방법론은 예측 및 예측 워크 로드의 가장 빠른 처리 속도를 제공 하지만 플랫폼 및 라이브러리 요구 사항과 함께 제공 됩니다. RevoScaleR 및 revoscalepy의 C++ 함수만 구현할 수 있습니다.

기본 점수 매기기를 사용 하려면 이미 학습 된 모델이 있어야 합니다. SQL Server 2017 Windows 또는 Linux 또는 Azure SQL Database에서는 Transact-sql에서 PREDICT 함수를 호출 하 여 입력 매개 변수로 제공 하는 새 데이터에 대해 네이티브 점수 매기기를 호출할 수 있습니다. PREDICT 함수는 사용자가 제공 하는 데이터 입력에 대 한 점수를 반환 합니다.

## <a name="how-native-scoring-works"></a>네이티브 점수 매기기 작동 방법

기본 점수 매기기는 C++ Microsoft의 네이티브 라이브러리를 사용 하 여 이미 학습 된 모델을 읽을 수 있으며, 이전에는 특수 이진 형식으로 저장 하거나 디스크에 원시 바이트 스트림으로 저장 하 고 사용자가 제공 하는 새 데이터 입력에 대 한 점수를 생성할 수 있습니다. 모델은 학습, 게시 및 저장 되므로 R 또는 Python 인터프리터를 호출 하지 않고도 점수 매기기에 사용할 수 있습니다. 이와 같이 여러 프로세스 상호 작용에 대 한 오버 헤드가 감소 하 여 엔터프라이즈 프로덕션 시나리오에서 훨씬 빠른 예측 성능을 생성 합니다.

네이티브 점수 매기기를 사용 하려면 PREDICT T-sql 함수를 호출 하 고 다음과 같은 필수 입력을 전달 합니다.

+ 지원 되는 알고리즘을 기반으로 하는 호환 모델입니다.
+ 입력 데이터-일반적으로 SQL 쿼리로 정의 됩니다.

함수는 입력 데이터에 대해 전달 하려는 원본 데이터의 열과 함께 예측을 반환 합니다.

## <a name="prerequisites"></a>사전 요구 사항

PREDICT는 SQL Server 2017 데이터베이스 엔진의 모든 버전에서 사용할 수 있으며 Windows의 SQL Server 2017 Machine Learning Services, SQL Server 2017 (Windows), SQL Server 2017 (Linux) 또는 Azure SQL Database를 비롯 하 여 기본적으로 사용 하도록 설정 되어 있습니다. R, Python을 설치 하거나 추가 기능을 사용 하도록 설정할 필요는 없습니다.

+ 모델은 아래에 나열 된 지원 되는 **rx** 알고리즘 중 하나를 사용 하 여 미리 학습 해야 합니다.

+ R에 [Rxserialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) 를 사용 하 고 Python에 [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) 를 사용 하 여 모델을 직렬화 합니다. 이러한 serialization 함수는 빠른 점수 매기기를 지원 하도록 최적화 되었습니다.

<a name="bkmk_native_supported_algos"></a> 

## <a name="supported-algorithms"></a>지원되는 알고리즘

+ revoscalepy 모델

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) 
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) 
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) 
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) 

+ RevoScaleR 모델

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

MicrosoftML 또는 MicrosoftML의 모델을 사용 해야 하는 경우 [sp_rxPredict에서 실시간 점수 매기기](real-time-scoring.md)를 사용 합니다.

지원 되지 않는 모델 형식에는 다음 유형이 포함 됩니다.

+ 다른 변환이 포함 된 모델
+ RevoScaleR 또는 revoscalepy `rxGlm` 와 `rxNaiveBayes` 동일한 또는 알고리즘을 사용 하는 모델
+ PMML 모델
+ 다른 오픈 소스 또는 타사 라이브러리를 사용 하 여 만든 모델

## <a name="example-predict-t-sql"></a>예: PREDICT (T-SQL)

이 예에서는 모델을 만든 다음 T-sql에서 실시간 예측 함수를 호출 합니다.

### <a name="step-1-prepare-and-save-the-model"></a>1단계. 모델 준비 및 저장

다음 코드를 실행 하 여 예제 데이터베이스 및 필요한 테이블을 만듭니다.

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

다음 문을 사용 하 여 데이터 테이블을 **iri** 데이터 집합의 데이터로 채웁니다.

```sql
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

이제 모델을 저장 하는 테이블을 만듭니다.

```sql
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

다음 코드에서는 **iri** 데이터 집합을 기반으로 모델을 만들고이를 **모델**이라는 테이블에 저장 합니다.

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
> RevoScaleR의 [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) 함수를 사용 하 여 모델을 저장 해야 합니다. 표준 R `serialize` 함수는 필요한 형식을 생성할 수 없습니다.

다음과 같은 문을 실행 하 여 이진 형식으로 저장 된 모델을 볼 수 있습니다.

```sql
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>2단계. 모델에 대해 PREDICT 실행

다음 단순 PREDICT 문은 **기본 점수 매기기** 함수를 사용 하 여 의사 결정 트리 모델에서 분류를 가져옵니다. 사용자가 제공 하는 특성을 기반으로 하는 조리개 종류 꽃잎 길이와 너비를 예측 합니다.

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

오류가 발생 하면 "함수 예측을 실행 하는 동안 오류가 발생 했습니다. 모델이 손상 되었거나 잘못 되었습니다. "라는 것은 일반적으로 쿼리가 모델을 반환 하지 않았음을 의미 합니다. 모델 이름을 올바르게 입력 했는지 확인 하거나 모델 테이블이 비어 있는지 확인 합니다.

> [!NOTE]
> **PREDICT** 에서 반환 된 열과 값은 모델 유형에 따라 다를 수 있으므로 **WITH** 절을 사용 하 여 반환 된 데이터의 스키마를 정의 해야 합니다.

## <a name="next-steps"></a>다음 단계

네이티브 점수 매기기를 포함 하는 전체 솔루션은 SQL Server 개발 팀에서 다음 샘플을 참조 하세요.

+ ML 스크립트를 배포 합니다. [Python 모델 사용](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ ML 스크립트를 배포 합니다. [R 모델 사용](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)