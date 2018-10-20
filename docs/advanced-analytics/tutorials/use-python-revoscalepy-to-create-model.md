---
title: Revoscalepy를 사용 하 여 Python을 사용 하 여 모델을 만드는 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 5c8ff387c3abda3f147700dce6349009a027a778
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461959"
---
# <a name="use-python-with-revoscalepy-to-create-a-model"></a>Revoscalepy를 사용 하 여 Python을 사용 하 여 모델을 만들려면
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 단원에서는 SQL Server에서 선형 회귀 모델 만들기를 원격 개발 클라이언트에서 Python 코드를 실행 하는 방법을 알아봅니다. 

## <a name="prerequisites"></a>필수 구성 요소

+ 이 단원에서는 이전 단원 보다 다양 한 데이터를 사용합니다. 이전 단원을 먼저 완료 되어야 할 필요가 없습니다. 그러나 이전 단원을 완료 하 고 Python을 실행 하도록 이미 구성 서버가 있는 경우 해당 서버 및 데이터베이스 컨텍스트로 사용할를 계산 합니다.
+ 컨텍스트에 계산으로 SQL Server를 사용 하 여 Python 코드를 실행할 SQL Server 2017 이상이 필요 합니다. 명시적으로 설치 하 고 기능을 사용 하도록 설정 해야 게다가 **Machine Learning Services**, Python 언어 옵션을 선택 합니다.

    SQL Server 2017의 시험판 버전을 설치한 경우 업데이트 해야에 적어도 RTM 버전입니다. 서비스 릴리스 이후 계속 해 서에 확장 하 고 Python 기능을 향상 합니다. 이 자습서의 일부 기능은 초기 시험판 버전에서 작동 하지 않을 수 있습니다.

+ 이 예제에서는 라는 미리 정의 된 Python 환경에 `PYTEST_SQL_SERVER`입니다. 포함 하도록 구성 된 환경 **revoscalepy** 및 기타 필요한 라이브러리입니다. 

    Python을 실행 하도록 구성 된 environment가 없는 경우 별도로 수행 해야 합니다. 또는 Python 환경을 수정 하는 방법에 대 한 설명은이 자습서의 범위를 벗어났습니다. 올바른 라이브러리를 포함 하는 Python 클라이언트를 설정 하는 방법에 대 한 자세한 내용은 참조 하세요. [설치 Python 클라이언트](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) 하 고 [도구 링크 Python](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)합니다.

## <a name="remote-compute-contexts-and-revoscalepy"></a>원격 계산 컨텍스트 및 revoscalepy

이 샘플 원격에서 Python 모델을 만드는 과정을 보여 줍니다 _계산 컨텍스트_, 클라이언트에서 작업 하지만 원격 환경, SQL Server, Spark Machine Learning Server 등을 선택할 수 있는 위치는 작업이 실제로 수행 됩니다. 계산 컨텍스트를 사용 하 여 쉽게 코드를 한 번 작성 하 고 지원 되는 모든 환경에 배포 합니다.

SQL Server에서 Python 코드를 실행 하려면 필요 합니다 **revoscalepy** 패키지 있습니다. 이 유사한 Microsoft에서 제공 하는 특별 한 Python 패키지를 **RevoScaleR** R 언어에 대 한 패키지입니다. 합니다 **revoscalepy** 패키지 계산 컨텍스트 만들기를 지원 하 고 로컬 워크스테이션 및 원격 서버 간에 데이터 및 모델을 전달 하기 위한 인프라를 제공 합니다. 합니다 **revoscalepy** 데이터베이스에서 코드 실행이 지 함수 [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver)합니다.

이 단원에서는 사용 하 여 데이터에서 SQL Server를 기반으로 선형 모델을 학습 하 [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)에서 함수 **revoscalepy** 매우 큰 데이터 집합을 통해 회귀를 지 합니다. 

이 단원에서는 기본 설정 하 고 다음을 사용 하는 방법 보여 줍니다는 **SQL Server 계산 컨텍스트에서** python에서입니다. 방법에 대 한 다른 플랫폼을 사용 하 여 계산 컨텍스트 작업 및 지원 되는 계산 컨텍스트 [Machine Learning Server에서 스크립트 실행에 대 한 계산 컨텍스트](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)

## <a name="prepare-the-database-and-sample-data"></a>데이터베이스 및 샘플 데이터 준비

1. 이 단원에서는 데이터베이스를 사용 **sqlpy**합니다. 이전 단원 중 하나를 완료 하지 않은 경우에 다음 코드를 실행 하 여 데이터베이스를 만들 수 있습니다.

    ```sql
    CREATE DATABASE sqlpy;
    GO
    USE sqlpy;
    GO
    ```

    > [!IMPORTANT]
    > 다른 데이터베이스를 사용 하려는 경우에 샘플 코드를 편집 하 고 연결 문자열에 데이터베이스 이름을 변경 해야 합니다.

2. 이 샘플에서는 R 및 Python 모두에 사용할 수 있는 항공사 데이터 집합을 사용 합니다. Python 샘플에 대 한 데이터베이스를 만든 후 여기에 설명 된 대로 데이터를 사용 하 여 테이블을 채웁니다: [RevoScaleR의 데이터 샘플링](https://docs.microsoft.com/machine-learning-server/r/sample-built-in-data)합니다.

3. 클라이언트에서 사용할 수 있는 환경을 사용 하도록이 환경의 이름을 변경 합니다.

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

데이터 원본에서 계산 컨텍스트를 다릅니다. 합니다 _데이터 원본_ 코드에 사용 된 데이터를 정의 합니다. 합니다 _계산 컨텍스트_ 코드를 실행 하는 위치를 정의 합니다. 그러나 동일한 정보 중 일부를 사용합니다.

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

에 대 한 호출에서이 계산 컨텍스트는 다시 [rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary):입니다.

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rxsetcomputecontext"></a>명시적으로 rx_set_compute_context를 사용 하 여 계산 컨텍스트를 설정 합니다.

함수 [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) 계산 이미 정의 된 컨텍스트 사이 전환할 수 있습니다.

설정한 후에 활성 계산 컨텍스트, 활성 변경한까지.

### <a name="using-parallel-processing-and-streaming"></a>병렬 처리 및 스트리밍을 사용 하 여

계산 컨텍스트를 정의할 때 매개 변수를 계산 컨텍스트에서 데이터 처리 방법을 제어 하는 또한 설정할 수 있습니다. 이러한 매개 변수 데이터 원본 유형에 따라 달라 집니다.

SQL Server 계산 컨텍스트를 일괄 처리 크기 설정 수도 있고 작업 실행에 사용할 병렬 처리 수준에 대 한 힌트를 제공할 수 있습니다.

+ 샘플 4 개의 프로세서를 사용 하 여 컴퓨터에서 실행 되므로 `num_tasks` 매개 변수는 리소스의 최대 사용을 허용 하도록 4로 설정 됩니다. 
+ 이 값을 0으로 설정 하면 SQL Server 서버에 대 한 현재 MAXDOP 설정에서 최대한 많은 작업이 병렬로 실행 하는 기본값을 사용 합니다. 그러나 할당할 수 있는 태스크 수가 정확한 서버 설정과 같은 다른 많은 요소를 실행 하는 다른 작업에 따라 달라 집니다.

## <a name="related-samples"></a>관련 된 샘플

이러한 추가 Python 샘플 및 자습서 원격 계산 컨텍스트 사용 뿐만 아니라 더 복잡 한 데이터 원본을 사용 하 여 종단 간 시나리오를 보여 줍니다.

+ [SQL 개발자를 위한 데이터베이스 내 Python](sqldev-in-database-python-for-sql-developers.md)
+ [Python 및 SQL Server를 사용 하 여 예측 모델 빌드](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
+ [Python 및 SQL Server를 사용 하 여 예측 모델 빌드](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
