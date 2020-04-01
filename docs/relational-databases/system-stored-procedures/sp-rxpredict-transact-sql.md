---
title: sp_rxPredict | 마이크로 소프트 문서
ms.date: 03/30/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- sp_rxPredict
- sp_rxPredict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_rxPredict procedure
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 752d9655096bc929ea9175577c7705dc58955652
ms.sourcegitcommit: 5c28603dd51d907544ebf8a50b678675d5414eaf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80471842"
---
# <a name="sp_rxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 데이터베이스의 이진 형식으로 저장된 기계 학습 모델로 구성된 지정된 입력에 대한 예측 값을 생성합니다.

R 및 파이썬 기계 학습 모델에 대한 점수를 거의 실시간으로 제공합니다. `sp_rxPredict`[RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) 및 [MicrosoftML의](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package) `rxPredict` R 함수에 대한 래퍼로 제공되는 저장 프로시저이며, [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) 및 [microsoftml에서](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) 파이썬 함수입니다. C++로 작성되었으며 점수 매기기 작업에 특별히 최적화되어 있습니다.

R 또는 Python을 사용하여 모델을 만들어야 하지만 대상 데이터베이스 엔진 인스턴스의 이진 형식으로 직렬화되고 저장되면 R 또는 Python 통합이 설치되지 않은 경우에도 해당 데이터베이스 엔진 인스턴스에서 사용할 수 있습니다. 자세한 내용은 sp_rxPredict 실시간 [채점을](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring)참조하십시오.

## <a name="syntax"></a>구문

```syntaxsql
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>인수

**model**

지원되는 형식의 미리 학습된 모델입니다. 

**input**

유효한 SQL 쿼리

### <a name="return-values"></a>반환 값

점수 열뿐만 아니라 입력 데이터 원본의 모든 통과 열이 반환됩니다.
알고리즘이 이러한 값의 생성을 지원하는 경우 신뢰 구간과 같은 추가 점수 열을 반환할 수 있습니다.

## <a name="remarks"></a>설명

저장 프로시저의 사용을 사용하려면 인스턴스에서 SQLCLR을 사용하도록 설정해야 합니다.

> [!NOTE]
> 이 옵션을 설명하는 데는 보안에 영향을 미칩니다. 서버에서 SQLCLR을 사용할 수 없는 경우 [거래-SQL PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql?view=sql-server-2017) 함수와 같은 대체 구현을 사용합니다.

사용자는 데이터베이스에 `EXECUTE` 대한 권한이 필요합니다.

### <a name="supported-algorithms"></a>지원되는 알고리즘

모델을 만들고 학습하려면 [SQL Server 2016 R 서비스,](https://docs.microsoft.com/sql/advanced-analytics/r/sql-server-r-services?view=sql-server-2017) [SQL Server 2016 R 서버(독립 실행형)](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone?view=sql-server-2016)또는 [SQL Server 2017 기계 학습 서비스(R 또는 파이썬)](../../advanced-analytics/what-is-sql-server-machine-learning.md?view=sql-server-2017)또는 [SQL Server 2017 서버(독립 실행형) (R 또는 파이썬)에서](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone?view=sql-server-2017)제공하는 R 또는 파이썬에 대한 지원되는 알고리즘 중 하나를 사용합니다.

#### <a name="r-revoscaler-models"></a>R: 반란 스케일R 모델

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree)
  + [rxd포레스트](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest)

#### <a name="r-microsoftml-models"></a>R: 마이크로소프트ML 모델

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rx패스트포레스트](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

#### <a name="r-transformations-supplied-by-microsoftml"></a>R: MicrosoftML에서 제공하는 변환

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

#### <a name="python-revoscalepy-models"></a>파이썬 : 반란 모델

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit)
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees)
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree)
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest)


#### <a name="python-microsoftml-models"></a>파이썬 : 마이크로 소프트 ml 모델

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

#### <a name="python-transformations-supplied-by-microsoftml"></a>파이썬 : 마이크로 소프트 ml에 의해 제공 된 변환

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)
  
### <a name="unsupported-model-types"></a>지원되지 않는 모델 형식

다음 모델 유형은 지원되지 않습니다.

+ RevoScaleR에서 `rxGlm` 또는 `rxNaiveBayes` 알고리즘을 사용하는 모델
+ R의 PMML 모델
+ 다른 타사 라이브러리를 사용하여 만든 모델 

## <a name="examples"></a>예

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
  @inputData = N'SELECT * FROM data';
```

유효한 SQL 쿼리이 될 뿐만 아니라 * \@inputData의* 입력 데이터에저장된 모델의 열과 호환되는 열이 포함되어야 합니다.

`sp_rxPredict`이중, 부동, 짧은, ushort, 긴, ulong 및 문자열 : 다음 .NET 열 유형만 지원합니다. 실시간 채점에 사용하기 전에 입력 데이터에서 지원되지 않는 형식을 필터링해야 할 수 있습니다. 

  해당하는 SQL 형식에 대한 자세한 내용은 [SQL-CLR 형식 매핑](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) 또는 [CLR 매개 변수 데이터 매핑](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)을 참조하세요.

