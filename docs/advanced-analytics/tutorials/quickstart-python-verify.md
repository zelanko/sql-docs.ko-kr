---
title: SQL Server에 있는 Python 확인 하기 위한 빠른 시작
description: Python 및 Machine Learning Services SQL Server에 있는지 확인 하기 위한 빠른 시작입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 25bf5a7e7d18810c782d1ce2f4986fc433421395
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57577933"
---
# <a name="quickstart-verify-python-exists-in-sql-server"></a>빠른 시작: SQL Server에 Python이 있는지 확인 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server에 있는 SQL Server 데이터에 대 한 데이터 과학 분석에 대 한 Python 언어 지원이 포함 됩니다. 다음 방법 중 하나를 사용 하 여 저장된 프로시저를 통해 스크립트 실행이 됩니다.

+ 기본 제공 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 저장 프로시저에서 Python 스크립트를 입력된 매개 변수로 전달 합니다.
+ Python 스크립트를 래핑하는 [사용자 지정 저장 프로시저](sqldev-in-database-r-for-sql-developers.md) 만든 합니다.

이 빠른 시작에서는 하는지 확인 [SQL Server 2017의 Machine Learning Services](../what-is-sql-server-machine-learning.md) 설치 및 구성 합니다.

## <a name="prerequisites"></a>사전 요구 사항

이 연습에 사용 하 여 SQL server 인스턴스에 대 한 액세스 필요 [SQL Server 2017의 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 설치 합니다.

SQL Server 인스턴스는 Azure 가상 머신 또는 온-프레미스에 있을 수 있습니다. 해야 하므로 해당 외부 스크립팅 기능이 기본적으로 비활성화 됩니다는 알고 있어야 [외부 스크립팅을 사용 하도록 설정](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) 되어 있는지 확인 하 고 **SQL Server 실행 패드 서비스** 시작 하기 전에 실행 됩니다.

또한 SQL 쿼리를 실행 하기 위한 도구가 필요 합니다. 데이터베이스 관리를 사용 하 여 Python 스크립트를 실행할 수도 있고 SQL Server 인스턴스에 연결 하는 T-SQL 쿼리 또는 저장된 프로시저를 실행 하기만 도구인 쿼리 수 있습니다. 이 빠른 시작에서는 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)합니다.

## <a name="verify-python-exists"></a>Python 있는지 확인

확인할 수 있습니다는 Machine Learning 서비스 (SQL Server 인스턴스 및 설치 된 Python의 버전에 대 한 활성화 됩니다. 다음 단계를 수행 합니다.

1. SQL Server Management Studio를 열고 SQL Server 인스턴스에 연결 합니다.

2. 아래 코드를 실행 합니다. 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import sys
    print(sys.version)';
    GO
    ```

3. Python `print` 함수는 버전을 반환 합니다 **메시지** 창입니다. 다음 예제 출력에서 볼 수 있습니다 SQL Server에이 경우 Python 버전 3.5.2 설치 해야 합니다.

    **결과**

    ```text
    STDOUT message(s) from external script: 
    3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
    ```

오류가 발생 하는 경우 인스턴스 및 Python 통신할 수 있도록 할 수 있는 작업의 다양 한 사항이 있습니다.

먼저 설치 문제를 배제 합니다. 설치 후 구성은 외부 코드 라이브러리를 사용 하도록 설정 하려면 필요 합니다. 참조 [SQL Server 2017 Machine Learning 서비스 설치](../install/sql-machine-learning-services-windows-install.md)합니다. 마찬가지로, 실행 패드 서비스가 실행 중인지 확인 합니다.

Windows 사용자 그룹을 추가 해야 `SQLRUserGroup` 실행 패드에 Python 및 SQL Server 간의 통신을 제공할 수 있는지 확인 하는 인스턴스 로그인으로 합니다. (동일한 그룹에는 모두 R 및 Python 코드 실행 합니다.) 자세한 내용은 [암시적된 인증 사용](../security/add-sqlrusergroup-to-database.md)합니다.

또한 비활성화 된 네트워크 프로토콜을 사용 하도록 설정 하거나 SQL Server는 외부 클라이언트와 통신할 수 있도록 방화벽을 열기 해야 합니다. 자세한 내용은 [설치 문제 해결](../common-issues-external-script-execution.md)합니다.

## <a name="call-revoscalepy-functions"></a>Revoscalepy 함수를 호출 합니다.

확인 하려면 **revoscalepy** 수를 포함 하는 예제 스크립트 실행 [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) 통계 요약 데이터를 생성 하는 합니다. 아래 스크립트 revoscalepy에 포함 된 기본 제공 샘플에서 샘플.xdf 데이터 파일을 검색 하는 방법에 설명 합니다. RxOptions 함수를 제공 합니다 **sampleDataDir** 샘플 파일의 위치를 반환 하는 매개 변수입니다.

Rx_summary 형식의 개체를 반환 하므로 `class revoscalepy.functions.RxSummary.RxSummaryResults`여러 요소를 포함 하는, pandas를 사용 하 여 바로 테이블 형식으로 데이터 프레임을 추출 합니다.

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

## <a name="list-python-packages"></a>Python 패키지를 나열 합니다.

Microsoft는 다양 한 SQL Server 인스턴스에서 Machine Learning 서비스를 사용 하 여 미리 설치 된 Python 패키지를 제공 합니다. python 패키지 설치 된 버전을 포함 하 여 목록을 보려면 다음 단계를 수행 합니다.

1. SQL Server 인스턴스에서 아래 스크립트를 실행 합니다.

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import pip
    for i in pip.get_installed_distributions():
        print(i)';
    GO
    ```

2. 출력은 `pip.get_installed_distributions()` Python에서 반환 하 고 `STDOUT` 메시지입니다.

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

인스턴스 Python과 함께 사용할 준비가 되었는지 확인 했으므로 자세히 보기 기본 Python 상호 작용을 수행 합니다.

> [!div class="nextstepaction"]
> [빠른 시작: SQL Server에서 "hello world" Python 스크립트](quickstart-python-run-using-t-sql.md)
