---
title: sp_rxPredict를 사용하여 실시간 채점
description: SQL Server의 sp_rxPredict 시스템 저장 프로시저를 사용하여 예측 워크로드에서 고성능 예측 또는 점수를 제공하는 실시간 채점을 수행하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/31/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: 19f9f1c6cfc293bfba0d44e34e0a30bf386bdb3d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470964"
---
# <a name="real-time-scoring-with-sp_rxpredict-in-sql-server"></a>SQL Server의 sp_rxPredict를 사용한 실시간 채점
[!INCLUDE[sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

SQL Server의 [sp_rxPredict](../../relational-databases/system-stored-procedures/sp-rxpredict-transact-sql.md) 시스템 저장 프로시저를 사용하여 예측 워크로드에서 고성능 예측 또는 점수를 제공하는 실시간 채점을 수행하는 방법을 알아봅니다.

`sp_rxPredict`를 사용한 실시간 채점은 언어 제한이 없으며 [Machine Learning Services](../sql-server-machine-learning-services.md) 또는 [R Services](../r/sql-server-r-services.md)에서 R 또는 Python 런타임에 대한 종속성 없이 실행됩니다. Microsoft 기능을 사용하여 모델을 만들고 학습시킨 다음, SQL Server에서 이진 형식으로 직렬화한다고 가정하면 실시간 채점을 사용하여 R 또는 Python 추가 기능이 설치되지 않은 SQL Server 인스턴스의 새 데이터 입력에 대해 예측된 결과를 생성할 수 있습니다.

## <a name="how-real-time-scoring-works"></a>실시간 채점 작동 방식

실시간 채점은 R의 [RevoScaleR](../r/ref-r-revoscaler.md) 또는 [MicrosoftML](../r/ref-r-microsoftml.md), Python의 [revoscalepy](../python/ref-py-revoscalepy.md) 또는 [microsoftml](../python/ref-py-microsoftml.md)에서 함수를 기반으로 특정 모델 유형에 대해 지원됩니다. 특수 이진 형식으로 저장된 기계 학습 모델에 제공된 사용자 입력을 기준으로 네이티브 C++ 라이브러리를 사용하여 점수를 생성합니다.

[Machine Learning Services](../sql-server-machine-learning-services.md) 또는 [R Services](../r/sql-server-r-services.md)에서 외부 언어 런타임을 호출할 필요 없이 학습된 모델을 채점에 사용할 수 있기 때문에 여러 프로세스의 오버헤드가 줄어듭니다. 

실시간 채점은 다중 단계 프로세스입니다.

1. 채점을 수행하는 저장 프로시저는 데이터베이스 단위로 설정해야 합니다.
2. 미리 학습된 모델을 이진 형식으로 로드합니다.
3. 테이블 형식 또는 단일 행의 채점할 새 입력 데이터를 모델에 대한 입력으로 제공합니다.
4. 점수를 생성하려면 [sp_rxPredict](../../relational-databases/system-stored-procedures/sp-rxpredict-transact-sql.md) 저장 프로시저를 호출합니다.

## <a name="prerequisites"></a>사전 요구 사항

+ [SQL Server CLR 통합을 사용하도록 설정합니다](../../relational-databases/clr-integration/clr-integration-enabling.md).

+ [실시간 채점을 사용하도록 설정합니다](#bkmk_enableRtScoring).

+ 지원되는 **rx** 알고리즘 중 하나를 사용하여 모델을 미리 학습시켜야 합니다. R의 경우 `sp_rxPredict`에 대한 실시간 채점은 [RevoScaleR 및 MicrosoftML 지원 알고리즘](#bkmk_rt_supported_algos)과 함께 작동합니다. Python의 경우 [revoscalepy 및 microsoftml 지원 알고리즘](#bkmk_py_supported_algos)을 참조하세요.

+ R에는 [rxSerialize](/machine-learning-server/r-reference/revoscaler/rxserializemodel)를, Python에는 [rx_serialize_model](/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)을 사용하여 모델을 직렬화합니다. 이러한 직렬화 함수는 빠른 채점을 지원하도록 최적화되었습니다.

+ 모델을 호출하려는 데이터베이스 엔진 인스턴스에 모델을 저장합니다. 이 인스턴스에는 R 또는 Python 런타임 확장이 필요하지 않습니다.

> [!Note]
> 실시간 채점은 현재 몇 개의 행에서 수십만 개의 행까지, 더 작은 데이터 세트에 대한 빠른 예측에 최적화되어 있습니다. 빅 데이터 세트에서 [rxPredict](/machine-learning-server/r-reference/revoscaler/rxpredict)를 사용하는 것이 더 빠를 수 있습니다.

<a name ="bkmk_enableRtScoring"></a> 

## <a name="enable-real-time-scoring"></a>실시간 채점 사용

채점에 사용하려는 각 데이터베이스에 대해 이 기능을 사용하도록 설정해야 합니다. 서버 관리자는 RevoScaleR 패키지에 포함된 명령줄 유틸리티인 RegisterRExt.exe를 실행해야 합니다.

> [!NOTE]
> 실시간 채점이 작동하려면 인스턴스에서 SQL CLR 기능을 사용하도록 설정해야 합니다. 또한 데이터베이스를 신뢰할 수 있는 것으로 표시해야 합니다. 스크립트를 실행하면 이러한 작업이 자동으로 수행됩니다. 그러나 이 작업을 수행하기 전에 추가 보안 문제를 고려해야 합니다.

1. 관리자 권한 명령 프롬프트를 열고 RegisterRExt.exe가 있는 폴더로 이동합니다. 기본 설치에서는 다음 경로를 사용할 수 있습니다.

    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. 확장 저장 프로시저를 사용하도록 설정하려는 인스턴스 이름 및 대상 데이터베이스로 바꾼 상태로 다음 명령을 실행합니다.

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    예를 들어 기본 인스턴스의 CLRPredict 데이터베이스에 확장 저장 프로시저를 추가하려면 다음을 입력합니다.

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    데이터베이스가 기본 인스턴스에 있는 경우 인스턴스 이름은 선택 사항입니다. 명명된 인스턴스를 사용하는 경우 인스턴스 이름을 지정해야 합니다.

3. RegisterRExt.exe는 다음 개체를 만듭니다.

    + 신뢰할 수 있는 어셈블리
    + 저장 프로시저 `sp_rxPredict`
    + 새 데이터베이스 역할 `rxpredict_users`. 데이터베이스 관리자는 이 역할을 사용하여 실시간 채점 기능을 사용하는 사용자에게 사용 권한을 부여할 수 있습니다.

4. `sp_rxPredict`를 실행해야 하는 모든 사용자를 새 역할에 추가합니다.

> [!NOTE]
>
> SQL Server 2017 이상에서는 CLR 통합 문제를 방지하기 위해 추가 보안 조치가 준비되어 있습니다. 이러한 조치는 이 저장 프로시저의 사용에도 추가적인 제한을 둡니다.

## <a name="disable-real-time-scoring"></a>실시간 채점 비활성화

실시간 채점 기능을 사용하지 않도록 설정하려면 관리자 권한 명령 프롬프트를 열고 `RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]` 명령을 실행합니다.

<a name="bkmk_py_supported_algos"></a>

## <a name="supported-algorithms"></a>지원되는 알고리즘

### <a name="python-algorithms-using-real-time-scoring"></a>실시간 채점을 사용하는 Python 알고리즘

+ revoscalepy 모델

  + [rx_lin_mod](/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) \*
  + [rx_logit](/machine-learning-server/python-reference/revoscalepy/rx-logit) \*
  + [rx_btrees](/machine-learning-server/python-reference/revoscalepy/rx-btrees) \*
  + [rx_dtree](/machine-learning-server/python-reference/revoscalepy/rx-dtree) \*
  + [rx_dforest](/machine-learning-server/python-reference/revoscalepy/rx-dforest) \*
  
  \*가 표시된 모델은 PREDICT 함수를 사용하는 네이티브 채점도 지원합니다.

+ microsoftml 모델

  + [rx_fast_trees](/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_net](/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

+ microsoftml에서 제공하는 변환

  + [featurize_text](/machine-learning-server/python-reference/microsoftml/featurize-text)
  + [concat](/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](/machine-learning-server/python-reference/microsoftml/categorical-hash)

<a name="bkmk_rt_supported_algos"></a>

### <a name="r-algorithms-using-real-time-scoring"></a>실시간 채점을 사용하는 R 알고리즘

+ RevoScaleR 모델

  + [rxLinMod](/machine-learning-server/r-reference/revoscaler/rxlinmod) \*
  + [rxLogit](/machine-learning-server/r-reference/revoscaler/rxlogit) \*
  + [rxBTrees](/machine-learning-server/r-reference/revoscaler/rxbtrees) \*
  + [rxDtree](/machine-learning-server/r-reference/revoscaler/rxdtree) \*
  + [rxdForest](/machine-learning-server/r-reference/revoscaler/rxdforest) \*
  
  \*가 표시된 모델은 PREDICT 함수를 사용하는 네이티브 채점도 지원합니다.

+ MicrosoftML 모델

  + [rxFastTrees](/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](/machine-learning-server/r-reference/microsoftml/rxfastlinear)

+ MicrosoftML에서 제공하는 변환

  + [featurizeText](/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](/machine-learning-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>지원되지 않는 모델 형식

실시간 채점은 인터프리터를 사용하지 않습니다. 따라서 인터프리터를 필요로 하는 모든 기능은 채점 단계에서 지원되지 않습니다.  여기에는 다음이 포함될 수 있습니다.

+ `rxGlm` 또는 `rxNaiveBayes` 알고리즘을 사용하는 모델은 지원되지 않습니다.

+ 변환 함수 또는 변환이 포함된 수식(예: `A ~ log(B`)을 사용하는 모델은 실시간 채점에서 지원되지 않습니다. 이 형식의 모델을 사용하려면 데이터를 실시간 채점에 전달하기 전에 입력 데이터에 대해 변환을 수행하는 것이 좋습니다.

## <a name="example"></a>예제

이 섹션에서는 **실시간** 예측을 위한 모델을 준비하고 저장하는 데 필요한 단계를 설명하고 T-SQL에서 함수를 호출하는 방법의 R 예제를 제공합니다.

### <a name="step-1-prepare-and-save-the-model"></a>1단계. 모델 준비 및 저장

sp\_rxPredict에 필요한 이진 형식은 PREDICT 함수를 사용하는 데 필요한 형식과 동일합니다. 따라서 R 코드에서 [rxSerializeModel](/machine-learning-server/r-reference/revoscaler/rxserializemodel)에 대한 호출을 포함하고 다음 예제와 같이 `realtimeScoringOnly = TRUE`를 지정해야 합니다.

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-2-call-sp_rxpredict"></a>2단계. sp_rxPredict 호출

다른 저장 프로시저와 마찬가지로 `sp_rxPredict`를 호출합니다. 현재 릴리스에서 저장 프로시저는 두 개의 매개 변수만 사용합니다. 즉, 모델에 대한 이진 형식의 _\@model_ 과 유효한 SQL 쿼리로 정의된 채점에 사용할 데이터에 대한 _\@inputData_ 가 그것입니다.

이진 형식은 PREDICT 함수에서 사용하는 것과 같으므로 이전 예제의 모델 및 데이터 테이블을 사용할 수 있습니다.

```sql
DECLARE @irismodel varbinary(max)
SELECT @irismodel = [native_model_object] from [ml_models]
WHERE model_name = 'iris.dtree' 
AND model_version = 'v1''

EXEC sp_rxPredict
@model = @irismodel,
@inputData = N'SELECT * FROM iris_rx_data'
```

> [!NOTE]
> 채점에 대한 입력 데이터에 모델 요구 사항과 일치하는 열이 포함되어 있지 않으면 `sp_rxPredict` 호출이 실패합니다. 현재는 double, float, short, ushort, long, ulong 및 string과 같은 .NET 데이터 형식만 지원됩니다.
>
> 따라서 실시간 채점에 사용하기 전에 입력 데이터에서 지원되지 않는 형식을 필터링해야 할 수도 있습니다.
>
> 해당하는 SQL 형식에 대한 자세한 내용은 [SQL-CLR 형식 매핑](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) 또는 [CLR 매개 변수 데이터 매핑](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

+ [SQL 기계 학습에서 PREDICT T-SQL 함수를 사용하는 네이티브 채점](native-scoring-predict-transact-sql.md)
+ [sp_rxPredict](../../relational-databases/system-stored-procedures/sp-rxpredict-transact-sql.md)
+ [SQL Machine Learning](../index.yml)