---
title: Java Runtime 호출
titleSuffix: SQL Server Language Extensions
description: SQL Server 언어 확장을 사용하여 SQL Server 저장 프로시저에서 Java 클래스를 호출하는 방법을 알아봅니다.
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bdff924b63b11eda850378987498e8601367d3fe
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73658891"
---
# <a name="how-to-call-the-java-runtime-in-sql-server-language-extensions"></a>SQL Server 언어 확장에서 Java 런타임을 호출하는 방법
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[SQL Server 언어 확장](../language-extensions-overview.md)은 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 시스템 저장 프로시저를 인터페이스로 사용하여 Java 런타임을 호출합니다. 

이 방법 문서에서는 SQL Server에서 실행되는 Java 클래스 및 메서드에 대한 구현 세부 정보를 제공합니다.

## <a name="where-to-place-java-classes"></a>Java 클래스 배치

SQL Server에서 Java 클래스를 호출하는 방법에는 두 가지가 있습니다.

1. **.class** 또는 **.jar** 파일을 [Java Classpath](#classpath)에 배치합니다. 

2. [외부 라이브러리](#external-library) DDL을 사용하여 컴파일된 클래스의 **.jar** 파일 및 기타 종속성을 데이터베이스에 업로드합니다. 

> [!NOTE]
> 일반적으로 개별 **.class** 파일이 아니라 **.jar** 파일을 사용하는 것이 좋습니다. 이는 Java에서 일반적인 방법이며 전반적인 환경을 더 쉽게 만듭니다. [클래스 파일에서 jar 파일을 만드는 방법](create-a-java-jar-file-from-class-files.md)도 참조하세요.

<a name="classpath"></a>

## <a name="use-classpath"></a>Classpath 사용

### <a name="basic-principles"></a>기본 원칙

다음은 SQL Server에서 Java를 실행할 때 몇 가지 기본 원칙입니다.

* 컴파일된 사용자 지정 Java 클래스는 Java Classpath에서 **.class** 파일 또는 **.jar** 파일로 존재해야 합니다. [CLASSPATH 매개 변수](#set-classpath)는 컴파일된 Java 파일의 경로를 제공합니다. 

* 호출하는 Java 메서드는 저장 프로시저의 **script** 매개 변수에 제공해야 합니다.

* 클래스가 패키지에 속하면 **packageName**를 제공해야 합니다.

* **params**는 Java 클래스에 매개 변수를 전달하는 데 사용합니다. 인수가 필요한 메서드 호출은 지원되지 않습니다. 따라서 매개 변수는 인수 값을 메서드에 전달하는 유일한 방법입니다. 

> [!NOTE]
> 이 릴리스 정보에서는 SQL Server 2019 릴리스 후보 1에서 Java와 관련하여 지원되는 작업과 지원되지 않는 작업을 설명합니다.
> * 저장 프로시저에는 입력 매개 변수가 지원됩니다. 출력 매개 변수는 지원되지 않습니다.

### <a name="call-java-class"></a>Java 클래스 호출

[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 시스템 저장 프로시저는 Java 런타임을 호출하는 데 사용되는 인터페이스입니다. 다음 예제에서는 Java 확장을 사용하는 `sp_execute_external_script`, 그리고 경로, 스크립트 및 사용자 지정 코드를 지정하는 매개 변수를 보여 줍니다.

> [!NOTE]
> 호출할 메서드는 정의할 필요가 없습니다. 기본적으로 **execute**라는 메서드가 호출됩니다. 즉, [SQL Server Java용 확장성 SDK](extensibility-sdk-java-sql-server.md)를 따르고 Java 클래스에서 execute 메서드를 구현해야 합니다.

```sql
DECLARE @param1 int
SET @param1 = 3

EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'<packageName>.<ClassName>'
, @input_data_1 = N'<Input Query>'
, @param1 = @param1
```

<a name="set-classpath"></a>

### <a name="set-classpath"></a>CLASSPATH 설정

Java 클래스 또는 클래스를 컴파일하고 Java Classpath에서 jar 파일을 만든 후에는 SQL Server Java 확장에 Classpath를 제공하는 두 가지 방법이 있습니다.

1. 외부 라이브러리 사용

    가장 쉬운 방법은 외부 라이브러리를 만들고 라이브러리에서 jar를 가리켜 SQL Server가 자동으로 클래스를 찾도록 하는 것입니다. [Java용 외부 라이브러리 사용](#external-library)

2. 시스템 환경 변수 등록

    시스템 환경 변수를 만들고 클래스를 포함하는 jar 파일의 경로를 제공할 수 있습니다. **CLASSPATH**라는 시스템 환경 변수를 만듭니다.

<a name="external-library"></a>

## <a name="use-external-library"></a>외부 라이브러리 사용

SQL Server 2019 릴리스 후보 1에서는 Windows 및 Linux에서 Java 언어용 외부 라이브러리를 사용할 수 있습니다. 클래스를 .jar 파일로 컴파일하고 [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) DDL을 사용하여 .jar 파일 및 기타 종속성을 데이터베이스에 업로드할 수 있습니다.

외부 라이브러리를 사용하여 .jar 파일을 업로드하는 방법 예:

```sql 
CREATE EXTERNAL LIBRARY myJar
FROM (CONTENT = '<local path to .jar file>') 
WITH (LANGUAGE = 'Java'); 
GO
```

외부 라이브러리를 만들면 SQL Server는 자동으로 Java 클래스에 액세스할 수 있으며 Classpath에 대한 특별한 사용 권한을 설정할 필요가 없습니다.

외부 라이브러리로 업로드된 패키지에서 클래스의 메서드를 호출하는 예제는 다음과 같습니다.

```sql
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'MyPackage.MyCLass'
, @input_data_1 = N'SELECT * FROM MYTABLE'
with result sets ((column1 int))
```

자세한 내용은 [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)를 참조하세요.

## <a name="next-steps"></a>다음 단계

+ [자습서: Java에서 정규식을 사용하여 문자열 검색](../tutorials/search-for-string-using-regular-expressions-in-java.md)