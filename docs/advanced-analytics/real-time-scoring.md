---
title: Sp_rxPredict 저장 프로시저를 사용 하 여 실시간 점수 매기기
description: Sp_rxPredict를 사용 하 여 예측을 생성 하 고 R로 작성 된 미리 학습 된 모델에 대 한 데이터 입력 점수를 SQL Server 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: b4284d77464597857eca500b4a8ad29e1f4d06ee
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469966"
---
# <a name="real-time-scoring-with-sprxpredict-in-sql-server-machine-learning"></a>기계 학습 SQL Server sp_rxPredict의 실시간 점수 매기기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

실시간 점수 매기기는 [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) 시스템 저장 프로시저와 SQL SERVER의 CLR 확장 기능을 사용 하 여 예측 워크 로드의 고성능 예측 또는 점수를 제공 합니다. 실시간 점수 매기기는 언어와 관계 없이 R 또는 Python 실행 시간에 대 한 종속성 없이 실행 됩니다. Microsoft 함수를 사용 하 여 모델을 만들고 학습 한 다음 SQL Server에서 이진 형식으로 serialize 하는 경우 실시간 점수 매기기를 사용 하 여 R 또는 Python 추가 기능이 없는 SQL Server 인스턴스에서 새 데이터 입력에 대 한 예측 결과를 생성할 수 있습니다. 설치한.

## <a name="how-real-time-scoring-works"></a>실시간 점수 매기기 작동 방법

RevoScaleR 또는 MicrosoftML 기능 (예: [rxLinMod (RevoScaleR)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)[rxneuralnet (MicrosoftML))](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)을 기반으로 하는 특정 모델 유형에 대해 SQL Server 2017 및 SQL Server 2016에서 실시간 점수가 지원 됩니다. 특수 이진 형식 C++ 으로 저장 된 기계 학습 모델에 제공 된 사용자 입력을 기준으로 기본 라이브러리를 사용 하 여 점수를 생성 합니다.

외부 언어 런타임을 호출할 필요 없이 학습 된 모델을 점수 매기기에 사용할 수 있기 때문에 여러 프로세스의 오버 헤드가 줄어듭니다. 이는 프로덕션 점수 매기기 시나리오에 대해 훨씬 빠른 예측 성능을 지원 합니다. 데이터는 SQL Server 되지 않으므로 R과 SQL 간에 데이터를 변환 하지 않고 결과를 생성 하 고 새 테이블에 삽입할 수 있습니다.

실시간 점수 매기기는 다중 단계 프로세스입니다.

1. 점수 매기기를 수행 하는 저장 프로시저는 데이터베이스 별로 설정 해야 합니다.
2. 미리 학습 된 모델을 이진 형식으로 로드 합니다.
3. 테이블 형식 또는 단일 행의 점수가 매겨진 새 입력 데이터를 모델에 대 한 입력으로 제공 합니다.
4. 점수를 생성 하려면 [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) 저장 프로시저를 호출 합니다.

## <a name="prerequisites"></a>사전 요구 사항

+ [SQL SERVER CLR 통합을 사용 하도록 설정](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration)합니다.

+ [실시간 점수 매기기를 사용](#bkmk_enableRtScoring)합니다.

+ 모델은 지원 되는 **rx** 알고리즘 중 하나를 사용 하 여 미리 학습 해야 합니다. R의 경우의 실시간 점수 매기기 `sp_rxPredict` 는 [RevoScaleR 및 MicrosoftML 지원 알고리즘과](#bkmk_rt_supported_algos)함께 작동 합니다. Python의 경우 [revoscalepy 및 microsoftml 지원 되는 알고리즘](#bkmk_py_supported_algos) 을 참조 하세요.

+ R에 [Rxserialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) 를 사용 하 고 Python에 [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) 를 사용 하 여 모델을 직렬화 합니다. 이러한 serialization 함수는 빠른 점수 매기기를 지원 하도록 최적화 되었습니다.

+ 모델을 호출 하려는 데이터베이스 엔진 인스턴스에 모델을 저장 합니다. 이 인스턴스에는 R 또는 Python 런타임 확장이 필요 하지 않습니다.

> [!Note]
> 실시간 점수 매기기는 현재 몇 개의 행에서 수백 개의 행까지 보다 작은 데이터 집합에 대 한 빠른 예측에 최적화 되어 있습니다. 빅 데이터 집합에서 [Rxpredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) 를 사용 하는 것이 더 빠를 수 있습니다.

<a name="bkmk_py_supported_algos"></a>

## <a name="supported-algorithms"></a>지원되는 알고리즘

### <a name="python-algorithms-using-real-time-scoring"></a>실시간 점수 매기기를 사용 하는 Python 알고리즘

+ revoscalepy 모델

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) \*
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) \*
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) \*
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) \*
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) \*
  
  로 \* 표시 된 모델은 PREDICT 함수를 사용 하 여 기본 점수 매기기도 지원 합니다.

+ microsoftml 모델

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_net](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

+ Microsoftml에서 제공 하는 변환

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)


<a name="bkmk_rt_supported_algos"></a>

### <a name="r-algorithms-using-real-time-scoring"></a>실시간 점수 매기기를 사용 하는 R 알고리즘

+ RevoScaleR 모델

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) \*
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) \*
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) \*
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) \*
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) \*
  
  로 \* 표시 된 모델은 PREDICT 함수를 사용 하 여 기본 점수 매기기도 지원 합니다.

+ MicrosoftML 모델

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

+ MicrosoftML에서 제공 하는 변환

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>지원 되지 않는 모델 유형

실시간 점수 매기기는 인터프리터를 사용 하지 않습니다. 따라서 인터프리터를 필요로 하는 모든 기능은 점수 매기기 단계에서 지원 되지 않습니다.  여기에는 다음이 포함 될 수 있습니다.

  + `rxGlm` 또는`rxNaiveBayes` 알고리즘을 사용 하는 모델은 지원 되지 않습니다.

  + 변환 함수 또는 변환이 포함 된 수식 (예: <code>A ~ log(B)</code> )을 사용 하는 모델은 실시간 점수 매기기에서 지원 되지 않습니다. 이 유형의 모델을 사용 하려면 데이터를 실시간 점수 매기기에 전달 하기 전에 입력 데이터에 대해 변환을 수행 하는 것이 좋습니다.


## <a name="example-sprxpredict"></a>예: sp_rxPredict

이 섹션에서는 **실시간** 예측을 설정 하는 데 필요한 단계에 대해 설명 하 고 t-sql에서 함수를 호출 하는 방법에 대 한 R의 예제를 제공 합니다.

<a name ="bkmk_enableRtScoring"></a> 

### <a name="step-1-enable-the-real-time-scoring-procedure"></a>1단계. 실시간 점수 매기기 절차 사용

점수 매기기에 사용 하려는 각 데이터베이스에 대해이 기능을 사용 하도록 설정 해야 합니다. 서버 관리자는 RevoScaleR 패키지에 포함 된 명령줄 유틸리티인 RegisterRExt .exe를 실행 해야 합니다.

> [!NOTE]
> 실시간 점수 매기기가 작동 하려면 인스턴스에서 SQL CLR 기능을 사용 하도록 설정 해야 합니다. 또한 데이터베이스를 신뢰할 수 있는 것으로 표시 해야 합니다. 스크립트를 실행 하면 이러한 작업이 수행 됩니다. 그러나이 작업을 수행 하기 전에 추가 보안 문제를 고려해 야 합니다.

1. 관리자 권한 명령 프롬프트를 열고 RegisterRExt .exe가 있는 폴더로 이동 합니다. 기본 설치에서는 다음 경로를 사용할 수 있습니다.
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. 다음 명령을 실행 하 여 확장 저장 프로시저를 사용 하도록 설정 하려는 인스턴스 이름 및 대상 데이터베이스를 대체 합니다.

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    예를 들어 기본 인스턴스의 CLRPredict 데이터베이스에 확장 저장 프로시저를 추가 하려면 다음을 입력 합니다.

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    데이터베이스가 기본 인스턴스에 있는 경우 인스턴스 이름은 선택 사항입니다. 명명 된 인스턴스를 사용 하는 경우 인스턴스 이름을 지정 해야 합니다.

3. RegisterRExt는 다음 개체를 만듭니다.

    + 신뢰할 수 있는 어셈블리
    + 저장 프로시저`sp_rxPredict`
    + 새 데이터베이스 역할 `rxpredict_users`입니다. 데이터베이스 관리자는이 역할을 사용 하 여 실시간 점수 매기기 기능을 사용 하는 사용자에 게 사용 권한을 부여할 수 있습니다.

4. 새 역할에 실행 `sp_rxPredict` 해야 하는 모든 사용자를 추가 합니다.

> [!NOTE]
> 
> SQL Server 2017에서는 CLR 통합 문제를 방지 하기 위해 추가 보안 조치가 준비 되었습니다. 이러한 측정값은이 저장 프로시저 사용에 대 한 추가 제한을 적용 합니다. 

### <a name="step-2-prepare-and-save-the-model"></a>2단계. 모델 준비 및 저장

Sp\_rxpredict에 필요한 이진 형식은 PREDICT 함수를 사용 하는 데 필요한 형식과 동일 합니다. 따라서 R 코드에서 [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)에 대 한 호출을 포함 하 고 다음 예제와 같이를 `realtimeScoringOnly = TRUE`지정 해야 합니다.

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>3단계. Sp_rxPredict 호출

다른 저장 프로시저\_와 마찬가지로 sp rxpredict를 호출 합니다. 현재 릴리스에서 저장 프로시저는 두 개의 매개 변수, 즉  _\@_ 이진 형식으로 모델에 대 한 모델을 사용 하 고  _\@_ , 점수 매기기에 사용할 데이터에 대 한 inputdata를 사용 하 여 유효한 SQL 쿼리로 정의 합니다.

이진 형식은 PREDICT 함수에서 사용 하는 것과 같으므로 이전 예제의 모델 및 데이터 테이블을 사용할 수 있습니다.

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
> 
> 점수 매기기를 위한\_입력 데이터에 모델 요구 사항과 일치 하는 열이 포함 되지 않은 경우 sp rxpredict 호출이 실패 합니다. 현재는 double, float, short, ushort, long, ulong 및 string과 같은 .NET 데이터 형식만 지원 됩니다.
> 
> 따라서 실시간 점수 매기기에 사용 하기 전에 입력 데이터에서 지원 되지 않는 형식을 필터링 해야 할 수도 있습니다.
> 
> 해당 SQL 형식에 대 한 자세한 내용은 [sql-Clr 형식 매핑](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) 또는 [CLR 매개 변수 데이터 매핑](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data)을 참조 하세요.

## <a name="disable-real-time-scoring"></a>실시간 점수 매기기 사용 안 함

실시간 점수 매기기 기능을 사용 하지 않도록 설정 하려면 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 합니다.`RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="next-steps"></a>다음 단계

SQL Server의 점수 매기기에 대 한 자세한 배경 정보 [는 SQL Server machine learning에서 예측을 생성 하는 방법](r/how-to-do-realtime-scoring.md)을 참조 하세요.
