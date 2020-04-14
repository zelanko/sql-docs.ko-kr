---
title: 확장성 프레임워크 API
titleSuffix: SQL Server Language Extensions
description: 확장성 프레임워크를 사용하여 SQL Server용 프로그래밍 언어 확장을 작성할 수 있습니다. Microsoft SQL Server용 확장성 프레임워크 API는 언어 확장에서 SQL Server와 상호 작용하고 데이터를 교환하는 데 사용할 수 있는 API입니다.
author: dphansen
ms.author: davidph
ms.date: 04/09/2020
ms.topic: reference
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bc33ebc4ae271841cba2de73cb9168e1a41e7b69
ms.sourcegitcommit: fbe0ab88fa8d5aa3ea96629f4ccfa4da5caf74f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2020
ms.locfileid: "81012429"
---
# <a name="extensibility-framework-api-for-sql-server"></a>SQL Server용 확장성 프레임워크 API

확장성 프레임워크를 사용하여 SQL Server용 프로그래밍 언어 확장을 작성할 수 있습니다. Microsoft SQL Server용 확장성 프레임워크 API는 언어 확장에서 SQL Server와 상호 작용하고 데이터를 교환하는 데 사용할 수 있는 API입니다.

언어 확장 작성자는 오픈 소스로 작성된 [SQL Server용 Java 언어 확장](../how-to/extensibility-sdk-java-sql-server.md)과 함께 이 참조를 사용하여 해당 API로 고유한 언어 확장을 작성하는 방법을 파악할 수 있습니다. Java 언어 확장의 소스 코드는 [aka.ms/mssql-lang-extensions](https://aka.ms/mssql-lang-extensions)에서 확인할 수 있습니다.

모든 API 함수의 구문 및 인수 정보는 아래에서 확인할 수 있습니다.

## <a name="return-value"></a>반환 값

모든 함수는 *SQLRETURN* 매개 변수를 반환합니다. 값이 *SQL_SUCCESS*가 아니면 오류로 처리되고 스크립트 실행이 중지됩니다.

## <a name="standard-output"></a>표준 출력

확장에서 표준 출력이나 오류 스트림에 출력하는 내용은 세션의 로그 파일로 추적되고, 궁극적으로 SQL Server로 다시 추적됩니다(SSMS 메시지 탭에 표시되는 내용과 유사).


## <a name="init"></a>Init

이 함수는 한 번만 호출되며, 실행할 런타임을 초기화하는 데 사용됩니다. 예를 들어 Java 확장은 JVM을 초기화합니다.

### <a name="syntax"></a>구문

```cpp
SQLRETURN Init(
    SQLCHAR *ExtensionParams,
    SQLULEN ExtensionParamsLength,
    SQLCHAR *ExtensionPath,
    SQLULEN ExtensionPathLength,
    SQLCHAR *PublicLibraryPath,
    SQLULEN PublicLibraryPathLength,
    SQLCHAR *PrivateLibraryPath,
    SQLULEN PrivateLibraryPathLength
);
```

### <a name="arguments"></a>인수

*ExtensionParams*  
\[입력\] [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) 또는 [ALTER EXTERNAL LANGUAGE](../../t-sql/statements/alter-external-language-transact-sql.md) 동안 제공된 `PARAMETERS` 값을 포함하는, Null로 종료된 문자열입니다.

*ExtensionParamsLength*  
\[입력\] *ExtensionParams*의 길이(바이트)입니다(null 종료 문자 제외).

*ExtensionPath*  
\[입력\] 확장 설치 디렉터리의 절대 경로를 포함하는, Null로 종료된 UTF-8 문자열입니다.

*ExtensionPathLength*  
\[입력\] *ExtensionPath*의 길이(바이트)입니다(null 종료 문자 제외).

*PublicLibraryPath*  
\[입력\] 이 외부 언어에 대한 퍼블릭 외부 라이브러리 디렉터리의 절대 경로를 포함하는, Null로 종료된 UTF-8 문자열입니다.

*PublicLibraryPathLength*  
\[입력\] *PublicLibraryPath*의 길이(바이트)입니다(null 종료 문자 제외).

*PrivateLibraryPath*  
\[입력\] 이 사용자 및 외부 언어에 대한 프라이빗 외부 라이브러리 디렉터리의 절대 경로를 포함하는, Null로 종료된 UTF-8 문자열입니다.

*PrivateLibraryPathLength*  
\[입력\] *PrivateLibraryPath*의 길이(바이트)입니다(null 종료 문자 제외).

## <a name="initsession"></a>InitSession

이 함수는 세션당 한 번 호출되며 세션별 설정을 초기화합니다.

### <a name="syntax"></a>구문

```cpp
SQLRETURN InitSession(
    SQLGUID         SessionId,
    SQLUSMALLINT    TaskId,
    SQLCHAR*        Script,
    SQLULEN         ScriptLength,
    SQLUSMALLINT    InputSchemaColumnsNumber,
    SQLUSMALLINT    ParametersNumber
    SQLCHAR*        InputDataName,
    SQLUSMALLINT    InputDataNameLength,
    SQLCHAR*        OutputDataName,
    SQLUSMALLINT    OutputDataNameLength
);
```

### <a name="arguments"></a>인수

*SessionId*  
\[입력\] 이 스크립트 세션을 고유하게 식별하는 GUID입니다.

*TaskId*  
\[입력\] 이 실행 프로세스를 고유하게 식별하는 정수입니다.

[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 `@parallel = 1`인 경우, 이 값의 범위는 0부터 쿼리의 병렬 처리 수준까지입니다.

*스크립트*  
\[입력\] [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)의 `@script`를 포함하는, Null로 종료된 UTF-8 문자열입니다.

*ScriptLength*  
\[입력\] *ScriptScript*의 길이(바이트)입니다(null 종료 문자 제외).

*InputSchemaColumnsNumber*  
\[입력\] [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 `@input_data_1`의 결과 집합에 있는 열 수입니다.

*ParametersNumber*  
\[입력\] [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 `@params`의 입력 매개 변수 수입니다.

*InputDataName*  
\[입력\] [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)의 `@input_data_1_name`를 포함하는, Null로 종료된 UTF-8 문자열입니다.

*InputDataNameLength*  
\[입력\] *InputDataName*의 길이(바이트)입니다(null 종료 문자 제외).

*OutputDataName*  
\[입력\] [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)의 `@output_data_1_name`를 포함하는, Null로 종료된 UTF-8 문자열입니다.

*OutputDataNameLength*  
\[입력\] *OutputDataName*의 길이(바이트)입니다(null 종료 문자 제외).

## <a name="initcolumn"></a>InitColumn

특정 세션의 지정된 열 정보를 초기화합니다.

이 함수는 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 `@input_data_1`의 결과 집합에 있는 각 열에 대해 호출됩니다.

이 결과 집합의 열 구조를 ‘입력 스키마’라고 합니다. 

### <a name="syntax"></a>구문

```cpp
SQLRETURN InitColumn(
    SQLGUID       SessionId,
    SQLUSMALLINT  TaskId,
    SQLUSMALLINT  ColumnNumber,
    SQLCHAR*      ColumnName,
    SQLSMALLINT   ColumnNameLength,
    SQLSMALLINT   DataType,
    SQLULEN       ColumnSize,
    SQLSMALLINT   DecimalDigits,
    SQLSMALLINT   Nullable,
    SQLSMALLINT   PartitionByNumber,
    SQLSMALLINT   OrderByNumber
);
```

### <a name="arguments"></a>인수

*SessionId*  
\[입력\] 이 스크립트 세션을 고유하게 식별하는 GUID입니다.

*TaskId*  
\[입력\] 이 실행 프로세스를 고유하게 식별하는 정수입니다.

[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 `@parallel = 1`인 경우, 이 값의 범위는 0부터 쿼리의 병렬 처리 수준까지입니다.

*ColumnNumber*  
\[입력\] 입력 스키마에서 이 열의 인덱스를 식별하는 정수입니다. 열은 0부터 시작하여 오름차순으로 번호가 매겨집니다.

*ColumnName*  
\[입력\] 열 이름을 포함하는, Null로 종료된 UTF-8 문자열입니다.

*ColumnNameLength*  
\[입력\] *ColumnName*의 길이(바이트)입니다(null 종료 문자 제외).

*DataType*  
\[입력\] 이 열의 데이터 형식을 식별하는 ODBC C 형식입니다.

*ColumnSize*  
\[입력\] 이 열에 있는 기본 데이터의 최대 크기(바이트)입니다.

SQL_C_CHAR, SQL_C_WCHAR 및 SQL_C_BINARY 데이터 형식의 경우 값이 8000보다 크면 이 열이 LOB 개체를 나타내고, 크기가 최대 2GB임을 나타냅니다.

*DecimalDigits*  
\[입력\] 이 열에 있는 기본 데이터의 10진수로, [10진수](../../odbc/reference/appendixes/decimal-digits.md)의 정의를 따릅니다.

*Null 허용*  
\[입력\] 이 열에 NULL 값을 포함할 수 있는지 여부를 나타내는 값입니다. 가능한 값은 다음과 같습니다.

- SQL_NO_NULLS: 열에 NULL 값을 포함할 수 없습니다.
- SQL_NULLABLE: 열에 NULL 값을 포함할 수 있습니다.

*PartitionByNumber*  
\[입력\] [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)의 `@input_data_1_partition_by_columns` 시퀀스에서 이 열의 인덱스를 나타내는 값입니다. 열은 0부터 시작하여 오름차순으로 번호가 매겨집니다. 이 열이 시퀀스에 포함되지 않는 경우 값은 -1입니다.

*OrderByNumber*  
\[입력\] [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)의 `@input_data_1_order_by_columns` 시퀀스에서 이 열의 인덱스를 나타내는 값입니다. 열은 0부터 시작하여 오름차순으로 번호가 매겨집니다. 이 열이 시퀀스에 포함되지 않는 경우 값은 -1입니다.

## <a name="initparam"></a>InitParam

특정 세션의 지정된 입력 매개 변수와 관련된 정보를 초기화합니다.

이 함수는 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 `@params`의 각 매개 변수에 대해 호출됩니다.

### <a name="syntax"></a>구문

```cpp
SQLRETURN InitParam(
    SQLGUID      SessionId,
    SQLUSMALLINT TaskId,
    SQLUSMALLINT ParamNumber,
    SQLCHAR*     ParamName,
    SQLSMALLINT  ParamNameLength,
    SQLSMALLINT  DataType,
    SQLULEN      ParamSize,
    SQLSMALLINT  DecimalDigits,
    SQLPOINTER   ParamValue,
    SQLINTEGER   StrLen_or_Ind,
    SQLSMALLINT  InputOutputType
);
```

### <a name="arguments"></a>인수

*SessionId*  
\[입력\] 이 스크립트 세션을 고유하게 식별하는 GUID입니다.

*TaskId*  
\[입력\] 이 실행 프로세스를 고유하게 식별하는 정수입니다.

[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 `@parallel = 1`인 경우, 이 값의 범위는 0부터 쿼리의 병렬 처리 수준까지입니다.

*ParamNumber*  
\[입력\] 이 매개 변수의 인덱스를 식별하는 정수입니다. 매개 변수는 0부터 시작하여 오름차순으로 번호가 매겨집니다.

*ParamName*  
\[입력\] 매개 변수 이름을 포함하는, Null로 종료된 UTF-8 문자열입니다.

*ParamNameLength*  
\[입력\] *ParamName*의 길이(바이트)입니다(null 종료 문자 제외).

*DataType*  
\[입력\] 이 매개 변수의 데이터 형식을 식별하는 ODBC C 형식입니다.

*ParamSize*  
\[입력\] 이 매개 변수에 있는 기본 데이터의 최대 크기(바이트)입니다.

SQL_C_CHAR, SQL_C_WCHAR 및 SQL_C_BINARY 데이터 형식의 경우 값이 8000보다 크면 이 매개 변수가 LOB 개체를 나타내고, 크기가 최대 2GB임을 나타냅니다.

*DecimalDigits*  
\[입력\] 이 매개 변수에 있는 기본 데이터의 10진수로, [10진수](../../odbc/reference/appendixes/decimal-digits.md)의 정의를 따릅니다.

*ParamValue*  
\[입력\] 매개 변수 값을 포함하는 버퍼에 대한 포인터입니다.

*StrLen_or_Ind*  
\[입력\] *ParamValue*의 길이(바이트)를 나타내는 정수 값이거나 데이터가 NULL임을 나타내는 SQL_NULL_DATA입니다.

열이 null을 허용하지 않고 SQL_C_CHAR, SQL_C_WCHAR, SQL_C_BINARY, SQL_C_NUMERIC 또는 SQL_C_TYPE_TIMESTAMP 데이터 형식 중 하나를 나타내지 않는 경우에는 StrLen_or_Ind\[col\]을 무시할 수 있습니다. 그렇지 않으면 \[RowsNumber\] 요소가 포함된 유효한 배열을 가리킵니다. 여기서, 각 요소는 해당 길이나 null 표시기 데이터를 포함합니다.

*InputOutputType*  
\[입력\] 매개 변수의 형식입니다. *InputOutputType* 인수는 다음 값 중 하나입니다.

- SQL_PARAM_INPUT
- SQL_PARAM_INPUT_OUTPUT

## <a name="execute"></a>Execute

[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)의 `@script`를 실행합니다.

이 함수는 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)의 `@input_data_1_partition_by_columns`에 있는 각 파티션과 각 스트림 청크 대해 한 번씩, 여러 번 호출할 수 있습니다.


### <a name="syntax"></a>구문

```cpp
SQLRETURN Execute(
    SQLGUID         SessionId,
    SQLUSMALLINT    TaskId,
    SQLULEN         RowsNumber,
    SQLPOINTER*     Data,
    SQLINTEGER**    StrLen_or_Ind,
    SQLUSMALLINT*   OutputSchemaColumnsNumber
);
```

### <a name="arguments"></a>인수

*SessionId*  
\[입력\] 이 스크립트 세션을 고유하게 식별하는 GUID입니다.

*TaskId*  
\[입력\] 이 실행 프로세스를 고유하게 식별하는 정수입니다.

[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 `@parallel = 1`인 경우, 이 값의 범위는 0부터 쿼리의 병렬 처리 수준까지입니다.

*RowsNumber*  
\[입력\] *Data*의 행 수입니다.

*Data*  
\[입력\] [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 `@input_data_1`의 결과 집합을 포함하는 2차원 배열입니다.

열의 총수는 [InitSession](#initsession) 호출에서 받은 *InputSchemaColumnsNumber*입니다. 각 열에는 [InitColumn](#initcolumn)의 열 형식에 따라 해석해야 하는 *RowsNumber* 요소가 포함됩니다.

*StrLen_or_Ind*에서 NULL로 표시된 요소는 유효하지 않을 수 있으므로 무시해야 합니다.

*StrLen_or_Ind*  
\[입력\] *Data*에 있는 각 값의 길이/NULL 표시기를 포함하는 2차원 배열입니다. 각 셀의 가능한 값은 다음과 같습니다.

- n(n > 0). 데이터의 길이(바이트)를 나타냅니다.
- SQL_NULL_DATA. NULL 값을 나타냅니다.

열의 총수는 [InitSession](#initsession) 호출에서 받은 *InputSchemaColumnsNumber*입니다. 각 열에는 [InitColumn](#initcolumn)의 열 형식에 따라 해석해야 하는 *RowsNumber* 요소가 포함됩니다.

한 열이 null을 허용하지 않고 SQL_C_CHAR, SQL_C_WCHAR, SQL_C_BINARY, SQL_C_NUMERIC 또는 SQL_C_TYPE_TIMESTAMP 데이터 형식 중 하나를 나타내지 않는 경우에는 StrLen_or_Ind\[col\]을 무시할 수 있습니다. 그렇지 않으면 *RowsNumber* 요소가 포함된 유효한 배열을 가리킵니다. 여기서, 각 요소는 해당 길이나 null 표시기 데이터를 포함합니다.

*OutputSchemaColumnsNumber*  
\[출력\] [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 `@script`의 예상 결과 집합에 있는 열 수를 반환할 버퍼에 대한 포인터입니다.

## <a name="getresultcolumn"></a>GetResultColumn

특정 세션의 지정된 출력 열과 관련된 정보를 검색합니다.

이 함수는 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 `@script`의 결과 집합에 있는 각 열에 대해 호출됩니다.
이 결과 집합의 열 구조를 ‘출력 스키마’라고 합니다.

### <a name="syntax"></a>구문

```cpp
SQLRETURN GetResultColumn(
    SQLGUID         SessionId,
    SQLUSMALLINT    TaskId,
    SQLUSMALLINT    ColumnNumber,
    SQLSMALLINT*    DataType,
    SQLINTEGER*     ColumnSize,
    SQLSMALLINT*    DecimalDigits,
    SQLSMALLINT*    Nullable
);
```

### <a name="arguments"></a>인수

*SessionId*  
\[입력\] 이 스크립트 세션을 고유하게 식별하는 GUID입니다.

*TaskId*  
\[입력\] 이 실행 프로세스를 고유하게 식별하는 정수입니다.

[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 `@parallel = 1`인 경우, 이 값의 범위는 0부터 쿼리의 병렬 처리 수준까지입니다.

*ColumnNumber*  
\[입력\] 출력 스키마에서 이 열의 인덱스를 식별하는 정수입니다. 열은 0부터 시작하여 오름차순으로 번호가 매겨집니다.

*DataType*  
\[출력\] 이 열의 데이터 형식을 식별하는 ODBC C 형식을 포함하는 버퍼에 대한 포인터입니다.

*ColumnSize*  
\[출력\] 이 열에 있는 기본 데이터의 최대 크기(바이트)를 포함하는 버퍼에 대한 포인터입니다.

*DecimalDigits*  
\[출력\] 이 열에 있는 기본 데이터의 10진수를 포함하는 버퍼에 대한 포인터로, [10진수](../../odbc/reference/appendixes/decimal-digits.md)의 정의를 따릅니다. 10진수 자릿수를 확인할 수 없거나 해당하지 않는 경우에는 값이 무시됩니다.

*Null 허용*  
\[출력\] 이 열에 NULL 값을 포함할 수 있는지 여부를 나타내는 값을 포함하는 버퍼에 대한 포인터입니다. 가능한 값은 다음과 같습니다.

- SQL_NO_NULLS: 열에 NULL 값을 포함할 수 없습니다.
- SQL_NULLABLE: 열에 NULL 값을 포함할 수 있습니다.

다른 값이 전달되면 실행이 중지됩니다.

## <a name="getresults"></a>GetResults

[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 `@script`를 실행한 결과 집합을 검색합니다.

이 함수는 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)의 `@input_data_1_partition_by_columns`에 있는 각 파티션과 각 스트림 청크 대해 한 번씩, 여러 번 호출할 수 있습니다.


### <a name="syntax"></a>구문

```cpp
SQLRETURN GetResults(
    SQLGUID         SessionId,
    SQLUSMALLINT    TaskId,
    SQLULEN*        RowsNumber,
    SQLPOINTER**    Data,
    SQLINTEGER***   StrLen_or_Ind
);
```

### <a name="arguments"></a>인수

*SessionId*  
\[입력\] 이 스크립트 세션을 고유하게 식별하는 GUID입니다.

*TaskId*  
\[입력\] 이 실행 프로세스를 고유하게 식별하는 정수입니다.

[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 `@parallel = 1`인 경우, 이 값의 범위는 0부터 쿼리의 병렬 처리 수준까지입니다.

*RowsNumber*  
\[출력\] *Data*의 행 수를 포함하는 버퍼에 대한 포인터입니다.

*Data*  
\[출력\] [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 `@script`의 결과 집합을 포함하는 2차원 배열에 대한 포인터로, 확장에서 할당됩니다.

열의 총수는 [Execute](#execute) 호출에서 검색된 *OutputSchemaColumnsNumber*여야 합니다. 각 열에는 [GetResultColumn](#getresultcolumn)의 열 형식에 따라 해석해야 하는 *RowsNumber* 요소가 포함되어야 합니다.

*StrLen_or_Ind*  
\[출력\] *Data*에 있는 각 값의 길이/NULL 표시기를 포함하는 2차원 배열에 대한 포인터로, 확장에서 할당됩니다. 각 셀의 가능한 값은 다음과 같습니다.

- n(n > 0). 데이터의 길이(바이트)를 나타냅니다.
- SQL_NULL_DATA. NULL 값을 나타냅니다.

열의 총수는 [Execute](#execute) 호출에서 받은 *OutputSchemaColumnsNumber*여야 합니다. 각 열에는 [GetResultColumn](#getresultcolumn)의 열 형식에 따라 해석해야 하는 *RowsNumber* 요소가 포함됩니다.

한 열이 null을 허용하지 않고 SQL_C_CHAR, SQL_C_WCHAR, SQL_C_BINARY [add dates] 데이터 형식 중 하나를 나타내지 않는 경우에는 StrLen_or_Ind\[col\]이 무시됩니다. 그렇지 않으면 *RowsNumber* 요소가 포함된 유효한 배열을 가리킵니다. 여기서, 각 요소는 해당 길이나 null 표시기 데이터를 포함합니다.

## <a name="getoutputparam"></a>GetOutputParam

특정 세션의 지정된 출력 매개 변수와 관련된 정보를 검색합니다.

이 함수는 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 OUTPUT으로 표시된 `@params`의 각 매개 변수에 대해 호출됩니다.

### <a name="syntax"></a>구문

```cpp
SQLRETURN GetOutputParam(
    SQLGUID        SessionId,
    SQLUSMALLINT   ParamNumber,
    SQLPOINTER*    ParamValue,
    SQLINTEGER*    StrLen_or_Ind
);
```

### <a name="arguments"></a>인수

*SessionId*  
\[입력\] 이 스크립트 세션을 고유하게 식별하는 GUID입니다.

*ParamValue*  
\[출력\] 매개 변수 값을 포함하는 버퍼에 대한 포인터입니다.

*StrLen_or_Ind* \[출력\] *ParamValue*의 길이(바이트)를 나타내는 정수 값을 포함하는 버퍼에 대한 포인트거나 데이터가 NULL임을 나타내는 SQL_NULL_DATA입니다.

## <a name="getinterfaceversion"></a>GetInterfaceVersion

인터페이스 버전을 검색합니다.
이 함수는 확장의 인터페이스 버전을 나타내는 정수를 반환합니다. 지원되는 값:
1. 버전 1은 초기 API 버전입니다. SQL Server 2019 RTM에서 지원됩니다.
1. 버전 2는 InstallExternalLibrary 및 UninstallExternalLibrary API 지원을 추가했으며 SQL Server 2019 CU3부터 지원됩니다.                            

### <a name="syntax"></a>구문

```cpp
SQLUSMALLINT GetInterfaceVersion();
```

## <a name="cleanupsession"></a>CleanupSession

세션별 정보를 정리합니다.

### <a name="syntax"></a>구문

```cpp
SQLRETURN CleanupSession(
    SQLGUID        SessionId,
    SQLUSMALLINT   TaskId
);
```

### <a name="arguments"></a>인수

*SessionId*  
\[입력\] 이 스크립트 세션을 고유하게 식별하는 GUID입니다.

*TaskId*  
\[입력\] 이 실행 프로세스를 고유하게 식별하는 정수입니다.

[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 `@parallel = 1`인 경우, 이 값의 범위는 0부터 쿼리의 병렬 처리 수준까지입니다.

## <a name="cleanup"></a>정리

전역 공유 정보(예: JVM)를 정리합니다.

### <a name="syntax"></a>구문

```cpp
SQLRETURN Cleanup();
```

## <a name="gettelemetryresults"></a>GetTelemetryResults

확장에서 원격 분석(키-값 쌍) 데이터를 검색합니다. 이 함수는 선택 사항으로, 구현이 필요하지 않습니다. 원격 분석은 `dm_db_external_script_execution_stats` DMV(동적 관리 뷰)를 통해 공개됩니다.

프레임워크에서 전송되는 script_executions라는 카운터가 있습니다. 이 이름은 확장에서 사용할 수 없습니다.

각 원격 분석 항목은 키-값 쌍입니다. 키는 문자열이고, 값은 64비트 정수 카운터입니다. 따라서 출력은 이름 및 해당 카운터라는 두 개의 논리적 배열로 구성됩니다. 각 배열은 출력입니다.

각 배열의 길이는 출력인 *RowsNumber*입니다. 첫 번째 논리적 출력에는 문자열에 대한 포인터가 포함되므로, *CounterNames*(실제 문자열 데이터) 및 *CounterNamesLength*(각 문자열의 길이)라는 두 개의 배열로 표시됩니다. 두 번째 논리적 출력은 *CounterValues* 포인터에 저장됩니다.

### <a name="syntax"></a>구문

```cpp
SQLRETURN GetTelemetryResults(
    SQLGUID        SessionId,
    SQLUSMALLINT   TaskId,
    SQLUINTEGER    *RowsNumber,
    SQLCHAR        ***CounterNames,
    SQLINTEGER      **CounterNamesLength,
    SQLBIGINT       **CounterValues
);
```

### <a name="arguments"></a>인수

*SessionId*  
\[입력\] 이 스크립트 세션을 고유하게 식별하는 GUID입니다.

*TaskId*  
\[입력\] 이 실행 프로세스를 고유하게 식별하는 정수입니다.

[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 `@parallel = 1`인 경우, 이 값의 범위는 0부터 쿼리의 병렬 처리 수준까지입니다.

*RowsNumber*  
\[출력\] 키-값 쌍 수입니다.

*CounterNames*  
\[출력\] 키를 포함하는 문자열 데이터입니다.

*CounterNamesLength*  
\[출력\] 각 키 문자열의 길이입니다.

*CounterValues*  
\[출력\] 값을 포함하는 64비트 정수 데이터입니다.

## <a name="installexternallibrary"></a>InstallExternalLibrary

라이브러리를 설치합니다. 이 함수는 선택 사항으로, 구현이 필요하지 않습니다. 기본 구현은 라이브러리([CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) 참조) 콘텐츠를 적절한 위치에 있는 파일에 복사하는 것입니다. 파일 이름은 라이브러리 이름입니다.

### <a name="syntax"></a>구문

```cpp
SQLRETURN InstallExternalLibrary(
    SQLGUID    SetupSessionId,
    SQLCHAR    *LibraryName,
    SQLINTEGER LibraryNameLength,
    SQLCHAR    *LibraryFile,
    SQLINTEGER LibraryFileLength,
    SQLCHAR    *LibraryInstallDirectory,
    SQLINTEGER LibraryInstallDirectoryLength,
    SQLCHAR    **LibraryError,
    SQLINTEGER *LibraryErrorLength
);
```

### <a name="arguments"></a>인수

*SetupSessionId*  
\[입력\] 이 스크립트 세션을 고유하게 식별하는 GUID입니다.

*LibraryName*  
\[입력\] 라이브러리 이름입니다.

*LibraryNameLength*  
\[입력\] 라이브러리 이름의 길이입니다.

*LibraryFile*  
\[입력\] [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)에서 지정된, 이진 콘텐츠를 포함하는 라이브러리 파일의 경로(문자열)입니다.

*LibraryFileLength*  
\[입력\] LibraryFile 문자열의 길이입니다.

*LibraryInstallDirectory*  
\[입력\] 라이브러리를 설치할 루트 디렉터리입니다.

*LibraryInstallDirectoryLength*  
\[입력\] LibraryInstallDirectory 문자열의 길이입니다.

*LibraryError*  
\[출력\] 선택적 출력 매개 변수입니다. 라이브러리를 설치하는 중 오류가 발생한 경우 LibraryError는 오류를 설명하는 문자열을 가리킵니다.

*LibraryErrorLength*  
\[출력\] LibraryError 문자열의 길이입니다.

## <a name="uninstalllibrary"></a>UninstallLibrary

라이브러리를 제거합니다. 이 함수는 선택 사항으로, 구현이 필요하지 않습니다. 기본 구현은 InstallExternalLibrary의 기본 구현에서 수행된 작업을 실행 취소하는 것입니다. 기본 구현에서는 *LibraryInstallDirectory*에 있는 *LibraryName* 파일의 콘텐츠를 삭제합니다.

### <a name="syntax"></a>구문

```cpp
SQLRETURN UninstallExternalLibrary(
    SQLGUID    SetupSessionId,
    SQLCHAR    *LibraryName,
    SQLINTEGER LibraryNameLength,
    SQLCHAR    *LibraryInstallDirectory,
    SQLINTEGER LibraryInstallDirectoryLength,
    SQLCHAR    **LibraryError,
    SQLINTEGER *LibraryErrorLength
);
```

### <a name="arguments"></a>인수

*SetupSessionId*  
\[입력\] 이 스크립트 세션을 고유하게 식별하는 GUID입니다.

*LibraryName*  
\[입력\] 라이브러리 이름입니다.

*LibraryNameLength*  
\[입력\] 라이브러리 이름의 길이입니다.

*LibraryFile*  
\[입력\] CREATE EXTERNAL LIBRARY에서 지정된, 이진 콘텐츠를 포함하는 라이브러리 파일의 경로(문자열)입니다.

*LibraryFileLength*  
\[입력\] LibraryFile 문자열의 길이입니다.

*LibraryInstallDirectory*  
\[입력\] 라이브러리를 설치할 루트 디렉터리입니다.

*LibraryInstallDirectoryLength*  
\[입력\] LibraryInstallDirectory 문자열의 길이입니다.

*LibraryError*  
\[출력\] 라이브러리 오류 문자열입니다.

*LibraryErrorLength*  
\[출력\] LibraryError 문자열의 길이입니다.

## <a name="next-steps"></a>다음 단계

- [SQL Server에 대한 Java용 Microsoft 확장성 SDK](../how-to/extensibility-sdk-java-sql-server.md) 
