---
title: Java 샘플 및 SQL Server 2019-SQL Server Machine Learning Services에 대 한 자습서
description: SQL Server 데이터를 사용 하 여 Java 언어 확장을 사용 하는 단계를 알아보려면 SQL Server 2019에서 Java 샘플 코드를 실행 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 000318716b07f58e94bd5c482d9c349e5d4e5481
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473756"
---
# <a name="sql-server-regex-java-sample"></a>SQL Server Regex Java 샘플

이 예제에서는 SQL Server에서 두 개의 열 (ID 및 텍스트)를 수신 하 고도 입력된 매개 변수로 정규식을 사용 하는 Java 클래스를 보여 줍니다. 클래스는 SQL Server (ID 및 텍스트)를 다시 두 개의 열을 반환합니다.

Java 클래스 보낼 텍스트 열에 지정된 된 텍스트에 대 한 코드를 확인 하는 경우 지정된 된 정규식 수행 되 고이 원래 ID와 함께 해당 텍스트를 반환 하는 

이 특정 예제의 텍스트는 "Java" 또는 "java" 단어를 포함 하는 경우를 확인 하는 정규식을 사용 합니다.

## <a name="microsoft-extensibility-sdk-for-java-for-microsoft-sql-server"></a>Microsoft 확장성 Microsoft SQL Server에 대 한 Java 용 SDK

 CTP 2.5에서는 SQL Server를 사용 하 여 통신 하도록 Java 언어 확장을 사용 하는 Java 코드를 구현 하는 방법은 변경 하 고 있습니다. 이렇게 하면 Java에서 SQL Server와 상호 작용할 때 더 나은 개발자 환경을 제공 됩니다.

SDK는 쉽게 수 있도록 SQL Server에 대해 실행 되는 Java 코드를 구현 하는 도우미 인터페이스로 고려해 야 합니다.

> [!NOTE]
> SDK의 소개는 이전 Ctp의 큰 변화입니다. 작업 했던 이전 샘플은 SDK를 사용 하도록 업데이트 해야 합니다.

자세한 내용은 참조는 [SDK 설명서](java-sdk.md)합니다.

## <a name="prerequisites"></a>사전 요구 사항

+ 확장성 프레임 워크 및 확장을 프로그래밍 하는 Java를 사용 하 여 SQL Server 2019 데이터베이스 엔진 인스턴스 [Windows에](../install/sql-machine-learning-services-windows-install.md) 하거나 [linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup)합니다. 시스템 구성에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019에 Java 언어 확장](extension-java.md)합니다. 코딩 요구 사항에 대 한 자세한 내용은 참조 하세요. [SQL Server에서 Java를 호출 하는 방법을](howto-call-java-from-sql.md)합니다.

+ SQL Server Management Studio 또는 T-SQL을 실행 하기 위한 Azure 데이터 Studio.

+ JDK (Java SE Development Kit) 8 또는 JRE 8에서 Windows 또는 Linux입니다.

+ [Microsoft SQL Server 용 Microsoft Java 확장성 SDK](http://aka.ms/mssql-java-lang-extension) java 언어 extension.jar mssql.

명령줄 컴파일에서 사용 하 여 **javac** 이 자습서에 충분 합니다.

## <a name="1---create-sample-data-in-a-sql-server-table"></a>1-SQL Server 테이블에서 예제 데이터 만들기

먼저 만들고 채우는 *testdata* 사용 하 여 테이블 **ID** 하 고 **텍스트** 열. SQL Server에 연결 하 고 테이블을 만들려면 다음 스크립트를 실행 합니다.

```sql
CREATE DATABASE javatest
GO
USE javatest
GO

-- Create table for test data
DROP TABLE IF exists testdata;
GO

CREATE TABLE testdata(
id int NOT NULL,
"text" nvarchar(100) NOT NULL)
GO

TRUNCATE TABLE testdata
GO

-- Insert data into test table
INSERT INTO testdata(id, "text") VALUES (1, 'This sentence contains java')
INSERT INTO testdata(id, "text") VALUES (2, 'This sentence does not')
INSERT INTO testdata(id, "text") VALUES (3, 'I love Java!')
GO
Select * FROM testdata
```

## <a name="2---class-regexsamplejava"></a>2-RegexSample.java 클래스

기본 클래스를 만들어 시작 합니다.

이 단계에서는 라는 클래스를 만듭니다 **RegexSample.java** 해당 파일에 다음 Java 코드를 복사 합니다.

이 기본 클래스는이 클래스에서 사용 가능 해야 하는 1 단계에서 다운로드 한 jar 파일 즉 SDK를 가져오는 중입니다.

> [!NOTE]
> 이 클래스는 Java 확장 SDK 패키지를 가져옵니다는 note 합니다.
에 대 한 문서를 참조 합니다 [Microsoft SQL Server에 대 한 Java에 대 한 Microsoft 확장 SDK](java-sdk.md) 대 한 자세한 내용은 합니다.

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

## <a name="3-compile-and-create-jar-file"></a>3 컴파일하고.jar 파일 만들기

클래스 및 종속성.jar 파일을 패키지 하는 것이 좋습니다. Eclipse 또는 IntelliJ 지원 생성과 같은 대부분의 Java Ide jar 때 있습니다 빌드/컴파일 프로젝트 파일. 이 샘플에서 jar 파일 명명 **regex.jar**합니다.

.Jar 파일을 수동으로 만드는 경우에 단계에 따라, 참조 수 있습니다 [jar 파일을 만드는 방법](extension-java.md#create-jar)합니다.

> [!NOTE]
> 이 샘플은 사용 패키지, 즉,는 pkg"패키지" 클래스의 맨 위에 있는 제공 하면 컴파일된 코드는 "패키지" 라는 하위 폴더에 저장 됩니다. 이 자동으로 처리 되는 IDE를 사용 하는 경우 하지만 클래스를 사용 하 여 수동으로 컴파일하는 경우 **javac**을 수동으로 패키지 하위 폴더에 컴파일된 코드를 배치 해야 합니다.

## <a name="4---create-external-libraries"></a>4-외부 라이브러리 만들기

외부 라이브러리를 만들어 SQL Server jar 파일에 대 한 액세스를 자동으로 포함 됩니다 하 고 클래스 경로에 모든 특수 사용 권한을 설정할 필요가 없습니다.

이 샘플에서는 두 외부 라이브러리를 만드는 해야 합니다. SDK에 대 한 하나 및 Regex Java 샘플에 대 한 합니다.

1.  다운로드 [Microsoft SQL Server에 대 한 Java에 대 한 Microsoft 확장 SDK](http://aka.ms/mssql-java-lang-extension) java 언어 extension.jar mssql.

1. Sdk에 대 한 외부 라이브러리 만들기

```sql
-- Create external library for the SDK
CREATE EXTERNAL LIBRARY sdk
FROM (CONTENT = '<path>/mssql-java-lang-extension.jar')
WITH (LANGUAGE = 'Java');
GO
```

3. Regex 샘플에 대 한 외부 라이브러리 만들기

```sql
-- Create external library for the regex sample
CREATE EXTERNAL LIBRARY regex
FROM (CONTENT = '<path>/regex.jar')
WITH (LANGUAGE = 'Java');
GO
```

## <a name="5---set-permissions-skip-if-you-performed-step-4"></a>5-사용 권한 (4 단계를 수행한 경우에 생략)를 설정 합니다.

외부 라이브러리를 사용 하는 경우에이 단계가 필요 하지 않습니다. 작업 하는 권장된 방법을 있습니다 jar에서 외부 라이브러리를 만드는 것입니다.

외부 라이브러리를 사용 하지 않으려는 경우에 필요한 사용 권한을 설정 해야 합니다. 스크립트 실행 프로세스 id가 코드에 액세스 하는 경우에 성공 합니다. 사용 권한을 설정 하는 방법에 대 한 자세한 정보를 찾을 수 있습니다 [여기](extension-java.md)합니다.

### <a name="on-linux"></a>On Linux

하도록 클래스 경로에 대 한 읽기/실행 권한을 부여 합니다 **mssql_satellite** 사용자입니다.

### <a name="on-windows"></a>Windows에서

에 '읽기 및 실행' 권한 부여 **SQLRUserGroup** 하며 **모든 응용 프로그램 패키지** SID 컴파일된 Java 코드를 포함 하는 폴더에 있습니다. 

전체 트리는 권한이, 루트에서 부모 마지막 하위 폴더 해야 합니다. 
 
1. 폴더 (예: ' C:\myJavaCode')를 마우스 오른쪽 단추로 차례로 **속성** > **보안**합니다.
2. **편집**을 클릭합니다.
3. **추가**를 클릭합니다.
4. **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택**:
   + 클릭 **개체 유형** 있는지 확인 하 고 *기본 제공 보안 원칙* 하 고 *그룹* 선택 됩니다.
   + 클릭 **위치** 목록의 맨 위에 있는 로컬 컴퓨터 이름을 선택 합니다.
5. 입력 **SQLRUserGroup**이름을 확인 하 고 그룹을 추가 하려면 확인을 클릭 합니다.
6. 입력 **ALL APPLICATION PACKAGES**이름을 확인 하 고 추가 확인을 클릭 합니다. 이름을 해결 되지 않으면 위치 단계를 다시 확인 합니다. SID를 컴퓨터에 로컬입니다.

'두 보안 id 읽기 및 실행 권한이 ' 폴더 및 "패키지" 하위 폴더에 있는지 확인 합니다.

<a name="call-method"></a>

## <a name="2---call-the-java-class"></a>2-Java 클래스를 호출 합니다.

SQL Server에서 Java 코드를 호출 하려면 sp_execute_external_script를 호출 하는 저장된 프로시저를 만듭니다. "Script" 매개 변수에 [패키지] 정의 하겠습니다. [class]를 호출 하려고 합니다. 이 샘플에서는 클래스 라는 패키지에 속해 **pkg** 클래스 파일을 호출 하 고 **RegexSample.java**합니다.

> [!NOTE]
>호출할 메서드를 정의 하지 않습니다. 기본적으로 **실행** 메서드가 호출 됩니다. 이 SQL Server에서 클래스를 호출 하는 일을 할 수 있도록 하려는 경우 SDK 인터페이스를 따르고 Java 클래스의 execute 메서드를 구현 해야 하는 것을 의미 합니다.

```sql
/*
This stored procedure takes an input query (input dataset) and a regular expression and returns the rows that fulfilled the given regular expression. This sample uses a regular expression that checks if a text contains the word "Java" or "java" ([Jj]ava) 
*/

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

호출을 실행 한 후 결과 행의 두 개의 집합을 가져와야 합니다.

![Java 샘플에서 결과](../media/java/java-sample-results.png "샘플 결과")

### <a name="if-you-get-an-error"></a>오류가 발생 하는 경우

+ 클래스를 컴파일할 때 "패키지" 하위 폴더에는 세 클래스 모두에 대 한 컴파일된 코드를 포함 해야 합니다.

+ 마지막으로, 외부 라이브러리를 사용 하지 않는 경우 사용 권한을 확인 온 *각* 외부 프로세스를 실행 하는 보안 id를 읽고 코드를 실행할 수 있는 권한이 있는지 확인 하려면 "패키지" 하위 폴더로 루트 폴더입니다.

## <a name="next-steps"></a>다음 단계

+ [Microsoft 확장성 Microsoft SQL Server에 대 한 Java 용 SDK](java-sdk.md)
+ [SQL Server에서 Java를 호출 하는 방법](howto-call-java-from-sql.md)
+ [SQL Server에서 Java 확장](extension-java.md)
+ [Java와 SQL Server 데이터 형식](java-sql-datatypes.md)
