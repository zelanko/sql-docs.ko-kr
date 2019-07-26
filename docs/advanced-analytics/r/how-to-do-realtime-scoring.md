---
title: 기계 학습 모델을 사용 하 여 예측 및 예측 생성
description: RxPredict 또는 sp_rxPredict를 사용 하 여 실시간 점수 매기기를 사용 하거나, SQL Server Machine Learning에서 R 및 Pythin의 예측 및 예측에 대 한 네이티브 점수 매기기를 위한 T-sql을 예측 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 39edb40da1ebbddfff805aca321b99ea766f085c
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470121"
---
# <a name="how-to-generate-forecasts-and-predictions-using-machine-learning-models-in-sql-server"></a>SQL Server에서 기계 학습 모델을 사용 하 여 예측 및 예측을 생성 하는 방법
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

기존 모델을 사용 하 여 새 데이터 입력에 대 한 결과를 예측 또는 예측 하는 것은 기계 학습의 핵심 작업입니다. 이 문서에서는 SQL Server에서 예측을 생성 하는 방법을 열거 합니다. 이러한 방법 중 하나는 고속 예측에 대 한 내부 처리 방법입니다. 여기서 속도는 런타임 종속성의 증분 축소를 기반으로 합니다. 종속성이 적을수록 더 빠른 예측을 의미 합니다.

내부 처리 인프라 (실시간 또는 원시 점수 매기기)를 사용 하는 경우 라이브러리 요구 사항이 적용 됩니다. 함수는 Microsoft 라이브러리에서 가져와야 합니다. CLR 또는 C++ 확장에서는 오픈 소스 또는 타사 함수를 호출 하는 R 또는 Python 코드가 지원 되지 않습니다.

다음 표에서는 예측 및 예측에 대 한 점수 매기기 프레임 워크를 요약 합니다. 

| 방법           | 인터페이스         | 라이브러리 요구 사항 | 처리 속도 |
|-----------------------|-------------------|----------------------|----------------------|
| 확장성 프레임워크 | [rxPredict (R)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) <br/>[rx_predict (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | 없음 모델은 R 또는 Python 함수를 기반으로 할 수 있습니다. | 수백 밀리초. <br/>런타임 환경 로드에는 새 데이터 점수가 계산 되기 전에 3 ~ 600 밀리초의 고정 비용이 있습니다. |
| [실시간 점수 매기기 CLR 확장](../real-time-scoring.md) | 직렬화 된 모델의 [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) | R: RevoScaleR, MicrosoftML <br/>Python: revoscalepy, microsoftml | 수십 밀리초 (평균)입니다. |
| [네이티브 점수 C++ 매기기 확장](../sql-native-scoring.md) | 직렬화 된 모델에서 [t-sql 함수 예측](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) | R: RevoScaleR <br/>Python: revoscalepy | 평균적으로 20 밀리초 미만입니다. | 

처리 속도는 차별화 기능입니다. 동일한 함수 및 입력을 가정 하 여 점수가 매겨진 출력은 사용 하는 방법에 따라 달라 지지 않습니다.

모델은 지원 되는 함수를 사용 하 여 생성 된 다음 디스크에 저장 된 원시 바이트 스트림으로 serialize 되거나 데이터베이스에 이진 형식으로 저장 되어야 합니다. 저장 프로시저 또는 T-sql을 사용 하 여 R 또는 Python 언어 런타임에 대 한 오버 헤드 없이 이진 모델을 로드 하 고 사용 하 여 새 입력에 대 한 예측 점수를 생성할 때 완료 하는 데 걸리는 시간을 단축할 수 있습니다.

CLR 및 C++ 확장의 의미는 데이터베이스 엔진 자체에 근접 합니다. 데이터베이스 엔진의 네이티브 언어는 이며, C++이는에서 C++ 작성 된 확장이 더 낮은 종속성으로 실행 되는 것을 의미 합니다. 반면, CLR 확장은 .NET Core에 종속 됩니다. 

짐작할 수 있듯이 플랫폼 지원은 이러한 런타임 환경의 영향을 받습니다. 네이티브 데이터베이스 엔진 확장은 관계형 데이터베이스가 지원 되는 모든 위치에서 실행 됩니다. Windows, Linux, Azure. .NET Core 요구 사항이 포함 된 CLR 확장은 현재 Windows 전용입니다.

## <a name="scoring-overview"></a>점수 매기기 개요

_점수 매기기_ 는 2 단계 프로세스입니다. 먼저 테이블에서 로드할 이미 학습 된 모델을 지정 합니다. 그런 다음 함수에 새 입력 데이터를 전달 하 여 예측 값 (또는 _점수_)을 생성 합니다. 입력은 종종 테이블 형식 또는 단일 행을 반환 하는 T-sql 쿼리입니다. 확률을 나타내는 단일 열 값을 출력 하도록 선택 하거나 신뢰 간격, 오류 또는 예측에 대 한 기타 유용한 보충 등의 여러 값을 출력할 수 있습니다.

다시 한 번 수행 하면 모델을 준비한 다음 점수를 생성 하는 전체 프로세스를 이러한 방식으로 요약할 수 있습니다.

1. 지원 되는 알고리즘을 사용 하 여 모델을 만듭니다. 지원은 선택 하는 점수 매기기 방법에 따라 달라 집니다.
2. 모델을 학습 합니다.
3. 특수 이진 형식을 사용 하 여 모델을 직렬화 합니다.
3. 모델을 SQL Server에 저장 합니다. 일반적으로이는 serialize 된 모델을 SQL Server 테이블에 저장 하는 것을 의미 합니다.
4. 모델 및 데이터 입력을 매개 변수로 지정 하 여 함수 또는 저장 프로시저를 호출 합니다.

입력에 많은 데이터 행이 포함 된 경우 일반적으로 점수 매기기 프로세스의 일부로 예측 값을 테이블에 삽입 하는 것이 더 빠릅니다. 폼 이나 사용자 요청에서 입력 값을 가져오고 클라이언트 응용 프로그램에 점수를 반환 하는 시나리오에서는 단일 점수를 생성 하는 것이 더 일반적입니다. 연속 점수를 생성할 때 성능을 향상 시키려면 SQL Server 하 여 메모리에 다시 로드할 수 있도록 모델을 캐시할 수 있습니다.

## <a name="compare-methods"></a>메서드 비교

핵심 데이터베이스 엔진 프로세스의 무결성을 유지 하기 위해 RDBMS 처리에서 언어 처리를 격리 하는 이중 아키텍처에서 R 및 Python에 대 한 지원을 사용할 수 있습니다. SQL Server 2016부터 Microsoft는 T-sql에서 R 스크립트를 실행할 수 있도록 하는 확장성 프레임 워크를 추가 했습니다. SQL Server 2017에서는 Python 통합이 추가 되었습니다. 

확장성 프레임 워크는 간단한 함수에서 복잡 한 기계 학습 모델을 학습 하는 것에 이르기까지 R 또는 Python에서 수행할 수 있는 모든 작업을 지원 합니다. 그러나 이중 프로세스 아키텍처에서는 작업의 복잡성에 관계 없이 모든 호출에 대해 외부 R 또는 Python 프로세스를 호출 해야 합니다. 워크 로드가 테이블에서 미리 학습 된 모델을 로드 하 고 이미 SQL Server에 있는 데이터에 대해 점수를 매기는 경우 외부 프로세스를 호출 하는 오버 헤드로 인해 특정 상황에서 허용할 수 없는 대기 시간이 추가 됩니다. 예를 들어 사기 감지에는 신속 하 게 관련 된 점수가 필요 합니다.

사기 감지와 같은 시나리오의 점수 매기기 속도를 높이기 위해 기본 제공 되는 점수 매기기 C++ 라이브러리와 함께 R 및 Python 시작 프로세스의 오버 헤드를 제거 하는 CLR 확장을 추가 SQL Server.

[**실시간 점수 매기기**](../real-time-scoring.md) 는 고성능 점수 매기기를 위한 첫 번째 솔루션 이었습니다. SQL Server 2017 이전 버전의에서 도입 된 SQL Server 2016 업데이트에 대 한 실시간 점수 매기기는 RevoScaleR, MicrosoftML (R), revoscalepy 및의 Microsoft 제어 함수를 통해 R 및 Python을 처리 하는 CLR 라이브러리에 의존 합니다. microsoftml (Python). **Sp_rxPredict** 저장 프로시저를 사용 하 여 R 또는 Python 런타임을 호출 하지 않고 모든 지원 되는 모델 형식에서 점수를 생성 하는 CLR 라이브러리를 호출 합니다.

[**네이티브 점수 매기기**](../sql-native-scoring.md) 는 네이티브 C++ 라이브러리로 구현 되는 SQL Server 2017 기능이 며 RevoScaleR 및 revoscalepy 모델에만 사용할 수 있습니다. 가장 빠르고 안전한 방법 이지만 다른 방법론을 기준으로 더 작은 함수 집합을 지원 합니다.

## <a name="choose-a-scoring-method"></a>점수 매기기 방법 선택

플랫폼 요구 사항에 따라 사용 해야 하는 점수 매기기 방법이 결정 되는 경우가 많습니다.

| 제품 버전 및 플랫폼 | 방법 |
|------------------------------|-------------|
| Windows, SQL Server 2017 Linux 및 Azure SQL Database SQL Server 2017 | T-sql PREDICT를 사용 하는 **기본 점수 매기기** |
| SQL Server 2017 (Windows에만 해당), SQL Server 2016 R 서비스 SP1 이상 | Sp\_rxpredict 저장 프로시저를 사용 하 여 **실시간 점수 매기기** |

PREDICT 함수를 사용 하는 기본 점수 매기기를 사용 하는 것이 좋습니다. Sp\_rxpredict를 사용 하려면 SQLCLR 통합을 사용 하도록 설정 해야 합니다. 이 옵션을 사용 하도록 설정 하기 전에 보안 문제를 고려해 야 합니다.

## <a name="serialization-and-storage"></a>Serialization 및 저장소

빠른 점수 매기기 옵션 중 하나를 사용 하 여 모델을 사용 하려면 크기 및 점수 매기기 효율성을 위해 최적화 된 특수 한 직렬화 된 형식을 사용 하 여 모델을 저장 합니다.

+ [RxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) 를 호출 하 여 지원 되는 모델을 **원시** 형식으로 작성 합니다.
+ [RxUnserializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)를 호출 하 여 다른 R 코드에서 사용할 모델을 다시 구성할 수 있습니다. 또는 모델을 볼 수 있습니다.

**SQL 사용**

SQL 코드에서 [sp_execute_external_script](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)를 사용 하 여 모델을 학습 하 고, **varbinary (max)** 형식의 열에 학습 된 모델을 테이블에 직접 삽입할 수 있습니다. 간단한 예제는 [R에서 preditive 모델 만들기](../tutorials/rtsql-create-a-predictive-model-r.md) 를 참조 하세요.

**R 사용**

R 코드에서 RevoScaleR 패키지의 [rxWriteObject](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxwriteobject) 함수를 호출 하 여 모델을 데이터베이스에 직접 기록 합니다. **RxWriteObject ()** 함수는 SQL SERVER 같은 ODBC 데이터 원본에서 R 개체를 검색 하거나 SQL Server에 개체를 쓸 수 있습니다. API는 간단한 키-값 저장소 다음에 모델링 됩니다.
  
이 함수를 사용 하는 경우 먼저 [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) 를 사용 하 여 모델을 serialize 해야 합니다. 그런 다음 직렬화 단계를 반복 하지 않도록 **rxWriteObject** 의 *SERIALIZE* 인수를 FALSE로 설정 합니다.

모델을 이진 형식으로 serialize 하는 것이 유용 하지만, 확장성 프레임 워크에서 R 및 Python 런타임 환경을 사용 하 여 예측 점수를 매기는 경우에는 필요 하지 않습니다. 모델을 원시 바이트 형식으로 파일에 저장 한 다음 파일에서 SQL Server으로 읽을 수 있습니다. 이 옵션은 환경 간에 모델을 이동 하거나 복사 하는 경우에 유용할 수 있습니다.

## <a name="scoring-in-related-products"></a>관련 제품의 점수 매기기

[독립 실행형 서버](r-server-standalone.md) 또는 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)를 사용 하는 경우 예측을 신속 하 게 생성 하기 위해 저장 프로시저 및 t-sql 함수 외에 다른 옵션을 사용할 수 있습니다. 독립 실행형 서버와 Machine Learning Server는 모두 코드 배포를 위한 *웹 서비스* 의 개념을 지원 합니다. R 또는 Python 미리 학습 된 모델을 런타임에 호출 하 여 새 데이터 입력을 평가 하는 웹 서비스로 묶을 수 있습니다. 자세한 내용은 다음 문서를 참조하세요.

+ [Machine Learning Server 웹 서비스는 무엇 인가요?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [운영 화 란?](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)
+ [Azureml-모델-sdk를 사용 하 여 Python 모델을 웹 서비스로 배포](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [새 웹 서비스로 R 코드 블록 또는 실시간 모델 게시](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [R에 대 한 mrsdeploy 패키지](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)


## <a name="see-also"></a>참조

+ [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)  
+ [rxRealTimeScoring](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxrealtimescoring)
+ [sp-rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)
+ [T-SQL 예측](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)