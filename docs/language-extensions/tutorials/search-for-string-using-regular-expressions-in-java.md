---
title: '자습서: Java에서 Regex 문자열 검색'
description: 이 자습서에서는 SQL Server 언어 확장을 사용하고 정규식(regex)을 사용하여 문자열을 검색하는 Java 코드를 실행하는 방법을 보여 줍니다.
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: 3d03be56084be15175ec402eafd5b3d8ebdd921e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471684"
---
# <a name="tutorial-search-for-a-string-using-regular-expressions-regex-in-java"></a>자습서: Java에서 regex(정규식)를 사용하여 문자열 검색
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

이 자습서에서는 [SQL Server 언어 확장](../language-extensions-overview.md)을 사용하여 입력 매개 변수로 SQL Server에서 두 개의 열(ID 및 text)과 정규식(regex)을 받는 Java 클래스를 만드는 방법을 보여 줍니다. 클래스는 두 개의 열을 다시 SQL Server(ID 및 text)로 반환합니다.

코드는 Java 클래스로 전송된 텍스트 열의 지정된 텍스트에 대해 지정된 정규식이 충족되는지 확인하고 원래 ID와 함께 해당 텍스트를 반환합니다.

이 샘플 코드에서는 텍스트에 “Java” 또는 “java”라는 단어가 포함되어 있는지 확인하는 정규식을 사용합니다.

## <a name="prerequisites"></a>사전 요구 사항

+ [Windows](../install/windows-java.md) 또는 [Linux](../../linux/sql-server-linux-setup-language-extensions-java.md)에 대한 확장성 프레임워크 및 Java 프로그래밍 확장을 포함하는 SQL Server 2019 데이터베이스 엔진 인스턴스. 자세한 내용은 [SQL Server 2019 언어 확장](../language-extensions-overview.md)을 참조하세요. 코딩 요구 사항에 대한 자세한 내용은 [SQL Server에서 Java를 호출하는 방법](../how-to/call-java-from-sql.md)을 참조하세요.

+ T-SQL을 실행하기 위한 SQL Server Management Studio 또는 Azure Data Studio.

+ Windows 또는 Linux의 JDK(Java SE Development Kit) 8 또는 JRE 8

+ [Microsoft SQL Server용 Microsoft Java 확장성 SDK](../how-to/extensibility-sdk-java-sql-server.md)의 **mssql-java-lang-extension.jar** 파일.

이 자습서에서는 **javac** 를 사용하는 명령줄 컴파일이면 충분합니다.

## <a name="create-sample-data"></a>샘플 데이터 만들기

먼저 새 데이터베이스를 만들고 **ID** 및 **text** 열을 사용하여 **testdata** 테이블을 채웁니다.

```sql
CREATE DATABASE javatest
GO

USE javatest
GO

CREATE TABLE testdata (
    id int NOT NULL,
    "text" nvarchar(100) NOT NULL
)
GO

-- Insert data into test table
INSERT INTO testdata(id, "text") VALUES (1, 'This sentence contains java')
INSERT INTO testdata(id, "text") VALUES (2, 'This sentence does not')
INSERT INTO testdata(id, "text") VALUES (3, 'I love Java!')
GO
```

## <a name="create-the-main-class"></a>기본 클래스 만들기

이 단계에서는 **RegexSample.java** 라는 클래스 파일을 만들고 다음 Java 코드를 해당 파일에 복사합니다.

이 기본 클래스가 SDK를 가져옵니다. 즉, 이 클래스는 1단계에서 다운로드한 jar 파일을 검색할 수 있어야 합니다.

```java
package pkg;

import com.microsoft.sqlserver.javalangextension.PrimitiveDataset;
import com.microsoft.sqlserver.javalangextension.AbstractSqlServerExtensionExecutor;
import java.util.LinkedHashMap;
import java.util.LinkedList;
import java.util.ListIterator;
import java.util.regex.*;

public class RegexSample extends AbstractSqlServerExtensionExecutor {
    private Pattern expr;

    public RegexSample() {
        // Setup the expected extension version, and class to use for input and output dataset
        executorExtensionVersion = SQLSERVER_JAVA_LANG_EXTENSION_V1;
        executorInputDatasetClassName = PrimitiveDataset.class.getName();
        executorOutputDatasetClassName = PrimitiveDataset.class.getName();
    }
    
    public PrimitiveDataset execute(PrimitiveDataset input, LinkedHashMap<String, Object> params) {
        // Validate the input parameters and input column schema
        validateInput(input, params);

        int[] inIds = input.getIntColumn(0);
        String[] inValues = input.getStringColumn(1);
        int rowCount = inValues.length;

        String regexExpr = (String)params.get("regexExpr");
        expr = Pattern.compile(regexExpr);

        System.out.println("regex expression: " + regexExpr);

        // Lists to store the output data
        LinkedList<Integer> outIds = new LinkedList<Integer>();
        LinkedList<String> outValues = new LinkedList<String>();

        // Evaluate each row
        for(int i = 0; i < rowCount; i++) {
            if (check(inValues[i])) {
                outIds.add(inIds[i]);
                outValues.add(inValues[i]);
            }
        }

        int outputRowCount = outValues.size();

        int[] idOutputCol = new int[outputRowCount];
        String[] valueOutputCol = new String[outputRowCount];

        // Convert the list of output columns to arrays
        outValues.toArray(valueOutputCol);

        ListIterator<Integer> it = outIds.listIterator(0);
        int rowId = 0;

        System.out.println("Output data:");
        while (it.hasNext()) {
            idOutputCol[rowId] = it.next().intValue();

            System.out.println("ID: " + idOutputCol[rowId] + " Value: " + valueOutputCol[rowId]);
            rowId++;
        }

        // Construct the output dataset
        PrimitiveDataset output = new PrimitiveDataset();

        output.addColumnMetadata(0, "ID", java.sql.Types.INTEGER, 0, 0);
        output.addColumnMetadata(1, "Text", java.sql.Types.NVARCHAR, 0, 0);

        output.addIntColumn(0, idOutputCol, null);
        output.addStringColumn(1, valueOutputCol);

        return output;
    }

    private void validateInput(PrimitiveDataset input, LinkedHashMap<String, Object> params) {
        // Check for the regex expression input parameter
        if (params.get("regexExpr") == null) {
            throw new IllegalArgumentException("Input parameter 'regexExpr' is not found");
        }

        // The expected input schema should be at least 2 columns, (INTEGER, STRING)
        if (input.getColumnCount() < 2) {
            throw new IllegalArgumentException("Unexpected input schema, schema should be an (INTEGER, NVARCHAR or VARCHAR)");
        }

        // Check that the input column types are expected
        if (input.getColumnType(0) != java.sql.Types.INTEGER &&
                (input.getColumnType(1) != java.sql.Types.VARCHAR && input.getColumnType(1) == java.sql.Types.NVARCHAR )) {
            throw new IllegalArgumentException("Unexpected input schema, schema should be an (INTEGER, NVARCHAR or VARCHAR)");
        }
    }

    private boolean check(String text) {
        Matcher m = expr.matcher(text);

        return m.find();
    }
}
```

## <a name="compile-and-create-a-jar-file"></a>.jar 파일 컴파일 및 만들기

클래스 및 종속성을 `.jar` 파일에 패키지합니다. 대부분의 Java IDE(예: Eclipse 또는 IntelliJ)는 프로젝트를 빌드하거나 컴파일할 때 `.jar` 파일 생성을 지원합니다. `.jar` 파일의 이름을 **regex.jar** 로 지정합니다.

Java IDE를 사용하지 않는 경우 `.jar` 파일을 수동으로 만들 수 있습니다. 자세한 내용은 [클래스 파일에서 Java jar 파일을 만드는 방법](../how-to/create-a-java-jar-file-from-class-files.md)을 참조하세요.

> [!NOTE]
> 이 자습서에서는 패키지를 사용합니다. 클래스 맨 위의 `package pkg;` 라인은 컴파일된 코드가 **pkg** 라는 하위 폴더에 저장되도록 합니다. IDE를 사용하는 경우 컴파일된 코드가 자동으로 이 폴더에 저장됩니다. **javac** 를 사용하여 수동으로 클래스를 컴파일하는 경우 컴파일된 코드를 **pkg** 폴더에 넣어야 합니다.

## <a name="create-external-language"></a>외부 언어 만들기

데이터베이스에서 외부 언어를 만들어야 합니다. 외부 언어는 데이터베이스 범위 개체입니다. 즉, Java와 같은 외부 언어를 사용하려는 각 데이터베이스마다 외부 언어를 만들어야 합니다.

### <a name="create-external-language-on-windows"></a>Windows에서 외부 언어 만들기

Windows를 사용하는 경우 다음 단계를 수행하여 Java용 외부 언어를 만듭니다.

1. 확장을 포함하는 .zip 파일을 만듭니다.

    Windows에서 SQL Server 설정의 일부로 Java 확장 **.zip** 파일이 다음 위치에 설치됩니다. `[SQL Server install path]\MSSQL\Binn\java-lang-extension.zip`. 이 zip 파일에는 **javaextension.dll** 이 포함되어 있습니다.

2. .zip 파일에서 외부 언어 Java를 만듭니다.

    ```sql
    CREATE EXTERNAL LANGUAGE Java
    FROM
    (CONTENT = N'[SQL Server install path]\MSSQL\Binn\java-lang-extension.zip', FILE_NAME = 'javaextension.dll',
    ENVIRONMENT_VARIABLES = N'{"JRE_HOME":"<path to JRE>"}' );
    GO
    ```

### <a name="create-external-language-on-linux"></a>Linux에서 외부 언어 만들기

설치의 일부로 확장 **.tar.gz** 파일이 다음 경로에 저장됩니다. `/opt/mssql-extensibility/lib/java-lang-extension.tar.gz`.

외부 언어 Java를 만들려면 Linux에서 다음 T-SQL 문을 실행합니다.

```sql
CREATE EXTERNAL LANGUAGE Java
FROM (CONTENT = N'/opt/mssql-extensibility/lib/java-lang-extension.tar.gz', file_name = 'javaextension.so',
ENVIRONMENT_VARIABLES = N'{"JRE_HOME":"<path to JRE>"}' );
GO
```

### <a name="permissions-to-execute-external-language"></a>외부 언어 실행 권한 부여

Java 코드를 실행하려면 사용자에게 해당 언어에서 외부 스크립트를 실행할 권한을 부여해야 합니다.

자세한 내용은 [외부 언어 만들기](../../t-sql/statements/create-external-language-transact-sql.md)를 참조하세요.

## <a name="create-external-libraries"></a>외부 라이브러리 만들기

[외부 라이브러리 만들기](../../t-sql/statements/create-external-library-transact-sql.md)를 사용하여 `.jar` 파일용 외부 라이브러리를 만듭니다. SQL Server는 `.jar` 파일에 액세스할 수 있으며, **Classpath** 에 대한 특별한 권한을 설정할 필요가 없습니다.

이 샘플에서는 두 개의 외부 라이브러리를 만듭니다. 하나는 SDK용이고 다른 하나는 RegEx Java 코드용입니다.

1. SDK jar 파일 **mssql-java-lang-extension.jar** 는 Windows 및 Linux 모두에서 SQL Server 2019의 일부로 설치됩니다.

    + Windows 기본 설치 경로: **[인스턴스 설치 홈 디렉터리]\MSSQL\Binn\mssql-java-lang-extension.jar**

    + Linux 기본 설치 경로: **/opt/mssql/lib/mssql-java-lang-extension.jar**

    이 코드 역시 오픈 소스이며 [SQL Server 언어 확장 GitHub 리포지토리](https://github.com/microsoft/sql-server-language-extensions)에서 찾을 수 있습니다. 자세한 내용은 [Microsoft SQL Server용 Microsoft Java 확장성 SDK](../how-to/extensibility-sdk-java-sql-server.md)를 참조하세요.

2. SDK에 대한 외부 라이브러리를 만듭니다.

    ```sql
    CREATE EXTERNAL LIBRARY sdk
    FROM (CONTENT = '<OS specific path from above>/mssql-java-lang-extension.jar')
    WITH (LANGUAGE = 'Java');
    GO
    ```

3. RegEx 코드에 대한 외부 라이브러리를 만듭니다.

    ```sql
    CREATE EXTERNAL LIBRARY regex
    FROM (CONTENT = '<path>/regex.jar')
    WITH (LANGUAGE = 'Java');
    GO
    ```

## <a name="set-permissions"></a>권한 설정

> [!NOTE]
> 이전 단계에서 외부 라이브러리를 사용한 경우 이 단계를 건너뜁니다. `.jar` 파일에서 외부 라이브러리를 만드는 것이 좋습니다.

외부 라이브러리를 사용하지 않으려면 필요한 권한을 설정해야 합니다. 프로세스 ID가 코드에 액세스할 수 있는 경우에만 스크립트 실행이 성공합니다. 권한 설정에 대한 자세한 내용은 [설치 가이드](../install/windows-java.md)에서 확인할 수 있습니다.

### <a name="on-linux"></a>Linux

**mssql_satellite** 사용자에게 Classpath에 대한 읽기/실행 권한을 부여합니다.

### <a name="on-windows"></a>Windows

컴파일된 Java 코드를 포함하는 폴더의 **SQLRUserGroup** 및 **모든 애플리케이션 패키지** SID에 대한 ‘읽기 및 실행’ 권한을 부여합니다.

전체 트리에는 루트 부모에서 마지막 하위 폴더까지 권한이 있어야 합니다.

1. 폴더(`C:\myJavaCode`)를 마우스 오른쪽 단추로 클릭하고 **속성** > **보안** 을 선택합니다.
2. **편집** 을 클릭합니다.
3. **추가** 를 클릭합니다.
4. **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 에서
   1. **개체 형식** 을 클릭하고 *기본 제공 보안 원칙* 및 *그룹* 이 선택되어 있는지 확인합니다.
   2. **위치** 를 클릭하여 목록의 맨 위에 있는 로컬 컴퓨터 이름을 선택합니다.
5. **SQLRUserGroup** 을 입력하고 이름을 확인한 다음 확인을 클릭하여 그룹을 추가합니다.
6. **ALL APPLICATION PACKAGES** 를 입력하고 이름을 확인한 다음 확인을 클릭하여 추가합니다. 
    이름이 확인되지 않으면 위치 단계부터 다시 시작합니다. SID는 컴퓨터에 대해 로컬입니다.

두 보안 ID가 폴더 및 **pkg** 하위 폴더에 대한 **읽기 및 실행** 권한이 있어야 합니다.

<a name="call-method"></a>

## <a name="call-the-java-class"></a>Java 클래스 호출

`sp_execute_external_script`를 호출하여 SQL Server에서 Java 코드를 호출하는 저장 프로시저를 만듭니다. **script** 매개 변수에서 호출할 `package.class`를 정의합니다. 아래 코드에서 클래스는 **pkg** 라는 패키지와 **RegexSample.java** 라는 클래스 파일에 속합니다.

> [!NOTE]
> 코드는 호출할 메서드를 정의하지 않습니다. 기본적으로 **execute** 메서드가 호출됩니다. 즉, SQL Server에서 클래스를 호출할 수 있으려면 SDK 인터페이스를 따르고 Java 클래스에서 execute 메서드를 구현해야 합니다.

저장 프로시저는 입력 쿼리(입력 데이터 세트) 및 정규식을 사용하고 지정된 정규식을 충족하는 행을 반환합니다. 텍스트에 **Java** 또는 **java** 라는 단어가 포함되어 있는지 확인하는 정규식 `[Jj]ava`가 사용됩니다.

```sql
CREATE OR ALTER PROCEDURE [dbo].[java_regex] @expr nvarchar(200), @query nvarchar(400)
AS
BEGIN
--Call the Java program by giving the package.className in @script
--The method invoked in the Java code is always the "execute" method
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'pkg.RegexSample'
, @input_data_1 = @query
, @params = N'@regexExpr nvarchar(200)'
, @regexExpr = @expr
with result sets ((ID int, text nvarchar(100)));
END
GO

--Now execute the above stored procedure and provide the regular expression and an input query
EXECUTE [dbo].[java_regex] N'[Jj]ava', N'SELECT id, text FROM testdata'
GO
```

### <a name="results"></a>결과

호출을 실행한 후 두 개의 행을 포함하는 결과 집합을 가져와야 합니다.

![Java 샘플 결과](../media/java/java-sample-results.png "샘플 결과")

### <a name="if-you-get-an-error"></a>오류가 발생하는 경우

+ 클래스를 컴파일할 때 **pkg** 하위 폴더는 세 클래스 모두에 대해 컴파일된 코드를 포함해야 합니다.

+ 외부 라이브러리를 사용하지 않는 경우에는 **root** 에서 **pkg** 하위 폴더까지 *각* 폴더에 대한 권한을 확인하여 외부 프로세스를 실행하는 보안 ID에 코드 읽기 및 실행 권한이 있는지 확인합니다.

## <a name="next-steps"></a>다음 단계

+ [SQL Server에서 Java를 호출하는 방법](../how-to/call-java-from-sql.md)
+ [SQL Server의 Java 확장](../language-extensions-overview.md)
+ [Java 및 SQL Server 데이터 형식](../how-to/java-to-sql-data-types.md)