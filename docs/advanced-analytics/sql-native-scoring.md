---
title: 예측 T-SQL 문-SQL Server Machine Learning Services를 사용 하 여 네이티브 점수 매기기
description: SQL Server에서 R 또는 Python에서 작성 하는 미리 학습 된 모델에 대해 dta 입력 점수 매기기, 예측 T-SQL 함수를 사용 하 여 예측을 생성 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a14a4b188aa27acdef0bc836e939a7df0021e522
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645132"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>예측 T-SQL 함수를 사용 하 여 네이티브 점수 매기기
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

사용 하 여 점수 매기기 네이티브 [예측 T-SQL 함수](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) 및 예측 값을 생성 하려면 SQL Server 2017의 c + +는 네이티브 확장 기능 또는 *점수* 거의 실시간으로 새 데이터 입력에 대 한 합니다. 이 방법론 예측 및 예측 작업의 가장 가능한 처리 속도 제공 하지만 플랫폼과 라이브러리 요구 사항: RevoScaleR 및 revoscalepy 함수 c + + 구현이 합니다.

네이티브 점수 매기기 이미 학습 된 모델을가 있어야 합니다. SQL Server 2017 Windows 또는 Linux에서 또는 Azure SQL Database에서 호출할 수 있습니다 PREDICT 함수를 호출 하는 Transact sql에서 입력된 매개 변수로 제공 하는 새 데이터 점수를 매길 네이티브. PREDICT 함수는 제공 하는 데이터 입력에 대해 점수를 반환 합니다.

## <a name="how-native-scoring-works"></a>어떻게 네이티브 점수 매기기 작업

네이티브 점수 매기기는 네이티브 c + + 라이브러리를 이미 학습 된 모델을 읽을 수 있는 Microsoft 이전에 특수 이진 형식으로 저장 또는 원시 바이트 스트림, 디스크에 저장 하 고 사용자가 제공한 새 데이터 입력에 대 한 점수를 생성 합니다. 모델을 학습 하기 때문에 게시 및 저장을 사용할 수 R 또는 Python 인터프리터를 호출 하지 않고도 점수 매기기에 대 한 합니다. 이와 같이 여러 프로세스 상호 작용 하는 오버 헤드 감소, 엔터프라이즈 프로덕션 시나리오에서 예측 성능이 훨씬 더 빠릅니다.

네이티브 점수 매기기를 사용 하려면 예측 T-SQL 함수를 호출 하 고 다음 필요한 입력을 전달 합니다.

+ 호환 되는 지원 되는 알고리즘을 기반으로 합니다.
+ 일반적으로 SQL 쿼리로 정의 된 입력된 데이터입니다.

함수를 통해 전달 하려는 원본 데이터의 열과 함께 입력된 데이터에 대 한 예측을 반환 합니다.

## <a name="prerequisites"></a>사전 요구 사항

예측은 SQL Server 2017 데이터베이스 엔진의 모든 버전에서 사용할 수 있으며, 기본적으로 Windows, SQL Server 2017 (Windows), SQL Server 2017 (Linux) 또는 Azure SQL Database에서 SQL Server 2017 Machine Learning Services를 포함 하 여 사용 하도록 설정 합니다. R, Python, 설치 하거나 추가 기능을 활성화할 필요가 없습니다.

+ 사전에 지원 되는 중 하나를 사용 하 여 모델을 학습 해야 합니다 **rx** 아래에 나열 된 알고리즘입니다.

+ 사용 하 여 모델 serialize [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) R에 대 한 및 [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) Python에 대 한 합니다. 이러한 serialization 함수 빠른 점수 매기기를 지원 하도록 최적화 되었습니다.

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

MicrosoftML 또는 microsoftml에서 모델을 사용 하는 경우 사용할 [sp_rxPredict를 사용 하 여 실시간 점수 매기기](real-time-scoring.md)합니다.

지원 되지 않는 모델 유형은 다음과가 같습니다.

+ 다른 변환이 포함 된 모델
+ 사용 하 여 모델을 `rxGlm` 또는 `rxNaiveBayes` 에서 RevoScaleR 또는 revoscalepy 해당 하는 알고리즘
+ PMML 모델
+ 다른 오픈 소스 또는 타사 라이브러리를 사용 하 여 만든 모델

## <a name="example-predict-t-sql"></a>예: 예측 (T-SQL)

이 예제에서는 모델을 만들고 T-SQL에서 실시간 예측 함수를 호출 합니다.

### <a name="step-1-prepare-and-save-the-model"></a>1단계. 준비 및 모델 저장

샘플 데이터베이스 및 필요한 테이블을 만들려면 다음 코드를 실행 합니다.

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

데이터를 사용 하 여 데이터 테이블을 구성 하려면 다음 문을 사용 합니다 **아이리스** 데이터 집합입니다.

```sql
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

이제 모델을 저장 하는 것에 대 한 테이블을 만듭니다.

```sql
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

다음 코드를 기반으로 모델을 만듭니다는 **iris** 데이터 집합 이라는 테이블에 저장 **모델**합니다.

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
> 사용 해야 합니다 [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) 모델을 저장 하는 RevoScaleR 함수입니다. 표준 R `serialize` 함수에 필요한 형식을 생성할 수 없습니다.

이진 형식으로 저장 된 모델을 보려면 다음을과 같은 문은 실행할 수 있습니다.

```sql
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>2단계. 모델에 예측을 실행 합니다.

다음 간단한 예측 문을 사용 하 여 의사 결정 트리 모델에서 분류를 가져옵니다 합니다 **네이티브 점수 매기기** 함수입니다. 사용자가 제공한 특성, 꽃잎 길이 너비에 따라 붓 꽃 종류를 예측 합니다.

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

오류를 받게 되 면 "동안 오류가 발생 했습니다 PREDICT 함수를 실행 합니다. 모델이 손상 되었거나 잘못 된", 일반적으로 쿼리 모델을 반환 하지 않았습니다.을 의미 합니다. 모델 이름을 올바르게 입력 여부 또는 모델 테이블이 비어 있는지 확인 합니다.

> [!NOTE]
> 열 및 값을 반환 하므로 **PREDICT** 모델 유형별로 다를 수 있습니다 사용 하 여 반환된 된 데이터의 스키마를 정의 해야 합니다는 **WITH** 절.

## <a name="next-steps"></a>다음 단계

네이티브 점수 매기기를 포함 하는 완벽 한 솔루션, SQL Server 개발 팀에서 이러한 샘플을 참조 하세요.

+ 기계 학습 스크립트를 배포 합니다. [Python 모델을 사용 하 여](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ 기계 학습 스크립트를 배포 합니다. [R 모델을 사용 하 여](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)