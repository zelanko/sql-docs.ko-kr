---
title: 예측 생성
description: 실시간 채점에 rxPredict 또는 sp_rxPredict를 사용하거나, SQL Server Machine Learning에서 R 및 Python의 예측에 대한 네이티브 채점에 T-SQL을 사용합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/30/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3f431d1598038d0789579697fccbaeffe5ef1fd0
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487842"
---
# <a name="how-to-generate-forecasts-and-predictions-using-machine-learning-models-in-sql-server"></a>SQL Server에서 기계 학습 모델을 사용하여 예측을 생성하는 방법
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

기존 모델을 사용하여 새 데이터 입력의 결과를 예측하는 것은 기계 학습의 핵심 작업입니다. 이 문서에서는 SQL Server에서 예측을 생성하는 방법을 열거합니다. 이 방법 중 하나로 고속 예측을 위한 내부 처리 방법이 있습니다. 여기서 속도는 런타임 종속성의 증분 감소를 기반으로 합니다. 종속성이 적을수록 더 빠르게 예측됩니다.

내부 처리 인프라(실시간 또는 네이티브 채점)를 사용하려면 라이브러리 요구 사항이 적용됩니다. 함수는 Microsoft 라이브러리에서 가져와야 합니다. 오픈 소스 또는 타사 함수를 호출하는 R 또는 Python 코드는 CLR 또는 C++ 확장에서 지원되지 않습니다.

다음 표에서는 예측을 위한 채점 프레임워크를 요약합니다. 

| 방법           | 인터페이스         | 라이브러리 요구 사항 | 처리 속도 |
|-----------------------|-------------------|----------------------|----------------------|
| 확장성 프레임워크 | [rxPredict(R)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) <br/>[rx_predict(Python)](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | 없음 모델은 R 또는 Python 함수를 기반으로 할 수 있음 | 수백 밀리초. <br/>런타임 환경 로드에는 새 데이터가 채점되기 전에 평균 300~600밀리초의 고정 비용이 있습니다. |
| [실시간 채점 CLR 확장](../real-time-scoring.md) | 직렬화된 모델의 [sp_rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) | R: RevoScaleR, MicrosoftML <br/>Python: revoscalepy, microsoftml | 평균 수십 밀리초. |
| [네이티브 채점 C++ 확장](../sql-native-scoring.md) | 직렬화된 모델의 [PREDICT T-SQL 함수](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) | R: RevoScaleR <br/>Python: revoscalepy | 평균 20밀리초 미만. | 

차별화 기능은 출력 자체가 아니라 처리 속도입니다. 동일한 함수 및 입력을 가정할 경우 사용하는 방법에 따라 채점된 출력이 달라지지 않아야 합니다.

모델은 지원되는 함수를 사용하여 생성된 후 디스크에 저장된 원시 바이트 스트림으로 직렬화되거나 데이터베이스에 이진 형식으로 저장됩니다. 저장 프로시저 또는 T-SQL을 사용하면 R 또는 Python 언어 런타임의 오버헤드 없이 이진 모델을 로드하고 사용할 수 있으므로 새 입력에 대한 예측 점수를 생성할 때 완료 시간이 단축됩니다.

CLR 및 C++ 확장의 significance는 데이터베이스 엔진 자체에 근접합니다. 데이터베이스 엔진의 네이티브 언어는 C++입니다. 즉, C++로 작성된 확장은 더 낮은 종속성으로 실행됩니다. 반면, CLR 확장은 .NET Core를 사용합니다. 

예상하는 대로 플랫폼 지원은 이 런타임 환경의 영향을 받습니다. 네이티브 데이터베이스 엔진 확장은 관계형 데이터베이스가 지원되는 모든 위치에서 실행됩니다. Windows, Linux, Azure. .NET Core 요구 사항이 포함된 CLR 확장은 현재 Windows 전용입니다.

## <a name="scoring-overview"></a>채점 개요

_채점_은 2단계 프로세스입니다. 먼저 테이블에서 로드할 이미 학습된 모델을 지정합니다. 그런 다음, 함수에 새 입력 데이터를 전달하여 예측 값(또는 _점수_)를 생성합니다. 입력은 일반적으로 테이블 형식 또는 단일 행을 반환하는 T-SQL 쿼리입니다. 확률을 나타내는 단일 열 값을 출력하도록 선택하거나, 예측에 대한 신뢰 구간, 오류 또는 기타 유용한 보충 항목과 같은 여러 값을 출력할 수 있습니다.

모델을 준비한 후 점수를 생성하는 전체 프로세스는 다음과 같이 요약될 수 있습니다.

1. 지원되는 알고리즘을 사용하여 모델을 만듭니다. 지원은 선택하는 채점 방법에 따라 달라집니다.
2. 모델을 학습시킵니다.
3. 특수 이진 형식을 사용하여 모델을 직렬화합니다.
3. SQL Server에 모델을 저장합니다. 일반적으로 이는 직렬화된 모델을 SQL Server 테이블에 저장하는 것을 의미합니다.
4. 함수 또는 저장 프로시저를 호출하여 모델 및 데이터 입력을 매개 변수로 지정합니다.

입력에 많은 데이터 행이 포함된 경우 일반적으로 채점 프로세스의 일부로 예측 값을 테이블에 삽입하는 것이 더 빠릅니다. 양식 또는 사용자 요청에서 입력 값을 가져오고 클라이언트 애플리케이션에 점수를 반환하는 시나리오에서는 단일 점수를 생성하는 것이 더 일반적입니다. 연속 점수를 생성할 때 성능을 개선하기 위해 모델이 메모리에 다시 로드될 수 있도록 SQL Server가 모델을 캐시할 수 있습니다.

## <a name="compare-methods"></a>방법 비교

핵심 데이터베이스 엔진 프로세스의 무결성을 유지하기 위해 RDBMS 처리로부터 언어 처리를 격리하는 이중 아키텍처에서 R 및 Python 지원을 사용할 수 있습니다. SQL Server 2016부터 Microsoft는 T-SQL에서 R 스크립트를 실행할 수 있는 확장성 프레임워크를 추가했습니다. SQL Server 2017에는 Python 통합이 추가되었습니다. 

확장성 프레임워크는 간단한 함수부터 복잡한 기계 학습 모델 학습에 이르기까지 R 또는 Python에서 수행할 수 있는 모든 작업을 지원합니다. 그러나 이중 프로세스 아키텍처에서는 작업의 복잡성에 관계없이 모든 호출을 위해 외부 R 또는 Python 프로세스를 호출해야 합니다. 워크로드에 테이블에서 미리 학습된 모델을 로드하고 이미 SQL Server에 있는 데이터에서 채점하는 작업이 포함되면 외부 프로세스 호출의 오버헤드는 특정 상황에서 허용할 수 없는 대기 시간을 추가합니다. 예를 들어 사기 감지에는 관련성에 대한 빠른 채점이 필요합니다.

사기 감지 같은 시나리오의 채점 속도를 높이기 위해 SQL Server는 R 및 Python 시작 프로세스의 오버헤드를 제거하는 C++ 및 CLR 확장으로 기본 제공 채점 라이브러리를 추가했습니다.

[**실시간 채점**](../real-time-scoring.md)은 고성능 채점을 위한 첫 번째 솔루션이었습니다. SQL Server 2017 초기 버전과 SQL Server 2016의 이후 업데이트에 도입된 실시간 채점에서는 RevoScaleR, MicrosoftML(R), revoscalepy 및 microsoftml(Python)의 Microsoft 제어 함수에 대한 R 및 Python 처리를 대신하는 CLR 라이브러리를 사용합니다. CLR 라이브러리는 **sp_rxPredict** 저장 프로시저를 사용하여 R 또는 Python 런타임을 호출하지 않고 모든 지원되는 모델 형식에서 점수를 생성하는 작업에 관련됩니다.

[**네이티브 채점**](../sql-native-scoring.md)은 네이티브 C++ 라이브러리로 구현되지만 RevoScaleR 및 revoscalepy 모델에만 사용되는 SQL Server 2017 기능입니다. 가장 빠르고 더 안전한 방법이지만 다른 방법보다 적은 함수 세트를 지원합니다.

## <a name="choose-a-scoring-method"></a>채점 방법 선택

일반적으로 플랫폼 요구 사항에 따라 사용할 채점 방법이 결정됩니다.

| 제품 버전 및 플랫폼 | 방법 |
|------------------------------|-------------|
| Windows 및 Linux에서 SQL Server 2017 이상 | T-SQL PREDICT를 사용하는 **네이티브 채점** |
| SQL Server 2017(Windows 전용), SQL Server 2016 R Services SP1 이상 | sp\_rxPredict 저장 프로시저를 사용하는 **실시간 채점** |

PREDICT 함수를 사용하는 네이티브 채점을 추천합니다. sp\_rxPredict를 사용하려면 SQLCLR 통합을 사용하도록 설정해야 합니다. 이 옵션을 사용하도록 설정하기 전에 보안 문제를 고려해야 합니다.

## <a name="serialization-and-storage"></a>Serialization 및 스토리지

빠른 채점 옵션 중 하나를 통해 모델을 사용하려면 크기 및 채점 효율성에 최적화된 특별한 직렬화된 형식을 사용하여 모델을 저장합니다.

+ [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)을 호출하여 지원되는 모델을 **원시** 형식에 기록합니다.
+ [rxUnserializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)을 호출하여 다른 R 코드에서 사용할 모델을 재구성하거나 모델을 볼 수 있습니다.

**SQL 사용**

SQL 코드에서 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)를 사용하여 모델을 학습시키고 테이블의 **varbinary(max)** 형식 열에 학습된 모델을 직접 삽입할 수 있습니다. 간단한 예제는 [R에서 예측 모델 만들기](../tutorials/quickstart-r-train-score-model.md)를 참조하세요.

**R 사용**

R 코드에서 RevoScaleR 패키지의 [rxWriteObject](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxwriteobject) 함수를 호출하여 모델을 데이터베이스에 직접 기록합니다. **rxWriteObject()** 함수는 SQL Server 같은 ODBC 데이터 원본에서 R 개체를 검색하거나 SQL Server에 개체를 기록할 수 있습니다. API는 간단한 키-값 저장소 다음에 모델링됩니다.
  
이 함수를 사용하는 경우 먼저 [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)을 사용하여 모델을 직렬화해야 합니다. 그런 다음, serialization 단계를 반복하지 않도록 **rxWriteObject**의 *serialize* 인수를 FALSE로 설정합니다.

모델을 이진 형식으로 직렬화하는 것이 유용하지만, 확장성 프레임워크에서 R 및 Python 런타임 환경을 사용하여 예측을 채점하는 경우에는 필요하지 않습니다. 모델을 원시 바이트 형식으로 파일에 저장한 후 파일에서 SQL Server로 읽을 수 있습니다. 이 옵션은 환경 간에 모델을 이동하거나 복사하는 경우에 유용할 수 있습니다.

## <a name="scoring-in-related-products"></a>관련 제품의 채점

[독립 실행형 서버](r-server-standalone.md) 또는 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)를 사용하는 경우 예측을 빠르게 생성하기 위해 저장 프로시저 및 T-SQL 함수 외에 다른 옵션을 사용할 수 있습니다. 독립 실행형 서버와 Machine Learning Server는 모두 코드 배포를 위한 ‘웹 서비스’ 개념을 지원합니다.  R 또는 Python 미리 학습된 모델을 런타임에 호출되는 웹 서비스로 묶어서 새 데이터 입력을 평가할 수 있습니다. 자세한 내용은 다음 문서를 참조하세요.

+ [What are web services in Machine Learning Server?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)(Machine Learning Server의 웹 서비스란?)
+ [What is operationalization?](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)(운영화란?)
+ [Deploy a Python model as a web service with azureml-model-management-sdk](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)(azureml-model-management-sdk를 사용하여 Python 모델을 웹 서비스로 배포)
+ [Publish an R code block or a real-time model as a new web service](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)(R 코드 블록 또는 실시간 모델을 새 웹 서비스로 게시)
+ [mrsdeploy package for R](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)(R용 mrsdeploy 패키지)


## <a name="see-also"></a>참고 항목

+ [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)  
+ [rxRealTimeScoring](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxrealtimescoring)
+ [sp-rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)
+ [PREDICT T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)