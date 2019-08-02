---
title: revoscalepy Python 패키지
description: Python을 사용 하 여 SQL Server Machine Learning Services의 revoscalepy 모듈을 소개 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 76c68d0753c4ba29387b3378c1086ce9bce4f53b
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715771"
---
# <a name="revoscalepy-python-module-in-sql-server"></a>revoscalepy (SQL Server)의 Python 모듈
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**revoscalepy** 는 분산 컴퓨팅, 원격 계산 컨텍스트 및 고성능 데이터 과학 알고리즘을 지 원하는 Microsoft의 Python35 호환 모듈입니다. R에 대 한 **RevoScaleR** 패키지 (Microsoft R Server 및 SQL Server R Services와 함께 배포 됨)를 기반으로 하 여 비슷한 기능을 제공 합니다.

+ 동일한 버전의 **revoscalepy** 를 포함 하는 시스템의 로컬 및 원격 계산 컨텍스트
+ 데이터 변환 및 시각화 함수
+ 분산 또는 병렬 처리를 통해 확장 가능한 데이터 과학 함수
+ Intel math library 사용을 포함 하 여 향상 된 성능

**Revoscalepy** 에서 만든 데이터 원본 및 계산 컨텍스트는 기계 학습 알고리즘 에서도 사용할 수 있습니다. 이러한 알고리즘에 대 한 소개는 [Microsoftml Python module in SQL Server](ref-py-microsoftml.md)를 참조 하세요.

## <a name="full-reference-documentation"></a>전체 참조 설명서

**Revoscalepy** 라이브러리는 여러 Microsoft 제품에 배포 되지만, SQL Server 또는 다른 제품에 라이브러리를 가져올 때 사용 됩니다. 함수는 동일 하기 때문에 [개별 revoscalepy 함수에 대 한 설명서](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) 는 Microsoft Machine Learning Server에 대 한 [Python 참조](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) 아래의 한 위치에만 게시 됩니다. 제품별 동작이 있는 경우 함수 도움말 페이지에 차이점이 표시 됩니다.

## <a name="versions-and-platforms"></a>버전 및 플랫폼

**Revoscalepy** 모듈은 Python 3.5을 기반으로 하며 다음 Microsoft 제품 또는 다운로드 중 하나를 설치한 경우에만 사용할 수 있습니다.

+ [SQL Server 컴퓨터 학습 서비스](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 이상](https://docs.microsoft.com/machine-learning-server/)
+ [데이터 과학 클라이언트용 Python 클라이언트 라이브러리](setup-python-client-tools-sql.md)

> [!NOTE]
> 전체 제품 릴리스 버전은 SQL Server 2017부터 Windows 전용입니다. **Revoscalepy** 에 대 한 Linux 지원은 [SQL Server 2019 미리 보기](../../linux/sql-server-linux-setup-machine-learning.md)의 새로운 기능입니다.

## <a name="functions-by-category"></a>범주별 함수

이 섹션에서는 각 함수를 사용 하는 방법에 대 한 아이디어를 제공 하기 위해 범주별로 함수를 나열 합니다. [목차](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) 를 사용 하 여 알파벳 순서로 함수를 찾을 수도 있습니다.

## <a name="1-data-source-and-compute"></a>1-데이터 원본 및 계산

**revoscalepy** 에는 데이터 원본을 만들고 계산이 수행 되는 위치 또는 *계산 컨텍스트*를 설정 하는 함수가 포함 되어 있습니다. SQL Server 시나리오와 관련 된 함수는 아래 표에 나와 있습니다.

SQL Server와 Python은 경우에 따라 다른 데이터 형식을 사용 합니다. SQL 및 Python 데이터 형식 간의 매핑 목록은 [Python에서 sql로의 데이터 형식](python-libraries-and-data-types.md)을 참조 하세요.

| 함수| 설명|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) |  계산 컨텍스트 개체 SQL Server 만들어 원격 인스턴스에 계산을 푸시합니다. 여러 **revoscalepy** 함수는 계산 컨텍스트를 인수로 사용 합니다. 컨텍스트 전환 예제를 보려면 [revoscalepy를 사용 하 여 모델 만들기](../tutorials/use-python-revoscalepy-to-create-model.md)를 참조 하세요.|
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxsqlserverdata) | SQL Server 쿼리나 테이블을 기반으로 데이터 개체를 만듭니다. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxodbcdata)| ODBC 연결을 기반으로 데이터 원본을 만듭니다. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxxdfdata) | 로컬 XDF 파일을 기반으로 데이터 원본을 만듭니다. XDF 파일은 종종 메모리 내 데이터를 디스크로 오프 로드 하는 데 사용 됩니다. XDF 파일은 한 일괄 처리의 데이터베이스에서 전송 될 수 있는 것 보다 더 많은 데이터를 사용 하거나 메모리에 포함할 수 있는 것 보다 많은 데이터를 사용할 때 유용할 수 있습니다. 예를 들어 데이터베이스를 각 R 작업에 대해 반복적으로 쿼리 하는 대신 데이터베이스에서 로컬 워크스테이션으로 데이터를 정기적으로 이동 하는 경우 XDF 파일을 일종의 캐시로 사용 하 여 데이터를 로컬로 저장 한 다음 R 작업 영역에서 사용할 수 있습니다. |

> [!TIP]
> 데이터 원본 또는 계산 컨텍스트의 아이디어를 처음 접하는 경우 Microsoft Machine Learning Server 설명서에서 [분산 컴퓨팅](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) 을 시작 하는 것이 좋습니다.

## <a name="2-data-manipulation-etl"></a>2-데이터 조작 (ETL)

| 함수 | 설명 |
|----------|-------------|
|[rx_import](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-import) | .Xdf 파일 또는 데이터 프레임으로 데이터를 가져옵니다.|
|[rx_data_step](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-data-step) | 입력 데이터 집합의 데이터를 출력 데이터 집합으로 변환 합니다.|

<a name="bkmk_algorithms"></a>

## <a name="3-training-and-summarization"></a>3-교육 및 요약

| 함수| 설명|
| ------- | ---------- |
|[rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) | 추계 그라데이션 승격 의사 결정 트리 맞추기|
|[rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) | 분류 및 회귀 의사 결정 포리스트에 맞춤|
|[rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) | 분류 및 회귀 트리 맞춤 |
|[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) | 선형 회귀 모델 만들기|
|[rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) | 로지스틱 회귀 모델 만들기|
|[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) | Revoscalepy에서 개체의 요약을 생성 합니다.|

또한 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 의 함수를 검토 하 여 추가 접근 방식을 확인 해야 합니다.

<a name="ml-scoring"></a>

## <a name="4-scoring-functions"></a>4-점수 매기기 함수

| 함수| 설명|
| ------- | ---------- |
| [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | 학습 된 모델에서 예측 생성|) | 학습 된 모델에서 예측을 생성 하 고 실시간 점수 매기기에 사용할 수 있습니다. |
|[rx_predict_default](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-default) | Rx_lin_mod 및 rx_logit 개체를 사용 하 여 예측 값과 잔차를 계산 합니다. |
|[rx_predict_rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dforest) | Rx_dforest 또는 rx_btrees 개체에서 데이터 집합에 대 한 예측 또는 맞춤 값을 계산 합니다. |
|[rx_predict_rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dtree) | Rx_dtree 개체에서 데이터 집합에 대 한 예측 또는 맞춤 값을 계산 합니다. |

## <a name="how-to-work-with-revoscalepy"></a>Revoscalepy로 작업 하는 방법

**Revoscalepy** 의 함수는 저장 프로시저에 캡슐화 된 Python 코드에서 호출할 수 있습니다. 대부분의 개발자는 **revoscalepy** 솔루션을 로컬로 빌드한 다음 배포 연습으로 완성 된 Python 코드를 저장 프로시저로 마이그레이션합니다.

로컬로 실행 하는 경우 일반적으로 명령줄 또는 Python 개발 환경에서 Python 스크립트를 실행 하 고 **revoscalepy** 함수 중 하나를 사용 하 여 SQL Server 계산 컨텍스트를 지정 합니다. 전체 코드 또는 개별 함수에 대 한 원격 계산 컨텍스트를 사용할 수 있습니다. 예를 들어 최신 데이터를 사용 하 고 데이터 이동을 방지 하기 위해 모델 학습을 서버에 오프 로드할 수 있습니다.

저장 프로시저 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)에 Python 스크립트를 캡슐화 할 준비가 되 면 명확 하 게 정의 된 입력 및 출력을 포함 하는 단일 함수로 코드를 다시 작성 하는 것이 좋습니다. 

입력 및 출력은 데이터 프레임 **pandas** 합니다. 이 작업이 완료 되 면 T-sql을 지 원하는 모든 클라이언트에서 저장 프로시저를 호출 하 고, SQL 쿼리를 입력으로 쉽게 전달 하 고, 결과를 SQL 테이블에 저장할 수 있습니다. 예를 들어 [SQL 개발자를 위한 데이터베이스 내 Python 분석](../tutorials/sqldev-in-database-python-for-sql-developers.md)에 대해 알아보기를 참조 하세요.

### <a name="using-revoscalepy-with-microsoftml"></a>Microsoftml와 함께 revoscalepy 사용

[Microsoftml](ref-py-microsoftml.md) 에 대 한 Python 함수는 revoscalepy에 제공 된 계산 컨텍스트 및 데이터 원본과 통합 됩니다. Microsoftml에서 함수를 호출 하는 경우, 예를 들어 모델을 정의 하 고 학습 하는 경우 revoscalepy 함수를 사용 하 여 로컬로 또는 SQl Server 원격 계산 컨텍스트에서 Python 코드를 실행 합니다.

다음 예제에서는 Python 코드에서 모듈을 가져오는 구문을 보여 줍니다. 그런 다음 필요한 개별 함수를 참조할 수 있습니다.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>참조

+ [Python 자습서](../tutorials/sql-server-python-tutorials.md)
+ [자습서: T-sql에 Python 코드 포함](../tutorials/run-python-using-t-sql.md)
+ [Python 참조 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)
