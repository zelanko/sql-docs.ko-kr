---
title: '빠른 시작: Python 스크립트 실행'
titleSuffix: SQL machine learning
description: SQL Server, 빅 데이터 클러스터 또는 Azure SQL Managed Instances에서 Machine Learning Services를 사용하여 간단한 Python 스크립트 세트를 실행합니다. 저장 프로시저 sp_execute_external_script를 사용하여 스크립트를 실행하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/28/2020
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.custom: contperfq1
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 9f2b729273362afd7a14cb60434416996b186557
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870174"
---
# <a name="quickstart-run-simple-python-scripts-with-sql-machine-learning"></a>빠른 시작: SQL 기계 학습에서 간단한 Python 스크립트 실행
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

이 빠른 시작에서는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md), [Azure SQL Managed Instance Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview) 또는 [SQL Server 빅 데이터 클러스터](../../big-data-cluster/machine-learning-services.md)를 사용하여 간단한 Python 스크립트 세트를 실행합니다. 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 SQL Server 인터페이스에서 스크립트를 실행하는 방법을 알아봅니다.

## <a name="prerequisites"></a>사전 요구 사항

이 빠른 시작을 실행하려면 다음과 같은 필수 구성 요소가 필요합니다.

- 다음 플랫폼 중 하나에 있는 SQL 데이터베이스:
  - [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md). 설치하려면 [Windows 설치 가이드](../install/sql-machine-learning-services-windows-install.md) 또는 [Linux 설치 가이드](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json)를 참조하세요.
  - SQL Server 빅 데이터 클러스터. [SQL Server 빅 데이터 클러스터에서 Machine Learning Services 사용](../../big-data-cluster/machine-learning-services.md)을 참조하세요.
  - Azure SQL Managed Instance Machine Learning Services. 자세한 내용은 [Azure SQL Managed Instance Machine Learning Services 개요](/azure/azure-sql/managed-instance/machine-learning-services-overview)를 참조하세요.

- Python 스크립트가 포함된 SQL 쿼리를 실행하기 위한 도구. 이 빠른 시작에서는 [Azure Data Studio](../../azure-data-studio/what-is.md)를 사용합니다.

## <a name="run-a-simple-script"></a>간단한 스크립트 실행

Python 스크립트를 실행하려면 이를 시스템 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 대한 인수로 전달합니다. 이 시스템 저장 프로시저는 SQL 기계 학습의 컨텍스트에서 Python 런타임을 시작하고 데이터를 Python으로 전달하고, Python 사용자 세션을 안전하게 관리하고, 모든 결과를 클라이언트에 반환합니다.

다음 단계에서는 데이터베이스에서 이 예제 Python 스크립트를 실행합니다.

```python
a = 1
b = 2
c = a/b
d = a*b
print(c, d)
```

1. SQL 인스턴스에 연결된 **Azure Data Studio** 에서 새 쿼리 창을 엽니다.

1. 전체 Python 스크립트를 `sp_execute_external_script` 저장 프로시저에 전달합니다.

   스크립트는 `@script` 인수를 통해 전달됩니다. `@script` 인수 안의 모든 항목이 유효한 Python 코드여야 합니다.

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

1. 올바른 결과가 계산되고 Python `print` 함수가 결과를 **메시지** 창에 반환합니다.

   다음과 비슷합니다.

    **결과**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>Hello World 스크립트 실행

일반적인 예제 스크립트는 "Hello World" 문자열만 출력하는 스크립트입니다. 다음 명령을 실행합니다.

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'OutputDataSet = InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

`sp_execute_external_script` 저장 프로시저에 대한 입력에는 다음이 포함됩니다.

| 입력 | Description |
|-|-|
| @language | 호출할 언어 확장을 정의합니다(이 경우에는 Python). |
| @script | Python 런타임으로 전달되는 명령을 정의합니다. 이 인수에서 전체 Python 스크립트는 유니코드 텍스트로 묶어야 합니다. **nvarchar** 형식의 변수에 텍스트를 추가한 다음, 변수를 호출할 수도 있습니다. |
| @input_data_1 | 쿼리에서 반환된 데이터는 Python 런타임에 전달되고, R 런타임은 데이터를 데이터 프레임으로 전달합니다. |
| WITH RESULT SETS | 절은 SQL 기계 학습에 대해 반환된 데이터 테이블의 스키마를 정의하여 "Hello World"를 열 이름으로 추가하고 데이터 형식으로 **int** 를 추가합니다. |

이 명령은 다음 텍스트를 출력합니다.

| Hello World |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>입력 및 출력 사용

기본적으로 `sp_execute_external_script`는 일반적으로 사용자가 유효한 SQL 쿼리의 형식으로 제공하는 단일 데이터 세트를 입력으로 사용합니다. 그런 후 단일 Python 데이터 프레임을 출력으로 반환합니다.

지금은 `sp_execute_external_script`의 기본 입력 및 출력을 사용합니다. **InputDataSet** 및 **OutputDataSet**.

1. 테스트 데이터의 작은 테이블을 만듭니다.

    ```sql
    CREATE TABLE PythonTestData (col1 INT NOT NULL)
    
    INSERT INTO PythonTestData
    VALUES (1);
    
    INSERT INTO PythonTestData
    VALUES (10);
    
    INSERT INTO PythonTestData
    VALUES (100);
    GO
    ```

1. `SELECT` 문을 사용하여 테이블을 쿼리합니다.
  
    ```sql
    SELECT *
    FROM PythonTestData
    ```

    **결과**

    ![PythonTestData 테이블의 콘텐츠](./media/select-pythontestdata.png)

1. 다음 Python 스크립트를 실행합니다. `SELECT` 문을 사용하여 테이블에서 데이터를 검색하고 Python 런타임을 통해 이를 전달하고 데이터를 데이터 프레임으로 반환합니다. `WITH RESULT SETS` 절은 SQL에 대한 반환된 데이터 테이블의 스키마를 정의하고, 열 이름 *NewColName* 을 추가합니다.

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **결과**

    ![테이블에서 데이터를 반환하는 Python 스크립트의 출력](./media/python-output-pythontestdata.png)

1. 이제 입력 및 출력 변수의 이름을 변경합니다. 기본 입력 및 출력 변수 이름은 **InputDataSet** 및 **OutputDataSet** 입니다. 다음 스크립트는 이름을 **SQL_in** 및 **SQL_out** 으로 변경합니다.

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'SQL_out = SQL_in;'
        , @input_data_1 = N'SELECT 12 as Col;'
        , @input_data_1_name  = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    Python은 대/소문자를 구분합니다. Python 스크립트(**SQL_out**, **SQL_in**)에 사용되는 입력 및 출력 변수는 대/소문자를 포함하여 `@input_data_1_name` 및 `@output_data_1_name`으로 정의된 이름과 일치해야 합니다.

    > [!TIP]
    > 하나의 입력 데이터 세트만 매개 변수로 전달할 수 있으며 하나의 데이터 세트만 반환할 수 있습니다. 그러나 Python 코드 내에서 다른 데이터 세트를 호출할 수 있으며 데이터 세트 외에 다른 유형의 출력을 반환할 수 있습니다. 또한 모든 매개 변수에 OUTPUT 키워드를 추가하여 결과와 함께 반환되게 만들 수 있습니다.

1. 또한 입력 데이터 없이 Python 스크립트를 사용하여 값을 생성할 수도 있습니다(`@input_data_1`이 빈 값으로 설정됨).

    다음 스크립트는 "hello" 및 "world" 텍스트를 출력합니다.

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'
    import pandas as pd
    mytextvariable = pandas.Series(["hello", " ", "world"]);
    OutputDataSet = pd.DataFrame(mytextvariable);
    '
        , @input_data_1 = N''
    WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
    ```

    **결과**

    ![@script를 입력으로 사용하는 쿼리 결과](./media/python-data-generated-output.png)

> [!NOTE]
> Python은 선행 공백을 사용하여 문을 그룹화합니다. 따라서 앞의 스크립트와 같이 포함된 Python 스크립트가 여러 줄에 걸쳐 있으면 SQL 명령과 일치하도록 Python 명령을 들여쓰기 하지 마십시오. 예를 들어 다음 스크립트는 오류가 발생합니다.
>
> ```sql
> EXECUTE sp_execute_external_script @language = N'Python'
>       , @script = N'
>       import pandas as pd
>       mytextvariable = pandas.Series(["hello", " ", "world"]);
>       OutputDataSet = pd.DataFrame(mytextvariable);
>       '
>       , @input_data_1 = N''
> WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
> ```

## <a name="check-python-version"></a>Python 버전 확인

서버에 설치된 Python 버전을 확인하려면 다음 스크립트를 실행합니다.

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import sys
print(sys.version)
'
GO
```

Python `print` 함수는 **메시지** 창에 버전을 반환합니다. 여기에서는 아래 출력 창에서 Python 버전 3.5.2가 설치된 것을 확인할 수 있습니다.

**결과**

```text
STDOUT message(s) from external script:
3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
```

## <a name="list-python-packages"></a>Python 패키지 나열

Microsoft는 Machine Learning Services와 함께 미리 설치된 여러 Python 패키지를 제공합니다.

버전을 포함하여 설치된 Python 패키지 목록을 보려면 다음 스크립트를 실행하세요.

```SQL
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import pkg_resources
import pandas
dists = [str(d) for d in pkg_resources.working_set]
OutputDataSet = pandas.DataFrame(dists)
'
WITH RESULT SETS(([Package] NVARCHAR(max)))
GO
```

이 목록은 Python의 `pkg_resources.working_set`에서 데이터 프레임으로 SQL에 반환됩니다.

**결과**

:::image type="content" source="media/python-package-list.png" alt-text="설치된 Python 패키지 목록":::

## <a name="next-steps"></a>다음 단계

SQL 기계 학습에서 Python을 사용할 때 데이터 구조를 사용하는 방법을 알아보려면 다음 빠른 시작을 수행하세요.

> [!div class="nextstepaction"]
> [빠른 시작: Python을 사용하는 데이터 구조 및 개체](quickstart-python-data-structures.md)
