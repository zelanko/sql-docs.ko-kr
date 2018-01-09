---
title: "실시간 점수 매기기 | Microsoft Docs"
ms.custom: 
ms.date: 11/03/2017
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dcd65909bf896e97bba715db6318b459b06fc015
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="realtime-scoring"></a>실시간 점수 매기기

SQL Server 2016과 거의 실시간에 기계 학습 모델에서 점수 매기기를 지 원하는 SQL Server 2017에서 제공 되는 기능에 설명 합니다.

> [!TIP]
> 기본 점수 매기기 되며 실시간 점수 매기기를 구현 하는 특별 한 네이티브 T-SQL 예측 함수를 사용 하 여 매우 빠르며 점수 매기기에 대 한 SQL Server 2017 에서만 사용할 수 있습니다. 자세한 내용은 참조 [기본 점수 매기기](sql-native-scoring.md)합니다.

## <a name="how-realtime-scoring-works"></a>실시간 점수 매기기의 작동 방식

실시간 점수 매기기는 SQL Server 2017와 SQL Server 2016에서 지원 됨 RevoScaleR 또는 MicrosoftML 알고리즘을 사용 하 여 만든 특정 모델 유형에 대해 지원 됩니다. 네이티브 c + + 라이브러리를 사용 하 여 점수를 기반으로 기계 학습 특수 이진 형식으로 저장 하는 모델에 제공 된 사용자 입력으로 생성 합니다.

학습된 된 모델 외부 언어 런타임 호출 하지 않고도 점수를 매기기 위해 사용할 수 있으므로 여러 프로세스의 오버 헤드가 줄어듭니다. 이 훨씬 빠른 예측 성능을 프로덕션 시나리오 점수 매기기에 대 한 지원 합니다. 데이터를 벗어나지 SQL Server, 때문에 결과 생성 하 고 R와 SQL 간의 데이터 변환 하지 않고도 새 테이블에 삽입할 수입니다.

실시간 점수 매기기 다단계 프로세스입니다.

1. 데이터베이스 단위로 점수 매기기를 수행 하는 저장된 프로시저를 사용할 수 있어야 합니다.
2. 이진 형식으로 미리 학습 된 모델을 로드 합니다.
3. 모델의 입력으로 새 입력된 데이터를 테이블 형식 또는 단일 행을 제공 합니다.
4. 점수를 생성 하려면 sp_rxPredict 저장 프로시저를 호출 합니다.

## <a name="get-started"></a>시작

코드 예제 및 지침에 대 한 참조 [기본 점수 매기기 또는 실시간 점수 매기기를 수행 하는 방법을](r/how-to-do-realtime-scoring.md)합니다.

점수를 매기기 위해 rxPredict 수 하는 방법의 예에 사용 되는 경우 참조 [최종 대출 ChargeOff 예측 빌드를 사용 하 여 Azure HDInsight Spark 클러스터 및 SQL Server 2016 R 서비스에 대 한 끝](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

> [!TIP]
> R 코드에서 단독으로 작업 하는 경우 사용할 수도 있습니다는 [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) 빠른 점수 매기기에 대 한 함수입니다.

## <a name="requirements"></a>요구 사항

실시간 점수 매기기는 이러한 플랫폼에서 지원 됩니다.

+ SQL Server 2017 Machine Learning Services
+ 9.1.0 Microsoft R Server는 R 서비스 인스턴스의 업그레이드 된 SQL Server R Services 2016 이상 버전
+ Machine Learning Server(독립 실행형)

SQL Server에서 기능을 미리 점수 매기기 실시간 사용 하도록 설정 해야 합니다. 기능을 사용 하려면 SQL Server에 CLR 기반 라이브러리의 설치 때문입니다.

실시간 대 한 자세한 내용은 Microsoft R Server에 기반 하 여 분산된 환경에서 점수 매기기를 참조 하십시오는 [publishService](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice) 함수에서 사용할 수는 [mrsDeploy 패키지](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)를 지 원하는 실시간 새 점수 매기기 R 서버에서 실행 되는 웹 서비스에 대 한 모델을 게시 합니다.

### <a name="restrictions"></a>Restrictions

+ 사전에 지원 되는 중 하나를 사용 하 여 모델을 학습 해야 **rx** 알고리즘입니다. 자세한 내용은 참조 [알고리즘 지원](#bkmk_rt_supported_algos)합니다. 실시간 점수 매기기 `sp_rxPredict` RevoScaleR와 MicrosoftML 알고리즘을 지원 합니다.

+ 새 serialization 함수를 사용 하 여 모델을 저장 해야 합니다: [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) R에 대 한 및 [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) Python에 대 한 합니다. 이러한 serialization 함수 빠른 점수 매기기를 지원 하도록 최적화 되었습니다.

+ 실시간 점수 매기기 인터프리터 해석기; 사용 하지 않습니다. 따라서 해석기 필요할 수 있는 모든 기능 점수 매기기 단계에서 지원 되지 않습니다.  여기에 포함 됩니다.

  + 사용 하 여 모델의 `rxGlm` 또는 `rxNaiveBayes` 알고리즘이 지원 되지 않습니다

  + R 변환 함수를 또는 같은 변환을 포함 하는 수식을 사용 하는 RevoScaleR 모델 <code>A ~ log(B)</code> 실시간 점수 매기기에서 지원 되지 않습니다. 이 유형의 모델을 사용 하려면 대 변환을 수행 하는 권장는 실시간 점수 매기기에 데이터를 전달 하기 전에 데이터를 입력 합니다.

+ 실시간 점수 매기기 몇 행에서 수백 개의 행 천 까지의 보다 작은 데이터 집합에 대 한 빠른 예측에 대 한 현재 최적화 되어 있습니다. 사용 하 여 매우 큰 데이터 집합에서 [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) 빠르게 보낼 수 있습니다.

### <a name="a-namebkmkrtsupportedalgosalgorithms-that-support-realtime-scoring"></a><a name="bkmk_rt_supported_algos">지 원하는 실시간 점수 매기기 알고리즘

+ RevoScaleR 모델

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)\*
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)\*
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)\*
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree)\*
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest)\*
  
  으로 표시 된 모델 \* 도 PREDICT 함수 기본 점수 매기기를 지원 합니다.

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
  + [범주](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>지원 되지 않는 모델 유형

다음 모델 유형에 지원 되지 않습니다.

+ 지원 되지 않는 유형의 R 변환 포함 하는 모델
+ 사용 하 여 모델의 `rxGlm` 또는 `rxNaiveBayes` RevoScaleR에서 알고리즘
+ PMML 모델
+ CRAN 또는 다른 저장소에서 다른 R 라이브러리를 사용 하 여 만든 모델
+ 다른 종류의 여기 나열 되지 않은 R 변환 포함 하는 모델

### <a name="known-issues"></a>알려진 문제

+ `sp_rxPredict`모델과 NULL 값이 전달 되는 정확 하지 않은 메시지를 반환 합니다.: "System.Data.SqlTypes.SqlNullValueException:Data에서 Null"입니다.

## <a name="next-steps"></a>다음 단계

[실시간 점수 매기기를 수행 하는 방법](r/how-to-do-realtime-scoring.md)
