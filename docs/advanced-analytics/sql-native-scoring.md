---
title: SQL Server machine learning에서 네이티브 점수 매기기 | Microsoft Docs
description: SQL Server에서 R 또는 Python에서 작성 하는 미리 학습 된 모델에 대해 dta 입력 점수 매기기, 예측 T-SQL 함수를 사용 하 여 예측을 생성 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: bf8f9a6362b72efddccbf5c2b0e54096c6e86aa7
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2018
ms.locfileid: "40392671"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>예측 T-SQL 함수를 사용 하 여 네이티브 점수 매기기
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

미리 학습 된 모델을 만든 후 예측 값을 생성 하는 함수에 새 입력된 데이터를 전달할 수 있습니다 또는 *점수*합니다. SQL Server 2017 Windows 또는 Linux에서 또는 Azure SQL Database에서 네이티브 점수 매기기를 지원 하도록 TRANSACT-SQL의 PREDICT 함수를 사용할 수 있습니다. T-SQL을 사용 하 여 호출할 수 있는 모델 학습 이미 있다고만 필요 합니다. 

+ 실시간 점수 매기기 및 점수 매기기 네이티브 란
+ 작동 방법
+ 지원 되는 플랫폼 및 요구 사항

## <a name="what-is-native-scoring-and-how-is-it-different-from-real-time-scoring"></a>네이티브 점수 매기기는 것이 무엇이 고 어떻게 다른가요 실시간 점수 매기기 있습니까?

Microsoft은 SQL Server 2016에서 T-SQL에서 실행할 R 스크립트를 허용 하는 확장성 프레임 워크를 만들었습니다. 이 프레임 워크는 간단한 함수에서 교육 복잡 한 기계 학습 모델에 이르기까지 R에서 수행할 수 있는 모든 작업을 지원 합니다. 그러나 이중 프로세스 아키텍처 작업의 복잡성에 관계 없이 모든 호출에 대해 외부 R 프로세스를 호출 해야 합니다. 테이블 및 SQL Server에 이미 있는 데이터에 대 한 점수 매기기에서 미리 학습 된 모델을 로드 하는 경우 외부 R 프로세스를 호출 하는 오버 헤드는 불필요 한 성능 비용을 나타냅니다.

_점수 매기기_ 은 두 단계로 이루어집니다. 먼저 테이블에서 로드 하려면 미리 학습 된 모델을 지정 합니다. 둘째, 새 패스 입력 예측 값을 생성 하는 함수, 데이터 (또는 _점수_). 입력 테이블 또는 단일 행을 수 있습니다. 확률을 나타내는 단일 열 값을 출력 하도록 선택할 수 있습니다 또는 신뢰 구간, 오류 또는 기타 유용한 보수 하 여 예측과 같은 여러 값을 출력할 수 있습니다.

입력 데이터 행 수를 포함 하는 경우 것이 일반적으로 더 빠릅니다 점수 매기기 프로세스의 일부로 테이블에 예측 값을 삽입 합니다.  단일 점수를 생성 하는 것이 더 일반적 시나리오는 폼 또는 사용자 요청에서 입력된 값을 얻으려면 하 고 클라이언트 응용 프로그램에는 점수를 반환 합니다. 연속 된 점수를 생성 하는 경우 성능 향상을 위해 SQL Server 메모리로 다시 로드 될 수 있도록 모델을 캐시 될 수 있습니다.

빠른 점수 매기기를 지원 하려면 SQL Server Machine Learning 서비스 (및 Microsoft Machine Learning Server) 또는 T-SQL의 R에서 작동 하는 기본 점수 매기기 라이브러리를 제공 합니다. 버전에 따라 다른 옵션이 있습니다.

**네이티브 점수 매기기**

+ TRANSACT-SQL의 PREDICT 함수는 지원 _네이티브 점수 매기기_ SQL Server 2017의 모든 인스턴스에서 합니다. T-SQL을 사용 하 여 호출할 수 있는 모델 학습 이미 있다고만 필요 합니다. T-SQL을 사용 하 여 네이티브 점수 매기기 이러한 이점이 있습니다.

    + 추가적인 서버 구성은 필요하지 않습니다.
    + R 런타임을 호출 되지 않습니다. R을 설치 하지 않아도

**실시간 점수 매기기**

+ **sp_rxPredict** R 런타임을 호출 하지 않고 모든 지원 되는 모델 형식에서 점수를 생성 실시간 점수 매기기에 사용 될 수 있는 저장된 프로시저입니다.

  이 저장된 프로시저도 Microsoft R server 독립 실행형 설치 관리자를 사용 하 여 R 구성 요소를 업그레이드 하는 경우 SQL Server 2016에서 제공 됩니다. SQL Server 2017 sp_rxPredict 에서도 지원 됩니다. 따라서 없습니다 PREDICT 함수 모델 유형을 사용 하 여 점수를 생성할 때이 함수를 사용할 수 있습니다.

+ R 코드 내에서 빠른 점수를 매기기 위해 rxPredict 함수를 사용할 수 있습니다.

모든 이러한 점수 매기기 방법에 대해 지원 되는 RevoScaleR 또는 MicrosoftML 알고리즘 중 하나를 사용 하 여 학습 된 모델을 사용 해야 합니다.

작업에서 실시간 점수 매기기의 예제를 참조 하세요. [종단 간 최종 대출 상각 예측 빌드를 사용 하 여 Azure HDInsight Spark 클러스터 및 SQL Server 2016 R 서비스](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

## <a name="how-native-scoring-works"></a>어떻게 네이티브 점수 매기기 작업

네이티브 점수 매기기 모델에서 특수 이진 형식을 읽고 수 점수를 생성 하는 Microsoft에서 네이티브 c + + 라이브러리를 사용 합니다. 모델을 게시 하 고 R 인터프리터를 호출 하지 않고도 점수 매기기에 사용 되는 수, 때문에 여러 프로세스 상호 작용의 오버 헤드가 줄었습니다. 따라서 네이티브 점수 매기기 엔터프라이즈 프로덕션 시나리오에서 성능이 더 빠른 예측을 지원합니다.

이 라이브러리를 사용 하 여 점수를 생성 하려면 점수 매기기 함수를 호출 하 고 다음 필요한 입력을 전달 합니다.

+ 호환 되는 모델입니다. 참조 된 [요구 사항](#Requirements) 세부 정보에 대 한 섹션입니다.
+ 입력된 데이터를 일반적으로 SQL 쿼리로 정의

함수를 통해 전달 하려는 원본 데이터의 열과 함께 입력된 데이터에 대 한 예측을 반환 합니다.

필요한 이진 형식으로 모델을 준비 하는 방법에 대 한 지침과 함께 코드 샘플에 대 한이 문서를 참조 하세요.

+ [실시간 점수 매기기를 수행 하는 방법](r/how-to-do-realtime-scoring.md)

네이티브 점수 매기기를 포함 하는 완벽 한 솔루션, SQL Server 개발 팀에서 이러한 샘플을 참조 하세요.

+ 기계 학습 스크립트를 배포 합니다. [Python 모델을 사용 하 여](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ 기계 학습 스크립트를 배포 합니다. [R 모델을 사용 하 여](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)

## <a name="requirements"></a>요구 사항

지원 되는 플랫폼은 다음과 같습니다.

+ SQL Server 2017 Machine Learning Services (Microsoft R Server 9.1.0 포함)
    
    네이티브 점수 매기기 예측을 사용 하 여 SQL Server 2017이 필요 합니다.
    Linux를 포함 하 여 SQL Server 2017의 모든 버전에서 작동 합니다.

    또한 실시간 sp_rxPredict를 사용 하 여 점수 매기기을 수행할 수 있습니다. 이 저장된 프로시저를 사용 하려면 사용할 수 있도록 [SQL Server CLR 통합](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration)합니다.

+ SQL Server 2016

   사용 하 여 점수 매기기 실시간 sp_rxPredict 보다 SQL Server 2016 및 Microsoft R Server에서 실행할 수도 있습니다. 이 옵션을 사용할 SQLCLR 및 Microsoft R Server 업그레이드를 설치 하는 필요 합니다.
   자세한 내용은 참조 하세요. [실시간 점수 매기기](Real-time-scoring.md)

### <a name="model-preparation"></a>모델 준비

+ 사전에 지원 되는 중 하나를 사용 하 여 모델을 학습 해야 합니다 **rx** 알고리즘입니다. 자세한 내용은 참조 하세요 [알고리즘을 지원](#bkmk_native_supported_algos)합니다.
+ Microsoft R Server 9.1.0에서에서 제공 되는 새 serialization 함수를 사용 하 여 모델을 저장 해야 합니다. Serialization 함수는 빠른 점수 매기기를 지원 하도록 최적화 됩니다.

### <a name="bkmk_native_supported_algos"></a> 네이티브 점수 매기기를 지 원하는 알고리즘

+ RevoScaleR 모델

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

MicrosoftML에서 모델을 사용 하는 경우 sp_rxPredict를 사용 하 여 실시간 점수 매기기를 사용 합니다.

### <a name="restrictions"></a>Restrictions

모델은 지원 되지 않습니다.

+ 지원 되지 않는 유형의 R 변환 포함 하는 모델
+ 사용 하 여 모델을 `rxGlm` 또는 `rxNaiveBayes` RevoScaleR의 알고리즘
+ PMML 모델
+ CRAN 또는 다른 저장소에서 다른 R 라이브러리를 사용 하 여 만든 모델
+ 다른 R 변환을 포함 하는 모델

## <a name="see-also"></a>참고자료

[실시간 SQL Server machine learning에서 점수 매기기 ](real-time-scoring.md)