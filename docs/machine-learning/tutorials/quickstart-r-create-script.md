---
title: '빠른 시작: R 스크립트 실행'
titleSuffix: SQL machine learning
description: SQL 기계 학습에서 간단한 R 스크립트 세트를 실행합니다. 저장 프로시저 sp_execute_external_script를 사용하여 스크립트를 실행하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/21/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: b856f6171913470c87591e949b4e4165cccda2f1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470264"
---
# <a name="quickstart-run-simple-r-scripts-with-sql-machine-learning"></a>빠른 시작: SQL 기계 학습에서 간단한 R 스크립트를 실행합니다.
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
이 빠른 시작에서는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) 또는 [빅 데이터 클러스터](../../big-data-cluster/machine-learning-services.md)를 사용하여 간단한 R 스크립트 세트를 실행합니다. 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 SQL Server 인터페이스에서 스크립트를 실행하는 방법을 알아봅니다.
::: moniker-end
::: moniker range="=sql-server-2017"
이 빠른 시작에서는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md)를 사용하여 간단한 R 스크립트 세트를 실행합니다. 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 SQL Server 인터페이스에서 스크립트를 실행하는 방법을 알아봅니다.
::: moniker-end
::: moniker range="=sql-server-2016"
이 빠른 시작에서는 [SQL Server R Services](../r/sql-server-r-services.md)를 사용하여 간단한 R 스크립트 세트를 실행합니다. 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 SQL Server 인터페이스에서 스크립트를 실행하는 방법을 알아봅니다.
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
이 빠른 시작에서는 [Azure SQL Managed Instance Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)를 사용하여 간단한 R 스크립트 세트를 실행합니다. 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 데이터베이스에서 스크립트를 실행하는 방법을 알아봅니다.
::: moniker-end

## <a name="prerequisites"></a>사전 요구 사항

이 빠른 시작을 실행하려면 다음과 같은 필수 구성 요소가 필요합니다.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
- SQL Server Machine Learning Services. Machine Learning Services를 설치하려면 [Windows 설치 가이드](../install/sql-machine-learning-services-windows-install.md) 또는 [Linux 설치 가이드](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json)를 참조하세요. [SQL Server 빅 데이터 클러스터에서 Machine Learning Services를 사용하도록 설정](../../big-data-cluster/machine-learning-services.md)할 수도 있습니다.
::: moniker-end
::: moniker range="=sql-server-2017"
- SQL Server Machine Learning Services. Machine Learning Services를 설치하려면 [Windows 설치 가이드](../install/sql-machine-learning-services-windows-install.md)를 참조하세요. 
::: moniker-end
::: moniker range="=sql-server-2016"
- SQL Server 2016 R Services. R Services를 설치하려면 [Windows 설치 가이드](../install/sql-r-services-windows-install.md)를 참조하세요. 
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
- Azure SQL Managed Instance Machine Learning Services. 자세한 내용은 [Azure SQL Managed Instance Machine Learning Services 개요](/azure/azure-sql/managed-instance/machine-learning-services-overview)를 참조하세요.
::: moniker-end

- R 스크립트가 포함된 SQL 쿼리를 실행하기 위한 도구. 이 빠른 시작에서는 [Azure Data Studio](../../azure-data-studio/what-is.md)를 사용합니다.

## <a name="run-a-simple-script"></a>간단한 스크립트 실행

R 스크립트를 실행하려면 이를 시스템 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 대한 인수로 전달합니다. 이 시스템 저장 프로시저는 R 런타임을 시작하고, 데이터를 R에 전달하고, R 사용자 세션을 안전하게 관리하고, 결과를 클라이언트에 반환합니다.

다음 단계에서는 아래의 예제 R 스크립트를 실행합니다.

```r
a <- 1
b <- 2
c <- a/b
d <- a*b
print(c(c, d))
```

1. **Azure Data Studio** 를 열고 서버에 연결합니다.

1. R Python 스크립트를 `sp_execute_external_script` 저장 프로시저에 전달합니다.

   스크립트는 `@script` 인수를 통해 전달됩니다. `@script` 인수 안의 모든 항목이 유효한 R 코드여야 합니다.

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))
    '
    ```

1. 올바른 결과가 계산되고 R `print` 함수가 결과를 **메시지** 창에 반환합니다.

   다음과 비슷합니다.

    **결과**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>Hello World 스크립트 실행

일반적인 예제 스크립트는 "Hello World" 문자열만 출력하는 스크립트입니다. 다음 명령을 실행합니다.

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'OutputDataSet<-InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

`sp_execute_external_script` 저장 프로시저에 대한 입력에는 다음이 포함됩니다.

| 입력 | Description |
|-|-|
| @language | 호출할 언어 확장을 정의합니다(이 경우에는 R). |
| @script | R 런타임으로 전달되는 명령을 정의합니다. 전체 R 스크립트는 이 인수에 유니코드 텍스트로 묶어야 합니다. **nvarchar** 형식의 변수에 텍스트를 추가한 다음, 변수를 호출할 수도 있습니다. |
| @input_data_1 | 쿼리에서 반환된 데이터는 R 런타임에 전달되고, R 런타임은 데이터를 데이터 프레임으로 전달합니다. |
|WITH RESULT SETS | 이 절은 반환된 데이터 테이블의 스키마를 정의하고, "Hello World"를 열 이름으로 추가하고 데이터 형식으로 **int** 를 추가합니다. |

이 명령은 다음 텍스트를 출력합니다.

| Hello World |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>입력 및 출력 사용

기본적으로 `sp_execute_external_script`는 일반적으로 사용자가 유효한 SQL 쿼리의 형식으로 제공하는 단일 데이터 세트를 입력으로 사용합니다. 그런 후 단일 R 데이터 프레임을 출력으로 반환합니다.

지금은 `sp_execute_external_script`의 기본 입력 및 출력을 사용합니다. **InputDataSet** 및 **OutputDataSet**.

1. 테스트 데이터의 작은 테이블을 만듭니다.

    ```sql
    CREATE TABLE RTestData (col1 INT NOT NULL)
    
    INSERT INTO RTestData
    VALUES (1);
    
    INSERT INTO RTestData
    VALUES (10);
    
    INSERT INTO RTestData
    VALUES (100);
    GO
    ```

1. `SELECT` 문을 사용하여 테이블을 쿼리합니다.
  
    ```sql
    SELECT *
    FROM RTestData
    ```

    **결과**

    ![RTestData 테이블의 콘텐츠](./media/select-rtestdata.png)

1. 다음 R 스크립트를 실행합니다. `SELECT` 문을 사용하여 테이블에서 데이터를 검색하고 R 런타임을 통해 이를 전달하고 데이터를 데이터 프레임으로 반환합니다. `WITH RESULT SETS` 절은 SQL에 대한 반환된 데이터 테이블의 스키마를 정의하고, 열 이름 *NewColName* 을 추가합니다.

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **결과**

    ![테이블에서 데이터를 반환하는 R 스크립트의 출력](./media/r-output-rtestdata.png)

1. 이제 입력 및 출력 변수의 이름을 변경하겠습니다. 기본 입력 및 출력 변수 이름은 **InputDataSet** 및 **OutputDataSet** 입니다. 이 스크립트는 이름을 **SQL_in** 및 **SQL_out** 으로 변경합니다.

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N' SQL_out <- SQL_in;'
        , @input_data_1 = N' SELECT 12 as Col;'
        , @input_data_1_name = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    R은 대/소문자를 구분합니다. R 스크립트(**SQL_out**, **SQL_in**)에 사용되는 입력 및 출력 변수는 대/소문자를 포함하여 `@input_data_1_name` 및 `@output_data_1_name`으로 정의된 이름과 일치해야 합니다.

   > [!TIP]
   > 하나의 입력 데이터 세트만 매개 변수로 전달할 수 있으며 하나의 데이터 세트만 반환할 수 있습니다. 그러나 R 코드 내에서 다른 데이터 세트를 호출할 수 있으며 데이터 세트 외에 다른 유형의 출력을 반환할 수 있습니다. 또한 모든 매개 변수에 OUTPUT 키워드를 추가하여 결과와 함께 반환되게 만들 수 있습니다.

1. 입력 데이터 없이 R 스크립트만 사용하여 값을 생성할 수도 있습니다(`@input_data_1`이 공백으로 설정됨).

   다음 스크립트는 "hello" 및 "world" 텍스트를 출력합니다.

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    mytextvariable <- c("hello", " ", "world");
    OutputDataSet <- as.data.frame(mytextvariable);
    '
        , @input_data_1 = N''
    WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
    ```

    **결과**

    ![@script를 입력으로 사용하는 쿼리 결과](./media/r-data-generated-output.png)

## <a name="check-r-version"></a>R 버전 확인

설치된 R의 버전을 확인하려면 다음 스크립트를 실행합니다.

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(version)';
GO
```

R `print` 함수는 버전을 **메시지** 창으로 반환합니다. 아래 예제 출력에서 R 버전 3.4.4가 설치되어 있는 것을 확인할 수 있습니다.

**결과**

```text
STDOUT message(s) from external script:
                   _
platform       x86_64-w64-mingw32
arch           x86_64
os             mingw32
system         x86_64, mingw32
status
major          3
minor          4.4
year           2018
month          03
day            15
svn rev        74408
language       R
version.string R version 3.4.4 (2018-03-15)
nickname       Someone to Lean On
```

## <a name="list-r-packages"></a>R 패키지 나열
::: moniker range=">=sql-server-2017"
Microsoft는 Machine Learning Services와 함께 미리 설치된 여러 R 패키지를 제공합니다.
::: moniker-end
::: moniker range="=sql-server-2016"
Microsoft는 R Services와 함께 미리 설치된 여러 R 패키지를 제공합니다.
::: moniker-end

버전, 종속 항목, 라이선스 및 라이브러리 경로 정보를 포함하여 설치된 R 패키지 목록을 보려면 다음 스크립트를 실행합니다.

```SQL
EXEC sp_execute_external_script @language = N'R'
    , @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((
            Package NVARCHAR(255)
            , Version NVARCHAR(100)
            , Depends NVARCHAR(4000)
            , License NVARCHAR(1000)
            , LibPath NVARCHAR(2000)
            ));
```

R의 `installed.packages()`에서 출력이 생성되고 결과 집합으로 반환됩니다.

**결과**

![R의 설치된 패키지](./media/rsql-installed-packages.png) 

## <a name="next-steps"></a>다음 단계

SQL 기계 학습에서 R을 사용할 때 데이터 구조를 사용하는 방법을 알아보려면 다음 빠른 시작을 수행하세요.

> [!div class="nextstepaction"]
> [SQL 기계 학습에서 R을 사용하여 데이터 형식 및 개체 처리](quickstart-r-data-types-and-objects.md)
