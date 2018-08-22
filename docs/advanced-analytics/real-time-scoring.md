---
title: SQL Server machine learning에서 실시간 점수 매기기 | Microsoft Docs
description: Sp_rxPredict, SQL Server에서 R로 작성 된 미리 학습 된 모델에 대해 dta 입력 점수 매기기를 사용 하 여 예측을 생성 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d5a3d0318f925918ef98ae18744e4287d6b81108
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2018
ms.locfileid: "40394787"
---
# <a name="real-time-scoring-with-sprxpredict-in-sql-server-machine-learning"></a>SQL Server machine learning에서 sp_rxPredict으로 실시간 점수 매기기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server 관계형 데이터에 대 한 거의 실시간으로 작동 하는 방법을 점수 매기기, machine learning을 사용한 모델 R에서 작성 된 설명 

> [!Note]
> 네이티브 점수 매기기는 매우 빠르게 평가 하는 것에 대 한 네이티브 T-SQL 예측 함수를 사용 하는 실시간 점수 매기기의 특수 구현 합니다. 자세한 내용 및 가용성을 참조 하세요 [네이티브 점수 매기기](sql-native-scoring.md)합니다.

## <a name="how-real-time-scoring-works"></a>실시간 점수 매기기 작업

같은 RevoScaleR 또는 MicrosoftML 함수에 따라 특정 모델 유형에 대해 SQL Server 2017 및 SQL Server 2016에서 지원 되는 실시간 점수 매기기 [(RevoScaleR) rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) 또는 [rxNeuralNet (MicrosoftML)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet). 네이티브 c + + 라이브러리를 사용 하 여 기계 학습 모델을 특수 이진 형식으로 저장을 위해 제공 하는 사용자 입력을 기반으로 점수를 생성 합니다.

외부 언어 런타임을 호출 하지 않고도 점수를 매기기 위해 학습 된 모델을를 사용할 수 있으므로 여러 프로세스의 오버 헤드가 줄었습니다. 이 시나리오를 평가 하는 프로덕션에 대 한 훨씬 더 빠른 예측 성능을 지원 합니다. 데이터를 SQL 서버를 벗어나지, 때문에 결과 생성 하 고 R과 SQL 간 데이터 변환 하지 않고도 새 테이블에 삽입할 수 있습니다.

실시간 점수 매기기는 다단계 프로세스입니다.

1. 점수 매기기를 수행 하는 저장된 프로시저에서 데이터베이스 단위로 활성화 되어야 합니다.
2. 이진 형식으로 미리 학습 된 모델을 로드 합니다.
3. 모델에 대 한 입력으로 새 입력된 데이터를 테이블 형식 또는 단일 행을 제공합니다.
4. 점수를 생성 하려면 sp_rxPredict 저장 프로시저를 호출 합니다.

## <a name="get-started"></a>시작

코드 예제 및 지침을 참조 하세요 [네이티브 점수 매기기 또는 실시간 점수 매기기를 수행 하는 방법을](r/how-to-do-realtime-scoring.md)합니다.

점수를 매기기 위해 rxPredict를 사용할 수 있는 방법을의 예제를 참조 하세요. [종단 간 최종 대출 상각 예측 빌드를 사용 하 여 Azure HDInsight Spark 클러스터 및 SQL Server 2016 R 서비스](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

> [!TIP]
> R 코드에서 단독으로 작업 하는 경우 사용할 수도 있습니다는 [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) 빠른 점수를 매기기 위해는 함수입니다.

## <a name="requirements"></a>요구 사항

실시간 점수 매기기는 이러한 플랫폼에서 지원 됩니다.

+ SQL Server 2017 Machine Learning Services
+ 이상 버전 9.1.0으로 R 구성 요소를 업그레이드를 사용 하 여 SQL Server R Services 2016

SQL Server에서 SQL Server에 CLR 기반 라이브러리를 추가 하기 전에 실시간 점수 매기기 기능을 설정 해야 합니다.

Microsoft R Server를 기반으로 하는 분산된 환경에서 실시간 점수 매기기에 대 한 정보를 참조 합니다 [publishService](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice) 함수에서 사용할 수 있는 [mrsDeploy 패키지](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)를 지 원하는 실시간 점수 매기기 모델을 새 R Server에서 실행 되는 웹 서비스를 게시 합니다.

### <a name="restrictions"></a>Restrictions

+ 사전에 지원 되는 중 하나를 사용 하 여 모델을 학습 해야 합니다 **rx** 알고리즘입니다. 자세한 내용은 참조 하세요 [알고리즘을 지원](#bkmk_rt_supported_algos)합니다. 사용 하 여 실시간 점수 매기기 `sp_rxPredict` RevoScaleR 및 MicrosoftML 알고리즘을 지원 합니다.

+ 새로운 직렬화 함수를 사용 하 여 모델을 저장 해야 합니다. [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) R에 대 한 및 [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) Python에 대 한 합니다. 이러한 serialization 함수 빠른 점수 매기기를 지원 하도록 최적화 되었습니다.

+ 실시간 점수 매기기 인터프리터; 사용 하지 않습니다. 따라서 인터프리터 필요할 수 있는 모든 기능 점수 매기기 단계에서 지원 되지 않습니다.  이러한 포함 될 수 있습니다.

  + 사용 하 여 모델을 `rxGlm` 또는 `rxNaiveBayes` 알고리즘이 현재 지원 되지 않습니다

  + R 변환 함수를 사용 하 여 또는 같은 변환을 포함 하는 수식을 사용 하는 RevoScaleR 모델 <code>A ~ log(B)</code> 실시간 점수 매기기에서 지원 되지 않습니다. 이 유형의 모델을 사용 하려면에서 변환을 수행 하는 권장 된 실시간 점수 매기기 데이터를 전달 하기 전에 데이터를 입력 합니다.

+ 실시간 점수 매기기 몇 행에서 수백 수천 개의 행에 이르기까지 더 작은 데이터 집합에 대 한 빠른 예측에 대 한 현재 최적화 됩니다. 사용 하 여 큰 데이터 집합 [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) 빠를 수 있습니다.

### <a name="a-namebkmkrtsupportedalgosalgorithms-that-support-real-time-scoring"></a><a name="bkmk_rt_supported_algos">실시간 점수 매기기를 지 원하는 알고리즘

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

이전 섹션에서 명시적으로 나열 된 것 이외의 R 변환에 대 한 실시간 점수 매기기 지원 되지 않습니다. 

RevoScaleR 및 다른 Microsoft R 관련 라이브러리를 사용 하 여 작업에 익숙한 개발자를 위한 지원 되지 않는 함수를 포함 `rxGlm` 또는 `rxNaiveBayes` RevoScaleR에 PMML 모델에서 알고리즘 및 CRAN에서 다른 R 라이브러리를 사용 하 여 만든 다른 모델 또는 다른 리포지토리입니다.

### <a name="known-issues"></a>알려진 문제

+ `sp_rxPredict` NULL 값을 모델로 전달 될 때 부정확 한 메시지를 반환 합니다. "System.Data.SqlTypes.SqlNullValueException:Data에서 Null"입니다.

## <a name="next-steps"></a>다음 단계

[실시간 점수 매기기를 수행 하는 방법](r/how-to-do-realtime-scoring.md)
