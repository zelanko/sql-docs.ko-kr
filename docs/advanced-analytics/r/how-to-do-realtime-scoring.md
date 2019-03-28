---
title: 예측 및 기계 학습 모델-SQL Server Machine Learning Services를 사용 하 여 예측을 생성 합니다.
description: 기본 예측 점수 매기기 및 R 및 SQL Server Machine Learning에서 Pythin 예측에 대 한 실시간 점수 매기기 또는 예측 T-SQL rxPredict, 또는 sp_rxPredict를 사용 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 001b90eafd26c90f730e5647f0dc62d756ca9d1b
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510090"
---
# <a name="how-to-generate-forecasts-and-predictions-using-machine-learning-models-in-sql-server"></a>예측 및 SQL Server에서 기계 학습 모델을 사용 하 여 예측을 생성 하는 방법
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

기존 모델을 사용 하 여 예측 또는 새 데이터 입력에 대 한 결과 예측할 기계 학습의 핵심 작업입니다. 이 문서에서는 SQL Server에서 예측을 생성 하는 방법을 열거 합니다. 접근 방식 간의 내부 처리 방법론 속도의 증분을 줄이는 것은 기반 고속 예측에 대해 실행 됩니다 시간 종속성. 더 빠른 예측이 더 적은 종속성을 의미합니다.

내부 처리 인프라를 사용 하 여 라이브러리 요구 사항 함께 제공 됩니다 (실시간 또는 네이티브 점수 매기기). Microsoft 라이브러리의 함수 여야 합니다. 오픈 소스 또는 타사 함수를 호출 하는 R 또는 Python 코드는 CLR 또는 c + + 확장에서 지원 되지 않습니다.

다음 표에서 예측 및 예측에 대 한 점수 매기기 프레임 워크를 보여 줍니다. 

| 방법           | 인터페이스         | 라이브러리 요구 사항 | 처리 속도 |
|-----------------------|-------------------|----------------------|----------------------|
| 확장성 프레임워크 | [rxPredict (R)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) <br/>[rx_predict (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | 없음 모델 기반으로 모든 R 또는 Python 함수 | 수백 밀리초입니다. <br/>로드 된 런타임 환경에 새 데이터 점수를 매길 전에 3부터 6 백 밀리초 평균 고정된 비용. |
| [실시간 점수 매기기 CLR 확장](../real-time-scoring.md) | [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) 직렬화 된 모델 | R: RevoScaleR, MicrosoftML <br/>Python: revoscalepy를 microsoftml | 평균 시간 (밀리초)을 수만 있습니다. |
| [네이티브 점수 매기기 c + + 확장](../sql-native-scoring.md) | [예측 T-SQL 함수](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) 직렬화 된 모델 | R: RevoScaleR <br/>Python: revoscalepy | 평균적으로 20 밀리초입니다. | 

처리 속도 출력의 물질 하지 차별화 기능입니다. 동일한 기능 및 입력을 가정 하지 점수가 매겨진된 출력 해야 사용 하는 방법에 따라 다릅니다.

모델을 지원 되는 함수를 사용 하 여 만든 다음 디스크에 저장 하거나 데이터베이스에 이진 형식으로 저장 하는 원시 바이트 스트림으로 serialize 될 해야 합니다. 저장된 프로시저 또는 T-SQL을 사용 하 여 로드 하 고는 R 또는 Python을 실행 하는 언어 시간 오버 헤드 없이 이진 모델을 사용 하 여 더 빠르게 완료 될 때까지 새 입력에 대 한 예측 점수를 생성할 때 발생 합니다.

CLR 및 c + + 확장의 중요 한 이유는 자체 데이터베이스 엔진에 근접 합니다. 데이터베이스 엔진의 기본 언어는 c + +, 더 적은 종속성을 사용 하 여 실행 하는 c + +로 작성 된 확장을 의미 합니다. 반면 CLR 확장.NET Core에 따라 달라 집니다. 

예상할 수 있듯이 이러한 런타임 환경에서 지원 되는 플랫폼 저하 됩니다. 네이티브 데이터베이스 엔진 확장 관계형 데이터베이스는 어디서 나 실행: Windows, Linux, Azure. .NET Core 필요가 있는 CLR 확장은 현재 Windows만 있습니다.

## <a name="scoring-overview"></a>점수 매기기 개요

_점수 매기기_ 은 두 단계로 이루어집니다. 먼저 테이블에서 로드를 이미 학습 된 모델을 지정 합니다. 둘째, 새 패스 입력 예측 값을 생성 하는 함수, 데이터 (또는 _점수_). 입력은 테이블 형식 또는 단일 행을 반환 하는 T-SQL 쿼리 경우가 많습니다. 확률을 나타내는 단일 열 값을 출력 하도록 선택할 수 있습니다 또는 신뢰 구간, 오류 또는 기타 유용한 보수 하 여 예측과 같은 여러 값을 출력할 수 있습니다.

단계를 수행 합니다. 모델을 준비 하는 전체 프로세스 하 고 점수를 생성 한 다음 요약할 수 있습니다. 이러한 방식으로:

1. 지원 되는 알고리즘을 사용 하 여 모델을 만듭니다. 지원은 선택 하면 점수 매기기 방법에 따라 다릅니다.
2. 모델을 학습 합니다.
3. 특수 이진 형식을 사용 하 여 모델을 serialize 합니다.
3. SQL Server로 모델을 저장 합니다. 일반적으로 즉, SQL Server 테이블에 직렬화 된 모델을 저장 합니다.
4. 함수 또는 모델 및 데이터 입력을 매개 변수로 지정 하는 저장된 프로시저를 호출 합니다.

입력 데이터 행 수를 포함 하는 경우 것이 일반적으로 더 빠릅니다 점수 매기기 프로세스의 일부로 테이블에 예측 값을 삽입 합니다. 단일 점수를 생성 하는 것이 더 일반적 시나리오는 폼 또는 사용자 요청에서 입력된 값을 얻으려면 하 고 클라이언트 응용 프로그램에는 점수를 반환 합니다. 연속 된 점수를 생성 하는 경우 성능 향상을 위해 SQL Server 메모리로 다시 로드 될 수 있도록 모델을 캐시 될 수 있습니다.

## <a name="compare-methods"></a>메서드를 비교 합니다.

핵심 데이터베이스 엔진 프로세스의 무결성을 유지 하려면 R 및 Python 지원이 RDBMS 처리에서 언어 처리를 분리 하는 이중 아키텍처에서 설정 됩니다. Microsoft은 SQL Server 2016부터 T-SQL에서 실행할 R 스크립트를 허용 하는 확장성 프레임 워크를 추가 합니다. SQL Server 2017의 Python 통합이 추가 되었습니다. 

확장성 프레임 워크는 R 또는 Python에서 간단한 함수에서 교육 복잡 한 기계 학습 모델에 이르기까지에서 수행할 수 있는 모든 작업을 지원 합니다. 그러나 이중 프로세스 아키텍처 작업의 복잡성에 관계 없이 모든 호출에 대해 외부 R 또는 Python 프로세스를 호출 해야 합니다. 테이블에서 미리 학습 된 모델을 로드 하 고 SQL Server에 이미 있는 데이터에 대 한 점수 매기기 작업에 수반 되는 경우 외부 프로세스를 호출 하는 오버 헤드는 특정 상황에서 사용할 수 있는 대기 시간을 추가 합니다. 예를 들어 사기 감지에 관련 되도록 빠른 점수 매기기 필요 합니다.

사기 감지 시나리오에 대 한 점수 매기기 속도 높이려면 SQL Server는 R 및 Python 시작 프로세스의 오버 헤드를 제거 하는 c + + 및 CLR 확장으로 기본 점수 매기기 라이브러리를 추가 합니다.

[**실시간 점수 매기기** ](../real-time-scoring.md) 고성능 점수 매기기에 대 한 첫 번째 솔루션 이었습니다. R 및 Python RevoScaleR, MicrosoftML (R), revoscalepy를 Microsoft 제어 함수 처리는 CLR 라이브러리에 의존 실시간 점수 매기기 초기 버전의 SQL Server 2017 및 이후 업데이트에서는 SQL Server 2016에 도입 하 고 microsoftml (Python)입니다. CLR 라이브러리를 사용 하 여 호출 되는 **sp_rxPredict** 저장된 프로시저를 R 또는 Python 런타임을 호출 하지 않고도 모든 지원 되는 모델 형식에서 점수를 생성 합니다.

[**네이티브 점수 매기기** ](../sql-native-scoring.md) 는 SQL Server 2017 기능을 네이티브 c + + 라이브러리로 하지만 RevoScaleR 및 revoscalepy 모델에 대해서만 구현 합니다. 빠르고 보다 안전한 방법은 하지만 더 작은 다른 방법론을 기준으로 하는 함수 집합을 지원 합니다.

## <a name="choose-a-scoring-method"></a>점수 매기기 방법 선택

플랫폼 요구 사항에는 종종는 점수 매기기 방법입니다.

| 제품 버전 및 플랫폼 | 방법 |
|------------------------------|-------------|
| Windows, SQL Server 2017 Linux 및 Azure SQL Database의 SQL Server 2017 | **네이티브 점수 매기기** 사용 하 여 T-SQL 예측 |
| SQL Server 2017 (Windows에만 해당), SQL Server 2016 R Services sp1 이상 | **실시간 점수 매기기** sp\_rxPredict 저장 프로시저 |

PREDICT 함수를 사용 하 여 네이티브 점수 매기기는 것이 좋습니다. Sp를 사용 하 여\_rxPredict SQLCLR 통합을 사용 해야 합니다. 이 옵션을 사용 하기 전에 보안 문제를 고려 합니다.

## <a name="serialization-and-storage"></a>Serialization 및 저장소

빠른 점수 매기기 옵션 중 하나를 사용 하 여 모델을 사용 하려면 크기에 대 한 최적화 된 특수 한 serialize 된 형식을 사용 하 여 및 효율성을 점수 매기기 모델을 저장 합니다.

+ 호출 [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) 지원 되는 모델을 작성 하는 **원시** 형식입니다.
+ 호출 [rxUnserializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)' 다른 R 코드에서 사용 하 여 모델을 다시 구성 하기 위해 또는 모델을 표시 합니다.

**SQL을 사용 하 여**

사용 하 여 모델 학습 수 SQL 코드에서 [sp_execute_external_script](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)에서 직접 학습된 된 모델에 테이블 형식의 열을 삽입할 **varbinary (max)** 합니다. 간단한 예제를 보려면 [R에서 preditive 모델 만들기](../tutorials/rtsql-create-a-predictive-model-r.md)

**R을 사용 하 여**

R 코드에서 호출 된 [rxWriteObject](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxwriteobject) 모델 데이터베이스에 직접 쓸 RevoScaleR 패키지의 함수입니다. 합니다 **rxWriteObject()** 함수 SQL Server와 같은 ODBC 데이터 소스에서 R 개체를 검색 또는 SQL Server 개체를 쓸 수 있습니다. API는 간단한 키-값 저장소를 따라 모델링 됩니다.
  
이 함수를 사용 하는 경우 반드시 사용 하 여 모델 serialize [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) 첫 번째입니다. 그런 다음 설정 합니다 *serialize* 에서 인수 **rxWriteObject** serialization 단계를 반복 하지 않으려면 FALSE로 합니다.

이진 형식으로 모델을 직렬화 하는 것은 유용 하지만 R을 사용 하 여 예측의 점수를 매기는 경우 및 Python 확장성 프레임 워크에서 런타임 환경 실행 해야 하는 아닙니다. Raw 바이트 형식으로 파일에 모델을 저장할 수 있으며 그런 다음 SQL Server에 파일에서 읽을 수 있습니다. 이동 하거나 환경 간에 모델을 복사 하는 경우에이 옵션이 유용할 수 있습니다.

## <a name="scoring-in-related-products"></a>관련된 제품에서 점수 매기기

사용 중인 경우는 [독립 실행형 서버](r-server-standalone.md) 또는 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), 저장된 프로시저 및 예측을 신속 하 게 생성 하기 위한 T-SQL 함수 외에 다른 옵션이 있습니다. 독립 실행형 서버 및 Machine Learning Server 지원의 개념을 *웹 서비스* 코드 배포에 대 한 합니다. 번들로 R 또는 Python 미리 학습 된 모델을 웹 서비스로 새 데이터 입력을 평가 하려면 런타임에 호출 합니다. 자세한 내용은 다음 문서를 참조하세요.

+ [Machine Learning Server에 웹 서비스는 무엇입니까?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [운영 화 란?](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)
+ [Python 모델 azureml 모델-관리 sdk를 사용 하 여 웹 서비스로 배포](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [R 코드 블록 또는 실시간 모델을 새 웹 서비스로 게시](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [R에 대 한 mrsdeploy 패키지](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)


## <a name="see-also"></a>참고자료

+ [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)  
+ [rxRealTimeScoring](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxrealtimescoring)
+ [sp-rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)
+ [T-SQL을 예측 합니다.](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)