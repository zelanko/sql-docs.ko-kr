---
title: SQL-SQL Server Machine Learning Services에서에서 Java를 호출 하는 방법
description: 이 Java 프로그래밍 언어 확장에 SQL Server 2019를 사용 하 여 SQL Server 저장 프로시저에서 Java 클래스를 호출 하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/07/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 438c1096a933932e08c5cbf21722ba75874bb1dc
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53644762"
---
# <a name="how-to-call-java-from-sql-server-2019-preview"></a>SQL Server 2019 미리 보기에서 Java를 호출 하는 방법

사용 하는 경우는 [Java 언어 확장](extension-java.md)서 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 시스템 저장된 프로시저는 Java 런타임을 호출 하는 인터페이스입니다. 데이터베이스에 대 한 권한을 Java 코드 실행에 적용 됩니다.

이 문서는 Java 클래스 및 SQL Server에서 실행 되는 메서드에 대 한 구현 세부 정보를 설명 합니다. 이러한 세부 정보를 사용 하 여 잘 알고 있다면, 검토 합니다 [Java 샘플](java-first-sample.md) 다음 단계로 합니다.

## <a name="basic-principles"></a>기본 원칙

* 컴파일된 사용자 지정 Java 클래스.class 파일 또는 Java 클래스 경로에.jar 파일에 있어야 합니다. 합니다 [CLASSPATH 매개 변수](#set-classpath) 컴파일된 Java 파일의 경로를 제공 합니다. 

* Java 메서드를 호출 하는 저장된 프로시저 "script" 매개 변수에 제공 되어야 합니다.

* 클래스를 패키지에 속하는 경우 "packageName"를 제공 해야 합니다.

* "매개 변수"는 매개 변수는 Java 클래스를 전달 하는 데 사용 됩니다. 인수를 필요로 하는 메서드를 호출 지원 되지 않습니다, 매개 변수를 메서드로 인수 값을 전달 하는 유일한 방법은 수 있습니다. 

> [!Note]
> 이 CTP에서 Java 관련 된 지원 되거나 지원 되지 않는 작업을 다시 작성 2.x입니다.
> * 저장된 프로시저에 입력된 매개 변수가 지원 됩니다. 출력 매개 변수는 없습니다.
> * Sp_execute_external_script 매개 변수를 사용 하 여 스트리밍을 **@r_rowsPerRead** 지원 되지 않습니다.
> * 사용 하 여 분할 **@input_data_1_partition_by_columns** 지원 되지 않습니다.
> * 사용 하 여 처리 병렬  **@parallel= 1** 지원 됩니다.

## <a name="call-spexecuteexternalscript"></a>Sp_execute_external_script 호출

Windows 및 Linux 모두에 적용 된 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 시스템 저장된 프로시저는 Java 런타임을 호출 하는 인터페이스입니다. 다음 예제에서는 Java 확장 및 매개 변수를 사용 하 여 경로, 스크립트 및 사용자 지정 코드를 지정 하는 데는 sp_execute_external_script를 보여 줍니다.

```sql
DECLARE @myClassPath nvarchar(30)
DECLARE @param1 int

SET @myClassPath = N'/<my path>/program.jar'
SET @param1 = 3

EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'<packageName>.<ClassName>.<methodName>'
, @input_data_1 = N'<Input Query>
, @params = N'@CLASSPATH nvarchar(30), @param1 INT'
, @CLASSPATH = @myClassPath
, @param1 = @param1
```

<a name="set-classpath"></a>

## <a name="set-classpath"></a>CLASSPATH 설정

Java 클래스 또는 클래스 컴파일된 하 고 Java 클래스 경로에.class 파일 또는.jar 파일에 배치 했으면, SQL Server Java 확장 하도록 클래스 경로 제공 하는 데는 두 가지 옵션이 있습니다.

**옵션 1: 매개 변수로 전달 합니다.**

Sp_execute_external_script 프로시저 입력된 매개 변수로 클래스 경로 설정 하 여 컴파일된 코드 경로 지정 하는 한 가지 방법이 됩니다. 합니다 [Java 샘플](java-first-sample.md#call-method) 이 기술을 보여 줍니다. 이 방법을 선택 하 고 여러 경로가 있는 경우 기본 운영 체제에 대 한 유효한 경로 구분 기호를 사용 해야 합니다.

* Linux에서 콜론을 사용 하 여 클래스 경로에서 경로 구분 ":".
* 세미콜론을 사용 하 여 별도 클래스 경로에서 경로 Windows에서 ";"

**옵션 2: 시스템 변수를 등록 합니다.**

JDK 실행 파일에 대 한 시스템 변수를 만든 것 처럼 코드 경로 대 한 시스템 변수를 만들 수 있습니다. 이렇게 하려면 "CLASSPATH" 이라는 시스템 환경 변수를 생성 합니다.

## <a name="class-requirements"></a>클래스 요구 사항

Java 런타임와 통신 하는 SQL Server에 대 한 순서 대로 정적 변수를 특정 클래스에서 구현 해야 합니다. SQL Server Java 언어 확장을 사용 하 여 Java 클래스 및 exchange 데이터의 다음 메서드를 실행할 수 있습니다.

> [!Note]
> 개발자를 위한 환경을 개선 하기 위해 노력 하는 대로 향후 Ctp에서 변경 구현 세부 정보를 기대 합니다.

## <a name="method-requirements"></a>메서드 요구 사항
인수를 전달 하려면 사용 합니다 **@param** sp_execute_external_script에서 매개 변수입니다. 메서드 자체는 모든 인수를 사용할 수 없습니다. 반환 형식은 void 여야 합니다.  

```java
public static void test()  {}
```

## <a name="data-inputs"></a>데이터 입력 

이 섹션에서는 Java를 사용 하 여 SQL Server 쿼리 데이터를 푸시하는 방법을 설명 **InputDataSet** sp_execute_external_script에서.

SQL 쿼리 푸시에서 Java까지 모든 입력된 열에 대 한 배열을 선언 해야 합니다.

### <a name="inputdatacol"></a>inputDataCol

Java 확장의 현재 버전에서의 **inputDataColN** 변수가 필요한 경우 여기서 *N* 열 번호입니다. 

```java
public static <type>[] inputDataColN = new <type>[1]
```

이러한 배열은 초기화할 필요가 (배열 크기를 0 보다 커야 하며 열의 실제 길이 반영 하지 않아도).

예: `public static int[] inputDataCol1 = new int[1];`

이러한 배열 변수는 SQL server 쿼리 Java 프로그램을 실행 하기 전에 호출 하는 입력 데이터로 채워집니다.

### <a name="inputnullmap"></a>inputNullMap

Null 지도 값이 null 인지 알고 있어야 확장에서 사용 됩니다. 이 변수가 채워집니다 null 값에 대 한 정보를 사용 하 여 SQL Server에서 사용자 함수를 실행 하기 전에 합니다.

사용자만이 변수를 초기화 해야 할 (및 0 보다 큰 배열 크기 해야) 합니다.

```java
public static boolean[][] inputNullMap = new boolean[1][1];
```

## <a name="data-outputs"></a>데이터 출력 

이 섹션에서는 설명 **OutputDataSet**, 보내기 및 SQL Server에서 유지할 수 있는 Java에서 반환 된 출력 데이터 집합입니다.

> [!Note]
> 출력에서 매개 변수 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 이 버전에서 지원 되지 않습니다.

### <a name="outputdatacoln"></a>outputDataColN

비슷합니다 **inputDataSet**, Java 프로그램 SQL 서버에 다시 보내는 모든 출력 열에 대 한 배열 변수를 선언 해야 합니다. 모든 **outputDataCol** 배열이 동일한 길이 갖도록 해야 합니다. 클래스 실행이 완료 된 시간을 기준으로이 초기화 되는지 확인 해야 합니다.

```java
public static <type>[] outputDataColN = new <type>[]
```

### <a name="numberofoutputcols"></a>numberofOutputCols

사용자 함수 실행이 끝날 때 예상한 출력 데이터 열 수가이 변수를 설정 합니다.

```java
public static short numberofOutputCols = <expected number of output columns>;
```

### <a name="outputnullmap"></a>outputNullMap

Null 맵 확장에서 어떤 값이 null을 나타내기 위해 사용 됩니다. 기본 형식을 null 지원 하지 않으므로이 필요 합니다. 현재도 필요 null 지도 문자열 형식에 대 한 문자열은 null 일 수에 합니다. Null 값은 "true"로 표시 됩니다.

열 및 SQL Server를 반환 하는 행의 예상된 수를 사용 하 여이 NullMap 채워야 합니다.

```java
public static boolean[][] outputNullMap
```
<a name="create-external-library"></a>


## <a name="next-steps"></a>다음 단계

+ [SQL Server에서 Java 샘플](java-first-sample.md)
+ [Java와 SQL Server 데이터 형식](java-sql-datatypes.md)
+ [SQL Server에서 Java 언어 확장](extension-java.md)
