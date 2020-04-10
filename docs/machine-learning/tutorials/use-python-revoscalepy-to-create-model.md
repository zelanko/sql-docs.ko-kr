---
title: Python 모델 만들기 - revoscalepy
description: revoscalepy 함수를 사용하여 SQL Server에서 원격으로 실행되는 데이터 과학 모델을 만드는 Python 스크립트를 작성합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5faa8688f3036f80b947ccc5d99c09c4612f26fb
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116026"
---
# <a name="use-python-with-revoscalepy-to-create-a-model-that-runs-remotely-on-sql-server"></a>revoscalepy와 함께 Python을 사용하여 SQL Server에서 원격으로 실행되는 모델 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Microsoft의 [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) Python 라이브러리는 데이터 탐색, 시각화, 변환 및 분석을 위한 데이터 과학 알고리즘을 제공합니다. 이 라이브러리는 SQL Server의 Python 통합 시나리오에서 전략적으로 중요합니다. 다중 코어 서버에서는 **revoscalepy** 함수를 병렬로 실행할 수 있습니다. 중앙 서버와 클라이언트 워크스테이션(별도의 물리적 컴퓨터, 모두 동일한 **revoscalepy** 라이브러리를 갖고 있음)을 사용하는 분산 아키텍처에서는 실행을 로컬로 시작한 후 데이터가 상주하는 원격 SQL Server 인스턴스로 이동하는 Python 코드를 작성할 수 있습니다.

**revoscalepy**는 다음과 같은 Microsoft 제품 및 배포판에서 찾을 수 있습니다.

+ [SQL Server Machine Learning Services(데이터베이스 내)](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server(비-SQL, 독립 실행형 서버)](https://docs.microsoft.com/machine-learning-server/index)
+ [클라이언트 쪽 Python 라이브러리(개발 워크스테이션의 경우)](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) 

이 연습에서는 컴퓨팅 컨텍스트를 입력으로 허용하는 **revoscalepy**의 알고리즘 중 하나인 [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)를 기반으로 선형 회귀 모델을 만드는 방법을 보여줍니다. 이 연습에서 실행할 코드는 원격 컴퓨팅 컨텍스트를 지원하는 **revoscalepy** 함수를 사용하여 코드 실행을 로컬에서 원격 컴퓨팅 환경으로 이동합니다.

이 자습서를 완료하면 다음 작업 방법을 배울 수 있습니다.

> [!div class="checklist"]
> * **revoscalepy**를 사용하여 선형 모델 만들기
> * 작업을 로컬에서 원격 컴퓨팅 컨텍스트로 이동

## <a name="prerequisites"></a>사전 요구 사항

이 연습에 사용되는 샘플 데이터는 [**flightdata**](demo-data-airlinedemo-in-sql.md) 데이터베이스입니다.

이 문서의 샘플 코드를 실행하려면 IDE가 필요하며, IDE는 Python 실행 파일에 연결되어야 합니다.

컴퓨팅 컨텍스트 이동을 연습하려면 [로컬 워크스테이션](../python/setup-python-client-tools-sql.md)과 [Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 및 Python을 사용하는 SQL Server 데이터베이스 엔진 인스턴스가 필요합니다. 

> [!Tip]
> 컴퓨터가 하나밖에 없는 경우 관련 애플리케이션을 설치하여 물리적 컴퓨터 한 대로 원격 컴퓨팅 컨텍스트를 시뮬레이션할 수 있습니다. 첫째, [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 설치는 "원격" 인스턴스로 작동합니다. 둘째, [Python 클라이언트 라이브러리 설치](../python/setup-python-client-tools-sql.md)는 클라이언트로 작동합니다. 동일한 머신에 동일한 Python 배포판 및 Microsoft Python 라이브러리의 복사본 두 개가 생성됩니다. 연습을 성공적으로 완료하려면 파일 경로와 사용하는 Python.exe의 복사본을 계속 추적해야 합니다.

## <a name="remote-compute-contexts-and-revoscalepy"></a>원격 컴퓨팅 컨텍스트 및 revoscalepy

이 샘플은 원격 컴퓨팅 컨텍스트에서 Python 모델을 만드는 프로세스를 보여줍니다. 이렇게 하면 클라이언트에서 작업을 수행할 수 있지만, 작업이 실제로 수행되는 SQL Server, Spark 또는 Machine Learning Server 같은 원격 환경을 선택해야 합니다. 원격 컴퓨팅 컨텍스트의 목적은 데이터가 상주하는 위치로 컴퓨팅을 가져오는 것입니다.

SQL Server에서 Python 코드를 실행 하려면 **revoscalepy** 패키지가 필요합니다. 이 패키지는 Microsoft에서 제공하는 특수 Python 패키지이며, R 언어용 **RevoScaleR** 패키지와 비슷합니다. **revoscalepy** 패키지는 컴퓨팅 컨텍스트 만들기를 지원하며, 로컬 워크스테이션과 원격 서버 간에 데이터와 모델을 전달하기 위한 인프라를 제공합니다. 데이터베이스 내 코드 실행을 지원하는 **revoscalepy** 함수는 [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver)입니다.

이 단원에서는 매우 큰 데이터 세트에 대한 회귀를 지원하는 **revoscalepy**의 함수인 [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)를 기반으로 SQL Server의 데이터를 사용하여 선형 모델을 학습시킵니다. 

또한 이 단원에서는 Python에서 **SQL Server 컴퓨팅 컨텍스트**를 설정하고 사용하는 방법의 기본 사항도 보여줍니다. 컴퓨팅 컨텍스트가 다른 플랫폼과 함께 작동하는 방법 및 지원되는 컴퓨팅 컨텍스트에 대한 자세한 내용은 [Machine Learning Server에서 스크립트를 실행하기 위한 컴퓨팅 컨텍스트](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)를 참조하세요.


## <a name="run-the-sample-code"></a>샘플 코드 실행

데이터베이스를 준비하고 학습용 데이터를 테이블에 저장한 후에는 Python 개발 환경을 열고 코드 샘플을 실행합니다.

이 코드는 다음 단계를 수행합니다.

1. 필요한 라이브러리 및 함수를 가져옵니다.
2. SQL Server에 대한 연결을 만듭니다. 데이터를 작업하기 위한 **데이터 원본** 개체를 만듭니다.
3. 로지스틱 회귀 알고리즘에 사용할 수 있도록 **변환**을 사용하여 데이터를 수정합니다.
4. `rx_lin_mod`를 호출하고 모델 조정에 사용되는 수식을 정의합니다.
5. 원본 데이터를 기반으로 예측 세트를 생성합니다.
6. 예상된 값을 기준으로 요약을 만듭니다.

모든 작업은 SQL Server 인스턴스를 컴퓨팅 컨텍스트로 사용하여 수행됩니다.

> [!NOTE]
> 명령줄에서 이 샘플을 실행하는 데모는 다음 비디오를 참조하세요. [Python을 사용하는 SQL Server 2017 고급 분석](https://www.youtube.com/watch?v=FcoY795jTcc)

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

### <a name="defining-a-data-source-vs-defining-a-compute-context"></a>데이터 원본 정의와 컴퓨팅 컨텍스트 정의의 비교

데이터 원본은 컴퓨팅 컨텍스트와 다릅니다. *데이터 원본*은 코드에 사용되는 데이터를 정의합니다. 컴퓨팅 컨텍스트는 코드가 실행될 위치를 정의합니다. 그러나 다음과 같은 동일한 정보를 둘 다 사용합니다.

+ 데이터 원본을 정의하는 `sql_query` 및 `sql_connection_string` 같은 Python 변수. 

    이러한 변수를 [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) 생성자에 전달하여 `data_source`라는 **데이터 원본 개체**을 구현합니다.

+ [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) 생성자를 사용하여 **컴퓨팅 컨텍스트 개체**를 만듭니다. 그 결과로 얻는 **컴퓨팅 컨텍스트 개체**의 이름은 `sql_cc`입니다.

    이 예제에서는 데이터가 컴퓨팅 컨텍스트로 사용할 SQL Server 인스턴스와 동일한 인스턴스에 있다는 가정 하에 데이터 원본에서 사용한 것과 동일한 연결 문자열을 다시 사용 합니다. 
    
    그러나 데이터 원본과 컴퓨팅 컨텍스트가 서로 다른 서버에 있을 수 있습니다.
 
### <a name="changing-compute-contexts"></a>컴퓨팅 컨텍스트 변경

컴퓨팅 컨텍스트를 정의한 후에는 **활성 컴퓨팅 컨텍스트**를 설정해야 합니다. 

기본적으로 대부분의 작업은 로컬로 실행됩니다. 즉, 다른 컴퓨팅 컨텍스트를 지정하지 않으면 데이터 원본에서 데이터가 페치되고, 코드가 현재 Python 환경에서 실행됩니다.

다음과 같이 활성 컴퓨팅 컨텍스트를 설정하는 두 가지 방법이 있습니다.
+ 메서드 또는 함수의 인수로
+ `rx_set_computecontext` 호출

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>컴퓨팅 컨텍스트를 메서드 또는 함수의 인수로 설정

이 예제에서는 개별 **rx** 함수의 인수를 사용하여 컴퓨팅 컨텍스트를 설정합니다.
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

이 컴퓨팅 컨텍스트는 [rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) 호출에서 다시 사용됩니다.

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rx_set_compute_context"></a>rx_set_compute_context를 사용하여 명시적으로 컴퓨팅 컨텍스트 설정

[rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) 함수를 사용하면 이미 정의된 컴퓨팅 컨텍스트 간에 전환할 수 있습니다.

활성 컴퓨팅 컨텍스트를 설정하면 변경할 때까지 활성 상태로 유지됩니다.

### <a name="using-parallel-processing-and-streaming"></a>병렬 처리 및 스트리밍 사용

컴퓨팅 컨텍스트를 정의할 때 컴퓨팅 컨텍스트에서 데이터를 처리하는 방법을 제어하는 매개 변수를 설정할 수도 있습니다. 이러한 매개 변수는 데이터 원본 형식에 따라 다릅니다.

SQL Server 컴퓨팅 컨텍스트의 경우 일괄 처리 크기를 설정하거나 실행 중인 작업에 사용할 병렬 처리 수준에 대한 힌트를 제공할 수 있습니다.

+ 샘플은 4개의 프로세서가 있는 컴퓨터에서 실행되었으므로, `num_tasks` 매개 변수는 리소스를 최대로 사용할 수 있도록 4로 설정됩니다. 
+ 이 값을 0으로 설정하면 SQL Server는 서버의 현재 MAXDOP 설정 하에서 기본값을 사용하며, 기본값은 최대한 많은 작업을 병렬로 실행합니다. 그러나 할당될 수 있는 작업의 정확한 수는 서버 설정, 실행 중인 다른 작업 등의 여러 요소에 따라 다릅니다.

## <a name="next-steps"></a>다음 단계

다음 추가 Python 샘플 및 자습서에서는 원격 컴퓨팅 컨텍스트 사용 외에도 좀 더 복잡한 데이터 원본을 사용하는 엔드투엔드 시나리오를 보여줍니다.

+ [SQL 개발자를 위한 데이터베이스 내 Python](sqldev-in-database-python-for-sql-developers.md)
+ [Python 및 SQL Server를 사용하여 예측 모델 빌드](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
