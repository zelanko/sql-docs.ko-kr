---
title: 간단한 Python 스크립트 만들기 및 실행
titleSuffix: SQL Server Machine Learning Services
description: SQL Server Machine Learning Services를 사용 하 여 SQL Server 인스턴스에서 간단한 Python 스크립트를 만들고 실행 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ecf99f1ae70cf44b32955ae164dbe3017bdf5f24
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72006122"
---
# <a name="quickstart-create-and-run-simple-python-scripts-with-sql-server-machine-learning-services"></a>빠른 시작: SQL Server Machine Learning Services를 사용 하 여 간단한 Python 스크립트 만들기 및 실행
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 빠른 시작에서는 [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md)를 사용 하 여 간단한 Python 스크립트 집합을 만들고 실행 합니다. 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 에서 올바른 형식의 Python 스크립트를 래핑하고 SQL Server 인스턴스에서 스크립트를 실행 하는 방법에 대해 알아봅니다.

## <a name="prerequisites"></a>사전 요구 사항

- 이 빠른 시작에서는 Python 언어가 설치 된 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 를 사용 하 여 SQL Server 인스턴스에 액세스할 수 있어야 합니다.

- 또한 Python 스크립트를 포함 하는 SQL 쿼리를 실행 하기 위한 도구도 필요 합니다. 모든 데이터베이스 관리 또는 쿼리 도구를 사용 하 여 이러한 스크립트를 실행 하 고 SQL Server 인스턴스에 연결 하 고 T-sql 쿼리 또는 저장 프로시저를 실행할 수 있습니다. 이 빠른 시작에서는 [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)를 사용 합니다.

## <a name="run-a-simple-script"></a>간단한 스크립트 실행

Python 스크립트를 실행 하려면 시스템 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 인수로 전달 합니다.
이 시스템 저장 프로시저는 SQL Server 컨텍스트에서 Python 런타임을 시작 하 고, 데이터를 Python에 전달 하 고, Python 사용자 세션을 안전 하 게 관리 하 고, 결과를 클라이언트에 반환 합니다.

다음 단계에서는 SQL Server 인스턴스에서이 예제 Python 스크립트를 실행 합니다.

```python
a = 1
b = 2
c = a/b
d = a*b
print(c, d)
```

1. SQL Server 인스턴스에 연결 된 **SQL Server Management Studio** 에서 새 쿼리 창을 엽니다.

1. @No__t-0 저장 프로시저에 전체 Python 스크립트를 전달 합니다.

   스크립트는 `@script` 인수를 통해 전달 됩니다. @No__t-0 인수 내의 모든 항목은 유효한 Python 코드 여야 합니다.

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

1. 올바른 결과가 계산 되 고 Python `print` 함수는 결과를 **메시지** 창에 반환 합니다.

   다음과 같이 표시 됩니다.

    **결과**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>Hello World 스크립트 실행

일반적인 예제 스크립트는 "Hello World" 문자열을 출력 하는 것입니다. 다음 명령을 실행합니다.

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'OutputDataSet = InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

@No__t-0 저장 프로시저에 대 한 입력은 다음과 같습니다.

| | |
|-|-|
| @language | 호출할 언어 확장 (이 경우 Python)을 정의 합니다. |
| @script | Python 런타임으로 전달 되는 명령을 정의 합니다.<br>전체 Python 스크립트는이 인수에 유니코드 텍스트로 묶어야 합니다. **Nvarchar** 형식의 변수에 텍스트를 추가한 다음 변수를 호출할 수도 있습니다. |
| @input_data_1 | 쿼리에서 반환 되는 데이터로, Python 런타임으로 전달 되며 SQL Server 데이터를 데이터 프레임으로 반환 합니다. |
|WITH RESULT SETS | 절은 SQL Server에 대해 반환 된 데이터 테이블의 스키마를 정의 합니다 .이 경우 열 이름으로 "Hello World"를 추가 하 고 데이터 형식에 대해 **int** 를 추가 합니다. |

명령은 다음 텍스트를 출력 합니다.

| 전 세계 여러분 안녕하세요 |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>입력 및 출력 사용

기본적으로 `sp_execute_external_script`은 단일 데이터 집합을 입력으로 허용 합니다 .이는 일반적으로 유효한 SQL 쿼리 형식으로 제공 합니다. 그런 다음 단일 Python 데이터 프레임을 출력으로 반환 합니다.

지금은 `sp_execute_external_script`의 기본 입력 및 출력 변수를 사용 하겠습니다. **Inputdataset** 및 **outputdataset**

1. 작은 테스트 데이터 테이블을 만듭니다.

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

1. @No__t-0 문을 사용 하 여 테이블을 쿼리 합니다.
  
    ```sql
    SELECT *
    FROM PythonTestData
    ```

    **결과**

    ![PythonTestData 테이블의 내용](./media/select-pythontestdata.png)

1. 다음 Python 스크립트를 실행 합니다. @No__t-0 문을 사용 하 여 테이블에서 데이터를 검색 하 고, Python 런타임을 통해 전달 하 고, 데이터를 데이터 프레임으로 반환 합니다. @No__t-0 절은 열 이름 *NewColName*을 추가 하 여 SQL에 대해 반환 된 데이터 테이블의 스키마를 정의 합니다.

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **결과**

    ![테이블에서 데이터를 반환 하는 Python 스크립트의 출력](./media/python-output-pythontestdata.png)

1. 이제 입력 및 출력 변수의 이름을 변경 합니다. 기본 입력 및 출력 변수 이름은 **inputdataset** 및 **outputdataset**이며, 다음 스크립트는 이름을 **SQL_in** 및 **SQL_out**로 변경 합니다.

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'SQL_out = SQL_in;'
        , @input_data_1 = N'SELECT 12 as Col;'
        , @input_data_1_name  = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    Python은 대/소문자를 구분 합니다. Python 스크립트 (**SQL_out**, **SQL_in**)에서 사용 되는 입력 및 출력 변수는 대/소문자를 포함 하 여 `@input_data_1_name` 및 `@output_data_1_name`으로 정의 된 이름과 일치 해야 합니다.

   > [!TIP]
   > 하나의 입력 데이터 세트만 매개 변수로 전달할 수 있으며 하나의 데이터 세트만 반환할 수 있습니다. 그러나 Python 코드 내에서 다른 데이터 집합을 호출할 수 있으며 데이터 집합 외에 다른 형식의 출력을 반환할 수 있습니다. 또한 모든 매개 변수에 OUTPUT 키워드를 추가하여 결과와 함께 매개 변수를 반환할 수도 있습니다.

1. 입력 데이터 없이 Python 스크립트를 사용 하 여 값을 생성할 수도 있습니다 (`@input_data_1`이 blank로 설정 됨).

   다음 스크립트는 "hello" 및 "세계" 텍스트를 출력 합니다.

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

   ![@No__t-0을 입력으로 사용 하 여 쿼리 결과](./media/python-data-generated-output.png)

> [!NOTE]
> Python은 선행 공백을 사용 하 여 문을 그룹화 합니다. 따라서 포함 된 Python 스크립트가 이전 스크립트와 같이 여러 줄에 걸쳐 있는 경우에는 Python 명령을 SQL 명령에 맞게 들여씁니다. 예를 들어 다음 스크립트는 오류를 생성 합니다.

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

SQL Server 인스턴스에 설치 된 Python 버전을 확인 하려면 다음 스크립트를 실행 합니다.

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import sys
print(sys.version)
'
GO
```

Python `print` 함수는 버전을 **메시지** 창에 반환 합니다. 아래 예제 출력에서이 경우 Python 버전 3.5.2가 설치 되어 있는 것을 확인할 수 있습니다.

**결과**

```text
STDOUT message(s) from external script: 
3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
```

## <a name="list-python-packages"></a>Python 패키지 나열

Microsoft는 SQL Server 인스턴스에서 SQL Server Machine Learning Services와 함께 미리 설치 된 다양 한 Python 패키지를 제공 합니다.

버전을 포함 하 여 설치 된 Python 패키지 목록을 보려면 다음 스크립트를 실행 합니다.

```SQL
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import pip
for i in pip.get_installed_distributions():
    print(i)
'
GO
```

출력은 Python에서 `pip.get_installed_distributions()`이 고 `STDOUT` 메시지로 반환 됩니다.

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
. . .
```

## <a name="next-steps"></a>다음 단계

SQL Server Machine Learning Services에서 Python을 사용 하는 경우 데이터 구조를 사용 하는 방법을 알아보려면 다음 빠른 시작을 따르세요.

> [!div class="nextstepaction"]
> [SQL Server Machine Learning Services에서 Python을 사용 하 여 데이터 형식 및 개체를 처리 합니다.](quickstart-python-data-structures.md)

SQL Server Machine Learning Services에서 Python을 사용 하는 방법에 대 한 자세한 내용은 다음 문서를 참조 하세요.

- [SQL Server Machine Learning Services를 사용 하 여 고급 Python 함수 작성](quickstart-python-functions.md)
- [SQL Server Machine Learning Services를 사용 하 여 Python에서 예측 모델을 만들고 점수 매기기](quickstart-python-train-score-model.md)
- [SQL Server Machine Learning Services (Python 및 R)는 무엇 인가요?](../what-is-sql-server-machine-learning.md)
