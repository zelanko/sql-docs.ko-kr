---
title: 프로젝트 설정 (변환) (OracleToSQL) | Microsoft Docs
description: 프로젝트 설정 대화 상자의 변환 페이지를 사용 하 여 SSMA가 Oracle 구문을 SQL Server 구문으로 변환 하는 방법을 사용자 지정 하는 방법을 알아봅니다.
author: nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 12/17/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a98a5e07-eb5e-47b9-a6f2-e2cb3a18309c
ms.author: alexiva
ms.openlocfilehash: 5c99ab8dec72a621ddb3f312e581907b0e4ba6d4
ms.sourcegitcommit: a16b98d3bf3eeb58f5d2aeece2464f8a96e2b4a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2020
ms.locfileid: "97665874"
---
# <a name="project-settings-conversion-oracletosql"></a>프로젝트 설정(변환)(OracleToSQL)

**프로젝트 설정** 대화 상자의 **변환** 페이지에는 ssma가 Oracle 구문을 구문으로 변환 하는 방법을 사용자 지정 하는 설정이 포함 되어 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

**변환** 창은 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자에서 사용할 수 있습니다.

- 모든 SSMA 프로젝트에 대 한 설정을 지정 하려면 **도구** 메뉴에서 **기본 프로젝트 설정** 을 클릭 하 고 마이그레이션 **대상 버전** 드롭다운에서 표시 또는 변경 해야 하는 설정에 대 한 마이그레이션 프로젝트 형식을 선택한 다음 왼쪽 창의 맨 아래에서 **일반** 을 클릭 하 고 **변환** 을 클릭 합니다.

- 현재 프로젝트에 대 한 설정을 지정 하려면 **도구** 메뉴에서 **프로젝트 설정** 을 클릭 하 고 왼쪽 창의 맨 아래에 있는 **일반** 을 클릭 한 다음 **변환** 을 클릭 합니다.

## <a name="built-in-functions-and-supplied-packages"></a>기본 제공 함수 및 제공 된 패키지

|용어|정의|
|-|-|
|**COUNT 함수를 COUNT_BIG 변환**|`COUNT`함수가 2147483647 보다 큰 값 (2<sup>31</sup>-1)을 반환할 가능성이 있는 경우 함수를로 변환 해야 합니다 `COUNT_BIG` .<br /><br />**예** 를 선택 하면 ssma가 모든 사용 `COUNT` 을로 변환 `COUNT_BIG` 합니다.<br /><br />**아니요** 를 선택 하면 함수는로 유지 됩니다 `COUNT` . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 함수에서 2<sup>31</sup>-1 보다 큰 값을 반환 하면에서 오류를 반환 합니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/전체 모드:** 예로<br />**낙관적 모드:** 아니요|
|**SUBSTR 함수 호출을 하위 문자열 함수 호출로 변환**|SSMA는 `SUBSTR` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `substring` 매개 변수의 수에 따라 Oracle 함수 호출을 함수 호출로 변환할 수 있습니다. SSMA `SUBSTR` 가 함수 호출을 변환할 수 없거나 매개 변수 수가 지원 되지 않는 경우 SSMA는 `SUBSTR` 함수 호출을 사용자 지정 ssma 함수 호출로 변환 합니다.<br /><br />**예** 를 선택 하는 경우 ssma는 `SUBSTR` 세 개의 매개 변수를 사용 하는 함수 호출을로 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `substring` 합니다. 다른 `SUBSTR` 함수는 사용자 지정 SSMA 함수를 호출 하도록 변환 됩니다.<br /><br />**아니요** 를 선택 하면 ssma는 `SUBSTR` 함수 호출을 사용자 지정 ssma 함수 호출로 변환 합니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적 모드:** 예로<br />**전체 모드:** 아니요|
|**TO_CHAR (date, format) 함수 호출 변환**|SSMA는 Oracle을 `TO_CHAR(date, format)` 스키마의 프로시저로 변환할 수 있습니다 `ssma_oracle` .<br /><br />**TO_CHAR_DATE 함수 사용** 을 선택 하는 경우 ssma는 `TO_CHAR(date, format)` `TO_CHAR_DATE` 변환에 영어를 사용 하 여 into 함수를 변환 합니다.<br /><br />**TO_CHAR_DATE_LS 함수 (NLS) 사용** 을 선택 하는 경우 ssma는 `TO_CHAR(date, format)` `TO_CHAR_DATE_LS` 변환에 대 한 세션 언어를 사용 하 여 into 함수를 변환 합니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적 모드:** TO_CHAR_DATE 함수 사용<br />**전체 모드:** TO_CHAR_DATE_LS 함수 사용 (NLS 주의)|
|**DBMS_SQL에 대 한 오류를 생성 합니다. 구문 분석**|**오류** 를 선택 하면 변환 시 ssma에서 오류를 생성 `DBMS_SQL.PARSE` 합니다.<br /><br />**경고** 를 선택 하면 변환 시 ssma에서 경고를 생성 `DBMS_SQL.PARSE` 합니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br />**기본/최적/전체 모드:** 메시지가|
|**CONCAT 함수 호출에서 ISNULL 사용**|`ISNULL` 문은 `CONCAT` Oracle 동작을 에뮬레이트하는 함수 호출에 사용 됩니다. 이 설정에 대해 제공 되는 옵션은 다음과 같습니다.<br /><br />YES<br /><br />아니요<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적 모드:** 아니요<br />**전체 모드:** 예로|
|**REPLACE 함수 호출에서 ISNULL 사용**|`ISNULL` 문은 `REPLACE` Oracle 동작을 에뮬레이트하는 함수 호출에 사용 됩니다. 이 설정에 대해 제공 되는 옵션은 다음과 같습니다.<br /><br />YES<br /><br />아니요<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적 모드:** 아니요<br />**전체 모드:** 예로|
|**가능 하면 네이티브 convert 함수 사용**|**예** 를 선택 하는 경우 ssma는 `TO_CHAR(date, format)` 가능 하면를 네이티브 convert 함수로 변환 합니다.<br /><br />**아니요** 를 선택 하는 경우 ssma는를 `TO_CHAR(date, format)` 또는로 변환 합니다 `TO_CHAR_DATE` `TO_CHAR_DATE_LS` .이 옵션은 **Convert TO_CHAR (날짜, 형식)** 옵션으로 정의 됩니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적 모드:** 예로<br />**전체 모드:** 아니요|

## <a name="conversion-messages"></a>변환 메시지

|용어|정의|
|-|-|
|**문제에 대 한 메시지 생성**|SSMA가 변환 중에 정보 메시지를 생성 하는지 여부를 지정 하 고 출력 창에 표시 한 다음 변환 된 코드에 추가 합니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적 모드:** 아니요<br />**전체 모드:** 아니요|

## <a name="miscellaneous-options"></a>기타 옵션

|용어|정의|
|-|-|
|**정수로 ROWNUM 식 캐스트**|SSMA는 식을 변환 하는 경우 식을 절로 변환 하 고 `ROWNUM` `TOP` 그 뒤에 식을 변환 합니다. 다음 예에서는 `ROWNUM` Oracle 문을 보여 줍니다 `DELETE` .<br /><br />`DELETE FROM Table1`<br />`WHERE ROWNUM < expression and Field1 >= 2`<br /><br />다음 예에서는 결과를 보여 줍니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] .<br /><br />`DELETE TOP (expression-1)`<br />`FROM Table1`<br />`WHERE Field1>=2`<br /><br />에서는 `TOP` `TOP` 절 식이 정수로 계산 되어야 합니다. 정수가 음수인 경우 문은 오류를 생성 합니다.<br /><br />**예** 를 선택 하면 ssma가 식을 정수로 캐스팅 합니다.<br /><br />**아니요** 를 선택 하면 ssma는 변환 된 코드에서 모든 정수가 아닌 식을 오류로 표시 합니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/전체 모드:** 아니요<br />**낙관적 모드:** 예로|  
|**기본 스키마 매핑**|이 설정은 Oracle 스키마를 SQL Server 스키마에 매핑하는 방법을 지정 합니다. 이 설정에서는 다음 두 가지 옵션을 사용할 수 있습니다.<br /><br />**데이터베이스 스키마:** 이 모드에서 Oracle 스키마 `sch1` 는 기본적으로 `dbo` SQL Server 데이터베이스의 SQL Server 스키마에 매핑됩니다 `sch1` .<br /><br />스키마 스키마 **:** 이 모드에서는 Oracle 스키마 `sch1` 가 기본적으로 `sch1` 연결 대화 상자에서 제공 하는 기본 SQL Server 데이터베이스 SQL Server 스키마에 매핑됩니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 스키마를 데이터베이스로|
|**ORDER BY 절에서 Oracle null 동작 에뮬레이트**|`NULL` 값은 및 Oracle에서 다르게 정렬 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br />에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `NULL` 값은 순서가 지정 된 목록의 가장 작은 값입니다. 오름차순 목록에는 `NULL` 먼저 값이 표시 됩니다.<br /><br />Oracle에서 `NULL` 값은 순서가 지정 된 목록에서 가장 높은 값입니다. 기본적으로 값은 내림차순 `NULL` 목록에서 마지막에 표시 됩니다.<br /><br />Oracle에 `NULLS FIRST` 는 및 절이 있으므로 `NULLS LAST` oracle의 순서를 변경할 수 있습니다 `NULL` .<br /><br />SSMA는 `ORDER BY` 값을 확인 하 여 Oracle 동작을 에뮬레이트할 수 있습니다 `NULL` . 그런 다음 먼저 지정 된 순서로 값을 기준으로 정렬 한 `NULL` 다음 다른 값을 기준으로 정렬 합니다.<br /><br />**예** 를 선택 하면 ssma는 oracle 동작을 에뮬레이트하는 방식으로 oracle 문을 변환 합니다 `ORDER BY` .<br /><br />**아니요** 를 선택 하면 Ssma는 Oracle 규칙을 무시 하 고 및 절이 나타날 때 오류 메시지를 생성 합니다 `NULLS FIRST` `NULLS LAST` .<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적 모드:** 아니요<br />**전체 모드:** 예로|
|**SELECT의 행 개수 예외 에뮬레이션**|`SELECT`INTO 절이 있는 문이 행을 반환 하지 않는 경우 Oracle에서 `NO_DATA_FOUND` 예외가 발생 합니다. 문에서 둘 이상의 행을 반환 하는 경우 `TOO_MANY_ROWS` 예외가 발생 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]행 개수가 1과 다른 경우의 변환 된 문은 예외를 발생 시 키 지 않습니다.<br /><br />**예** 를 선택 하면 ssma는 각 문 뒤에 특수 프로시저에 대 한 호출을 추가 `db_error_exact_one_row_check` `SELECT` 합니다. 이 프로시저는 `NO_DATA_FOUND` 및 예외를 에뮬레이트합니다 `TOO_MANY_ROWS` . 이는 기본값 이며 Oracle 동작을 최대한 가깝게 재현할 수 있습니다. 소스 코드에 이러한 오류를 처리 하는 예외 처리기가 있는 경우 항상 **예** 를 선택 해야 합니다. `SELECT`문이 사용자 정의 함수 내에서 발생 하는 경우 저장 프로시저 실행 및 예외 발생이 함수 컨텍스트와 호환 되지 않기 때문에이 모듈은 저장 프로시저로 변환 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br />**아니요** 를 선택 하면 예외가 생성 되지 않습니다. 이는 SSMA에서 사용자 정의 함수를 변환 하 고 해당 함수를에서 함수를 유지 하려는 경우에 유용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 예로|
|**수정 관리자 사용**|이 기능을 사용 하도록 설정 하면 SSMA는 대상 T-sql 코드에서 수정한 내용 으로부터 학습을 시도 하 고, 비슷한 패턴을 적용할 수 있는 다른 위치에서 잠재적 코드 수정을 제안 합니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 예로|
|**상수 식 열 별칭 생성**|목록의 식에 `SELECT` 별칭이 누락 된 경우 SSMA는, 등의 상수 별칭을 생성 `expr1` `expr2` 하거나 식 자체를 별칭으로 사용할 수 있습니다. 식의 길이는 상당히 길고 열 이름 길이는 제한 되므로 이러한 별칭에는 상수 기본 이름을 사용 하는 것이 더 안전 합니다. 안전한 옵션 이지만 결과 데이터 집합에 대 한 외부 종속성이 있을 수 있기 때문에 경우에 따라 가능 하지 않습니다. 이러한 경우 Oracle의 동작과 유사 하 게 해당 값 식에 따라 열 이름을 지정할 수 있습니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적 모드:** 예로<br />**전체 모드:** 아니요|
|**확장 속성 생략**|사용 하도록 설정 하면 SSMA는 대상 데이터베이스에서 만든 개체에 확장 속성을 추가 하지 않습니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 아니요|
|**오류 코드 변환**|사용 하도록 설정 하면 매핑이 발견 될 경우 대상 SQL Server 쪽의 오류 번호가 Oracle 오류 코드로 변환 됩니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/전체 모드:** 예로<br />**낙관적 모드:** 아니요|
|**형식 참조에 대 한 전체 형식 지정 사용**|사용 하도록 설정 하면 SSMA는 루틴 매개 변수 및 반환 값에 대 한 전체 형식 사양 (배율 및 전체 자릿수 포함)을 고려 합니다. Oracle에서는 루틴 매개 변수에 대 한 데이터 형식 인수를 허용 하지 않지만 및 특성을 사용 하는 경우와 같이 암시적으로 파생 될 수 있는 경우가 있습니다 `%TYPE` `%ROWTYPE` . 이러한 경우 SSMA는 SQL Server로 변환할 때 전체 형식 사양 (전체 자릿수 및 소수 자릿수 포함)을 사용할 수 있습니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적 모드:** 예로<br />**전체 모드:** 아니요|
|**문자열 연결에 ISNULL 사용**|문자열 연결이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 값을 포함 하는 경우 Oracle 및는 서로 다른 결과를 반환 `NULL` 합니다. Oracle은 `NULL` 빈 문자 집합과 같은 값을 처리 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 `NULL`을 반환합니다.<br /><br />**예** 를 선택 하는 경우 Ssma는 Oracle 연결 문자 (&#124;&#124;)를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 문자 (+)로 바꿉니다. 또한 SSMA는 값에 대 한 연결의 양쪽에 있는 식을 확인 `NULL` 합니다.<br /><br />**아니요** 를 선택 하면 ssma는 연결 문자를 대체 하지만 값은 확인 하지 않습니다 `NULL` .<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 예로|

## <a name="objects-conversion"></a>개체 변환

|용어|정의|
|-|-|
|**NULL이 아닌 열에 대해 SET NULL 참조 동작으로 외래 키 변환**|Oracle에서는 `SET NULL` 참조 된 열에 null이 허용 되지 않으므로 동작을 수행할 수 없는 foreign key 제약 조건을 만들 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 이러한 외래 키 구성을 허용 하지 않습니다.<br /><br />**예** 를 선택 하는 경우 Ssma는 Oracle에서와 같이 참조 동작을 생성 하지만에 제약 조건을 로드 하기 전에 수동 변경을 수행 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 예를 들어 대신를 선택할 수 있습니다 `NO ACTION` `SET NULL` .<br /><br />**아니요** 를 선택 하면 제약 조건이 오류로 표시 됩니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 아니요|
|**하위 형식 변환**|SSMA는 다음과 같은 두 가지 방법으로 PL/SQL 하위 유형을 변환할 수 있습니다.<br /><br />**예** 를 선택 하면 ssma가 하위 형식 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 사용자 정의 형식을 만들고이 하위 형식의 각 변수에 사용 합니다.<br /><br />**아니요** 를 선택 하면 ssma는 하위 형식의 모든 원본 선언을 기본 형식으로 대체 하 고 일반적인 방식으로 결과를 변환 합니다. 이 경우에는 추가 형식이 생성 되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 아니요|
|**동의어 변환**|다음 Oracle 개체에 대 한 동의어를로 마이그레이션할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br />테이블 및 개체 테이블<br /><br />뷰 및 개체 뷰<br /><br />저장 프로시저 및 함수<br /><br />구체화된 보기<br /><br />**다음에 대 한 동의어** Oracle 개체는 개체에 대 한 직접 참조로 대체 될 수 있습니다.<br /><br />시퀀스<br /><br />패키지<br /><br />Java 클래스 스키마 개체<br /><br />사용자 정의 개체 유형<br /><br />다른 동의어는 마이그레이션할 수 없습니다. SSMA는 동의어와 동의어를 사용 하는 모든 참조에 대해 오류 메시지를 생성 합니다.<br /><br />**예** 를 선택 하는 경우 ssma는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 동의어를 만들고 이전 목록에 따라 개체 참조를 직접 만듭니다.<br /><br />**아니요** 를 선택 하면 ssma에서 여기에 나열 된 모든 동의어에 대 한 직접 개체 참조를 만듭니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 예로|
|**로컬 모듈 변환**|독립 실행형 저장 프로시저 또는 함수에서 선언 된 Oracle 중첩 subprogram의 유형을 정의 합니다.<br /><br />**인라인으로** 를 선택 하는 경우 중첩 된 subprogram 호출은 본문으로 대체 됩니다.<br /><br />**저장 프로시저** 를 선택 하면 중첩 된 subprogram가 SQL Server 저장 프로시저로 변환 되 고이 프로시저 호출에서 해당 호출이 대체 됩니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 인라인|

## <a name="records-conversion"></a>레코드 변환

|용어|정의|
|-|-|
|**레코드를 구분 변수 목록으로 변환**|SSMA는 Oracle 레코드를 특정 구조를 사용 하는 XML 변수 및 구분 변수로 변환할 수 있습니다.<br /><br />**예** 를 선택 하는 경우 ssma는 가능한 경우 레코드를 구분 변수 목록으로 변환 합니다.<br /><br />**아니요** 를 선택 하면 ssma는 레코드를 특정 구조체로 XML 변수로 변환 합니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 예로|
|**SELECT ...를 사용 합니다. SELECT ...를 변환할 때 FOR XML 레코드 변수에 대 한 INTO**|레코드 변수를 선택할 때 XML 결과 집합을 생성할지 여부를 지정 합니다.<br /><br />**예** 를 선택 하는 경우 SELECT 문은 XML을 반환 합니다.<br /><br />**아니요** 를 선택 하는 경우 select 문은 결과 집합을 반환 합니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 아니요|

## <a name="returning-clause-conversion"></a>절 변환 반환

|용어|정의|
|-|-|
|**DELETE 문의 반환 절을 출력으로 변환**|Oracle은 `RETURNING` 삭제 된 값을 즉시 가져오는 방법으로 절을 제공 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 절을 사용 하 여 해당 기능을 제공 `OUTPUT` 합니다.<br /><br />**예** 를 선택 하면 ssma는 `RETURNING` `DELETE` 문의 절을 절로 변환 `OUTPUT` 합니다. 테이블의 트리거가 값을 변경할 수 있기 때문에 반환 된 값은 Oracle의 경우와 다를 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br />**아니요** 를 선택 하면 ssma에서 `SELECT` 반환 된 값을 검색 하기 전에 문을 생성 `DELETE` 합니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 예로|
|**INSERT 문의 반환 절을 출력으로 변환**|Oracle은 `RETURNING` 삽입 된 값을 즉시 가져오는 방법으로 절을 제공 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 절을 사용 하 여 해당 기능을 제공 `OUTPUT` 합니다.<br /><br />**예** 를 선택 하면 ssma가 `RETURNING` 문의 절을로 변환 `INSERT` `OUTPUT` 합니다. 테이블의 트리거가 값을 변경할 수 있기 때문에 반환 된 값은 Oracle의 경우와 다를 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br />**아니요** 를 선택 하면 ssma가 참조 테이블에서 값을 삽입 한 다음 선택 하 여 Oracle 기능을 에뮬레이트합니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 예로|
|**UPDATE 문의 반환 절을 출력으로 변환**|Oracle은 `RETURNING` 업데이트 된 값을 즉시 가져오는 방법으로 절을 제공 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 절을 사용 하 여 해당 기능을 제공 `OUTPUT` 합니다.<br /><br />**예** 를 선택 하면 ssma는 `RETURNING` `UPDATE` 문의 절을 절로 변환 `OUTPUT` 합니다. 테이블의 트리거가 값을 변경할 수 있기 때문에 반환 된 값은 Oracle의 경우와 다를 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br />**아니요** 를 선택 하면 ssma는 문 뒤에 select 문을 생성 `UPDATE` 하 여 반환 값을 검색 합니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 예로|

## <a name="rowid-generation"></a>ROWID 생성

|용어|정의|
|-|-|
|**ROWID 열 생성**|SSMA가에 테이블 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 만들 때 ROWID 열을 만들 수 있습니다. 데이터가 마이그레이션되면 각 행은 `UNIQUEIDENTIFIER` 함수에 의해 생성 된 새 값을 가져옵니다 `newid()` .<br /><br />**예** 를 선택 하면 `ROWID` 열이 모든 테이블에 생성 되 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 값을 삽입할 때 guid를 생성 합니다. SSMA 테스터를 사용할 계획인 경우 항상 **예** 를 선택 합니다.<br /><br />**아니요** 를 선택 하면 ROWID 열이 테이블에 추가 되지 않습니다.<br /><br />트리거가 있는 테이블에 **대해 ROWID 열 추가** `ROWID` 는 트리거가 포함 된 테이블에 대해 추가 합니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적 모드:** 트리거가 있는 테이블에 대해 ROWID 열 추가<br /><br />**전체 모드:** 예로|
|**ROWID 열에 고유 인덱스 생성**|SSMA가 생성 된 열에 고유 인덱스 열을 생성할지 여부를 지정 `ROWID` 합니다. 옵션을 "예"로 설정 하면 고유 인덱스가 생성 되 고 "아니요"로 설정 된 경우 열에 고유 인덱스가 생성 되지 않습니다 `ROWID` .<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 예로|

## <a name="sequence-and-identity-conversion"></a>시퀀스 및 Id 변환

|용어|정의|
|-|-|
|**Id를로 변환**|Oracle은 id 열에 대 한 여러 구성 옵션을 제공 합니다. 이러한 옵션 중 일부는 SQL Server의 id 기능에서 지원 되지 않습니다.<br /><br />이러한 옵션을 유지 하는 방법은 id를 시퀀스로 변환 하는 것입니다.<br /><br />**시퀀스** 를 선택 하면 Oracle id 열이 더 이상 SQL id 열로 변환 되지 않습니다. 대신 시퀀스를 만들고 사용 하 여 열에 대 한 기본값을 생성 합니다.<br /><br />**Id** 를 선택 하면 Oracle identity 열이 SQL identity 열로 변환 됩니다. 지원 되지 않는 옵션은 변환 되지 않습니다. <br /><br />**최적 맞춤** 을 선택 하는 경우 Ssma는 Oracle id 열의 구성에 따라 가장 적합 한 변환 방법 (Id 또는 시퀀스)을 결정 합니다.|
|**시퀀스 생성기 변환**|Oracle에서는 시퀀스를 사용 하 여 고유 식별자를 생성할 수 있습니다.<br /><br />SSMA는 시퀀스를 다음으로 변환할 수 있습니다.<br /><br />SQL Server 시퀀스 생성기를 사용 합니다.<br /><br />SSMA 시퀀스 생성기 사용.<br /><br />열 id 사용.<br /><br />기본 옵션은 SQL Server 시퀀스 생성기를 사용 하는 것입니다. 그러나 SQL Server는 현재 시퀀스 값 (예: Oracle 시퀀스 메서드) 가져오기를 지원 하지 않습니다 `CURRVAL` . Oracle 시퀀스 방법 마이그레이션에 대 한 지침은 SSMA 팀 블로그 사이트를 참조 하세요 `CURRVAL` .<br /><br />또한 SSMA는 Oracle 시퀀스를 SSMA 시퀀스 에뮬레이터로 변환 하는 옵션을 제공 합니다. 2012 이전의 SQL Server로 변환할 경우의 기본 옵션입니다.<br /><br />마지막으로 테이블의 열에 할당 된 시퀀스를 변환 하 여 id 값을 SQL Server 수도 있습니다. Oracle **테이블** 탭의 시퀀스와 id 열 간의 매핑을 지정 해야 합니다.|
|**트리거 외부에서 통화를 변환 합니다.**|**변환 시퀀스 생성기** 가 **열 id를 사용** 하도록 설정 된 경우에만 표시 됩니다. Oracle 시퀀스는 테이블과 별도의 개체 이므로 시퀀스를 사용 하는 많은 테이블은 트리거를 사용 하 여 새 시퀀스 값을 생성 하 고 삽입 합니다. SSMA는 이러한 문을 주석 처리 하거나 주석 처리 시 오류가 생성 될 때 오류로 표시 합니다.<br /><br />**예** 를 선택 하면 ssma는 변환 된 시퀀스의 외부 트리거에 대 한 모든 참조를 `CURRVAL` 경고와 함께 표시 합니다.<br /><br />**아니요** 를 선택 하면 ssma는 변환 된 시퀀스에서 외부 트리거에 대 한 모든 참조를 `CURRVAL` 오류로 표시 합니다.|

## <a name="statements-conversion"></a>문 변환

|용어|정의|
|-|-|
|**MERGE 문 변환**|**INSERT, UPDATE, DELETE 문 사용** 을 선택 하는 경우 ssma는 `MERGE` 문을 `INSERT` ,, 문으로 변환 `UPDATE` `DELETE` 합니다.<br /><br />**MERGE 문 사용** 을 선택 하는 경우 ssma는의 문을 문으로 변환 `MERGE` `MERGE` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** MERGE 문 사용|
|**기본 인수를 사용 하는 subprograms 호출을 변환 합니다.**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 함수는 함수 호출에서 매개 변수의 생략을 지원 하지 않습니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 함수 및 프로시저는 기본 매개 변수 값으로 식을 지원 하지 않습니다.<br /><br />**예** 를 선택 하 고 함수 호출에서 매개 변수를 생략 하는 경우 ssma는 함수에 **default** 키워드를 삽입 하 고 올바른 위치에서를 호출 합니다. 그런 다음 경고를 표시 하는 호출을 표시 합니다.<br /><br />**아니요** 를 선택 하면 ssma는 함수 호출을 오류로 표시 합니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 예로|
|**FORALL 문을 WHILE 문으로 변환**|SSMA가 `FORALL` PL/SQL collection 요소에 대해 루프를 처리 하는 방법을 정의 합니다.<br /><br />**예** 를 선택 하는 경우 ssma는 `WHILE` 컬렉션 요소가 하나씩 검색 되는 루프를 만듭니다.<br /><br />**아니요** 를 선택 하면 ssma는 메서드를 사용 하 여 컬렉션에서 행 집합을 생성 하 `nodes()` 고 단일 테이블로 사용 합니다. 이는 보다 효율적 이지만 출력 코드를 읽을 수 없게 만듭니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적 모드:** 아니요<br />**전체 모드:** 예로|
|**함수 호출을 프로시저 호출로 변환**|일부 Oracle 함수는 자치 트랜잭션으로 정의 되거나에서 유효 하지 않은 문을 포함 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 이러한 경우 SSMA는 프로시저에 대 한 래퍼로 프로시저 및 함수를 만듭니다. 변환 된 함수는 구현 하는 프로시저를 호출 합니다.<br /><br />SSMA는 래퍼 함수에 대 한 호출을 프로시저에 대 한 호출로 변환할 수 있습니다. 이렇게 하면 더 쉽게 읽을 수 있는 코드가 만들어지고 성능을 향상 시킬 수 있습니다. 그러나 컨텍스트가 항상 허용 하는 것은 아닙니다. 예를 들어 목록에서 함수 호출을 `SELECT` 프로시저 호출로 바꿀 수 없습니다. SSMA에는 일반적인 경우를 다루는 몇 가지 옵션이 있습니다.<br /><br />**Always** 를 선택 하면 ssma가 래퍼 함수 호출을 프로시저 호출로 변환 하려고 시도 합니다. 현재 컨텍스트에서이 변환을 허용 하지 않으면 오류 메시지가 생성 됩니다. 이러한 방식으로 함수 호출은 생성 된 코드에 남아 있지 않습니다.<br /><br />**가능 하면** 선택 하는 경우 ssma는 함수에 출력 매개 변수가 있는 경우에만 프로시저 호출로 이동 합니다. 이동할 수 없는 경우 매개 변수의 출력 특성이 제거 됩니다. 다른 모든 경우에는 모든 경우에 함수 호출을 남깁니다.<br /><br />**안 함** 을 선택 하면 ssma는 모든 함수 호출을 함수 호출로 유지 합니다. 성능상의 이유로 이러한 선택을 허용할 수 없는 경우도 있습니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 가능 하면|
|**잠금 테이블 문 변환**|SSMA는 많은 `LOCK TABLE` 문을 테이블 힌트로 변환할 수 있습니다. Ssma는,, `LOCK TABLE` 및 절을 포함 하는 문을 변환할 수 없으며 `PARTITION` `SUBPARTITION` `@dblink` `NOWAIT` 변환 오류 메시지로 이러한 문을 표시 합니다.<br /><br />**예** 를 선택 하면 ssma에서 지원 되는 `LOCK TABLE` 문을 테이블 힌트로 변환 합니다.<br /><br />**아니요** 를 선택 하면 ssma는 `LOCK TABLE` 변환 오류 메시지를 포함 하는 모든 문을 표시 합니다.<br /><br />다음 표에서는 SSMA가 Oracle 잠금 모드를 변환 하는 방법을 보여 줍니다.<br /><br />**Oracle 잠금 모드**<br /><br />`ROW SHARE`<br />`ROW EXCLUSIVE`<br />`SHARE UPDATE = ROW SHARE`<br />`SHARE`<br />`SHARE`<br />`EXCLUSIVE`<br /><br />**SQL Server 테이블 힌트**<br /><br />`ROWLOCK, HOLDLOCK`<br />`ROWLOCK, XLOCK, HOLDLOCK`<br />`ROWLOCK, HOLDLOCK`<br />`TABLOCK, HOLDLOCK`<br />`TABLOCK, XLOCK, HOLDLOCK`<br />`TABLOCKX, HOLDLOCK`<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 예로|
|**REF CURSOR OUT 매개 변수에 대 한 OPEN FOR 문 변환**|Oracle에서는 `OPEN .. FOR` 문을 사용 하 여 결과 집합을 형식의 subprogram 매개 변수로 반환할 수 있습니다 `OUT` `REF CURSOR` . 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저는 문의 결과를 직접 반환 `SELECT` 합니다.<br /><br />SSMA는 여러 문을 문으로 변환할 수 있습니다 `OPEN .. FOR` `SELECT` .<br /><br />**예** 를 선택 하면 ssma가 문을 문으로 변환 하 여 `OPEN .. FOR` `SELECT` 결과 집합을 클라이언트로 반환 합니다.<br /><br />**아니요** 를 선택 하면 ssma는 변환 된 코드와 출력 창에 오류 메시지를 생성 합니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 예로|
|**트랜잭션 처리 문 변환**|SSMA는 Oracle 트랜잭션 처리 문을 변환할 수 있습니다.<br /><br />**예** 를 선택 하면 ssma는 Oracle 트랜잭션 처리 문을 문으로 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.<br /><br />**아니요** 를 선택 하면 ssma는 트랜잭션 처리 문을 변환 오류로 표시 합니다.<br /><br />**참고:** Oracle은 트랜잭션을 암시적으로 엽니다. 에서이 동작을 에뮬레이트 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `BEGIN TRANSACTION` 트랜잭션을 시작 하려는 위치에 문을 수동으로 추가 해야 합니다. 또는 `SET IMPLICIT_TRANSACTIONS ON` 세션의 시작 부분에서 명령을 실행할 수 있습니다. SSMA `SET IMPLICIT_TRANSACTIONS ON` 는 자치 트랜잭션으로 서브루틴을 변환할 때 자동으로 추가 됩니다.<br /><br />**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.<br /><br />**기본/최적/전체 모드:** 예로|

## <a name="see-also"></a>참고 항목

[사용자 인터페이스 참조(OracleToSQL)](../../ssma/oracle/user-interface-reference-oracletosql.md)
