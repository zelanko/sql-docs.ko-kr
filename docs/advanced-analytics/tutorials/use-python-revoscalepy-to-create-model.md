---
title: Revoscalepy와 함께 Python을 사용 하 여 모델 만들기
description: Revoscalepy 함수를 사용 하 여 Python 스크립트를 작성 하 여 SQL Server에서 원격으로 실행 되는 데이터 과학 모델을 만듭니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 11a155a9c679a18fefc7b3c91434a0ca241c23f7
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68468502"
---
# <a name="use-python-with-revoscalepy-to-create-a-model-that-runs-remotely-on-sql-server"></a>Revoscalepy와 함께 Python을 사용 하 여 SQL Server에서 원격으로 실행 되는 모델 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Microsoft의 [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) Python 라이브러리는 데이터 탐색, 시각화, 변환 및 분석을 위한 데이터 과학 알고리즘을 제공 합니다. 이 라이브러리는 SQL Server의 Python 통합 시나리오에서 전략적으로 중요 합니다. 다중 코어 서버에서 **revoscalepy** 함수는 병렬로 실행 될 수 있습니다. 중앙 서버 및 클라이언트 워크스테이션 ( **revoscalepy** 라이브러리가 모두 동일한 별도의 물리적 컴퓨터)을 사용 하는 분산 아키텍처에서는 로컬에서 시작 하는 Python 코드를 작성 한 다음 실행을 원격 SQL Server 인스턴스로 이동할 수 있습니다. 데이터가 있는 위치입니다.

**Revoscalepy** 는 다음과 같은 Microsoft 제품 및 배포에서 찾을 수 있습니다.

+ [SQL Server Machine Learning Services (데이터베이스 내)](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server (SQL이 아닌 독립 실행형 서버)](https://docs.microsoft.com/machine-learning-server/index)
+ [클라이언트 쪽 Python 라이브러리 (개발 워크스테이션의 경우)](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) 

이 연습에서는 계산 컨텍스트를 입력으로 허용 하는 **revoscalepy** 알고리즘 중 하나인 [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)을 기반으로 선형 회귀 모델을 만드는 방법을 보여 줍니다. 이 연습에서 실행할 코드는 원격 컴퓨팅 환경을 사용 하는 **revoscalepy** 함수에서 사용 하도록 설정 된 로컬에서 원격 컴퓨팅 환경으로 코드 실행을 이동 합니다.

이 자습서를 완료 하면 다음을 수행 하는 방법을 배우게 됩니다.

> [!div class="checklist"]
> * **Revoscalepy** 를 사용 하 여 선형 모델 만들기
> * 로컬에서 원격 계산 컨텍스트로 전환 작업

## <a name="prerequisites"></a>사전 요구 사항

이 연습에서 사용 되는 샘플 데이터는 [**flightdata**](demo-data-airlinedemo-in-sql.md) 데이터베이스입니다.

이 문서의 샘플 코드를 실행 하려면 IDE가 필요 하며, IDE는 Python 실행 파일에 연결 되어야 합니다.

계산 컨텍스트 이동을 연습 하려면 [로컬 워크스테이션과](../python/setup-python-client-tools-sql.md) [Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 및 Python을 사용 하는 SQL Server 데이터베이스 엔진 인스턴스가 필요 합니다. 

> [!Tip]
> 두 대의 컴퓨터가 없는 경우 관련 응용 프로그램을 설치 하 여 물리적 컴퓨터 한 대에서 원격 계산 컨텍스트를 시뮬레이션할 수 있습니다. 먼저 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 설치는 "원격" 인스턴스로 작동 합니다. 둘째, [Python 클라이언트 라이브러리](../python/setup-python-client-tools-sql.md) 의 설치는 클라이언트로 작동 합니다. 동일한 컴퓨터에 동일한 Python 배포 및 Microsoft Python 라이브러리의 복사본 두 개가 포함 됩니다. 연습을 성공적으로 완료 하는 데 사용 하는 Python의 복사본 및 파일 경로를 추적 해야 합니다.

## <a name="remote-compute-contexts-and-revoscalepy"></a>원격 계산 컨텍스트 및 revoscalepy

이 샘플은 클라이언트에서 작업을 수행할 수 있도록 하는 원격 계산 컨텍스트에서 Python 모델을 만드는 프로세스를 보여 주지만, 작업을 실제로 수행 하는 SQL Server, Spark 또는 Machine Learning Server와 같은 원격 환경을 선택할 수 있습니다. 원격 계산 컨텍스트는 데이터가 있는 위치에 대 한 계산을 가져오는 것입니다.

SQL Server에서 Python 코드를 실행 하려면 **revoscalepy** 패키지가 필요 합니다. R 언어에 대 한 **RevoScaleR** 패키지와 유사 하 게 Microsoft에서 제공 하는 특수 Python 패키지입니다. **Revoscalepy** 패키지는 계산 컨텍스트 생성을 지원 하 고 로컬 워크스테이션과 원격 서버 간에 데이터와 모델을 전달 하기 위한 인프라를 제공 합니다. 데이터베이스 내 코드 실행을 지 원하는 **revoscalepy** 함수는 [Rxinsqlserver](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver)입니다.

이 단원에서는 SQL Server의 데이터를 사용 하 여 매우 큰 데이터 집합에 대 한 회귀를 지 원하는 **revoscalepy** 함수 인 [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)기반 선형 모델을 학습 합니다. 

또한이 단원에서는 Python에서 **SQL Server 계산 컨텍스트** 를 설정 하 고 사용 하는 방법의 기본 사항을 보여 줍니다. 계산 컨텍스트가 다른 플랫폼에서 작동 하는 방법 및 지원 되는 계산 컨텍스트에 대 한 자세한 내용은 [Machine Learning Server 스크립트 실행에 대 한 compute 컨텍스트](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)를 참조 하십시오.


## <a name="run-the-sample-code"></a>샘플 코드 실행

데이터베이스를 준비 하 고 학습 데이터를 테이블에 저장 한 후에는 Python 개발 환경을 열고 코드 샘플을 실행 합니다.

코드는 다음 단계를 수행 합니다.

1. 필요한 라이브러리 및 함수를 가져옵니다.
2. SQL Server에 대 한 연결을 만듭니다. 데이터 작업을 위한 **데이터 원본** 개체를 만듭니다.
3. 로지스틱 회귀 알고리즘에서 사용할 수 있도록 **변환을** 사용 하 여 데이터를 수정 합니다.
4. 를 `rx_lin_mod` 호출 하 고 모델에 맞게 사용 되는 수식을 정의 합니다.
5. 원본 데이터를 기반으로 예측 집합을 생성 합니다.
6. 예측 값을 기준으로 요약을 만듭니다.

모든 작업은 SQL Server 인스턴스를 계산 컨텍스트로 사용 하 여 수행 됩니다.

> [!NOTE]
> 명령줄에서 실행 되는이 샘플에 대 한 데모는 다음 비디오를 참조 하세요. [Python을 사용 하는 SQL Server 2017 고급 분석](https://www.youtube.com/watch?v=FcoY795jTcc)

### <a name="sample-code"></a>예제 코드

```python
from revoscalepy import RxComputeContext, RxInSqlServer, RxSqlServerData
from revoscalepy import rx_lin_mod, rx_predict, rx_summary
from revoscalepy import RxOptions, rx_import

import os

def test_linmod_sql():
    sql_server = os.getenv('PYTEST_SQL_SERVER', '.')
    
    sql_connection_string = 'Driver=SQL Server;Server=' + sqlServer + ';Database=sqlpy;Trusted_Connection=True;'
    print("connectionString={0!s}".format(sql_connection_string))

    data_source = RxSqlServerData(
        sql_query = "select top 10 * from airlinedemosmall",
        connection_string = sql_connection_string,

        column_info = {
            "ArrDelay" : { "type" : "integer" },
            "DayOfWeek" : {
                "type" : "factor",
                "levels" : [ "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday" ]
            }
        })

    sql_compute_context = RxInSqlServer(
        connection_string = sql_connection_string,
        num_tasks = 4,
        auto_cleanup = False
        )

    #
    # Run linmod locally
    #
    linmod_local = rx_lin_mod("ArrDelay ~ DayOfWeek", data = data_source)
    #
    # Run linmod remotely
    #
    linmod = rx_lin_mod("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)

    # Predict results
    # 
    predict = rx_predict(linmod, data = rx_import(input_data = data_source))
    summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)
```

### <a name="defining-a-data-source-vs-defining-a-compute-context"></a>데이터 원본 정의 및 계산 컨텍스트 정의

데이터 원본이 계산 컨텍스트와 다릅니다. *데이터 소스* 는 코드에서 사용 되는 데이터를 정의 합니다. 계산 컨텍스트는 코드가 실행 되는 위치를 정의 합니다. 그러나 다음과 같은 정보 중 일부를 사용 합니다.

+ `sql_query` 및`sql_connection_string`와 같은 Python 변수는 데이터의 원본을 정의 합니다. 

    이러한 변수를 [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) 생성자에 전달 하 여 `data_source`라는 **데이터 소스 개체** 를 구현 합니다.

+ [Rxinsqlserver](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) 생성자를 사용 하 여 **계산 컨텍스트 개체** 를 만듭니다. 결과 **계산 컨텍스트 개체** 의 이름은 `sql_cc`입니다.

    이 예에서는 데이터 원본에서 사용한 것과 동일한 연결 문자열을 사용 하 여 데이터를 계산 컨텍스트로 사용 하는 것과 동일한 SQL Server 인스턴스에 사용 한다고 가정 합니다. 
    
    그러나 데이터 원본 및 계산 컨텍스트는 서로 다른 서버에 있을 수 있습니다.
 
### <a name="changing-compute-contexts"></a>계산 컨텍스트 변경

계산 컨텍스트를 정의한 후에는 **활성 계산 컨텍스트**를 설정 해야 합니다. 

기본적으로 대부분의 작업은 로컬로 실행 됩니다. 즉, 다른 계산 컨텍스트를 지정 하지 않으면 데이터가 데이터 원본에서 인출 되 고 코드가 현재 Python 환경에서 실행 됩니다.

활성 계산 컨텍스트를 설정 하는 방법에는 다음 두 가지가 있습니다.
+ 메서드 또는 함수의 인수로
+ 호출 하 여`rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>계산 컨텍스트를 메서드 또는 함수의 인수로 설정 합니다.

이 예에서는 개별 **rx** 함수의 인수를 사용 하 여 계산 컨텍스트를 설정 합니다.
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

이 계산 컨텍스트는 [rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)호출에서 다시 사용 됩니다.

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rxsetcomputecontext"></a>Rx_set_compute_context를 사용 하 여 명시적으로 계산 컨텍스트 설정

[Rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) 함수를 사용 하면 이미 정의 된 계산 컨텍스트 간을 전환할 수 있습니다.

활성 계산 컨텍스트를 설정한 후에는 해당 컨텍스트를 변경할 때까지 활성 상태로 유지 됩니다.

### <a name="using-parallel-processing-and-streaming"></a>병렬 처리 및 스트리밍 사용

계산 컨텍스트를 정의 하는 경우 계산 컨텍스트에서 데이터를 처리 하는 방법을 제어 하는 매개 변수를 설정할 수도 있습니다. 이러한 매개 변수는 데이터 원본 유형에 따라 달라 집니다.

SQL Server 계산 컨텍스트의 경우 일괄 처리 크기를 설정 하거나 실행 중인 작업에 사용할 병렬 처리 수준에 대 한 힌트를 제공할 수 있습니다.

+ 샘플은 4 개의 프로세서가 `num_tasks` 있는 컴퓨터에서 실행 되었으므로 최대 리소스 사용을 허용 하도록 매개 변수를 4로 설정 합니다. 
+ 이 값을 0으로 설정 하면 SQL Server는 기본값을 사용 하 여 서버에 대 한 현재 MAXDOP 설정에서 가능한 한 많은 작업을 병렬로 실행 합니다. 그러나 할당 될 수 있는 작업의 정확한 수는 서버 설정 및를 실행 하는 다른 작업 등의 여러 요소에 따라 다릅니다.

## <a name="next-steps"></a>다음 단계

이러한 추가 Python 샘플 및 자습서에서는 원격 계산 컨텍스트를 사용 하는 것 뿐만 아니라 보다 복잡 한 데이터 원본을 사용 하는 종단 간 시나리오를 보여 줍니다.

+ [SQL 개발자를 위한 데이터베이스 내 Python](sqldev-in-database-python-for-sql-developers.md)
+ [Python 및 SQL Server를 사용 하 여 예측 모델 작성](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
