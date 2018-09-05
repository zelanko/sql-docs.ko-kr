---
title: SQL Server machine learning에서 실시간 점수 매기기 | Microsoft Docs
description: Sp_rxPredict, SQL Server에서 R로 작성 된 미리 학습 된 모델에 대해 입력 데이터 점수 매기기를 사용 하 여 예측을 생성 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 576526801188bc9459ec9e26470e5d17dd775f74
ms.sourcegitcommit: 2a47e66cd6a05789827266f1efa5fea7ab2a84e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2018
ms.locfileid: "43348303"
---
# <a name="real-time-scoring-with-sprxpredict-in-sql-server-machine-learning"></a>SQL Server machine learning에서 sp_rxPredict으로 실시간 점수 매기기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

실시간 점수 매기기 CLR 확장 기능이 고성능 예측 또는 워크 로드 예측의 점수에 대 한 SQL Server에서 사용 합니다. 실시간 점수 매기기 언어 중립적 이므로 R 종속 되지 않고 실행 하거나 Python 번 실행 합니다. Microsoft 함수에서 생성, 학습 및 SQL Server에서 이진 형식으로 직렬화 된 모델을 가정 하 고, 실시간 점수 매기기 하 여 R 또는 Python 추가 기능에 있지 않은 SQL Server 인스턴스에서 새 데이터 입력에 대해 예측 된 결과 생성 합니다. 설치 합니다.

## <a name="how-real-time-scoring-works"></a>실시간 점수 매기기 작업

같은 RevoScaleR 또는 MicrosoftML 함수에 따라 특정 모델 유형에 대해 SQL Server 2017 및 SQL Server 2016에서 지원 되는 실시간 점수 매기기 [(RevoScaleR) rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) 또는 [rxNeuralNet (MicrosoftML)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet). 네이티브 c + + 라이브러리를 사용 하 여 기계 학습 모델을 특수 이진 형식으로 저장을 위해 제공 하는 사용자 입력을 기반으로 점수를 생성 합니다.

외부 언어 런타임을 호출 하지 않고도 점수를 매기기 위해 학습 된 모델을를 사용할 수 있으므로 여러 프로세스의 오버 헤드가 줄었습니다. 이 시나리오를 평가 하는 프로덕션에 대 한 훨씬 더 빠른 예측 성능을 지원 합니다. 데이터를 SQL 서버를 벗어나지, 때문에 결과 생성 하 고 R과 SQL 간 데이터 변환 하지 않고도 새 테이블에 삽입할 수 있습니다.

실시간 점수 매기기는 다단계 프로세스입니다.

1. 점수 매기기를 수행 하는 저장된 프로시저에서 데이터베이스 단위로 활성화 되어야 합니다.
2. 이진 형식으로 미리 학습 된 모델을 로드 합니다.
3. 모델에 대 한 입력으로 새 입력된 데이터를 테이블 형식 또는 단일 행을 제공합니다.
4. 점수를 생성 하려면 sp_rxPredict 저장 프로시저를 호출 합니다.

> [!TIP]
> 작업에서 실시간 점수 매기기의 예제를 참조 하세요. [종단 간 최종 대출 상각 예측 빌드를 사용 하 여 Azure HDInsight Spark 클러스터 및 SQL Server 2016 R 서비스](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

## <a name="prerequisites"></a>필수 구성 요소

+ [SQL Server CLR 통합 사용](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration)합니다.

+ [실시간 점수 매기기를 사용 하도록 설정](#bkmk_enableRtScoring)합니다.

+ 사전에 지원 되는 중 하나를 사용 하 여 모델을 학습 해야 합니다 **rx** 알고리즘입니다. R의 경우으로 실시간 점수 매기기 `sp_rxPredict` 와 함께 [RevoScaleR 및 MicrosoftML 알고리즘 지원](#bkmk_rt_supported_algos)합니다. Python에 대 한 참조 [revoscalepy 및 microsoftml 알고리즘 지원](#bkmk_py_supported_algos)

+ 사용 하 여 모델 serialize [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) R에 대 한 및 [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) Python에 대 한 합니다. 이러한 serialization 함수 빠른 점수 매기기를 지원 하도록 최적화 되었습니다.

> [!Note]
> 실시간 점수 매기기 몇 행에서 수백 수천 개의 행에 이르기까지 더 작은 데이터 집합에 대 한 빠른 예측에 대 한 현재 최적화 됩니다. 사용 하 여 큰 데이터 집합 [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) 빠를 수 있습니다.

<a name="bkmk_py_supported_algos"></a>

## <a name="supported-algorithms"></a>지원되는 알고리즘

### <a name="python-algorithms-using-real-time-scoring"></a>실시간 점수 매기기를 사용 하 여 Python 알고리즘

+ revoscalepy 모델

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) \*
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) \*
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) \*
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) \*
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) \*
  
  모델 표시 \* 또한 PREDICT 함수를 사용 하 여 네이티브 점수 매기기를 지원 합니다.

+ microsoftml 모델

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_net](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

+ Microsoftml 제공한 변환

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)


<a name="bkmk_rt_supported_algos"></a>

### <a name="r-algorithms-using-real-time-scoring"></a>실시간 점수 매기기를 사용 하 여 R 알고리즘

+ RevoScaleR 모델

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) \*
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) \*
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) \*
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) \*
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) \*
  
  모델 표시 \* 또한 PREDICT 함수를 사용 하 여 네이티브 점수 매기기를 지원 합니다.

+ MicrosoftML 모델

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

+ MicrosoftML 제공한 변환

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>지원 되지 않는 모델 유형

실시간 점수 매기기 인터프리터; 사용 하지 않습니다. 따라서 인터프리터 필요할 수 있는 모든 기능 점수 매기기 단계에서 지원 되지 않습니다.  이러한 포함 될 수 있습니다.

  + 사용 하 여 모델을 `rxGlm` 또는 `rxNaiveBayes` 알고리즘이 지원 되지 않습니다.

  + 변환 함수 또는 같은 변환을 포함 하는 수식을 사용 하 여 모델 <code>A ~ log(B)</code> 실시간 점수 매기기에서 지원 되지 않습니다. 이 유형의 모델을 사용 하려면 실시간 점수 매기기 데이터를 전달 하기 전에 입력된 데이터 변환을 수행 하는 것이 좋습니다.


## <a name="example-sprxpredict"></a>예제: sp_rxPredict

이 섹션에서는 설정 하는 데 필요한 단계를 설명 **실시간** 예측, R에서 T-SQL에서 함수를 호출 하는 방법의 예제를 제공 합니다.

<a name ="bkmk_enableRtScoring"></a> 

### <a name="step-1-enable-the-real-time-scoring-procedure"></a>1단계. 실시간 점수 매기기 절차를 사용 하도록 설정

점수 매기기에 사용 하려는 각 데이터베이스에 대해이 기능을 활성화 해야 합니다. 서버 관리자에 RevoScaleR 패키지에 포함 되어 있는 명령줄 유틸리티를 RegisterRExt.exe를 실행 해야 합니다.

> [!NOTE]
> 작업 실시간 채 점을 위해 순서로 SQL CLR 기능을 사용 해야 인스턴스에; 또한 데이터베이스는 신뢰할 수 있는 표시 해야 합니다. 스크립트를 실행 하는 경우 이러한 함수를 수행 됩니다. 그러나이 작업을 수행 하기 전에 추가 보안에 미치는 영향을 고려해 야!

1. 관리자 권한 명령 프롬프트를 열고 RegisterRExt.exe가 있는 폴더로 이동 합니다. 기본 설치에서 경로 사용할 수 있습니다.
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. 인스턴스 및 확장된 저장된 프로시저를 사용 하도록 설정 하려는 대상 데이터베이스의 이름을 대체 하 여 다음 명령을 실행 합니다.

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    예를 들어 CLRPredict 데이터베이스 기본 인스턴스에서 확장된 저장된 프로시저에 추가 하려면 다음을 입력 합니다.

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    인스턴스 이름을 데이터베이스가 기본 인스턴스에 있는 경우 선택 사항입니다. 명명된 된 인스턴스를 사용 하는 경우 인스턴스 이름을 지정 해야 합니다.

3. RegisterRExt.exe 다음 개체를 만듭니다.

    + 신뢰할 수 있는 어셈블리
    + 저장된 프로시저 `sp_rxPredict`
    + 새 데이터베이스 역할을 `rxpredict_users`입니다. 데이터베이스 관리자가 실시간 점수 매기기 기능을 사용 하는 사용자에 권한을 부여 하려면이 역할을 사용 합니다.

4. 모든 사용자가 실행 해야 하는 추가 `sp_rxPredict` 새 역할을 합니다.

> [!NOTE]
> 
> SQL Server 2017에 추가 보안 조치의에서 경우 CLR 통합을 사용 하 여 문제를 방지 하기 위해 이러한 측정값도이 저장된 프로시저의 사용에 대해 추가적인 제한을 적용합니다. 

### <a name="step-2-prepare-and-save-the-model"></a>2단계. 준비 및 모델 저장

Sp에 의해 필요한 이진 형식\_rxPredict PREDICT 함수를 사용 하는 데 필요한 형식으로 동일 합니다. 따라서 R 코드에서 호출을 포함할 [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)를 지정 해야 하 고 `realtimeScoringOnly = TRUE`이 예제와 같이:

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>3단계. Sp_rxPredict 호출

Sp 호출\_rxPredict 것은 다른 저장 프로시저입니다. 현재 릴리스에서 저장된 프로시저는 두 개의 매개 변수를 사용 합니다.  _\@모델_ 이진 형식으로 모델에 대 한 및  _\@inputData_ 점수 매기기에 사용 하 여 데이터에 대 한 정의 유효한 SQL 쿼리입니다.

PREDICT 함수에서 사용 되는 동일한 이진 형식 이므로 앞의 예제에서 모델 및 데이터 테이블을 사용할 수 있습니다.

```SQL
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
> Sp에 대 한 호출\_rxPredict 점수 매기기에 대 한 입력된 데이터에 모델의 요구 사항과 일치 하는 열이 포함 되어 있지 않으면 실패 합니다. 현재 다음.NET 데이터 형식만 지원 됩니다: double, float, short, ushort, long, ulong 및 문자열입니다.
> 
> 따라서 실시간 점수 매기기에 사용 하기 전에 입력된 데이터에서 지원 되지 않는 형식 필터링 해야 합니다.
> 
> 해당 SQL 형식에 대 한 자세한 내용은 [SQL-CLR 형식 매핑](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) 하거나 [CLR 매개 변수 데이터 매핑](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data)합니다.

## <a name="disable-real-time-scoring"></a>실시간 점수 매기기를 사용 하지 않도록 설정

실시간 점수 매기기 기능을 사용 하지 않으려면 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 합니다. `RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="next-steps"></a>다음 단계

점수를 매기기 위해 rxPredict를 사용할 수 있는 방법을의 예제를 참조 하세요 [종단 간 최종 대출 상각 예측 빌드를 사용 하 여 Azure HDInsight Spark 클러스터 및 SQL Server 2016 R 서비스가](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)합니다.

SQL Server에서 점수 매기기 자세한 배경 정보를 참조 하세요 [SQL Server machine learning에서 예측을 생성 하는 방법을](r/how-to-do-realtime-scoring.md)합니다.
