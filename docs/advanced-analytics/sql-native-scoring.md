---
title: T-SQL PREDICT를 사용하는 네이티브 채점
description: PREDICT T-SQL 함수를 사용하여 예측을 생성하고, SQL Server에서 R 또는 Python으로 작성된 미리 학습된 모델에 대한 dta 입력 점수를 계산합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 766adecbc91f88ed0796e4214b7e4074fc564f01
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727290"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>PREDICT T-SQL 함수를 사용하는 네이티브 채점
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

기본 채점에서는 [PREDICT T-SQL 함수](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) 및 SQL Server 2017의 네이티브 C++ 확장 기능을 사용하여 새 데이터 입력에 대한 예측 값이나 *점수*를 거의 실시간으로 생성할 수 있습니다. 이 방법론은 예측 워크로드에 가장 빠른 처리 속도를 제공하지만 플랫폼 및 라이브러리 요구 사항이 있습니다. RevoScaleR 및 revoscalepy의 함수에만 C++를 구현할 수 있습니다.

네이티브 채점을 사용하려면 이미 학습된 모델이 있어야 합니다. SQL Server 2017 Windows 또는 Linux나 Azure SQL Database에서는 Transact-SQL에서 PREDICT 함수를 호출하여 입력 매개 변수로 제공하는 새 데이터에 대해 네이티브 채점을 호출할 수 있습니다. PREDICT 함수는 사용자가 제공하는 데이터 입력에 대한 점수를 반환합니다.

## <a name="how-native-scoring-works"></a>네이티브 채점의 작동 방법

네이티브 채점은 이전에 특수한 이진 형식에 저장되었거나 디스크에 원시 바이트 스트림으로 저장된, 이미 학습된 모델을 읽을 수 있는 Microsoft의 네이티브 C++ 라이브러리를 사용하고 사용자가 제공하는 새 데이터 입력에 대한 점수를 생성할 수 있습니다. 모델은 학습, 게시 및 저장되므로 R 또는 Python 인터프리터를 호출할 필요 없이 채점에 사용할 수 있습니다. 따라서 여러 프로세스 상호 작용에 대한 부담이 감소하여 엔터프라이즈 프로덕션 시나리오에서 예측 성능이 훨씬 빨라집니다.

네이티브 채점을 사용하려면 PREDICT T-SQL 함수를 호출하고 다음과 같은 필수 입력을 전달합니다.

+ 지원되는 알고리즘을 기반으로 하는 호환 모델입니다.
+ 일반적으로 SQL 쿼리로 정의되는 입력 데이터입니다.

함수는 전달하려는 원본 데이터의 열과 함께 입력 데이터에 대한 예측을 반환합니다.

## <a name="prerequisites"></a>사전 요구 사항

PREDICT는 Windows의 SQL Server Machine Learning Services, SQL Server 2017(Windows), SQL Server 2017(Linux) 또는 Azure SQL Database를 비롯한 SQL Server 2017 데이터베이스 엔진의 모든 버전에서 사용할 수 있으며 기본적으로 사용하도록 설정되어 있습니다. R, Python을 설치하거나 추가 기능을 사용하도록 설정할 필요는 없습니다.

+ 아래에 나열된 지원 되는 **rx** 알고리즘 중 하나를 사용하여 모델을 미리 학습시켜야 합니다.

+ R에는 [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)를, Python에는 [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)을 사용하여 모델을 직렬화합니다. 이러한 직렬화 함수는 빠른 채점을 지원하도록 최적화되었습니다.

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

MicrosoftML 또는 microsoftml의 모델을 사용해야 하는 경우 [sp_rxPredict를 사용한 실시간 채점](real-time-scoring.md)을 사용합니다.

지원되지 않는 모델 유형은 다음과 같습니다.

+ 다른 변환이 포함된 모델
+ RevoScaleR의 `rxGlm` 또는 `rxNaiveBayes` 알고리즘 또는 revoscalepy의 동급 알고리즘을 사용하는 모델
+ PMML 모델
+ 다른 오픈 소스 또는 타사 라이브러리를 사용하여 만든 모델

## <a name="example-predict-t-sql"></a>예제: PREDICT(T-SQL)

이 예에서는 모델을 만든 다음, T-SQL에서 실시간 예측 함수를 호출합니다.

### <a name="step-1-prepare-and-save-the-model"></a>1단계. 모델 준비 및 저장

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

### <a name="step-2-run-predict-on-the-model"></a>2단계. 모델에서 PREDICT 실행

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

## <a name="next-steps"></a>다음 단계

네이티브 채점을 포함하는 전체 솔루션은 SQL Server 개발 팀의 다음 샘플을 참조하세요.

+ ML 스크립트를 배포합니다. [Python 모델 사용](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ ML 스크립트를 배포합니다. [R 모델 사용](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)