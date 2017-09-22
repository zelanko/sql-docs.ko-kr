---
title: "Revoscalepy로 Python을 사용 하 여 모델을 만드는 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 09/19/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 4
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: c497ad3e302f2950a65cf41aaa41237f19171ab4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/21/2017

---
# <a name="use-python-with-revoscalepy-to-create-a-model"></a>Revoscalepy로 Python을 사용 하 여 모델을 만들려면

알고리즘을 사용 하 여 SQL Server에서 선형 회귀 모델을 만들 수는 방법을 보여 주는이 예제는 **revoscalepy** 패키지 합니다.

**revoscalepy** Python 포함 개체를 변환에 대해 제공 된 것과 유사한 알고리즘에 대 한 패키지는 **RevoScaleR** R 언어에 대 한 패키지입니다. 이 라이브러리와 계산 컨텍스트, 데이터를 변환 및 물류 및 선형 회귀, 의사 결정 트리 등과 같은 인기 있는 알고리즘을 사용 하 여 예측 모델을 학습 간에 데이터를 이동, 한 계산 컨텍스트를 만듭니다 수 있습니다.

자세한 내용은 참조 [revoscalepy 란?](../python/what-is-revoscalepy.md) 및 [Python 함수 참조](https://docs.microsoft.com/r-server/python-reference/introducing-python-package-reference)

## <a name="prerequisites"></a>필수 구성 요소

> [!IMPORTANT]
> SQL Server에서 Python 코드를 실행 하려면 먼저 설치 해야 SQL Server 2017 CTP 2.0 이상 및 설치 하 고 기능을 활성화 해야 **컴퓨터 학습 서비스** python 합니다. 다른 버전의 SQL Server는 Python 통합을 지원 하지 않습니다.

## <a name="run-the-sample-code"></a>샘플 코드를 실행 합니다.

이 코드에서는 다음 단계를 수행합니다.

1. 필요한 라이브러리 및 함수를 가져옵니다.
2. SQL Server에 연결 하 고 데이터로 작업 하기 위한 데이터 원본 개체를 만들고
3. 로지스틱 회귀 알고리즘에서 사용할 수 있도록 데이터를 수정 합니다.
4. 호출 `rx_lin_mod` 모델에 맞게 하는 데 사용 하는 수식을 정의 하 고
5. 원래 데이터 집합을 기반으로 예측 집합을 생성
6. 예측된 값을 기반으로 요약을 만듭니다.

SQL Server의 인스턴스를 사용 하 여 계산 컨텍스트로 써 모든 작업이 수행 됩니다.

일반적으로 원격 계산 컨텍스트에서 호출 Python 프로세스는 원격 계산 컨텍스트에서 R을 사용 하는 방법은 비슷합니다. 이 릴리스에서 제공 된 Python 통합 구성 요소를 포함 하는 Python 개발 환경을 사용 하 여 또는 명령줄에서 Python 스크립트와 샘플을 실행 합니다. 코드를 만들고 계산 컨텍스트 개체를 사용 하 여 특정 계산을 수행할 수 위치를 표시 합니다.

> [!NOTE]
> 데이터베이스 및 환경 이름을 적절 하 게 변경 해야 합니다.
> 
> 명령줄에서 실행이 샘플의 데모를 보려면이 비디오를 참조 하세요.: [python SQL Server 2017 고급 분석](https://www.youtube.com/watch?v=FcoY795jTcc)


### <a name="sample-code"></a>예제 코드

```python
from revoscalepy import RxComputeContext, RxInSqlServer, RxSqlServerData
from revoscalepy import rx_lin_mod, rx_predict, rx_summary
from revoscalepy import RxOptions, rx_import

from pandas import Categorical
import os

def test_linmod_sql():
    sql_server = os.getenv('PYTEST_SQL_SERVER', '.')
    
    sql_connection_string = 'Driver=SQL Server;Server=' + sqlServer + ';Database=PyTestDb;Trusted_Connection=True;'
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

## <a name="discussion"></a>토론

코드 검토 하 고 몇 가지 주요 단계를 강조 표시 해 보겠습니다.

### <a name="defining-a-data-source-and-compute-context"></a>원본 및 계산 컨텍스트는 데이터 정의

데이터 소스는 한 계산 컨텍스트와에서 다릅니다. _데이터 소스_ 코드에 사용 되는 데이터를 정의 합니다. _계산 컨텍스트_ 코드의 실행 수는 위치를 정의 합니다.

1. 과 같은 Python 변수를 만들 `sql_query` 및 `sql_connection_string`, 원본 및 사용 하려는 데이터를 정의 하는 합니다. 이러한 변수를 전달 하는 [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) 생성자를 구현 하는 **데이터 원본 개체** 라는 `data_source`합니다.
2. 계산 컨텍스트 개체를 사용 하 여 만들는 [RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserverdata) 생성자입니다. 이 예제에서는 계산 컨텍스트로 써 사용 하 여 동일한 SQL Server 인스턴스에서 데이터를 가정 하에서 이전에 정의 된 동일한 연결 문자열을 전달 합니다. 그러나 데이터 원본 및 계산 컨텍스트 서로 다른 서버에 있을 수 있습니다. 그 결과 **컨텍스트 개체를 계산** 라는 `sql_cc`합니다.
3. 현재 계산 컨텍스트를 선택 합니다. 기본적으로 즉, 다른 계산 컨텍스트를 지정 하지 않으면 작업을 로컬로 실행 하 고 데이터 원본에서 인출 되는 데이터가 모델 맞춤 현재 Python 환경에서 실행 됩니다.

### <a name="changing-compute-contexts"></a>계산 컨텍스트를 변경합니다.

이 예제에서는 개별의 인수를 사용 하 여 계산 컨텍스트로 설정 **rx** 함수입니다.
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

에 대 한 호출에서 적용 되는 동일한 **rxsummary**, 계산 컨텍스트를 다시 사용 합니다.

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

함수를 사용할 수도 있습니다 [rx_set_computecontext](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rx-set-compute-context) 이미 정의 하는 계산 컨텍스트를 전환할 수 있습니다.

### <a name="setting-the-degree-of-parallelism"></a>병렬 처리 수준을 설정

계산 컨텍스트를 정의할 때 매개 변수를 계산 컨텍스트에서 고 데이터를 처리 하는 방법을 제어 하는 설정할 수 있습니다. 이러한 매개 변수는 데이터 원본 유형에 따라 달라 집니다.

SQL Server 계산 컨텍스트를 위한 일괄 처리 크기를 설정 하거나 실행 중인 작업에 사용할 병렬 처리 수준에 대 한 힌트를 제공할 수 있습니다.

샘플 된 4 개의 프로세서가 있는 컴퓨터에서 실행 설정 되므로 *num_tasks* 4로 매개 변수입니다. 이 값을 0으로 설정 하면 SQL Server는 기본적으로 서버에 대 한 현재의 MAXDOP 설정 가능한 동시에 많은 작업을 실행 하는 것을 사용 합니다. 그러나 많은 프로세서를 포함 하는 서버에도 할당 될 수 있는 작업의 정확한 수에 따라 달라 집니다 서버 설정 등 다른 많은 요인 및 다른 실행 중인 작업을 합니다.

## <a name="related-samples"></a>관련 된 샘플

이러한 Python 샘플 및 고급 팁 및 종단 간 데모에 대 한 자습서를 참조 하십시오.

+ [SQL 개발자를 위해 데이터베이스에서 Python](sqldev-in-database-python-for-sql-developers.md)
+ [Python 및 SQL Server를 사용 하 여 예상 모델을 작성](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
+ [배포 및 Python 모델 사용](../python/publish-consume-python-code.md)

