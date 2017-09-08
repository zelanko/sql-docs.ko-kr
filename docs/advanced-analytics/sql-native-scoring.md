---
title: "기본 점수 매기기 | Microsoft Docs"
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e1cb06223e5274c1fa439eb9f7d82a005e93a47d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---

# <a name="native-scoring"></a>기본 점수 매기기

이 항목에서는 SQL Server 2017의 근 실시간에서 기계 학습 모델의 점수 매기기를 제공 하는 기능.

+ 실시간 점수 매기기 및 점수 매기기 네이티브 이란
+ 작동 방법
+ 지원 되는 플랫폼 및 요구 사항

## <a name="what-is-native-scoring-and-how-is-it-different-from-realtime-scoring"></a>기본 점수 매기기를 란 무엇이 고 어떻게 실시간 점수 매기기와의 차이점은?

Microsoft은 SQL Server 2016에서 T-SQL에서 실행할 R 스크립트를 허용 하는 확장 프레임 워크를 만들었습니다. 이 프레임 워크 R, 간단한 함수에서 학습 복잡 한 기계 학습 모델에 이르기까지에서 수행할 수 있는 작업을 지원 합니다. 그러나 이중 프로세스 아키텍처는 SQL Server와 함께 R 작업의 복잡성에 관계 없이 모든 호출에 대 한 외부 R 프로세스를 호출 해야 합니다를 의미 합니다. SQL Server에 이미 있는 데이터에 대 한 점수는 테이블에서 미리 학습 된 모델을 로드 하는 경우 외부 R 프로세스 호출의 오버 헤드는 불필요 한 성능 비용을 나타냅니다.

_점수 매기기_ 은 두 단계로: 미리 학습 된 모델 테이블에서 로드 되 고 새 입력된 데이터를 테이블 형식 또는 단일 행을 새 값을 생성 하는 모델에 전달 됩니다 (또는 _점수_). 확률을 나타내는 단일 열 값 또는 여러 값을 신뢰 구간, 오류 또는 예측에 유용한 기타 보완을 포함 하 여 출력 수 있습니다.

많은 데이터 행의 점수를 매길 때 새 값은 일반적으로 점수 매기기 절차의 일부로 테이블에 삽입 됩니다.  그러나 실시간으로 단일 점수를 검색할 수 있습니다. 연속 입력의 점수를 매길 때에 빠른 메모리로 다시 로드 될 수 있도록 모델 캐시 될 수 있습니다.

빠른 점수 매기기를 지원 하려면 SQL Server 컴퓨터 학습 서비스 (및 Microsoft 컴퓨터 학습 서버) 또는 T-SQL에서 R에서 작업 하는 기본 제공 점수 매기기 라이브러리를 제공 합니다. 버전에 따라 다른 옵션이 있습니다.

**기본 점수 매기기**

+ TRANSACT-SQL에서 PREDICT 함수에 사용할 수 있습니다 _기본 점수 매기기_ SQL Server 2017의 모든 인스턴스에서 합니다. 이미 학습 하 고 테이블에 저장 하는 모델이만 있어야 또는 T-SQL을 통해 호출할 수 있습니다. 네이티브 T-SQL 함수;를 사용 하는 종류의 실시간 점수 매기기 추가 구성이 필요 하지 않습니다.

   R 런타임을 호출 되지 않습니다 및 설치할 필요가 없습니다.

**실시간 점수 매기기**

+ **sp_rxPredict** 하는 R 런타임을 호출 하지 않고 모든 지원 되는 모델 형식에서 점수를 생성 하는 점수 매기기 실시간 사용 될 수 있는 저장된 프로시저를 인지 합니다.

  실시간 점수 매기기를 사용 하려면이 옵션의 Microsoft R Server 독립 실행형 설치 관리자를 사용 하 여 R 구성 요소를 업그레이드 하는 경우 SQL Server 2016에서 사용할 수 이기도 합니다. sp_rxPredict은 SQL Server 2017에도 지원 하며 PREDICT 함수에서 지원 되지 않습니다는 모델 유형에 점수를 매기는 경우에 적합 한 옵션을 수 있습니다.

+ R 코드 내에서 빠른 점수를 매기기 위해 rxPredict 함수를 사용할 수 있습니다.

모든 이러한 점수 매기기 방법에 대해 지원 되는 RevoScaleR 또는 MicrosoftML 알고리즘 중 하나를 사용 하 여 학습 된 모델을 사용 해야 합니다.

실시간 점수 매기기 작업의 예제를 보려면 [최종 대출 ChargeOff 예측 빌드를 사용 하 여 Azure HDInsight Spark 클러스터 및 SQL Server 2016 R 서비스에 대 한 끝](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

## <a name="how-native-scoring-works"></a>네이티브 works 점수 매기기

기본 점수 매기기 점수를 생성 하 고 특수 이진 형식에서 모델을 읽을 수 있는 Microsoft에서 네이티브 c + + 라이브러리를 사용 합니다. 모델을 게시 하 고 R 인터프리터를 호출 하지 않고도 점수 매기기에 사용 되는 수 때문에 여러 프로세스 상호 작용의 오버 헤드가 줄어듭니다. 이 훨씬 빠른 예측 성능을 엔터프라이즈 프로덕션 시나리오에서 지원합니다.

이 라이브러리를 사용 하 여 점수를 생성 하려면 점수 매기기 함수를 호출 하 고 다음 필요한 입력 값을 전달 합니다.

+ 호환 되는 모델입니다. 참조는 [요구 사항](#Requirements) 자세한 내용은 섹션.
+ 입력된 데이터를 일반적으로 SQL 쿼리로 정의

함수를 통해 전달 하려는 원본 데이터의 모든 열이 함께 입력된 데이터에 대 한 예측을 반환 합니다.

필요한 이진 형식에서 모델을 준비 하는 방법에 대 한 지침과 코드 샘플에 대 한이 문서를 참조 합니다.

+ [실시간 점수 매기기를 수행 하는 방법](r/how-to-do-realtime-scoring.md)

## <a name="requirements"></a>요구 사항

지원 되는 플랫폼은 다음과 같습니다.

+ SQL Server 2017 컴퓨터 학습 서비스 (Microsoft R Server 9.1.0 포함)
    
    기본 점수 매기기 PREDICT를 사용 하 여 SQL Server 2017 필요 합니다.
    Linux를 포함 하 여 SQL Server 2017 년의 모든 버전에서 작동 합니다.

    실시간 점수를 사용 하 여 수행할 수도 있습니다 sp_rxPredict SQL CLR을 설정 해야 합니다.

+ SQL Server 2016

   사용 하 여 점수 매기기 실시간 sp_rxPredict SQL Server 2016으로 및 Microsoft R 서버에서 실행할 수도 있습니다. 이 옵션을 사용 하도록 설정 하는 SQLCLR 및 Microsoft R Server 업그레이드를 설치 합니다.
   자세한 내용은 참조 [실시간 점수 매기기](Real-time-scoring.md)

### <a name="model-preparation"></a>모델 준비

+ 사전에 지원 되는 중 하나를 사용 하 여 모델을 학습 해야 **rx** 알고리즘입니다. 자세한 내용은 참조 [알고리즘 지원](#bkmk_native_supported_algos)합니다.
+ Microsoft R Server 9.1.0에에서 제공 된 새 serialization 함수를 사용 하 여 모델을 저장 해야 합니다. 직렬화 함수가 빠른 점수 매기기를 지원 하도록 최적화 됩니다.

### <a name="bkmk_native_supported_algos"></a>지 원하는 기본 점수 매기기 알고리즘

+ RevoScaleR 모델

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxdForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

MicrosoftML에서 모델을 사용 해야 하는 경우 실시간 sp_rxPredict 점수 매기기를 사용 합니다.

### <a name="restrictions"></a>제한 사항

다음 모델 유형에 지원 되지 않습니다.

+ 지원 되지 않는 유형의 R 변환 포함 하는 모델
+ 사용 하 여 모델의 `rxGlm` 또는 `rxNaiveBayes` RevoScaleR에서 알고리즘
+ PMML 모델
+ CRAN 또는 다른 저장소에서 다른 R 라이브러리를 사용 하 여 만든 모델
+ 다른 종류의 R 변환 포함 하는 모델

