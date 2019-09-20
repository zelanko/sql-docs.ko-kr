---
title: 간단한 R 스크립트 만들기 및 실행
titleSuffix: SQL Server Machine Learning Services
description: SQL Server Machine Learning Services를 사용 하 여 SQL Server 인스턴스에서 간단한 R 스크립트를 만들고 실행 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d723fa9b90659eb31e96626a3a85c1299c17fa2f
ms.sourcegitcommit: 1661c3e1bb38ed12f8485c3860fc2d2b97dd2c9d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2019
ms.locfileid: "71150316"
---
# <a name="quickstart-create-and-run-simple-r-scripts-with-sql-server-machine-learning-services"></a>빠른 시작: SQL Server Machine Learning Services를 사용 하 여 간단한 R 스크립트 만들기 및 실행
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 빠른 시작에서는 [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md)를 사용 하 여 간단한 R 스크립트 집합을 만들고 실행 합니다. 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 에서 올바른 형식의 R 스크립트를 래핑하고 SQL Server 인스턴스에서 스크립트를 실행 하는 방법에 대해 알아봅니다.

## <a name="prerequisites"></a>사전 요구 사항

- 이 빠른 시작을 사용 하려면 R 언어가 설치 된 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 를 사용 하 여 SQL Server 인스턴스에 액세스 해야 합니다.

  SQL Server 인스턴스는 Azure 가상 머신 또는 온-프레미스에 있을 수 있습니다. 외부 스크립팅 기능은 기본적으로 사용 하지 않도록 설정 되어 있으므로 [외부 스크립팅을 사용 하도록 설정](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) 하 고 시작 하기 전에 **SQL Server 실행 패드 서비스가** 실행 중인지 확인 해야 할 수 있습니다.

- R 스크립트를 포함 하는 SQL 쿼리를 실행 하기 위한 도구도 필요 합니다. 모든 데이터베이스 관리 또는 쿼리 도구를 사용 하 여 이러한 스크립트를 실행 하 고 SQL Server 인스턴스에 연결 하 고 T-sql 쿼리 또는 저장 프로시저를 실행할 수 있습니다. 이 빠른 시작에서는 [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)를 사용 합니다.

## <a name="run-a-simple-script"></a>간단한 스크립트 실행

R 스크립트를 실행 하려면 시스템 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 인수로 전달 합니다.
이 시스템 저장 프로시저는 SQL Server 컨텍스트에서 R 런타임을 시작 하 고, R에 데이터를 전달 하 고, R 사용자 세션을 안전 하 게 관리 하 고, 결과를 클라이언트에 반환 합니다.

다음 단계에서는 SQL Server 인스턴스에서 R 스크립트 예를 실행 합니다.

```r
a <- 1
b <- 2
c <- a/b
d <- a*b
print(c(c, d))
```

1. **SQL Server Management Studio** 를 열고 SQL Server 인스턴스에 연결 합니다.

1. 전체 R 스크립트를 `sp_execute_external_script` 저장 프로시저에 전달 합니다.

   스크립트는 인수를 `@script` 통해 전달 됩니다. `@script` 인수 내의 모든 항목은 유효한 R 코드 여야 합니다.

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

1. 올바른 결과를 계산 하 고 R `print` 함수에서 결과를 **메시지** 창에 반환 합니다.

   다음과 같이 표시 됩니다.

    **결과**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>Hello World 스크립트 실행

일반적인 예제 스크립트는 "Hello World" 문자열을 출력 하는 것입니다. 다음 명령을 실행합니다.

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'OutputDataSet<-InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

`sp_execute_external_script` 저장 프로시저에 대 한 입력은 다음과 같습니다.

| | |
|-|-|
| @language | 호출할 언어 확장 (이 경우 R)을 정의 합니다. |
| @script | R 런타임에 전달 되는 명령을 정의 합니다. 전체 R 스크립트는 이 인수에 유니코드 텍스트로 포함되어야 합니다. **Nvarchar** 형식의 변수에 텍스트를 추가한 다음 변수를 호출할 수도 있습니다. |
| @input_data_1 | 쿼리에서 반환 되는 데이터로, R 런타임으로 전달 되어 SQL Server 데이터를 데이터 프레임으로 반환 합니다. |
|결과 집합 포함 | 절은 SQL Server에 대해 반환 된 데이터 테이블의 스키마를 정의 하 고, 열 이름으로 "Hello World"를 추가 하 고, 데이터 형식에 대해 **int** 를 정의 합니다. |

명령은 다음 텍스트를 출력 합니다.

| 전 세계 여러분 안녕하세요 |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>입력 및 출력 사용

기본적으로에서는 `sp_execute_external_script` 단일 데이터 집합을 입력으로 허용 합니다 .이는 일반적으로 유효한 SQL 쿼리 형식으로 제공 합니다. 그런 다음 단일 R 데이터 프레임을 출력으로 반환 합니다.

지금은의 `sp_execute_external_script`기본 입력 및 출력 변수를 사용 하겠습니다. **Inputdataset** 및 **outputdataset**

1. 작은 테스트 데이터 테이블을 만듭니다.

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

1. `SELECT` 문을 사용 하 여 테이블을 쿼리 합니다.
  
    ```sql
    SELECT *
    FROM RTestData
    ```

    **결과**

    ![RTestData 테이블의 내용](./media/select-rtestdata.png)

1. 다음 R 스크립트를 실행 합니다. `SELECT` 문을 사용 하 여 테이블에서 데이터를 검색 하 고, R 런타임을 통해 전달 하 고, 데이터를 데이터 프레임으로 반환 합니다. 절 `WITH RESULT SETS` 은 열 이름 *NewColName*을 추가 하 여 SQL에 대해 반환 된 데이터 테이블의 스키마를 정의 합니다.

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **결과**

    ![테이블에서 데이터를 반환 하는 R 스크립트의 출력](./media/r-output-rtestdata.png)

1. 이제 입력 및 출력 변수의 이름을 변경해 보겠습니다. 기본 입력 및 출력 변수 이름은 **inputdataset** 및 **outputdataset**이며,이 스크립트는 이름을 **SQL_in** 및 **SQL_out**로 변경 합니다.

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N' SQL_out <- SQL_in;'
        , @input_data_1 = N' SELECT 12 as Col;'
        , @input_data_1_name = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    R은 대/소문자를 구분 합니다. R 스크립트 (**SQL_out**, **SQL_in**)에서 사용 되는 입력 및 출력 변수는 대/소문자를 포함 하 `@input_data_1_name` 여 `@output_data_1_name`및으로 정의 된 이름과 일치 해야 합니다.

   > [!TIP]
   > 하나의 입력 데이터 세트만 매개 변수로 전달할 수 있으며 하나의 데이터 세트만 반환할 수 있습니다. 그러나 R 코드 내에서 다른 데이터 세트를 호출할 수 있으며 데이터 세트 외에 다른 유형의 출력을 반환할 수 있습니다. 또한 모든 매개 변수에 OUTPUT 키워드를 추가하여 결과와 함께 매개 변수를 반환할 수도 있습니다.

1. 입력 데이터 없이 R 스크립트를 사용 하 여 값을 생성할 수도 있습니다 (`@input_data_1` 가 blank로 설정 됨).

   다음 스크립트는 "hello" 및 "세계" 텍스트를 출력 합니다.

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

    ![입력으로를 @script 사용 하 여 쿼리 결과](./media/r-data-generated-output.png)

## <a name="check-r-version"></a>R 버전 확인

SQL Server 인스턴스에 설치 된 R 버전을 확인 하려면 다음 스크립트를 실행 합니다.

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(version)';
GO
```

R `print` 함수는 버전을 **메시지** 창에 반환 합니다. 아래 예제 출력에서 R 버전 3.4.4가 설치 되어 있는 것을 확인할 수 있습니다.

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

Microsoft는 SQL Server Machine Learning Services와 함께 미리 설치 된 여러 R 패키지를 제공 합니다.

버전, 종속성, 라이선스 및 라이브러리 경로 정보를 포함 하 여 설치 된 R 패키지 목록을 보려면 다음 스크립트를 실행 합니다.

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

출력은 R의 `installed.packages()` 에서 가져온 것 이며 결과 집합으로 반환 됩니다.

**결과**

![R의 설치 된 패키지](./media/rsql-installed-packages.png) 

## <a name="next-steps"></a>다음 단계

SQL Server에서 R을 사용 하 여 기계 학습 모델을 만들려면이 빠른 시작을 수행 합니다.

> [!div class="nextstepaction"]
> [SQL Server를 사용 하 여 R에서 예측 모델 생성 및 점수 매기기 Machine Learning Services](quickstart-r-train-score-model.md)

Machine Learning Services SQL Server에 대 한 자세한 내용은 다음 문서를 참조 하세요.

- [SQL Server Machine Learning Services에서 R을 사용 하 여 데이터 형식 및 개체를 처리 합니다.](quickstart-r-data-types-and-objects.md)
- [SQL Server Machine Learning Services를 사용 하 여 고급 R 함수 작성](quickstart-r-functions.md)
- [SQL Server Machine Learning Services (Python 및 R)는 무엇 인가요?](../what-is-sql-server-machine-learning.md)
