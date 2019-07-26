---
title: SQL Server에 Python 확인을 위한 빠른 시작이 있습니다.
description: Python 및 Machine Learning Services가 SQL Server에 있는지 확인 하기 위한 빠른 시작입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0dd5714f47c90c0091daacbd792b80c05ec68675
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469695"
---
# <a name="quickstart-verify-python-exists-in-sql-server"></a>빠른 시작: SQL Server에 Python이 있는지 확인 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server에는 상주 하는 SQL Server 데이터에 대 한 데이터 과학 분석에 대 한 Python 언어 지원이 포함 됩니다. 다음 방법 중 하나를 사용 하 여 저장 프로시저를 통해 스크립트를 실행 합니다.

+ 에서 Python 스크립트를 입력 매개 변수로 전달 하는 기본 제공 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 저장 프로시저입니다.
+ 사용자가 만든 [사용자 지정 저장 프로시저](sqldev-in-database-r-for-sql-developers.md) 에 Python 스크립트를 래핑합니다.

이 빠른 시작에서는 [SQL Server 2017 Machine Learning Services](../what-is-sql-server-machine-learning.md) 설치 및 구성 되었는지 확인 합니다.

## <a name="prerequisites"></a>사전 요구 사항

이 연습을 수행 하려면 [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 설치 된 SQL Server 인스턴스에 대 한 액세스가 필요 합니다.

SQL Server 인스턴스는 Azure 가상 머신 또는 온-프레미스에 있을 수 있습니다. 외부 스크립팅 기능은 기본적으로 사용 하지 않도록 설정 되어 있으므로 [외부 스크립팅을 사용 하도록 설정](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) 하 고 시작 하기 전에 **SQL Server 실행 패드 서비스가** 실행 중인지 확인 해야 할 수 있습니다.

또한 SQL 쿼리를 실행 하기 위한 도구도 필요 합니다. SQL Server 인스턴스에 연결 하 고 T-sql 쿼리 또는 저장 프로시저를 실행 하는 경우 모든 데이터베이스 관리 또는 쿼리 도구를 사용 하 여 Python 스크립트를 실행할 수 있습니다. 이 빠른 시작에서는 [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)를 사용 합니다.

## <a name="verify-python-exists"></a>Python 존재 확인

Machine Learning Services (SQL Server 인스턴스에 대해 사용 하도록 설정 되 고 Python 버전이 설치 되어 있는지 확인할 수 있습니다. 다음 단계를 수행 합니다.

1. SQL Server Management Studio를 열고 SQL Server 인스턴스에 연결 합니다.

2. 아래 코드를 실행 합니다. 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import sys
    print(sys.version)';
    GO
    ```

3. Python `print` 함수는 버전을 **메시지** 창에 반환 합니다. 아래 예제 출력에서이 경우 SQL Server Python 버전 3.5.2이 설치 되어 있는 것을 확인할 수 있습니다.

    **결과**

    ```text
    STDOUT message(s) from external script: 
    3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
    ```

오류가 발생 하면 인스턴스와 Python이 통신할 수 있도록 다양 한 작업을 수행할 수 있습니다.

먼저 설치 문제를 모두 처리 합니다. 외부 코드 라이브러리를 사용 하도록 설정 하려면 설치 후 구성이 필요 합니다. [SQL Server 2017 Machine Learning Services 설치](../install/sql-machine-learning-services-windows-install.md)를 참조 하세요. 마찬가지로 실행 패드 서비스가 실행 중인지 확인 합니다.

또한 실행 패드에서 Python과 SQL Server 간에 `SQLRUserGroup` 통신을 제공할 수 있도록 Windows 사용자 그룹을 인스턴스의 로그인으로 추가 해야 합니다. 동일한 그룹이 R 및 Python 코드 실행에 모두 사용 됩니다. 자세한 내용은 [SQLRUserGroup에 대 한 로그인 만들기](../security/create-a-login-for-sqlrusergroup.md)를 참조 하세요.

또한 사용 하지 않도록 설정 된 네트워크 프로토콜을 사용 하도록 설정 하거나, SQL Server에서 외부 클라이언트와 통신할 수 있도록 방화벽을 열어야 할 수도 있습니다. 자세한 내용은 [설치 문제 해결](../common-issues-external-script-execution.md)을 참조 하세요.

## <a name="call-revoscalepy-functions"></a>Revoscalepy 함수 호출

**Revoscalepy** 를 사용할 수 있는지 확인 하려면 통계 요약 데이터를 생성 하는 [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) 를 포함 하는 예제 스크립트를 실행 합니다. 다음 스크립트는 revoscalepy에 포함 된 기본 제공 샘플에서 .sample df 데이터 파일을 검색 하는 방법을 보여 줍니다. RxOptions 함수는 샘플 파일의 위치를 반환 하는 **sampleDataDir** 매개 변수를 제공 합니다.

Rx_summary는 여러 요소를 포함 하 `class revoscalepy.functions.RxSummary.RxSummaryResults`는 형식의 개체를 반환 하므로 pandas를 사용 하 여 데이터 프레임을 테이블 형식 으로만 추출할 수 있습니다.

```sql
EXEC sp_execute_external_script @language = N'Python', 
@script = N'
import os
from pandas import DataFrame
from revoscalepy import rx_summary
from revoscalepy import RxXdfData
from revoscalepy import RxOptions

sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay + DayOfWeek", ds)
print(summary)
dfsummary = summary.summary_data_frame
OutputDataSet = dfsummary
'
WITH RESULT SETS  ((ColName nvarchar(25) , ColMean float, ColStdDev  float, ColMin  float,   ColMax  float, Col_ValidObs  float, Col_MissingObs int))
```

## <a name="list-python-packages"></a>Python 패키지 나열

Microsoft에서는 SQL Server 인스턴스에서 Machine Learning Services와 함께 미리 설치 된 많은 Python 패키지를 제공 합니다. 버전을 포함 하 여 설치 된 Python 패키지 목록을 보려면 다음 단계를 수행 합니다.

1. SQL Server 인스턴스에서 아래 스크립트를 실행 합니다.

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import pip
    for i in pip.get_installed_distributions():
        print(i)';
    GO
    ```

2. 출력은 Python의 `pip.get_installed_distributions()` 에서 가져온 것 이며 `STDOUT` 메시지로 반환 됩니다.

    **결과**

    ```text
    STDOUT message(s) from external script: 
    xlwt 1.2.0
    XlsxWriter 0.9.6
    xlrd 1.0.0
    win-unicode-console 0.5
    widgetsnbextension 2.0.0
    wheel 0.29.0
    Werkzeug 0.12.1
    wcwidth 0.1.7
    unicodecsv 0.14.1
    traitlets 4.3.2
    tornado 4.4.2
    toolz 0.8.2
    testpath 0.3
    tables 3.2.2
    sympy 1.0
    statsmodels 0.8.0
    sqlparse 0.1.19
    SQLAlchemy 1.1.9
    snowballstemmer 1.2.1
    six 1.10.0
    simplegeneric 0.8.1
    seaborn 0.7.1
    scipy 0.19.0
    scikit-learn 0.18.1
    ...
    ```

## <a name="next-steps"></a>다음 단계

이제 인스턴스가 Python을 사용할 준비가 되었는지 확인 했으므로 기본적인 Python 상호 작용에 대해 자세히 살펴보겠습니다.

> [!div class="nextstepaction"]
> [빠른 시작: SQL Server에서 "Hello 세계" Python 스크립트](quickstart-python-run-using-t-sql.md)
