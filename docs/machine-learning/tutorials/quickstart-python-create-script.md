---
title: '빠른 시작: Python 스크립트 실행'
description: SQL Server Machine Learning Services를 사용하여 간단한 Python 스크립트 집합을 실행합니다. 저장 프로시저 sp_execute_external_script를 사용하여 SQL Server 인터페이스에서 스크립트를 실행하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/27/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8c1347d58f0b8a4014a51a220b6ecded5a343082
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116356"
---
# <a name="quickstart-run-simple-python-scripts-with-sql-server-machine-learning-services"></a>빠른 시작: SQL Server Machine Learning Services로 간단한 Python 스크립트 실행
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 빠른 시작에서는 [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md)를 사용하여 간단한 Python 스크립트 세트를 실행합니다. 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 SQL Server 인터페이스에서 스크립트를 실행하는 방법을 알아봅니다.

## <a name="prerequisites"></a>사전 요구 사항

- 이 빠른 시작을 수행하려면 Python 언어가 설치된 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)가 포함된 SQL Server 인스턴스에 대한 액세스 권한이 필요합니다.

- 또한 Python 스크립트가 포함된 SQL 쿼리를 실행하기 위한 도구가 필요합니다. SQL Server 인스턴스에 연결할 수 있는 데이터베이스 관리 또는 쿼리 도구를 사용하여 이러한 스크립트를 실행하고 T-SQL 쿼리 또는 저장 프로시저를 실행할 수 있습니다. 이 빠른 시작에서는 [SSMS(SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)를 사용합니다.

## <a name="run-a-simple-script"></a>간단한 스크립트 실행

Python 스크립트를 실행하려면 이를 시스템 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 대한 인수로 전달합니다.
이 시스템 저장 프로시저는 SQL Server의 컨텍스트에서 Python 런타임을 시작하고 데이터를 Python으로 전달하고, Python 사용자 세션을 안전하게 관리하고, 모든 결과를 클라이언트에 반환합니다.

다음 단계에서는 이 예제 Python 스크립트를 SQL Server 인스턴스에서 실행합니다.

```python
a = 1
b = 2
c = a/b
d = a*b
print(c, d)
```

1. SQL Server 인스턴스에 연결된 **SQL Server Management Studio**에서 새 쿼리 창을 엽니다.

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

| | |
|-|-|
| @language | 호출할 언어 확장을 정의합니다(이 경우에는 Python). |
| @script | Python 런타임으로 전달되는 명령을 정의합니다.<br>이 인수에서 전체 Python 스크립트는 유니코드 텍스트로 묶어야 합니다. **nvarchar** 형식의 변수에 텍스트를 추가한 다음, 변수를 호출할 수도 있습니다. |
| @input_data_1 | 쿼리로 반환되고 Python 런타임으로 전달되는 데이터입니다. 데이터를 SQL Server에 데이터 프레임으로 반환합니다. |
|WITH RESULT SETS | 이 절은 SQL Server에 대해 반환된 데이터 테이블의 스키마를 정의합니다. 이 경우에는 "Hello World"를 열 이름 및 **int**(데이터 형식)로 추가합니다. |

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

1. 다음 Python 스크립트를 실행합니다. `SELECT` 문을 사용하여 테이블에서 데이터를 검색하고 Python 런타임을 통해 이를 전달하고 데이터를 데이터 프레임으로 반환합니다. `WITH RESULT SETS` 절은 SQL에 대한 반환된 데이터 테이블의 스키마를 정의하고, 열 이름 *NewColName*을 추가합니다.

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **결과**

    ![테이블에서 데이터를 반환하는 Python 스크립트의 출력](./media/python-output-pythontestdata.png)

1. 이제 입력 및 출력 변수의 이름을 변경합니다. 기본 입력 및 출력 변수 이름은 **InputDataSet** 및 **OutputDataSet**입니다. 다음 스크립트는 이름을 **SQL_in** 및 **SQL_out**으로 변경합니다.

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

  ```text
  EXECUTE sp_execute_external_script @language = N'Python'
      , @script = N'
      import pandas as pd
      mytextvariable = pandas.Series(["hello", " ", "world"]);
      OutputDataSet = pd.DataFrame(mytextvariable);
      '
      , @input_data_1 = N''
  WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
  ```

## <a name="check-python-version"></a>Python 버전 확인

SQL Server 인스턴스에 설치된 Python 버전을 확인하려면 다음 스크립트를 실행하세요.

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

Microsoft는 SQL Server 인스턴스에서 SQL Server Machine Learning Services로 사전 설치된 여러 Python 패키지를 제공합니다.

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

SQL Server Machine Learning Services에서 Python을 사용할 때 데이터 구조를 사용하는 방법을 알아보려면 다음 빠른 시작을 참조하세요.

> [!div class="nextstepaction"]
> [빠른 시작: SQL Server Machine Learning Services에서 Python을 사용하는 데이터 구조 및 개체](quickstart-python-data-structures.md)

SQL Server Machine Learning Services에서 Python 사용에 대한 자세한 내용은 다음 문서를 참조하세요.

- [SQL Server Machine Learning Services를 사용하여 고급 Python 함수 작성](quickstart-python-functions.md)
- [SQL Server Machine Learning Services를 사용하여 Python에서 예측 모델 만들기 및 점수 매기기](quickstart-python-train-score-model.md)
- [SQL Server Machine Learning Services(Python 및 R)란?](../what-is-sql-server-machine-learning.md)
