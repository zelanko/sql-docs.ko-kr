---
title: SQL-SQL Server Machine Learning Services에서에서 Java를 호출 하는 방법
description: 이 Java 프로그래밍 언어 확장에 SQL Server 2019를 사용 하 여 SQL Server 저장 프로시저에서 Java 클래스를 호출 하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a75878ccc4f14d03f84102dd48bfd43a6e04daea
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473560"
---
# <a name="how-to-call-java-from-sql-server-2019-preview"></a>SQL Server 2019 미리 보기에서 Java를 호출 하는 방법

사용 하는 경우는 [Java 언어 확장](extension-java.md)서 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 시스템 저장된 프로시저는 Java 런타임을 호출 하는 인터페이스입니다. 데이터베이스에 대 한 권한을 Java 코드 실행에 적용 됩니다.

이 문서는 Java 클래스 및 SQL Server에서 실행 되는 메서드에 대 한 구현 세부 정보를 설명 합니다. 이러한 세부 정보를 사용 하 여 잘 알고 있다면, 검토 합니다 [Java 샘플](java-first-sample.md) 다음 단계로 합니다.

SQL Server에서 Java 클래스를 호출 하는 방법은 두 가지가 있습니다.

1. .Class 또는.jar 파일을 배치할 하 [Java classpath](#classpath)합니다. Windows 및 Linux 모두에 대해 제공 됩니다.

2. .Jar 파일 및 기타 종속성을 사용 하 여 데이터베이스에서 컴파일된 클래스를 업로드 합니다 [외부 라이브러리](#external-library) DDL. 이 옵션은 Windows 및 Linux CTP 2.4에서 사용할 수 있습니다.

> [!NOTE]
> 일반 권장 사항,으로 개별이 아닌.class 파일과.jar 파일을 사용 합니다. Java의 일반적인 사례 이며 전반적인 환경을 더 쉽게 됩니다. 참고 항목: [클래스 파일에서 jar 파일을 만드는 방법](extension-java.md#create-jar)합니다.

<a name="classpath"></a>

## <a name="classpath"></a>클래스 경로

### <a name="basic-principles"></a>기본 원칙

* 컴파일된 사용자 지정 Java 클래스.class 파일 또는 Java 클래스 경로에.jar 파일에 있어야 합니다. 합니다 [CLASSPATH 매개 변수](#set-classpath) 컴파일된 Java 파일의 경로를 제공 합니다. 

* Java 메서드를 호출 하는 저장된 프로시저 "script" 매개 변수에 제공 되어야 합니다.

* 클래스를 패키지에 속하는 경우 "packageName"를 제공 해야 합니다.

* "매개 변수"는 매개 변수는 Java 클래스를 전달 하는 데 사용 됩니다. 인수를 필요로 하는 메서드를 호출 지원 되지 않습니다, 매개 변수를 메서드로 인수 값을 전달 하는 유일한 방법은 수 있습니다. 

> [!Note]
> 이 CTP에서 Java 관련 된 지원 되거나 지원 되지 않는 작업을 다시 작성 2.x입니다.
> * 저장된 프로시저에 입력된 매개 변수가 지원 됩니다. 출력 매개 변수는 없습니다.
> * Sp_execute_external_script 매개 변수를 사용 하 여 스트리밍 @r_rowsPerRead 지원 되지 않습니다.
> * 사용 하 여 분할 @input_data_1_partition_by_columns 지원 되지 않습니다.
> * 병렬 처리를 사용 하 여 @parallel= 1은 지원 됩니다.

### <a name="call-java-class"></a>Java 클래스를 호출 합니다.

Windows 및 Linux 모두에 적용 된 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 시스템 저장된 프로시저는 Java 런타임을 호출 하는 인터페이스입니다. 다음 예제에서는 Java 확장 및 매개 변수를 사용 하 여 경로, 스크립트 및 사용자 지정 코드를 지정 하는 데는 sp_execute_external_script를 보여 줍니다.

> [!NOTE]
> 호출할 메서드를 정의할 필요가 없는 참고 합니다. 기본적으로 메서드 호출 **실행** 라고 합니다. 이 SDK를 따르고 Java 클래스의 execute 메서드를 구현 해야 할 것을 의미 합니다.

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

한 번 컴파일한 Java 클래스 또는 클래스 있고 Java 클래스 경로에 jar 파일을 만든, SQL Server Java 확장 하도록 클래스 경로 제공 하기 위한 두 가지 옵션:

**옵션 1: 외부 라이브러리를 사용 하 여** 가장 쉬운 방법은 SQL Server를 자동으로 만들어 외부 라이브러리는 jar 라이브러리를 가리키는 클래스를 찾을 수 있도록 합니다. [Java 용 외부 라이브러리를 사용 합니다.](howto-call-java-from-sql.md#external-library)

**옵션 2: 시스템 환경 변수를 등록 합니다.**

Java 런타임 시스템 환경 변수를 만든 것 처럼 시스템 환경 변수를 만들고 클래스를 포함 하는 jar 파일에 경로 제공할 수 있습니다. 이 작업을 수행 하려면 "CLASSPATH" 이라는 시스템 환경 변수를 만들려면 해야 합니다.

<a name="external-library"></a>

## <a name="external-library"></a>외부 라이브러리

SQL Server 2019 CTP 2.4이 하에서는 Windows 및 Linux에서 Java 언어에 대 한 외부 라이브러리를 사용할 수 있습니다. 클래스를 컴파일하여.jar 파일 및.jar 파일 및 기타 종속성을 사용 하 여 데이터베이스에 업로드할 수는 [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) DDL.

외부 라이브러리를 사용 하 여.jar 파일을 업로드 하는 방법의 예:

```sql 
CREATE EXTERNAL LIBRARY myJar
FROM (CONTENT = '<local path to .jar file>') 
WITH (LANGUAGE = 'Java'); 
GO
```

외부 라이브러리를 만들어 SQL Server는 Java 클래스에 대 한 액세스를 자동으로 포함 됩니다 하 고 클래스 경로에 모든 특수 사용 권한을 설정할 필요가 없습니다.

예제 패키지에서 클래스에서 메서드를 호출 하는 외부 라이브러리로 업로드 합니다.

```sql
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'MyPackage.MyCLass'
, @input_data_1 = N'SELECT * FROM MYTABLE'
with result sets ((column1 int))
```

자세한 내용은 [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)합니다.

## <a name="next-steps"></a>다음 단계

+ [SQL Server에서 Java 샘플](java-first-sample.md)
+ [Java와 SQL Server 데이터 형식](java-sql-datatypes.md)
+ [SQL Server에서 Java 언어 확장](extension-java.md)
