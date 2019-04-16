---
title: Java 샘플 및 SQL Server 2019-SQL Server Machine Learning Services에 대 한 자습서
description: SQL Server 데이터를 사용 하 여 Java 언어 확장을 사용 하는 단계를 알아보려면 SQL Server 2019에서 Java 샘플 코드를 실행 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/27/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 25deba880827cc7396082dac9a2c86cc4dd66cd8
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582576"
---
# <a name="sql-server-java-sample-walkthrough"></a>SQL Server Java 샘플 연습

이 예제에서는 SQL Server에서 두 개의 열 (ID 및 텍스트)를 수신 하 고 두 개의 열 (ID 및 ngram) SQL Server로 다시 반환 하는 Java 클래스를 보여 줍니다. 이 코드는 지정 된 ID 및 문자열 조합에 대해 원래 ID와 함께 해당 순열 반환 ngrams (부분) 순열을 생성 합니다. ngram의 길이 Java 클래스에 보낸 매개 변수에 의해 정의 됩니다.

## <a name="prerequisites"></a>사전 요구 사항

+ 확장성 프레임 워크 및 확장을 프로그래밍 하는 Java를 사용 하 여 SQL Server 2019 데이터베이스 엔진 인스턴스 [Windows에](../install/sql-machine-learning-services-windows-install.md) 하거나 [linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup)합니다. 시스템 구성에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019에 Java 언어 확장](extension-java.md)합니다. 코딩 요구 사항에 대 한 자세한 내용은 참조 하세요. [SQL Server에서 Java를 호출 하는 방법을](howto-call-java-from-sql.md)합니다.

+ SQL Server Management Studio 또는 T-SQL을 실행 하기 위한 다른 도구입니다.

+ JDK (Java SE Development Kit) 8에서 Windows 또는 Linux입니다.

명령줄 컴파일에서 사용 하 여 **javac** 이 자습서에 충분 합니다. 

## <a name="1---load-sample-data"></a>1-샘플 데이터를 로드 합니다.

먼저 만들고 채우는 *검토* 사용 하 여 테이블 **ID** 하 고 **텍스트** 열. SQL Server에 연결 하 고 테이블을 만들려면 다음 스크립트를 실행 합니다.

```sql
DROP TABLE IF exists reviews;
GO
CREATE TABLE reviews(
    id int NOT NULL,
    "text" nvarchar(30) NOT NULL)

INSERT INTO reviews(id, "text") VALUES (1, 'AAA BBB CCC DDD EEE FFF')
INSERT INTO reviews(id, "text") VALUES (2, 'GGG HHH III JJJ KKK LLL')
INSERT INTO reviews(id, "text") VALUES (3, 'MMM NNN OOO PPP QQQ RRR')
GO
```

## <a name="2---class-ngramjava"></a>2-Ngram.java 클래스

기본 클래스를 만들어 시작 합니다. 이 세 가지 클래스의 첫 번째입니다.

이 단계에서는 라는 클래스를 만듭니다 **Ngram.java** 해당 파일에 다음 Java 코드를 복사 합니다. 


```java
//We will package our classes in a package called pkg
//Packages are option in Java-SQL, but required for this sample.
package pkg;

import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.IntStream;

public class Ngram {

    //Required: This is only required if you are passing data in @input_data_1
    //from SQL Server in sp_execute_external_script
    public static int[] inputDataCol1 = new int[1];
    public static String[] inputDataCol2 = new String[1];

    //Required: Input null map. Size just needs to be set to "1"
    public static boolean[][] inputNullMap = new boolean[1][1];

    //Required: Output data columns returned back to SQL Server
    public static int[] outputDataCol1;
    public static String[] outputDataCol2;

    //Required: Output null map. Is populated with true or false values 
    //to indicate nulls
    public static boolean[][] outputNullMap;

    //Optional: This is only required if parameters are passed with @params
    // from SQL Server in sp_execute_external_script
    // n is giving us the size of ngram substrings
    public static int param1;

    //Optional: The number of rows we will be returning
    public static int numberOfRows;

    //Required: Number of output columns returned
    public static short numberOfOutputCols;

    /*Java main method - Only for testing purposes outside of SQL Server
    public static void main(String... args) {
        //getNGrams();
    }*/

    //This is the method we will be calling from SQL Server
    public static void getNGrams() {

        System.out.println("inputDataCol1.length= "+ inputDataCol1.length);
        if (inputDataCol1.length == 0 ) {
            // TODO: Set empty return
            return;
        }
        //Using a stream to "loop" over the input data inputDataCol1.length. You can also use a for loop for this.
        final List<InputRow> inputDataSet = IntStream.range(0, inputDataCol1.length)
                .mapToObj(i -> new InputRow(inputDataCol1[i], inputDataCol2[i]))
                .collect(Collectors.toList());


        //Again, we are using a stream to loop over data
        final List<OutputRow> outputDataSet = inputDataSet.stream()
                // Generate ngrams of size n for each incoming string
                // Each invocation of ngrams returns a list. flatMap flattens
                // the resulting list-of-lists to a flat list.
                .flatMap(inputRow -> ngrams(param1, inputRow.text).stream().map(s -> new OutputRow(inputRow.id, s)))
                .collect(Collectors.toList());

        //Print the outputDataSet
        System.out.println(outputDataSet);

        //Set the number of rows and columns we will be returning
        numberOfOutputCols = 2;
        numberOfRows = outputDataSet.size();
        outputDataCol1 = new int[numberOfRows]; // ID column
        outputDataCol2 = new String[numberOfRows]; //The ngram column
        outputNullMap = new boolean[2][numberOfRows];// output null map

        //Since we don't have any null values, we will populate all values in the outputNullMap to false
        IntStream.range(0, numberOfRows).forEach(i -> {
            final OutputRow outputRow = outputDataSet.get(i);
            outputDataCol1[i] = outputRow.id;
            outputDataCol2[i] = outputRow.ngram;
            outputNullMap[0][i] = false;
            outputNullMap[1][i] = false;
        });
    }

    // Example: ngrams(3, "abcde") = ["abc", "bcd", "cde"].
    private static List<String> ngrams(int n, String text) {
        return IntStream.range(0, text.length() - n + 1)
                .mapToObj(i -> text.substring(i, i + n))
                .collect(Collectors.toList());
    }
}
```

## <a name="3---class-inputrowjava"></a>3-InputRow.java 클래스

두 번째 클래스를 만듭니다 **InputRow.java**, 다음 코드에서는 구성 및 동일한 위치에 저장 **Ngram.java**합니다.

```java
package pkg;

//This object represents one input row
public class InputRow {
    public final int id;
    public final String text;

    public InputRow(final int id, final String text) {
        this.id = id;
        this.text = text;
    }
}
```

## <a name="4---class-outputrowjava"></a>4-OutputRow.java 클래스

세 번째이자 마지막 클래스 라고 **OutputRow.java**합니다. 코드 복사 하 고 다른 동일한 위치에 OutputRow.java로 저장 합니다.

```java
package pkg;

//This object represents one output row
public class OutputRow {
    public final int id;
    public final String ngram;

    public OutputRow(final int id, final String ngram) {
        this.id = id;
        this.ngram = ngram;
    }

    @Override
    public String toString() { return id + ":" + ngram; }
}
```

## <a name="5---compile"></a>5-컴파일

준비가 되 면 수업을 설정 하는 ".class" 파일로 컴파일하는 javac 실행이 만든 후 (`javac Ngram.java InputRow.java OutputRow.java`). (Ngram.class, InputRow.class, 및 OutputRow.class)이이 샘플에 대 한 세 가지.class 파일을 가져와야 합니다.

클래스 경로 위치에 "패키지" 라는 하위 폴더에 컴파일된 코드를 배치 합니다. 개발 워크스테이션에서 작업 하는 경우이 단계는 SQL Server 컴퓨터에 파일을 복사한 것입니다.

Classpath는 컴파일된 코드의 위치입니다. Classpath 경우 Linux에서 예를 들어, '/ home/myclasspath /' 다음에 '/ home/myclasspath/pkg'.class 파일 이어야 합니다. 7 단계에서 예제 스크립트에서는 sp_execute_external_script에 제공 된 경로 ' / home/myclasspath ' (Linux 가정). 

Windows, 좋습니다 비교적 단순 폴더를 사용 하 여 구조를 하나 또는 두 개의 수준, 권한 간소화 합니다. 예를 들어 프로그램 클래스 경로 'C:\myJavaCode' 같은 '\pkg' 컴파일된 클래스가 포함 된 라는 하위 폴더를 사용 하 여 보일 수 있습니다. 

클래스 경로 대 한 자세한 내용은 참조 하세요. [CLASSPATH 설정](howto-call-java-from-sql.md#set-classpath)합니다. 

### <a name="using-jar-files"></a>.Jar 파일을 사용 하 여

클래스 및 종속성.jar 파일을 패키지 하려면 sp_execute_external_script 클래스 경로 매개 변수에서.jar 파일의 전체 경로 제공 합니다. 예를 들어, jar 파일을 'ngram.jar'를 호출 하면 CLASSPATH 됩니다 ' / home/myclasspath/ngram.jar' linux.

## <a name="6---create-external-library"></a>6-외부 라이브러리 만들기

외부 라이브러리를 만들어 SQL Server jar에 대 한 액세스를 자동으로 포함 됩니다 하 고 클래스 경로에 모든 특수 사용 권한을 설정할 필요가 없습니다.

```sql 
CREATE EXTERNAL LIBRARY ngram
FROM (CONTENT = '<path>/ngram.jar') 
WITH (LANGUAGE = 'Java'); 
GO
```

## <a name="7---set-permissions-skip-if-you-performed-step-6"></a>7-사용 권한 (6 단계를 수행한 경우에 생략)를 설정 합니다.

외부 라이브러리를 사용 하는 경우에이 단계가 필요 하지 않습니다. 작업 하는 권장된 방법을 있습니다 jar에서 외부 라이브러리를 만드는 것입니다. 

외부 라이브러리를 사용 하지 않으려는 경우에 필요한 사용 권한을 설정 해야 합니다. 스크립트 실행 프로세스 id가 코드에 액세스 하는 경우에 성공 합니다. 

### <a name="on-linux"></a>On Linux

하도록 클래스 경로에 대 한 읽기/실행 권한을 부여 합니다 **mssql_satellite** 사용자입니다.

### <a name="on-windows"></a>Windows에서

에 '읽기 및 실행' 권한 부여 **SQLRUserGroup** 하며 **모든 응용 프로그램 패키지** SID 컴파일된 Java 코드를 포함 하는 폴더에 있습니다. 

전체 트리는 권한이, 루트에서 부모 마지막 하위 해야 합니다. 
 
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

## <a name="8---call-getngrams"></a>8 - Call *getNgrams()*

SQL Server에서 코드를 호출 하려면 Java 메서드를 지정 **getNgrams()** sp_execute_external_script "script" 매개 변수에서입니다. 이 메서드 호출 "패키지" 라는 클래스 파일을 패키지에 속하는 **Ngram.java**합니다.

이 예제에서는 Java 파일의 경로를 제공 하기 클래스 경로 매개 변수를 전달 합니다. 또한 "매개 변수"를 사용 하 여 Java 클래스에 매개 변수를 전달 합니다. classpath 30 자를 초과 하지 않도록 확인 합니다. 이 경우 아래 스크립트에서 값을 늘립니다.

+ Linux에서 SQL Server Management Studio 또는 TRANSACT-SQL을 실행 하는 데 사용 되는 다른 도구에서 다음 코드를 실행 합니다. 

+ Windows를 변경 @myClassPath N'C:\myJavaCode를\' (가정 \pkg의 부모 폴더) SQL Server Management Studio 또는 다른 도구에서 쿼리를 실행 하기 전에 합니다.

```sql
DECLARE @myClassPath nvarchar(50)
DECLARE @n int 
--This is where you store your classes or jars.
--This is the size of the ngram
SET @n = 3
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'pkg.Ngram.getNGrams'
, @input_data_1 = N'SELECT id, text FROM reviews'
, @parallel = 0
, @params = N'@param1 INT'
, @param1 = @n
with result sets ((ID int, ngram varchar(20)))
GO
```

### <a name="results"></a>결과

호출을 실행 한 후을 보여 주는 결과를 집합이 두 개의 열을 받습니다.

![Java 샘플에서 결과](../media/java/java-sample-results.png "샘플 결과")

### <a name="if-you-get-an-error"></a>오류가 발생 하는 경우

+ 클래스를 컴파일할 때 "패키지" 하위 폴더에는 세 클래스 모두에 대 한 컴파일된 코드를 포함 해야 합니다.

+ 클래스 경로 길이 선언 된 값을 초과할 수 없습니다 (`DECLARE @myClassPath nvarchar(50)`). 이 경우 처음 50 개 문자를 경로 잘리고 컴파일된 코드가 로드 되지 않습니다. 수행할 수 있습니다는 `SELECT @myClassPath` 값을 확인 합니다. 50 자 충분 하지 않은 경우에 길이 늘립니다. 

+ 마지막으로, 사용 권한 확인 *각* 외부 프로세스를 실행 하는 보안 id를 읽고 코드를 실행할 수 있는 권한이 있는지 확인 하려면 "패키지" 하위 폴더에 루트 폴더입니다.

## <a name="see-also"></a>참고자료

+ [SQL Server에서 Java를 호출 하는 방법](howto-call-java-from-sql.md)
+ [SQL Server에서 Java 확장](extension-java.md)
+ [Java와 SQL Server 데이터 형식](java-sql-datatypes.md)
