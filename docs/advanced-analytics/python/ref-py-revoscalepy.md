---
title: revoscalepy Python 패키지-SQL Server Machine Learning 서비스
description: Python 사용 하 여 SQL Server 2017 Machine Learning Services revoscalepy 모듈을 소개 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3482a15392fa04f7f10d2acbb0843d124e27dc21
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962740"
---
# <a name="revoscalepy-python-module-in-sql-server"></a>revoscalepy (SQL Server에서 Python 모듈)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**revoscalepy** 분산 컴퓨팅을 지 원하는 Microsoft, 원격 계산 컨텍스트 및 고성능 데이터 과학 알고리즘에서 Python35-호환 되는 모듈입니다. 기반이 되는 **RevoScaleR** R (Microsoft R Server 및 SQL Server R Services를 사용 하 여 분산)에 대해 유사한 기능을 제공 하는 패키지:

+ 로컬 및 원격 계산 컨텍스트에서 동일한 버전의 시스템에서 **revoscalepy**
+ 데이터 변환 및 시각화 함수
+ 분산 또는 병렬 처리를 통해 확장 가능한 데이터 과학 함수
+ Intel math 라이브러리의 사용을 포함 하 여 성능 향상된

데이터 원본 및에서 만든 계산 컨텍스트 **revoscalepy** 기계 학습 알고리즘에서 사용할 수도 있습니다. 이러한 알고리즘에 대 한 소개를 참조 하세요 [SQL Server에서 microsoftml Python 모듈](ref-py-microsoftml.md)합니다.

## <a name="full-reference-documentation"></a>전체 참조 설명서

합니다 **revoscalepy** 라이브러리는 여러 Microsoft 제품을 배포 하지만 SQL Server 또는 다른 제품에서 라이브러리를 표시 하는지 여부를 사용량은 동일 합니다. 함수는 동일 하므로 [개별 revoscalepy 함수에 대 한 설명서](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) 아래에 있는 하나의 위치에 게시 되는 [Python 참조](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) Microsoft Machine Learning Server에 대 한 합니다. 모든 제품별 해야 동작 존재, 불일치 함수 도움말 페이지에 표시 됩니다.

## <a name="versions-and-platforms"></a>버전 및 플랫폼

합니다 **revoscalepy** 모듈은 Python 3.5에 기반 하 고 사용할 수 있는 다음과 같은 Microsoft 제품 또는 다운로드 중 하나를 설치 하는 경우에:

+ [SQL Server 2017 Machine Learning 서비스](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 이상](https://docs.microsoft.com/machine-learning-server/)
+ [데이터 과학 클라이언트에 대 한 Python 클라이언트 라이브러리](setup-python-client-tools-sql.md)

> [!NOTE]
> 전체 제품 릴리스 버전은 Windows 전용 SQL Server 2017을 사용 하 여 시작 합니다. 에 대 한 Linux 지원을 **revoscalepy** 의 새로운 [SQL Server 2019 Preview](../../linux/sql-server-linux-setup-machine-learning.md)합니다.

## <a name="functions-by-category"></a>범주별으로 함수

이 섹션에서는 범주를 각각 사용 하는 방법의 아이디어를 제공 하 여 함수를 나열 합니다. 사용할 수도 있습니다는 [목차](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) 알파벳 순서로 함수를 찾으려고 합니다.

## <a name="1-data-source-and-compute"></a>1-데이터 원본 및 계산

**revoscalepy** 데이터 원본을 만들고 위치를 설정 하기 위한 함수가 포함 됩니다 또는 *계산 컨텍스트*, 계산이 수행 되는 중입니다. SQL Server 시나리오와 관련 된 함수는 아래 표에 나열 됩니다.

SQL Server 및 Python에 따라서는 다른 데이터 형식을 사용합니다. SQL 및 Python 데이터 형식 간의 매핑 목록을 참조 하세요 [Python-SQL 데이터 형식](python-libraries-and-data-types.md)합니다.

| 함수| 설명|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) |  푸시 계산을 원격 인스턴스를 SQL Server 계산 컨텍스트 개체를 만듭니다. 몇 가지 **revoscalepy** 함수 인수로 계산 컨텍스트를 고려 합니다. 컨텍스트 전환 예제를 보려면 [revoscalepy를 사용 하 여 모델을 만드는](../tutorials/use-python-revoscalepy-to-create-model.md)합니다.|
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxsqlserverdata) | SQL Server 쿼리 또는 테이블 기반 데이터 개체를 만듭니다. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxodbcdata)| ODBC 연결에 따라 데이터 원본을 만듭니다. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxxdfdata) | 로컬 XDF 파일을 기반으로 데이터 원본을 만듭니다. XDF 파일을 메모리 내 데이터 디스크를 오프 로드 자주 사용 됩니다. XDF 파일을 하나의 일괄 처리를 데이터베이스에서 전송할 수 있습니다 보다 더 많은 데이터 또는 메모리에 맞출 수 있는 수보다 더 많은 데이터를 작업할 때 유용할 수 있습니다. 예를 들어, 주기적으로 이동 하면 많은 양의 데이터를 데이터베이스에서 로컬 워크스테이션, 쿼리 하는 대신 각 R 작업에 대해 반복 해 서 데이터베이스 사용할 수 있습니다 XDF 파일 캐시의 한 종류로 로컬로 데이터를 저장 하 고 다음 R 작업 영역에서 작업에. |

> [!TIP]
> 새 데이터 원본의 개념을 하거나 하는 경우 계산 컨텍스트를 시작 하는 것이 좋습니다 [분산 컴퓨팅](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) Microsoft Machine Learning Server 문서의 합니다.

## <a name="2-data-manipulation-etl"></a>2-데이터 조작 (ETL)

| 함수 | 설명 |
|----------|-------------|
|[rx_import](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-import) | .Xdf 파일 또는 데이터 프레임으로 데이터를 가져옵니다.|
|[rx_data_step](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-data-step) | 출력 데이터 집합에는 입력된 데이터 집합에서 데이터를 변환 합니다.|

<a name="bkmk_algorithms"></a>

## <a name="3-training-and-summarization"></a>3-학습 및 요약

| 함수| 설명|
| ------- | ---------- |
|[rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) | 적합된 한 stochastic 그라데이션 승격 의사 결정 트리|
|[rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) | 적합된 한 분류 및 회귀 의사 결정 포리스트|
|[rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) | 적합된 한 분류 및 회귀 트리 |
|[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) | 선형 회귀 모델 만들기|
|[rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) | 로지스틱 회귀 모델 만들기|
|[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) | Revoscalepy에서 개체의 단일 변량 요약을 생성 합니다.|

함수에도 검토 해야 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 추가 방법에 대 한 합니다.

<a name="ml-scoring"></a>

## <a name="4-scoring-functions"></a>4-점수 매기기 함수

| 함수| 설명|
| ------- | ---------- |
| [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | 학습된 된 모델에서 예측을 생성 합니다.|) | 학습된 된 모델에서 예측을 생성 하 고 실시간 점수 매기기에 사용할 수 있습니다. |
|[rx_predict_default](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-default) | 예측된 값 및 rx_lin_mod 및 rx_logit 개체를 사용 하 여 오차를 계산 합니다. |
|[rx_predict_rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dforest) | Rx_dforest 또는 rx_btrees 개체에서 데이터 집합에 대 한 예측 또는 맞춤 값을 계산 합니다. |
|[rx_predict_rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dtree) | Rx_dtree 개체에서 데이터 집합에 대 한 예측 또는 맞춤 값을 계산 합니다. |

## <a name="how-to-work-with-revoscalepy"></a>Revoscalepy를 사용 하는 방법

함수가 **revoscalepy** 저장된 프로시저에서 캡슐화 하는 Python 코드에서 호출할 수 있습니다. 대부분의 개발자는 빌드할 **revoscalepy** 솔루션을 로컬로 다음 배포 연습으로 저장된 프로시저에 완성 된 Python 코드를 마이그레이션합니다.

로컬로 실행할 때 일반적으로 명령줄에서 또는 Python 개발 환경에서 Python 스크립트를 실행 및 중 하나를 사용 하 여 SQL Server 계산 컨텍스트를 지정 합니다 **revoscalepy** 함수입니다. 전체 코드의 경우 또는 개별 함수에 대 한 원격 계산 컨텍스트를 사용할 수 있습니다. 예를 들어 다음 모델 학습 최신 데이터를 사용 하 고 데이터 이동을 방지 하기 위해 서버를 오프 로드 하는 것이 좋습니다.

저장된 프로시저 내에서 Python 스크립트를 캡슐화 할 준비가 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), 입력 및 출력에 명확 하 게 정의한 단일 함수로 코드를 다시 작성 하는 것이 좋습니다. 

입력 및 출력 해야 **pandas** 데이터 프레임입니다. 이 완료 되 면 T-SQL을 지 원하는 모든 클라이언트에서 저장된 프로시저를 호출, 쉽게 입력으로 SQL 쿼리를 전달 하 고 수 SQL 테이블에 결과 저장 합니다. 예를 들어 참조 [SQL 개발자를 위한 데이터베이스 내 Python 분석에 알아봅니다](../tutorials/sqldev-in-database-python-for-sql-developers.md)합니다.

### <a name="using-revoscalepy-with-microsoftml"></a>Microsoftml revoscalepy 사용

Python에 대 한 함수 [microsoftml](ref-py-microsoftml.md) revoscalepy에서 제공 되는 계산 컨텍스트 및 데이터 원본으로 통합 됩니다. Microsoftml에서 함수를 호출할 때 예를 들어 경우 정의 하 고 모델 학습 기능을 사용 revoscalepy Python을 실행 하려면 로컬로 코드 하거나 원격 SQl server에서 계산 컨텍스트.

다음 예제에서는 Python 코드에서 모듈을 가져오기에 대 한 구문을 보여 줍니다. 그런 다음 필요한 개별 함수를 참조할 수 있습니다.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>참조

+ [Python 자습서](../tutorials/sql-server-python-tutorials.md)
+ [자습서: T-sql로 Python 코드를 포함 합니다.](../tutorials/run-python-using-t-sql.md)
+ [Python 참조 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)
