---
title: sp_rxPredict | Microsoft Docs
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
f1_keywords:
- sp_rxPredict
- sp_rxPredict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_rxPredict procedure
author: HeidiSteen
ms.author: heidist
ms.openlocfilehash: dadaa5f51f359d9a6803d504d6b3a0da64f39852
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126417"
---
# <a name="sprxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

SQL Server 데이터베이스에 이진 형식으로 저장 된 모델을 학습 하는 컴퓨터의 구성 된 지정된 된 입력에 대 한 예측된 값을 생성 합니다.

R 및 Python 기계 학습 모델에서 거의 실시간으로 점수 매기기를 제공 합니다. `sp_rxPredict` 저장 프로시저에 대 한 래퍼를 제공 합니다 `rxPredict` R 함수 [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) 및 [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package), 및 [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) 에서Python함수[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) 하 고 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)합니다. 작성 된 C++ 작업을 점수 매기기에 맞게 최적화 되어 있습니다.

직렬화 되 고 대상 데이터베이스 엔진 인스턴스에서 이진 형식으로 저장 되 면 R 또는 Python을 사용 하 여 모델을 만들어야, 있지만 사용할 수는 데이터베이스 엔진 인스턴스에서 R 또는 Python 통합이 설치 되지 않은 경우에 합니다. 자세한 내용은 [sp_rxPredict를 사용 하 여 실시간 점수 매기기](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring)합니다.

## <a name="syntax"></a>구문

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>인수

**model**

지원 되는 형식에서 미리 학습 된 모델입니다. 

**input**

유효한 SQL 쿼리

### <a name="return-values"></a>반환 값

입력된 데이터 원본에서 통과 열 뿐만 아니라 점수 열 반환 됩니다.
추가 신뢰 구간 같은 열을 점수 매기기, 알고리즘은 이러한 값의 생성을 지원 하는 경우 반환 될 수 있습니다.

## <a name="remarks"></a>설명

저장된 프로시저를 사용할 수 있도록, SQLCLR 인스턴스에서 활성화 되어야 합니다.

> [!NOTE]
> 이 옵션은 enabing 야 할 보안 관련 문제입니다. 와 같은 대체 구현을 사용 합니다 [TRANSACT-SQL 예측](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql?view=sql-server-2017) 함수를 서버에서 SQLCLR을 사용할 수 없는 경우.

사용자가 필요한 `EXECUTE` 데이터베이스에 대 한 권한이 있습니다.

### <a name="supported-algorithms"></a>지원되는 알고리즘

만들기 및 모델을 학습, R 또는 Python에 대 한 지원 되는 알고리즘 중 하나를 사용 하 여 제공 [SQL Server 2016 R Services](https://docs.microsoft.com/sql/advanced-analytics/r/sql-server-r-services?view=sql-server-2017)를 [SQL Server 2016 R Server (독립 실행형)](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone?view=sql-server-2016), [SQL Server 2017 컴퓨터 서비스 (예: R 또는 Python) 학습](https://docs.microsoft.com//sql/advanced-analytics/what-is-sql-server-machine-learning?view=sql-server-2017), 또는 [SQL Server 2017 Server (독립 실행형) (R 또는 Python)](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone?view=sql-server-2017)합니다.

#### <a name="r-revoscaler-models"></a>R: RevoScaleR 모델

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree)
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest)

#### <a name="r-microsoftml-models"></a>R: MicrosoftML 모델

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

#### <a name="r-transformations-supplied-by-microsoftml"></a>R: MicrosoftML 제공한 변환

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

#### <a name="python-revoscalepy-models"></a>Python: revoscalepy 모델

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit)
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees)
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree)
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest)


#### <a name="python-microsoftml-models"></a>Python: microsoftml 모델

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

#### <a name="python-transformations-supplied-by-microsoftml"></a>Python: Microsoftml 제공한 변환

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)
  
### <a name="unsupported-model-types"></a>지원 되지 않는 모델 유형

모델은 지원 되지 않습니다.

+ 사용 하 여 모델을 `rxGlm` 또는 `rxNaiveBayes` RevoScaleR의 알고리즘
+ R에서 PMML 모델
+ 다른 타사 라이브러리를 사용 하 여 만든 모델 

## <a name="examples"></a>예

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

유효한 SQL 쿼리를 입력된 데이터에서 사용 될 뿐 아니라 *@inputData* 저장 된 모델의 열과 호환 되는 열을 포함 해야 합니다.

`sp_rxPredict` 다음.NET 열 유형만 지원: double, float, short, ushort, long, ulong 및 문자열입니다. 실시간 점수 매기기에 사용 하기 전에 입력된 데이터에서 지원 되지 않는 형식 필터링 해야 합니다. 

  해당 SQL 형식에 대 한 자세한 내용은 [SQL-CLR 형식 매핑](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) 하거나 [CLR 매개 변수 데이터 매핑](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)합니다.

