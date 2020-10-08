---
title: sp_rxPredict | Microsoft Docs
ms.date: 03/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning-services
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
ms.openlocfilehash: 625157885fa4494f4d8c70da5bea8ac70472d3b5
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809487"
---
# <a name="sp_rxpredict"></a>sp_rxPredict  
[!INCLUDE [SQL Server 2016 Windows only](../../includes/applies-to-version/sqlserver2016-windows-only.md)]

SQL Server 데이터베이스에서 이진 형식으로 저장 된 기계 학습 모델로 구성 된 지정 된 입력에 대 한 예측 값을 생성 합니다.

R 및 Python 기계 학습 모델에 대 한 점수를 거의 실시간으로 제공 합니다. `sp_rxPredict`은 `rxPredict` [RevoScaleR](/r-server/r-reference/revoscaler/revoscaler) 및 [MicrosoftML](/r-server/r-reference/microsoftml/microsoftml-package)에서 R 함수의 래퍼로 제공 되는 저장 프로시저로, [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) 및 [MicrosoftML](/machine-learning-server/python-reference/microsoftml/microsoftml-package)에서 Python 함수를 [rx_predict](/machine-learning-server/python-reference/revoscalepy/rx-predict) 합니다. 이는 c + +로 작성 되었으며 점수 매기기 작업을 위해 특별히 최적화 되어 있습니다.

모델은 R 또는 Python을 사용 하 여 만들어야 하지만, 대상 데이터베이스 엔진 인스턴스에서 이진 형식으로 직렬화 되 고 저장 된 후에는 R 또는 Python 통합이 설치 되지 않은 경우에도 해당 데이터베이스 엔진 인스턴스에서 사용 될 수 있습니다. 자세한 내용은 [sp_rxPredict를 사용한 실시간 점수 매기기](../../machine-learning/predictions/real-time-scoring.md)를 참조 하세요.

## <a name="syntax"></a>구문

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>인수

**model**

지원 되는 형식으로 사전 학습 된 모델 

**input**

유효한 SQL 쿼리

### <a name="return-values"></a>반환 값

점수 열이 반환 되 고 입력 데이터 원본의 통과 열도 반환 됩니다.
알고리즘이 이러한 값의 생성을 지 원하는 경우 신뢰 간격과 같은 추가 점수 열이 반환 될 수 있습니다.

## <a name="remarks"></a>설명

저장 프로시저를 사용 하려면 인스턴스에서 SQLCLR을 사용 하도록 설정 해야 합니다.

> [!NOTE]
> 이 옵션을 enabing 보안에 영향을 미칩니다. 서버에서 SQLCLR을 사용 하도록 설정할 수 없는 경우 [TRANSACT-SQL PREDICT](../../t-sql/queries/predict-transact-sql.md?view=sql-server-2017) 함수와 같은 대체 구현을 사용 합니다.

사용자에 게 `EXECUTE` 데이터베이스에 대 한 권한이 필요 합니다.

### <a name="supported-algorithms"></a>지원되는 알고리즘

모델을 만들고 학습 하려면 [SQL Server Machine Learning Services (r 또는 python)](../../machine-learning/sql-server-machine-learning-services.md)에서 제공 하는 r 또는 python에 대해 지원 되는 알고리즘 중 하나를 사용 하 고, [SQL Server 2016 R Services](../../machine-learning/r/sql-server-r-services.md), [SQL Server Machine Learning Server (독립 실행형) (r 또는 Python)](../../machine-learning/r/r-server-standalone.md)또는 [SQL Server 2016 R 서버 (독립 실행형)](../../machine-learning/r/r-server-standalone.md?view=sql-server-2016)를 사용 합니다.

#### <a name="r-revoscaler-models"></a>R: RevoScaleR 모델

  + [rxLinMod](/machine-learning-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](/machine-learning-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](/machine-learning-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](/machine-learning-server/r-reference/revoscaler/rxdtree)
  + [rxdForest](/machine-learning-server/r-reference/revoscaler/rxdforest)

#### <a name="r-microsoftml-models"></a>R: MicrosoftML 모델

  + [rxFastTrees](/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](/machine-learning-server/r-reference/microsoftml/rxfastlinear)

#### <a name="r-transformations-supplied-by-microsoftml"></a>R: MicrosoftML에서 제공 하는 변환

  + [featurizeText](/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](/machine-learning-server/r-reference/microsoftml/selectFeatures)

#### <a name="python-revoscalepy-models"></a>Python: revoscalepy 모델

  + [rx_lin_mod](/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](/machine-learning-server/python-reference/revoscalepy/rx-logit)
  + [rx_btrees](/machine-learning-server/python-reference/revoscalepy/rx-btrees)
  + [rx_dtree](/machine-learning-server/python-reference/revoscalepy/rx-dtree)
  + [rx_dforest](/machine-learning-server/python-reference/revoscalepy/rx-dforest)


#### <a name="python-microsoftml-models"></a>Python: microsoftml 모델

  + [rx_fast_trees](/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_network](/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

#### <a name="python-transformations-supplied-by-microsoftml"></a>Python: microsoftml에서 제공 하는 변환

  + [featurize_text](/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [concat](/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](/machine-learning-server/python-reference/microsoftml/categorical-hash)
  
### <a name="unsupported-model-types"></a>지원되지 않는 모델 형식

다음 모델 유형은 지원 되지 않습니다.

+ `rxGlm` `rxNaiveBayes` RevoScaleR에서 또는 알고리즘을 사용 하는 모델
+ R의 PMML 모델
+ 다른 타사 라이브러리를 사용 하 여 만든 모델 

## <a name="examples"></a>예

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

* \@ Inputdata* 의 입력 데이터에는 유효한 SQL 쿼리가 될 뿐만 아니라 저장 된 모델의 열과 호환 되는 열이 포함 되어야 합니다.

`sp_rxPredict` 는 double, float, short, ushort, long, ulong 및 string과 같은 .NET 열 유형만 지원 합니다. 실시간 점수 매기기에 사용 하기 전에 입력 데이터에서 지원 되지 않는 형식을 필터링 해야 할 수도 있습니다. 

  해당하는 SQL 형식에 대한 자세한 내용은 [SQL-CLR 형식 매핑](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) 또는 [CLR 매개 변수 데이터 매핑](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)을 참조하세요.