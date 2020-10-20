---
description: 프로젝트 설정(변환)(SybaseToSQL)
title: 프로젝트 설정 (변환) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/19/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1f4d616b964a1e9e9eed391e3386b16e9df54e44
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195535"
---
# <a name="project-settings-conversion-sybasetosql"></a>프로젝트 설정(변환)(SybaseToSQL)

**프로젝트 설정** 대화 상자의 **변환** 페이지에는 Ssma에서 SAP 적응 서버 엔터프라이즈 (ASE) 구문을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL 구문으로 변환 하는 방법을 사용자 지정 하는 설정이 포함 되어 있습니다.

**변환** 창은 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자에서 사용할 수 있습니다.

- 모든 SSMA 프로젝트에 대 한 설정을 지정 하려면 **도구** 메뉴에서 **기본 프로젝트 설정**을 선택 하 고 왼쪽 창의 맨 아래에 있는 **일반** 을 클릭 한 다음 **변환**을 클릭 합니다.

- 현재 프로젝트에 대 한 설정을 지정 하려면 **도구** 메뉴에서 **프로젝트 설정**을 선택 하 고 왼쪽 창의 맨 아래에 있는 **일반** 을 클릭 한 다음 **변환**을 클릭 합니다.

## <a name="miscellaneous-section"></a>기타 섹션

### <a name="error"></a>@@ERROR

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL 및 ASE는 서로 다른 오류 코드를 사용 합니다.

이 설정을 사용 하 여 ASE 코드의에 대 한 참조가 발견 될 때 SSMA에서 출력 또는 오류 목록 창에 표시 하는 메시지 유형 (경고 또는 오류)을 지정할 수 `@@ERROR` 있습니다.

- 변환을 선택 하 **고 경고를 표시**하는 경우 ssma는 문을 변환 하 고 경고 주석으로 표시 합니다.
- **표시를 오류로 표시**를 선택 하면 ssma는 변환을 건너뛰고 문을 오류 주석으로 표시 합니다.

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|경고를 사용 하 여 변환 및 표시|
|Optimistic|경고를 사용 하 여 변환 및 표시|
|전체|오류로 표시|

### <a name="conversion-of-like-operator"></a>LIKE 연산자의 변환

`LIKE`SAP ASE 동작과 일치 하도록 피연산자를 변환할지 여부를 지정 합니다. ASE는 ASE가 like 패턴에서 후행 공백을 트리밍하는 점입니다. 해결 방법은 최대 전체 자릿수를 사용 하 여 고정 길이 데이터 형식으로 오른쪽 식을 캐스트 하는 것입니다.
  
- 수정 하지 않고 식을 변환 하려면 **단순 변환** 을 선택 합니다.
- ASE 동작을 사용 하려면 **고정 길이로 캐스트를 선택 합니다.**
  
모드 상자에서 변환 모드를 선택 하면 SSMA가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|간단한 변환|
|Optimistic|간단한 변환|
|전체|고정 길이로 캐스트|

### <a name="convert-or-cast-empty-strings-to-numeric-types"></a>빈 문자열을 숫자 형식으로 변환 또는 캐스팅

`CONVERT`숫자 형식이 datatype 인수인 또는 식 내에서 빈 문자열 또는 빈 문자열을 처리 하는 방법을 지정 합니다 `CAST` . 이 설정에 사용할 수 있는 옵션은 다음과 같습니다.

- 수정 하지 않고 식을 변환 하려면 **단순 변환** 을 선택 합니다.
- **빈 문자열을 0으로** 선택 하면 문자열 매개 변수가 `{s}` 식으로 대체 됩니다 `CASE ltrim(rtrim({s})) WHEN "" THEN 0 else {s} END` .

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|간단한 변환|
|Optimistic|간단한 변환|
|전체|숫자가 0 인 빈 문자열|

### <a name="concatenation-of-null"></a>NULL 연결

이 설정은를 사용 하 여 문자열 연결을 변환 하는 방법을 지정 합니다 `NULL` . 이 특정 설정에 대해 다음과 같은 옵션을 설정할 수 있습니다.

- **Wrap 함수를 사용 하 여 Wrap 함수** 옵션을 선택 하면 `string_expression` 연결의 모든 비상수는로 래핑되 `ISNULL(string_expression)` 며 `NULL` s는 빈 문자열로 바뀝니다.
- **현재 구문을 유지** 하면 원래 구문이 유지 됩니다.

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|현재 구문 유지|
|Optimistic|현재 구문 유지|
|전체|ISNULL 함수를 사용 하 여 래핑|

### <a name="conversion-of-empty-strings"></a>빈 문자열 변환

이 설정은 빈 문자열을 변환 하는 방법을 지정 합니다. 이 특정 설정에 대해 다음과 같은 옵션을 설정할 수 있습니다.

- **모든 문자열 식을 공백으로 바꿉니다.**
- **빈 문자열 상수를 공백으로 바꾸기**

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL 동작을 사용 하려면 **현재 구문 유지**를 선택 합니다.

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|현재 구문 유지|
|Optimistic|현재 구문 유지|
|전체|모든 문자열 식을 공백으로 바꿉니다.|

### <a name="convert-and-cast-binary-string-conversion"></a>이진 문자열 변환 변환 및 캐스트

이진 값을 숫자로 변환 하는 경우 다른 플랫폼에서 다른 값을 반환할 수 있습니다. 예를 들어 x86 프로세서에서는 `CONVERT(integer, 0x00000100)` ASE로를 반환 하지만에서는를 반환 `65536` `256` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 또한 ASE는 바이트 순서에 따라 다른 값을 반환 합니다.

이 설정을 사용 하 여 SSMA `CONVERT` 에서 `CAST` 이진 값을 포함 하는 및 식을 변환 하는 방법을 제어 합니다.

- 경고 또는 수정 없이 식을 변환 하려면 **단순 변환** 을 선택 합니다. ASE 서버에 이진 값을 변경할 필요가 없는 바이트 순서가 있는 경우이 설정을 사용 합니다.
- **변환 및 수정** 을 선택 하 여 ssma에서 사용할 식을 변환 하 고 수정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 리터럴 상수의 바이트 순서가 반대로 바뀝니다. 다른 모든 이진 값 (예: 이진 변수 및 열)은 오류로 표시 됩니다. ASE 서버에 이진 값을 변경 해야 하는 바이트 순서가 있는 경우이 값을 사용 합니다.

변환 **및 경고로 표시** 를 선택 하 여 ssma가 식을 변환 하 고 수정 하도록 한 다음 변환 된 모든 식을 경고 주석으로 표시 합니다.

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|경고를 사용 하 여 변환 및 표시|
|Optimistic|간단한 변환|
|전체|변환 및 수정|

### <a name="dynamic-sql"></a>동적 SQL

이 설정을 사용 하 여 ASE 코드에서 동적 SQL을 발견할 때 SSMA에서 **출력** 또는 **오류 목록** 창에 표시 하는 메시지 유형 (경고 또는 오류)을 지정할 수 있습니다.

- 변환을 선택 하 **고 경고를 표시**하는 경우 ssma는 동적 SQL을 변환 하 고 문을 경고 주석으로 표시 합니다.
- **표시를 오류로 표시**를 선택 하면 ssma는 변환을 건너뛰고 문을 오류 주석으로 표시 합니다.

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|경고를 사용 하 여 변환 및 표시|
|Optimistic|경고를 사용 하 여 변환 및 표시|
|전체|오류로 표시|

### <a name="equality-check-conversion"></a>같음 확인 변환

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/AZURE sql에서 `ANSI_NULLS` 설정이 on 인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 같음 비교에 값이 포함 되어 있으면/azure sql이 반환 됩니다 `UNKNOWN` `NULL` . `ANSI_NULLS`가 off 인 경우 값을 포함 하는 같음 비교는 비교 되는 `NULL` 열과 식 또는 두 식이 모두 인 경우 true를 반환 합니다 `NULL` . 기본적으로 ( `ANSINULL OFF` ) SAP ASE 같음 비교는 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 으)로/Azure SQL과 같이 동작 `ANSI_NULLS OFF` 합니다.

- **단순 변환**을 선택 하는 경우 ssma는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 값에 대 한 추가 검사 없이 ASE 코드를/azure SQL 구문으로 변환 합니다 `NULL` . `ANSI_NULLS`가/ `OFF` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure SQL에 있거나 case를 기준으로 같음 비교를 수정 하려는 경우이 설정을 사용 합니다.
- **NULL 값 고려**를 선택 하는 경우 ssma는 `NULL` and 절을 사용 하 여 값에 대 한 검사를 추가 `IS NULL` `IS NOT NULL` 합니다.

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|간단한 변환|
|Optimistic|간단한 변환|
|전체|NULL 값 고려|

### <a name="format-strings"></a>형식 문자열

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL은 `format_string` 및 문에서 인수를 더 이상 지원 하지 않습니다 `PRINT` `RAISERROR` . `format_string`인수는 대체 가능 매개 변수를 문자열에 직접 배치한 다음 런타임에 매개 변수를 대체 하는 데 사용할 수 있습니다. 대신에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문자열 리터럴 또는 변수를 사용 하 여 작성 된 문자열을 사용 하 여 전체 문자열이 필요 합니다. 자세한 내용은 [PRINT ( [!INCLUDE[tsql](../../includes/tsql-md.md)] )](../../t-sql/language-elements/print-transact-sql.md) 항목을 참조 하세요.

SSMA가 인수를 발견 하는 경우 `format_string` 변수를 사용 하 여 문자열 리터럴을 작성 하거나 새 변수를 만들고 해당 변수를 사용 하 여 문자열을 작성할 수 있습니다.

- 및 함수에 문자열 리터럴을 사용 `PRINT` 하려면 `RAISERROR` **새 문자열 만들기**를 선택 합니다.

    이 모드에서 PRINT 또는 RAISERROR 문이 자리 표시자 및 지역 변수를 사용 하지 않는 경우 문은 변경 되지 않습니다. 2% 문자 (%%) 인쇄 문자열 리터럴의 1% 문자%로 변경 됩니다.

    PRINT 또는 RAISERROR 문에서 다음 예제와 같이 자리 표시자와 하나 이상의 지역 변수를 사용 하는 경우:

    ```sql
    PRINT 'Total: %1!%%', @percent
    ```

    SSMA는 다음 구문으로 변환 합니다.

    ```sql
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'
    ```

    `format_string`이 변수인 경우는 다음과 같습니다.  

    ```sql
    PRINT @fmt, @arg1, @arg2
    ```

    SSMA는 간단한 문자열 변환을 수행할 수 없으며 새 변수를 만들어야 합니다.

    ```sql
    DECLARE @print_format_1 varchar(max)
    SET @print_format_1 =
        REPLACE (@fmt, '%%', '%')
    SET @print_format_1 =
        REPLACE (@print_format_1, '%1!',
        CAST (@arg1 AS varchar(max)))
    SET @print_format_1 =
        REPLACE (@print_format_1, '%2!',
        CAST (@arg2 AS varchar(max)))
    PRINT @print_format_1
    ```

    **새 문자열 모드 만들기** 를 사용 하는 경우 ssma는 옵션이 인 것으로 가정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `CONCAT_NULL_YIELDS_NULL` `OFF` 합니다. 따라서 SSMA는 null 인수를 확인 하지 않습니다.

- SSMA에서 각 및 문에 대해 새 변수를 작성 하 게 한 `PRINT` `RAISERROR` 다음 해당 변수를 문자열 값으로 사용 하려면 **새 변수 만들기**를 선택 합니다.

    이 모드에서 `PRINT` 또는 `RAISERROR` 문이 자리 표시자 및 지역 변수를 사용 하지 않는 경우 ssma는 모든 더블% 문자 ( `%%` )를 단일 백분율 문자로 대체 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /azure SQL 구문을 준수 합니다.

    `PRINT`또는 `RAISERROR` 문에서 다음 예제와 같이 자리 표시자와 하나 이상의 지역 변수를 사용 하는 경우입니다.

    ```sql
    PRINT 'Total: %1!%%', @percent
    ```

    SSMA는 다음 구문으로 변환 합니다.

    ```sql
    DECLARE @print_format_1 varchar(max)
    SET @print_format_1 = 'Total: %1!%'
    SET @print_format_1 =
        REPLACE (@print_format_1, '%1!',
        ISNULL(CAST (@percent AS VARCHAR(max)), ''))
    PRINT @print_format_1
    ```

    `format_string`이 변수인 경우는 다음과 같습니다.

    ```sql
    PRINT @fmt, @arg1, @arg2
    ```

    SSMA는 다음과 같이 새 변수를 만들고 각 인수에서 null 값을 확인 합니다.

    ```sql
    DECLARE @print_format_1 varchar(max)
    SET @print_format_1 =
        REPLACE (@fmt, '%%', '%')
    SET @print_format_1 =
        REPLACE (@print_format_1, '%1!',
        ISNULL(CAST (@arg1 AS varchar(max)),''))
    SET @print_format_1 =
        REPLACE (@print_format_1, '%2!',
        ISNULL(CAST (@arg2 AS varchar(max)),''))
    PRINT @print_format_1
    ```

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|새 문자열 만들기|
|Optimistic|새 문자열 만들기|
|전체|새 변수 만들기|

### <a name="insert-an-explicit-value-into-a-timestamp-column"></a>Timestamp 열에 명시적 값 삽입

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL은 타임 스탬프 열에 명시적 값을 삽입 하는 것을 지원 하지 않습니다.

- 문에서 timestamp 열을 제외 하려면 `INSERT` **열 제외**를 선택 합니다.
- 타임 스탬프 열이 문에 있을 때마다 오류 메시지를 인쇄 하려면 `INSERT` **오류 표시**를 선택 합니다. 이 모드에서 `INSERT` 문은 변환 되지 않으며 오류 주석으로 표시 됩니다.

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|열 제외|
|Optimistic|열 제외|
|전체|오류로 표시|

### <a name="store-temporary-objects-defined-in-procedures"></a>프로시저에 정의 된 임시 개체 저장

이 설정은 프로시저에 표시 되는 임시 개체 정의를 변환 하는 동안 원본 메타 데이터에 저장 해야 하는지 여부를 지정 합니다.

- 메타 데이터에 저장 하려면 **예** 를 선택 합니다.
- 개체를 저장 하지 않아도 되는 경우 **아니요** 를 선택 합니다.

|Mode|값|
|-|-|
|기본값|예|
|Optimistic|예|
|전체|예|

### <a name="proxy-table-conversion"></a>프록시 테이블 변환

ASE 프록시 테이블이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /AZURE SQL 테이블로 변환 되는지, 아니면 변환 되지 않고 코드에 오류 주석이 표시 되는지 여부를 지정 합니다.

- **변환** 을 선택 하 여 프록시 테이블을 일반 테이블로 변환 합니다.
- 오류가 **있는 표시** 를 선택 하 여 프록시 테이블 코드를 오류 주석으로 표시 하기만 하면 됩니다.

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|오류로 표시|
|Optimistic|오류로 표시|
|전체|오류로 표시|

### <a name="raiserror-base-message-number"></a>RAISERROR 기준 메시지 번호

ASE 사용자 메시지는 각 데이터베이스에 저장 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 메시지는 중앙에서 저장 되며 카탈로그 뷰를 통해 사용할 수 있게 됩니다 `sys.messages` . 또한 ASE 사용자 메시지는에서 시작 `20000` 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 메시지는에서 시작 `50001` 합니다.

이 설정은 ASE 사용자 메시지 번호에 추가 하 여 사용자 메시지로 변환 하는 번호를 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]카탈로그 뷰에 사용자 메시지가 있는 경우 `sys.messages` 이 숫자를 더 높은 값으로 변경 해야 할 수 있습니다. 이는 변환 된 메시지 번호가 기존 메시지 번호와 충돌 하지 않도록 하기 위한 것입니다.

다음 사항에 유의하세요.
  
- 범위의 ASE 메시지 `17000` - `19999` 는 시스템 테이블에서 가져온 것 `sysmessages` 이며 변환 되지 않습니다.
- 문에서 참조 되는 메시지 번호가 `RAISERROR` 상수인 경우 SSMA는 상수에 기본 메시지 번호를 추가 하 여 새 사용자 메시지 번호를 확인 합니다.
- 참조 되는 메시지 번호가 변수 또는 식인 경우 SSMA는 중간 지역 변수를 만듭니다.
- **낙관적 모드**에서 ssma는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 옵션이 이며 `CONCAT_NULL_YIELDS_NULL` `OFF` 인수를 확인 하지 않는 것으로 가정 `NULL` 합니다.
- **전체 모드**에서 ssma는 인수를 확인 `NULL` 합니다.
- `RAISERROR` with `arg-list` 인수는 변환 되지 않습니다.

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|30001|
|Optimistic|30001|
|전체|30001|

### <a name="system-objects"></a>시스템 개체

이 설정을 사용 하 여 ASE 시스템 개체를 사용 하는 경우 SSMA에서 **출력** 또는 **오류 목록** 창에 표시 하는 메시지 유형 (경고 또는 오류)을 지정할 수 있습니다.

- 변환을 선택 하 **고 경고를 표시**하는 경우 ssma는 참조를 시스템 개체로 변환 하 고 문을 경고 주석으로 표시 합니다.
- **표시를 오류로 표시**를 선택 하면 ssma는 시스템 개체에 대 한 참조를 변환 하지 않으며 문을 오류 주석으로 표시 합니다.

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|경고를 사용 하 여 변환 및 표시|
|Optimistic|경고를 사용 하 여 변환 및 표시|
|전체|오류로 표시|

### <a name="unresolved-identifiers"></a>확인 되지 않은 식별자

이 설정을 사용 하 여 id를 확인할 수 없는 경우 SSMA에서 **출력** 또는 **오류 목록** 창에 표시 하는 메시지 유형 (경고 또는 오류)을 지정할 수 있습니다.

- **변환 및 경고로 표시**를 선택 하는 경우 ssma는 확인 되지 않은 식별자에 대 한 참조를 변환 하려고 시도 하 고 문을 경고 주석으로 표시 합니다.
- **표시를 오류로 표시**를 선택 하면 ssma는 확인 되지 않은 식별자에 대 한 참조를 변환 하지 않으며 문을 오류 주석으로 표시 합니다.

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|경고를 사용 하 여 변환 및 표시|
|Optimistic|경고를 사용 하 여 변환 및 표시|
|전체|오류로 표시|

## <a name="system-functions-section"></a>시스템 함수 섹션

### <a name="charindex-function"></a>CHARINDEX 함수

ASE에서 `CHARINDEX` `NULL` 는 모든 입력 식이 인 경우에만를 반환 `NULL` 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL은 `NULL` 입력 식이 인 경우을 반환 `NULL` 합니다.

- ASE 동작을 사용 하려면 **바꾸기 함수**를 선택 합니다. 함수에 대 한 모든 호출은 `CHARINDEX` `CHARINDEX_VARCHAR`  `CHARINDEX_NVARCHAR` SAP ASE 동작을 에뮬레이트하는 전달 된 매개 변수 형식 (스키마 이름으로 사용자 데이터베이스에서 만들어짐)을 기반으로 하는 또는 사용자 정의 함수에 대 한 호출로 대체 됩니다 `s2ss` .
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL 동작을 사용 하려면 **현재 구문 유지**를 선택 합니다.

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|현재 구문 유지|
|Optimistic|현재 구문 유지|
|전체|Replace 함수|
  
### <a name="datalength-function"></a>DATALENGTH 함수

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL 및 ASE는 `DATALENGTH` 값이 단일 공간 일 때 함수에서 반환 하는 값과 다릅니다. 이 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /CERS SQL은를 반환 `0` 하 고 ASE는를 반환 `1` 합니다.

- ASE 동작을 사용 하려면 **바꾸기 함수**를 선택 합니다. 함수에 대 한 모든 호출은 `DATALENGTH` `CASE` SAP ASE 동작을 에뮬레이트하는 식으로 대체 됩니다.
- 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /AZURE SQL 동작을 사용 하려면 **현재 구문 유지**를 선택 합니다.

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|현재 구문 유지|
|Optimistic|현재 구문 유지|
|전체|Replace 함수|

### <a name="index_col-function"></a>INDEX_COL 함수

ASE는 `user_id` 함수에 대 한 선택적 인수를 지원 `INDEX_COL` 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /Azure SQL은이 인수를 지원 하지 않습니다. 인수를 사용 하는 경우 `user_id` 이 함수를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /AZURE SQL 구문으로 변환할 수 없습니다.

- ASE 동작을 사용 하려면 **Convert 함수**를 선택 합니다. 코드에 인수가 포함 된 경우 `user_id` SSMA는 오류를 표시 합니다.
- 발생할 때마다 오류 메시지를 표시 하려면 `INDEX_COL` **오류 표시**를 선택 합니다. SSMA는 함수에 대 한 참조를 변환 하지 않으며 문을 오류 주석으로 표시 합니다.

|Mode|값|
|-|-|
|기본값|오류로 표시|
|Optimistic|오류로 표시|
|전체|오류로 표시|

### <a name="index_colorder-function"></a>INDEX_COLORDER 함수

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL에는 `INDEX_COLORDER` 시스템 함수가 없습니다.

- ASE 동작을 사용 하려면 **Convert 함수**를 선택 합니다. 함수에 대 한 모든 호출은 `INDEX_COLORDER` SAP ASE 동작을 에뮬레이트하는 동일한 이름의 사용자 정의 함수 `INDEX_COLORDER` (스키마 이름에 따라 사용자 데이터베이스에서 만들어짐)로 대체 됩니다 `s2ss` .
- 발생할 때마다 오류 메시지를 인쇄 하려면 `INDEX_COLORDER` **오류 표시**를 선택 합니다. SSMA는 함수에 대 한 참조를 변환 하지 않으며 문을 오류 주석으로 표시 합니다.

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|오류로 표시|
|Optimistic|오류로 표시|
|전체|오류로 표시|

### <a name="left-and-right-functions"></a>LEFT 및 RIGHT 함수

`LEFT``RIGHT`ASE의 및 함수는 음수 길이 매개 변수에 대해 다르게 동작 합니다.

- ASE 동작을 사용 하려면 **바꾸기 함수**를 선택 합니다. 그러면 길이 매개 변수가 `CASE` 음수 값을 반환 하는 식으로 바뀝니다 `NULL` .
- SQL Server 동작을 사용 하려면 **현재 구문 유지**를 선택 합니다.

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|현재 구문 유지|
|Optimistic|현재 구문 유지|
|전체|Replace 함수|

> [!NOTE]
> 길이 매개 변수가 복소수 식이 아닌 리터럴 값 이면 길이 값은 항상 `NULL` 프로젝트 설정에 관계 없이로 바뀝니다.

### <a name="next_identity-function"></a>NEXT_IDENTITY 함수

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL에는 `NEXT_IDENTITY` 시스템 함수가 없습니다.

- ASE 동작을 사용 하려면 **Convert 함수**를 선택 합니다. 함수에 대 한 모든 호출은 `NEXT_IDENTITY` SAP ASE 동작을 에뮬레이트하는 식으로 대체 됩니다 `(IDENT_CURRENT(parameter Value) + IDENT_INCR(parameter Value)` .
- 발생할 때마다 오류 메시지를 인쇄 하려면 `NEXT_IDENTITY` **오류 표시**를 선택 합니다. SSMA는 함수에 대 한 참조를 변환 하지 않으며 문을 오류 주석으로 표시 합니다.

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|오류로 표시|
|Optimistic|오류로 표시|
|전체|오류로 표시|

**기본/최적/전체 모드:** 오류로 표시

### <a name="patindex-function"></a>PATINDEX 함수

`PATINDEX`SAP ASE 동작과 일치 하도록 함수를 변환할지 여부를 지정 합니다. ASE는 검색 패턴에서 후행 공백을 잘라내는 것입니다. 해결 방법은 최대 전체 자릿수를 사용 하 고 `rtrim` 함수를 검색 패턴에 적용 하 여 고정 길이 데이터 형식으로 값 식을 캐스팅 하는 것입니다.

- ASE 동작을 사용 하려면 **사용**을 선택 합니다.  
- 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /AZURE SQL 동작을 사용 하려면 사용 안 **함**을 선택 합니다.

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|사용 안 함|
|Optimistic|사용 안 함|
|전체|기능|

### <a name="replicate-function"></a>REPLICATE 함수

`REPLICATE`함수는 지정 된 횟수 만큼 문자열을 반복 합니다. ASE에서 문자열을 0 회 반복 하도록 지정 하는 경우 결과는 `NULL` 입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/AZURE SQL에서 결과는 빈 문자열입니다.

- ASE 동작을 사용 하려면 **바꾸기 함수**를 선택 합니다. 함수에 대 한 모든 호출은 `REPLICATE` `REPLICATE_VARCHAR` `REPLICATE_NVARCHAR` SAP ASE 동작을 에뮬레이트하는 전달 된 매개 변수 형식 (스키마 이름으로 사용자 데이터베이스에서 만들어짐)을 기반으로 하는 또는 사용자 정의 함수에 대 한 호출로 대체 됩니다 `s2ss` .
- 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /AZURE SQL 동작을 사용 하려면 **함수 바꾸기**를 선택 합니다.

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|Replace 함수|
|Optimistic|Replace 함수|
|전체|Replace 함수|

### <a name="trim-ltrim-rtrim-function"></a>TRIM (LTRIM, RTRIM) 함수

이 설정은에 대 한 호출을 `TRIM` , `LTRIM` 및 함수를 `RTRIM` SAP ASE와 동등한 구문 함수로 바꿀지 아니면 현재 구문을 유지할지를 지정 합니다. 이 특정 설정에 대해 다음 옵션이 제공 됩니다.

- **Replace 함수**
- **현재 구문 유지**

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|Replace 함수|
|Optimistic|Replace 함수|
|전체|Replace 함수|

### <a name="substring-function"></a>SUBSTRING 함수

ASE에서 함수는 `SUBSTRING(expression, start, length)` `NULL` 식의 문자 수보다 큰 시작 값이 지정 된 경우를 반환 하 고, 길이가 0 이면를 반환 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL에서 해당 하는 식은 빈 문자열을 반환 합니다.

- ASE 동작을 사용 하려면 **바꾸기 함수**를 선택 합니다. 함수에 대 한 모든 호출은 `SUBSTRING` `SUBSTRING_VARCHAR` `SUBSTRING_NVARCHAR` `SUBSTRING_VARBINARY` `s2ss` SAP ASE 동작을 에뮬레이트하는 전달 된 매개 변수 형식 (스키마 이름으로 사용자 데이터베이스에서 만들어짐)을 기반으로 하는 또는 사용자 정의 함수에 대 한 호출로 대체 됩니다.
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL 동작을 사용 하려면 **현재 구문 유지**를 선택 합니다.

**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.

|Mode|값|
|-|-|
|기본값|현재 구문 유지|
|Optimistic|현재 구문 유지|
|전체|Replace 함수|

## <a name="tables-section"></a>테이블 섹션

### <a name="add-primary-key"></a>기본 키 추가

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SAP ASE 테이블에 기본 키 또는 고유 인덱스가 없는 경우 또는 AZURE SQL 테이블에 새 기본 키를 만듭니다.

|Mode|값|
|-|-|
|기본값|예|
|Optimistic|예|
|전체|예|

> [!NOTE]
> Azure SQL에 연결 된 경우 기본적으로 **예** 입니다.

## <a name="see-also"></a>참고 항목

[사용자 인터페이스 참조(SybaseToSQL)](../../ssma/sybase/user-interface-reference-sybasetosql.md)
