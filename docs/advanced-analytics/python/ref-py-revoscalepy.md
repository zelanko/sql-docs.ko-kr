---
title: revoscalepy Python 패키지
description: Python을 포함하는 SQL Server Machine Learning Services의 revoscalepy 모듈을 소개합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c6de9072c32155446b3ff40df3f81af9073c1090
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706819"
---
# <a name="revoscalepy-python-module-in-sql-server"></a>revoscalepy(SQL Server의 Python 모듈)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**revoscalepy**는 분산 컴퓨팅, 원격 컴퓨팅 컨텍스트 및 고성능 데이터 과학 알고리즘을 지원하는 Microsoft의 Python35 호환 모듈입니다. 이 모듈은 R용 **RevoScaleR** 패키지(Microsoft R Server 및 SQL Server R Services와 함께 배포됨)를 기준으로 하며, 다음과 같은 비슷한 기능을 제공합니다.

+ 동일한 **revoscalepy** 버전을 포함하는 시스템의 로컬 및 원격 컴퓨팅 컨텍스트
+ 데이터 변환 및 시각화 함수
+ 분산 또는 병렬 처리를 통해 확장 가능한 데이터 과학 함수
+ Intel 수학 라이브러리 사용을 포함하는 향상된 성능

**revoscalepy**에서 만든 데이터 원본 및 컴퓨팅 컨텍스트를 기계 학습 알고리즘에서도 사용할 수 있습니다. 이러한 알고리즘에 대한 소개를 보려면 [SQL Server의 microsoftml Python 모듈](ref-py-microsoftml.md)을 참조하세요.

## <a name="full-reference-documentation"></a>전체 참조 설명서

**revoscalepy** 라이브러리는 여러 Microsoft 제품에 배포되지만, SQL Server에서 라이브러리를 가져오든, 다른 제품에서 라이브러리를 가져오든, 사용 방식은 동일합니다. 함수는 동일하기 때문에 [개별 revoscalepy 함수에 대한 설명서](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)는 Microsoft Machine Learning Server에 대한 [Python 참조](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) 아래의 한 위치에만 게시됩니다. 제품별로 고유한 동작이 있는 경우 함수 도움말 페이지에 차이점이 표시됩니다.

## <a name="versions-and-platforms"></a>버전 및 플랫폼

**revoscalepy** 모듈은 Python 3.5을 기준으로 하며, 다음 Microsoft 제품 또는 다운로드 중 하나를 설치한 경우에만 사용할 수 있습니다.

+ [SQL Server 컴퓨터 학습 서비스](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 이상](https://docs.microsoft.com/machine-learning-server/)
+ [데이터 과학 클라이언트용 Python 클라이언트 라이브러리](setup-python-client-tools-sql.md)

> [!NOTE]
> 전체 제품 릴리스 버전은 SQL Server 2017에서 Windows 전용입니다. Windows 및 Linux는 [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md)의 **revoscalepy**에서 둘 다 지원됩니다.

## <a name="functions-by-category"></a>범주별 함수

이 섹션에서는 사용 방법에 대한 이해를 돕기 위해 각 함수를 범주별로 구분해서 제공합니다. [목차](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)를 사용하여 사전순으로 함수를 찾을 수도 있습니다.

## <a name="1-data-source-and-compute"></a>1 - 데이터 원본 및 컴퓨팅

**revoscalepy**에는 데이터 원본을 만들고 위치를 설정하기 위한 함수 또는 컴퓨팅이 수행되는 *컴퓨팅 컨텍스트*가 포함되어 있습니다. SQL Server 시나리오와 관련된 함수는 아래 표에 나와 있습니다.

경우에 따라 SQL Server와 Python은 다른 데이터 형식을 사용합니다. SQL 및 Python 데이터 형식 간 매핑 목록은 [Python-SQL 데이터 형식](python-libraries-and-data-types.md)을 참조하세요.

| 함수| 설명|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) |  SQL Server 컴퓨팅 컨텍스트 개체를 만들어 원격 인스턴스에 컴퓨팅을 푸시합니다. 여러 **revoscalepy** 함수는 컴퓨팅 컨텍스트를 인수로 사용합니다. 컨텍스트 전환 예제는 [revoscalepy를 사용하여 모델 만들기](../tutorials/use-python-revoscalepy-to-create-model.md)를 참조하세요.|
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxsqlserverdata) | SQL Server 쿼리나 테이블을 기준으로 데이터 개체를 만듭니다. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxodbcdata)| ODBC 연결을 기준으로 데이터 원본을 만듭니다. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxxdfdata) | 로컬 XDF 파일을 기준으로 데이터 원본을 만듭니다. XDF 파일은 종종 메모리 내 데이터를 디스크로 오프로드하는 데 사용됩니다. XDF 파일은 데이터베이스에서 하나의 일괄 처리로 전송될 수 있는 것보다 많은 데이터 또는 메모리에 맞출 수 있는 것보다 많은 데이터를 사용할 경우 유용할 수 있습니다. 예를 들어, R 작업별로 반복적으로 데이터베이스를 쿼리하지 않고 대용량 데이터를 데이터베이스에서 로컬 워크스테이션으로 주기적으로 이동하면 XDF 파일을 일종의 캐시로 사용하여 데이터를 로컬에 저장하고 R 작업 공간에서 작업을 수행할 수 있습니다. |

> [!TIP]
> 데이터 원본 또는 컴퓨팅 컨텍스트를 처음 접하는 경우에는 Microsoft Machine Learning Server 설명서에서 [분산 컴퓨팅](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)부터 살펴보는 것이 좋습니다.

## <a name="2-data-manipulation-etl"></a>2 - 데이터 조작(ETL)

| 함수 | 설명 |
|----------|-------------|
|[rx_import](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-import) | .xdf 파일 또는 데이터 프레임으로 데이터를 가져옵니다.|
|[rx_data_step](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-data-step) | 입력 데이터 세트의 데이터를 출력 데이터 세트로 변환합니다.|

<a name="bkmk_algorithms"></a>

## <a name="3-training-and-summarization"></a>3 - 학습 및 요약

| 함수| 설명|
| ------- | ---------- |
|[rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) | 확률 그래디언트 부스팅 의사 결정 트리 맞추기|
|[rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) | 분류 및 회귀 의사 결정 포리스트 맞추기|
|[rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) | 분류 및 회귀 트리 맞추기 |
|[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) | 선형 회귀 모델 만들기|
|[rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) | 로지스틱 회귀 모델 만들기|
|[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) | revoscalepy에서 개체의 일변량 요약을 생성합니다.|

또한 추가 접근 방법에 대해서는 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)의 함수도 검토해야 합니다.

<a name="ml-scoring"></a>

## <a name="4-scoring-functions"></a>4 - 점수 매기기 함수

| 함수| 설명|
| ------- | ---------- |
| [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | 학습된 모델에서 예측 생성|) | 학습된 모델에서 예측을 생성하고 실시간 점수 매기기에 사용할 수 있습니다. |
|[rx_predict_default](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-default) | rx_lin_mod 및 rx_logit 개체를 사용하여 예측 값과 나머지를 계산합니다. |
|[rx_predict_rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dforest) | rx_dforest 또는 rx_btrees 개체에서 데이터 세트에 대한 예측 또는 맞춤 값을 계산합니다. |
|[rx_predict_rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dtree) | rx_dtree 개체에서 데이터 세트에 대한 예측 또는 맞춤 값을 계산합니다. |

## <a name="how-to-work-with-revoscalepy"></a>revoscalepy로 작업하는 방법

**revoscalepy**의 함수는 저장 프로시저에서 캡슐화된 Python 코드에서 호출할 수 있습니다. 대부분의 개발자는 **revoscalepy** 솔루션을 로컬로 빌드한 다음, 완성된 Python 코드를 배포 연습으로 사용하기 위해 저장 프로시저로 마이그레이션합니다.

로컬로 실행하는 경우 일반적으로 명령줄 또는 Python 개발 환경에서 Python 스크립트를 실행하고, **revoscalepy** 함수 중 하나를 사용하여 SQL Server 컴퓨팅 컨텍스트를 지정합니다. 전체 코드 또는 개별 함수에 대한 원격 컴퓨팅 컨텍스트를 사용할 수 있습니다. 예를 들어, 최신 데이터를 사용하고 데이터 이동을 방지하도록 모델 학습을 서버에 오프로드할 수 있습니다.

저장 프로시저 내에서 Python 스크립트 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)를 캡슐화할 준비가 되면 코드를 입력 및 출력이 명확하게 정의된 단일 함수로 다시 작성하는 것이 좋습니다. 

입력 및 출력은 **pandas** 데이터 프레임이어야 합니다. 이 작업이 완료되면 T-SQL을 지원하는 모든 클라이언트에서 저장 프로시저를 호출하고, SQL 쿼리를 입력으로 쉽게 전달하고, 결과를 SQL 테이블에 저장할 수 있습니다. 예제를 보려면 [SQL 개발자를 위한 데이터베이스 내 Python 분석 학습](../tutorials/sqldev-in-database-python-for-sql-developers.md)을 참조하세요.

### <a name="using-revoscalepy-with-microsoftml"></a>microsoftml에서 revoscalepy 사용

[microsoftml](ref-py-microsoftml.md)에 대한 Python 함수는 revoscalepy에 제공된 컴퓨팅 컨텍스트 및 데이터 원본과 통합됩니다. microsoftml에서 함수를 호출하는 경우, 예를 들어 모델을 정의하고 학습할 때 revoscalepy 함수를 사용하여 로컬로 또는 SQl Server 원격 컴퓨팅 컨텍스트에서 Python 코드를 실행합니다.

다음 예제에서는 Python 코드에 모듈을 가져오는 구문을 보여 줍니다. 그런 후 필요한 개별 함수를 참조할 수 있습니다.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>관련 항목:

+ [Python 자습서](../tutorials/sql-server-python-tutorials.md)
+ [자습서: T-SQL에 Python 코드 포함](../tutorials/run-python-using-t-sql.md)
+ [Python 참조(Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)
