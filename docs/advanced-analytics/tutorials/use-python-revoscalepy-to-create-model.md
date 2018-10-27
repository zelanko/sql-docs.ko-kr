---
title: Revoscalepy를 사용 하 여 Python를 사용 하 여 SQL Server에서 모델 만들기 | Microsoft Docs
description: Revoscalepy 함수를 사용 하 여 SQL Server에서 원격으로 실행 되는 데이터 과학 모델을 만드는 Python 스크립트를 작성 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f554badcba282bad7fb386daf8c4c0f4106804b4
ms.sourcegitcommit: 9f2edcdf958e6afce9a09fb2e572ae36dfe9edb0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50100164"
---
# <a name="use-python-with-revoscalepy-to-create-a-model-that-runs-remotely-on-sql-server"></a>Revoscalepy를 사용 하 여 Python을 사용 하 여 SQL Server에서 원격으로 실행 되는 모델을 만들려면
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

합니다 [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) Microsoft에서 Python 라이브러리는 데이터 탐색, 시각화, 변환 및 분석에 대 한 데이터 과학 알고리즘을 제공 합니다. 이 라이브러리는 SQL Server의 Python 통합 시나리오에서 전략적 중요도 있습니다. 다중 코어 서버의 **revoscalepy** 함수 병렬로 실행할 수 있습니다. 중앙 서버 및 클라이언트 워크스테이션을 사용 하 여 분산된 아키텍처에서 (같은 모든 물리적 컴퓨터를 구분 **revoscalepy** 라이브러리), 로컬에서 시작 되지만 다음 실행을 이동 하는 Python 코드를 작성할 수는 데이터가 있는 원격 SQL Server 인스턴스.

찾을 수 있습니다 **revoscalepy** 다음과 같은 Microsoft 제품에 배포 합니다.

+ [SQL Server Machine Learning Services (in-database)](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server (독립 실행형 서버, 비 SQL)](https://docs.microsoft.com/machine-learning-server/index)
+ [클라이언트 쪽 Python 라이브러리 (개발 워크스테이션)](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) 

이 연습에는 기반으로 선형 회귀 모델을 만드는 방법을 보여 줍니다 [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)에서 알고리즘 중 하 나와 **revoscalepy** 입력으로 계산 컨텍스트를 수락 하는 합니다. 이 연습에서 실행할 코드를 로컬에서 사용 하 여 원격 컴퓨팅 환경에 코드 실행을 이동 **revoscalepy** 계산 컨텍스트를 원격을 사용 하도록 설정 하는 함수입니다.

이 자습서를 완료 하 여 학습할 방법:

> [!div class="checklist"]
> * 사용 하 여 **revoscalepy** 선형 모델을 만들려면
> * 원격 계산 컨텍스트를 로컬에서 작업을 이동

## <a name="prerequisites"></a>필수 구성 요소

이 연습에서 사용 하는 샘플 데이터를 [ **flightdata** ](demo-data-airlinedemo-in-sql.md) 데이터베이스입니다.

이 문서의 샘플 코드를 실행 하는 IDE 및 IDE Python 실행 파일에 연결 되어 있어야 합니다.

계산 컨텍스트 전환 사례를 하려면를 [로컬 워크스테이션](../python/setup-python-client-tools-sql.md) 및 사용 하 여 SQL Server 데이터베이스 엔진 인스턴스 [Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 및 Python을 사용 하도록 설정 합니다. 

> [!Tip]
> 두 대의 컴퓨터에 없는 경우에 관련 응용 프로그램을 설치 하 여 하나의 물리적 컴퓨터에서 원격 계산 컨텍스트를 시뮬레이션할 수 있습니다. 첫 번째, 설치 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) "원격" 인스턴스로 작동 합니다. 두 번째, 설치 합니다 [작동 하는 Python 클라이언트 라이브러리](../python/setup-python-client-tools-sql.md) 클라이언트입니다. 두 개는 동일한 Python 배포와 동일한 컴퓨터에 Microsoft Python 라이브러리를 해야 합니다. 파일 경로 및 연습을 성공적으로 완료 하는 데 사용 하는 복사본을 Python.exe 추적 해야 합니다.

## <a name="remote-compute-contexts-and-revoscalepy"></a>원격 계산 컨텍스트 및 revoscalepy

이 샘플 클라이언트에서 작업 하지만 원격 환경, SQL Server, Spark 등의 작업이 실제로 수행 되는 Machine Learning Server를 선택할 수 있는 원격 계산 컨텍스트를에서 Python 모델을 만드는 과정을 보여 줍니다. 데이터가 상주 하는 계산을 적용할 원격 계산 컨텍스트는.

SQL Server에서 Python 코드를 실행 하려면 필요 합니다 **revoscalepy** 패키지 있습니다. 이 유사한 Microsoft에서 제공 하는 특별 한 Python 패키지를 **RevoScaleR** R 언어에 대 한 패키지입니다. 합니다 **revoscalepy** 패키지 계산 컨텍스트 만들기를 지원 하 고 로컬 워크스테이션 및 원격 서버 간에 데이터 및 모델을 전달 하기 위한 인프라를 제공 합니다. 합니다 **revoscalepy** 데이터베이스에서 코드 실행이 지 함수 [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver)합니다.

이 단원에서는 사용 하 여 데이터에서 SQL Server를 기반으로 선형 모델을 학습 하 [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)에서 함수 **revoscalepy** 매우 큰 데이터 집합을 통해 회귀를 지 합니다. 

이 단원에서는 기본 설정 하 고 다음을 사용 하는 방법 보여 줍니다는 **SQL Server 계산 컨텍스트에서** python에서입니다. 방법에 대 한 다른 플랫폼을 사용 하 여 계산 컨텍스트 작업 및 지원 되는 계산 컨텍스트 [Machine Learning Server에서 스크립트 실행에 대 한 계산 컨텍스트](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)합니다.


## <a name="run-the-sample-code"></a>샘플 코드를 실행 합니다.

데이터베이스를 준비 하 고는 테이블에 저장 된 학습 데이터는 Python 개발 환경을 엽니다 후 코드 샘플을 실행 합니다.

코드에는 다음 단계를 수행합니다.

1. 필요한 라이브러리 및 함수를 가져옵니다.
2. SQL Server에 연결을 만듭니다. 만듭니다 **데이터 원본** 데이터로 작업 하기 위한 개체입니다.
3. 사용 하 여 데이터 수정 **변환을** 로지스틱 회귀 알고리즘에서 사용할 수 있도록 합니다.
4. 호출 `rx_lin_mod` 및 모델에 맞게 사용 되는 수식을 정의 합니다.
5. 원래 데이터를 기반으로 예측 집합을 생성 합니다.
6. 예측된 값을 기반으로 요약을 만듭니다.

모든 작업은 SQL Server의 인스턴스를 사용 하 여 계산 컨텍스트로 수행 됩니다.

> [!NOTE]
> 명령줄에서 실행이 샘플을 보려면이이 비디오를 참조 하세요.: [Python 사용 하 여 SQL Server 2017 고급 분석](https://www.youtube.com/watch?v=FcoY795jTcc)

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

### <a name="defining-a-data-source-vs-defining-a-compute-context"></a>계산 컨텍스트 정의 및 데이터 원본 정의

데이터 원본에서 계산 컨텍스트를 다릅니다. 합니다 *데이터 원본* 코드에 사용 된 데이터를 정의 합니다. 계산 컨텍스트는 코드를 실행 하는 위치를 정의 합니다. 그러나 동일한 정보 중 일부를 사용합니다.

+ Python 변수인와 같은 `sql_query` 및 `sql_connection_string`, 데이터의 원본을 정의 합니다. 

    이러한 변수를 전달 합니다 [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) 생성자를 구현 하는 **데이터 원본 개체** 라는 `data_source`합니다.

+ 만든를 **계산 컨텍스트 개체** 사용 하 여 합니다 [RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserverdata) 생성자입니다. 결과 **계산 컨텍스트 개체** 이름은 `sql_cc`합니다.

    다시이 예제에서는 데이터 원본의 데이터를 계산 컨텍스트로 사용 하는 동일한 SQL Server 인스턴스에서 있음을 가정 하에서 사용 했던 동일한 연결 문자열을 사용 합니다. 
    
    그러나 데이터 원본 및 계산 컨텍스트는 다른 서버의 수 있습니다.
 
### <a name="changing-compute-contexts"></a>계산 컨텍스트를 변경합니다.

계산 컨텍스트를 정의한 후에 설정 해야 합니다 **활성 계산 컨텍스트**합니다. 

기본적으로 즉, 다른 계산 컨텍스트를 지정 하지 않으면 대부분의 작업을 로컬로 실행 하 고 데이터를 데이터 원본에서 인출 되 코드는 현재 Python 환경에서 실행 됩니다.

두 가지 방법으로 활성 계산 컨텍스트를 설정 합니다.
+ 메서드 또는 함수의 인수로 서
+ 호출 하 여 `rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>메서드 또는 함수의 인수로 서 계산 컨텍스트를 설정 합니다.

이 예제에서는 개인의 인수를 사용 하 여 계산 컨텍스트 설정 **rx** 함수입니다.
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

에 대 한 호출에서이 계산 컨텍스트는 다시 [rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary):

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rxsetcomputecontext"></a>명시적으로 rx_set_compute_context를 사용 하 여 계산 컨텍스트를 설정 합니다.

함수 [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) 계산 이미 정의 된 컨텍스트 사이 전환할 수 있습니다.

설정한 후에 활성 계산 컨텍스트, 활성 변경한까지.

### <a name="using-parallel-processing-and-streaming"></a>병렬 처리 및 스트리밍을 사용 하 여

계산 컨텍스트를 정의할 때 매개 변수를 계산 컨텍스트에서 데이터 처리 방법을 제어 하는 또한 설정할 수 있습니다. 이러한 매개 변수 데이터 원본 유형에 따라 달라 집니다.

SQL Server 계산 컨텍스트를 일괄 처리 크기 설정 수도 있고 작업 실행에 사용할 병렬 처리 수준에 대 한 힌트를 제공할 수 있습니다.

+ 샘플 4 개의 프로세서를 사용 하 여 컴퓨터에서 실행 되므로 `num_tasks` 매개 변수는 리소스의 최대 사용을 허용 하도록 4로 설정 됩니다. 
+ 이 값을 0으로 설정 하면 SQL Server 서버에 대 한 현재 MAXDOP 설정에서 최대한 많은 작업이 병렬로 실행 하는 기본값을 사용 합니다. 그러나 할당할 수 있는 태스크 수가 정확한 서버 설정과 같은 다른 많은 요소를 실행 하는 다른 작업에 따라 달라 집니다.

## <a name="next-steps"></a>다음 단계

이러한 추가 Python 샘플 및 자습서 원격 계산 컨텍스트 사용 뿐만 아니라 더 복잡 한 데이터 원본을 사용 하 여 종단 간 시나리오를 보여 줍니다.

+ [SQL 개발자를 위한 데이터베이스 내 Python](sqldev-in-database-python-for-sql-developers.md)
+ [Python 및 SQL Server를 사용 하 여 예측 모델 빌드](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
