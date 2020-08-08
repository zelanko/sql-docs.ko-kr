---
title: 프로젝트 설정 (변환) (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 538c93cf-c5bb-43d5-b758-186d9fb00c19
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 998d8cc8e39599fd24994e241c1da02fa87b863e
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87933714"
---
# <a name="project-settings-conversion-db2tosql"></a>프로젝트 설정 (변환) (DB2ToSQL)
**프로젝트 설정** 대화 상자의 변환 페이지에는 SSMA에서 DB2 구문을 구문으로 변환 하는 방법을 사용자 지정 하는 설정이 포함 되어 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
변환 창은 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자에서 사용할 수 있습니다.  
  
-   모든 SSMA 프로젝트에 대 한 설정을 지정 하려면 **도구** 메뉴에서 **기본 프로젝트 설정**을 클릭 하 고 마이그레이션 **대상 버전** 드롭다운에서 표시 또는 변경 해야 하는 설정에 대 한 마이그레이션 프로젝트 형식을 선택한 다음 왼쪽 창의 맨 아래에서 **일반** 을 클릭 하 고 **변환**을 클릭 합니다.  
  
-   현재 프로젝트에 대 한 설정을 지정 하려면 **도구** 메뉴에서 **프로젝트 설정**을 클릭 하 고 왼쪽 창의 맨 아래에 있는 **일반** 을 클릭 한 다음 **변환**을 클릭 합니다.  
  
## <a name="conversion-messages"></a>변환 메시지  
  
### <a name="generate-messages-about-issues-applied"></a>적용 된 문제에 대 한 메시지 생성  
SSMA가 변환 중에 정보 메시지를 생성 하는지 여부를 지정 하 고 출력 창에 표시 한 다음 변환 된 코드에 추가 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 아니요  
  
**전체 모드:** 아니요  
  
## <a name="miscellaneous-options"></a>기타 옵션  
  
### <a name="cast-rownum-expressions-as-integers"></a>정수로 ROWNUM 식 캐스트  
SSMA는 ROWNUM 식을 변환 하는 경우 식을 TOP 절로 변환 하 고 그 뒤에 식을 변환 합니다. 다음 예에서는 DB2 DELETE 문의 ROWNUM을 보여 줍니다.  
  
`DELETE FROM Table1`  
  
`WHERE ROWNUM < expression and Field1 >= 2`  
  
다음 예에서는 결과를 보여 줍니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
`DELETE TOP (expression-1)`  
  
`FROM Table1`  
  
`WHERE Field1>=2`  
  
TOP을 사용 하려면 TOP 절 식이 정수로 계산 되어야 합니다. 정수가 음수인 경우 문은 오류를 생성 합니다.  
  
-   **예**를 선택 하면 ssma가 식을 정수로 캐스팅 합니다.  
  
-   **아니요**를 선택 하면 ssma는 변환 된 코드에서 모든 정수가 아닌 식을 오류로 표시 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/전체 모드:** 아니요  
  
**낙관적 모드:** 예로  
  
### <a name="default-schema-mapping"></a>기본 스키마 매핑  
이 설정은 DB2 스키마를 SQL Server 스키마에 매핑하는 방법을 지정 합니다. 이 설정에서는 다음 두 가지 옵션을 사용할 수 있습니다.  
  
1.  **데이터베이스 스키마:** 이 모드에서 DB2 스키마 ' sch1 '는 기본적으로 SQL Server 데이터베이스 ' sch1 '에 있는 ' dbo ' SQL Server 스키마에 매핑됩니다.  
  
2.  스키마 스키마 **:** 이 모드에서 DB2 스키마 ' sch1 '은 기본적으로 연결 대화 상자에서 제공 하는 기본 SQL Server 데이터베이스의 ' sch1 ' SQL Server 스키마에 매핑됩니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 스키마를 데이터베이스로  
  
### <a name="conversion-ways-of-merge-statement"></a>MERGE 문의 변환 방법  
  
-   **Insert, update, delete 문 사용**을 선택 하는 경우 SSMA는 병합기 문을 INSERT, UPDATE, delete 문으로 변환 합니다.  
  
-   **Merge 문 사용**을 선택 하는 경우 ssma는 병합기 문을의 MERGE 문으로 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
> [!WARNING]  
> 이 프로젝트 설정 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012, 2014 에서만 사용할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** MERGE 문 사용  
  
### <a name="convert-calls-to-subprograms-that-use-default-arguments"></a>기본 인수를 사용 하는 subprograms 호출을 변환 합니다.  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]함수는 함수 호출에서 매개 변수의 생략을 지원 하지 않습니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 함수 및 프로시저는 기본 매개 변수 값으로 식을 지원 하지 않습니다.  
  
-   **예** 를 선택 하 고 함수 호출에서 매개 변수를 생략 하는 경우 ssma는 함수에 **default** 키워드를 삽입 하 고 올바른 위치에서를 호출 합니다. 그런 다음 경고를 표시 하는 호출을 표시 합니다.  
  
-   **아니요**를 선택 하면 ssma는 함수 호출을 오류로 표시 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 예로  
  
### <a name="convert-count-function-to-count_big"></a>COUNT 함수를 COUNT_BIG 변환  
개수 함수가 2147483647 보다 큰 값 (2<sup>31</sup>-1)을 반환 하는 경우 함수를 COUNT_BIG으로 변환 해야 합니다.  
  
-   **예**를 선택 하는 경우 SSMA는 COUNT의 모든 사용을 COUNT_BIG로 변환 합니다.  
  
-   **아니요**를 선택 하면 함수는 카운트로 유지 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]함수에서 2<sup>31</sup>-1 보다 큰 값을 반환 하면에서 오류를 반환 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/전체 모드:** 예로  
  
**낙관적 모드:** 아니요  
  
### <a name="convert-forall-statement-to-while-statement"></a>FORALL 문을 WHILE 문으로 변환  
SSMA가 PL/SQL collection 요소에서 FORALL 루프를 처리 하는 방법을 정의 합니다.  
  
-   **예**를 선택 하는 경우 ssma는 컬렉션 요소가 하나씩 검색 되는 while 루프를 만듭니다.  
  
-   **아니요**를 선택 하면 ssma가 nodes () 메서드를 사용 하 여 컬렉션에서 행 집합을 생성 하 고 단일 테이블로 사용 합니다. 이는 보다 효율적 이지만 출력 코드를 읽을 수 없게 만듭니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 아니요  
  
**전체 모드:** 예로  
  
### <a name="convert-foreign-keys-with-set-null-referential-action-on-column-that-is-not-null"></a>NULL이 아닌 열에 대해 SET NULL 참조 동작으로 외래 키 변환  
D b 2에서는 foreign key 제약 조건을 만들 수 있습니다 .이 경우 NULL은 참조 된 열에서 허용 되지 않으므로 SET NULL 작업을 수행할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이러한 외래 키 구성을 허용 하지 않습니다.  
  
-   **예**를 선택 하면 SSMA에서 DB2와 같이 참조 동작을 생성 하지만에 제약 조건을 로드 하기 전에 수동으로 변경 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 예를 들어 NULL 설정 대신 작업 안 함을 선택할 수 있습니다.  
  
-   **아니요**를 선택 하면 제약 조건이 오류로 표시 됩니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 아니요  
  
### <a name="convert-function-calls-to-procedure-calls"></a>함수 호출을 프로시저 호출로 변환  
일부 DB2 함수는 자치 트랜잭션으로 정의 되거나에서 유효 하지 않은 문을 포함 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 이러한 경우 SSMA는 프로시저에 대 한 래퍼로 프로시저 및 함수를 만듭니다. 변환 된 함수는 구현 하는 프로시저를 호출 합니다.  
  
SSMA는 래퍼 함수에 대 한 호출을 프로시저에 대 한 호출로 변환할 수 있습니다. 이렇게 하면 더 쉽게 읽을 수 있는 코드가 만들어지고 성능을 향상 시킬 수 있습니다. 그러나 컨텍스트가 항상 허용 하는 것은 아닙니다. 예를 들어 SELECT 목록에서 함수 호출을 프로시저 호출로 바꿀 수 없습니다. SSMA에는 일반적인 경우를 다루는 몇 가지 옵션이 있습니다.  
  
-   **Always**를 선택 하면 ssma가 래퍼 함수 호출을 프로시저 호출로 변환 하려고 시도 합니다. 현재 컨텍스트에서이 변환을 허용 하지 않으면 오류 메시지가 생성 됩니다. 이러한 방식으로 함수 호출은 생성 된 코드에 남아 있지 않습니다.  
  
-   **가능 하면**선택 하는 경우 ssma는 함수에 출력 매개 변수가 있는 경우에만 프로시저 호출로 이동 합니다. 이동할 수 없는 경우 매개 변수의 출력 특성이 제거 됩니다. 다른 모든 경우에는 모든 경우에 함수 호출을 남깁니다.  
  
-   **안 함**을 선택 하면 ssma는 모든 함수 호출을 함수 호출로 유지 합니다. 성능상의 이유로 이러한 선택을 허용할 수 없는 경우도 있습니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 가능 하면  
  
### <a name="convert-lock-table-statements"></a>잠금 테이블 문 변환  
SSMA는 많은 잠금 테이블 문을 테이블 힌트로 변환할 수 있습니다. SSMA는 PARTITION, SUBPARTITION, 및 NOWAIT 절을 포함 하는 모든 잠금 테이블 문을 변환할 수 없으며 @dblink 이러한 문을 변환 오류 메시지로 표시 합니다.  
  
-   **예**를 선택 하면 ssma에서 지원 되는 잠금 테이블 문을 테이블 힌트로 변환 합니다.  
  
-   **아니요**를 선택 하면 ssma가 모든 LOCK TABLE 문을 변환 오류 메시지로 표시 합니다.  
  
다음 표에서는 SSMA에서 DB2 잠금 모드를 변환 하는 방법을 보여 줍니다.  
  
|DB2 잠금 모드|SQL Server 테이블 힌트|  
|-|-|  
|행 공유|ROWLOCK, HOLDLOCK|  
|행 제외|ROWLOCK, XLOCK, HOLDLOCK|  
|공유 업데이트 = 행 공유|ROWLOCK, HOLDLOCK|  
|공유|TABLOCK, HOLDLOCK|  
|행 배타 공유|TABLOCK, XLOCK, HOLDLOCK|  
|함께|TABLOCKX, HOLDLOCK|  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 예로  
  
### <a name="convert-open-for-statements-for-ref-cursor-out-parameters"></a>REF CURSOR OUT 매개 변수에 대 한 OPEN FOR 문 변환  
D b 2에서 OPEN 문을 사용 하 여 결과 집합을 REF CURSOR 형식의 subprogram OUT 매개 변수로 반환할 수 있습니다. 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저는 SELECT 문의 결과를 직접 반환 합니다.  
  
SSMA는 여러 개의 OPEN 문을 SELECT 문으로 변환할 수 있습니다.  
  
-   **예**를 선택 하면 SSMA에서 OPEN 문을 select 문으로 변환 하 여 결과 집합을 클라이언트에 반환 합니다.  
  
-   **아니요**를 선택 하면 ssma는 변환 된 코드와 출력 창에 오류 메시지를 생성 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 예로  
  
### <a name="convert-record-as-a-list-of-separates-variables"></a>레코드를 구분 변수 목록으로 변환  
SSMA는 DB2 레코드를 특정 구조를 사용 하는 XML 변수 및 구분 변수로 변환할 수 있습니다.  
  
-   **예**를 선택 하는 경우 ssma는 가능한 경우 레코드를 구분 변수 목록으로 변환 합니다.  
  
-   **아니요**를 선택 하면 ssma는 레코드를 특정 구조체로 XML 변수로 변환 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 예로  
  
### <a name="convert-substr-function-calls-to-substring-function-calls"></a>SUBSTR 함수 호출을 하위 문자열 함수 호출로 변환  
SSMA는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 매개 변수 수에 따라 DB2 SUBSTR 함수 호출을 **substring** 함수 호출로 변환할 수 있습니다. SSMA가 SUBSTR 함수 호출을 변환할 수 없거나 매개 변수 수가 지원 되지 않는 경우 SSMA는 SUBSTR 함수 호출을 사용자 지정 SSMA 함수 호출로 변환 합니다.  
  
-   **예**를 선택 하는 경우 ssma는 세 개의 매개 변수를 사용 하는 SUBSTR 함수 호출을 하위 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **문자열로**변환 합니다. 다른 SUBSTR 함수는 사용자 지정 SSMA 함수를 호출 하도록 변환 됩니다.  
  
-   **아니요**를 선택 하면 SSMA가 SUBSTR 함수 호출을 사용자 지정 ssma 함수 호출로 변환 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 예로  
  
**전체 모드:** 아니요  
  
### <a name="convert-subtypes"></a>하위 형식 변환  
SSMA는 다음과 같은 두 가지 방법으로 PL/SQL 하위 유형을 변환할 수 있습니다.  
  
-   **예**를 선택 하면 ssma가 하위 형식 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 사용자 정의 형식을 만들고이 하위 형식의 각 변수에 사용 합니다.  
  
-   **아니요**를 선택 하면 ssma는 하위 형식의 모든 원본 선언을 기본 형식으로 대체 하 고 일반적인 방식으로 결과를 변환 합니다. 이 경우에는 추가 형식이 생성 되지 않습니다.[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 아니요  
  
### <a name="convert-synonyms"></a>동의어 변환  
다음 DB2 개체에 대 한 동의어를로 마이그레이션할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   테이블 및 개체 테이블  
  
-   뷰 및 개체 뷰  
  
-   저장 프로시저 및 함수  
  
-   구체화된 보기  
  
다음 DB2 개체에 대 한 동의어는 개체에 대 한 직접 참조로 대체 될 수 있습니다.  
  
-   시퀀스  
  
-   패키지  
  
-   Java 클래스 스키마 개체  
  
-   사용자 정의 개체 유형  
  
다른 동의어는 마이그레이션할 수 없습니다. SSMA는 동의어와 동의어를 사용 하는 모든 참조에 대해 오류 메시지를 생성 합니다.  
  
-   **예**를 선택 하는 경우 ssma는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 동의어를 만들고 이전 목록에 따라 개체 참조를 직접 만듭니다.  
  
-   **아니요**를 선택 하면 ssma에서 여기에 나열 된 모든 동의어에 대 한 직접 개체 참조를 만듭니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 예로  
  
### <a name="convert-to_chardate-format"></a>변환 TO_CHAR (날짜, 형식)  
SSMA는 DB2 TO_CHAR (날짜, 형식)를 sysdb 데이터베이스의 프로시저로 변환할 수 있습니다.  
  
-   **TO_CHAR_DATE 함수 사용**을 선택 하는 경우 ssma는 변환에 영어를 사용 하 여 TO_CHAR (날짜, 형식)를 TO_CHAR_DATE 함수로 변환 합니다.  
  
-   **TO_CHAR_DATE_LS 함수 (NLS) 사용**을 선택 하는 경우 ssma는 변환에 대 한 세션 언어를 사용 하 여 TO_CHAR (날짜, 형식)를 TO_CHAR_DATE_LS 함수로 변환 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** TO_CHAR_DATE 함수 사용  
  
**전체 모드:** TO_CHAR_DATE_LS 함수 사용 (NLS 주의)  
  
### <a name="convert-transaction-processing-statements"></a>트랜잭션 처리 문 변환  
SSMA는 DB2 트랜잭션 처리 문을 변환할 수 있습니다.  
  
-   **예**를 선택 하면 ssma에서 DB2 트랜잭션 처리 문을 문으로 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
-   **아니요**를 선택 하면 ssma는 트랜잭션 처리 문을 변환 오류로 표시 합니다.  
  
> [!NOTE]  
> DB2는 트랜잭션을 암시적으로 엽니다. 에서이 동작을 에뮬레이트 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 트랜잭션을 시작 하려는 위치에 수동으로 BEGIN TRANSACTION 문을 추가 해야 합니다. 또는 세션 시작 부분에서 SET IMPLICIT_TRANSACTIONS ON 명령을 실행할 수 있습니다. SSMA는 자치 트랜잭션으로 서브루틴을 변환할 때 SET IMPLICIT_TRANSACTIONS ON을 자동으로 추가 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 예로  
  
### <a name="emulate-db2-null-behavior-in-order-by-clauses"></a>ORDER BY 절에서 DB2 null 동작 에뮬레이트  
NULL 값은 및 DB2에서 다르게 정렬 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NULL 값은 순서가 지정 된 목록의 가장 작은 값입니다. 오름차순 목록에서 NULL 값이 먼저 표시 됩니다.  
  
-   DB2에서 NULL 값은 순서가 지정 된 목록에서 가장 높은 값입니다. 기본적으로 NULL 값은 내림차순 목록에서 마지막에 표시 됩니다.  
  
-   DB2에 null FIRST 및 NULL LAST 절이 있으므로 DB2에서 Null을 주문 하는 방식을 변경할 수 있습니다.  
  
SSMA는 NULL 값을 확인 하 여 DB2 ORDER BY 동작을 에뮬레이트할 수 있습니다. 그런 다음 먼저 지정 된 순서로 NULL 값을 기준으로 정렬 한 다음 다른 값을 기준으로 정렬 합니다.  
  
-   **예**를 선택 하면 ssma에서 DB2 ORDER by 동작을 에뮬레이트하는 방식으로 db2 문을 변환 합니다.  
  
-   **아니요**를 선택 하면 SSMA에서 DB2 규칙을 무시 하 고 null FIRST 및 null LAST 절이 나타날 때 오류 메시지를 생성 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 아니요  
  
**전체 모드:** 예로  
  
### <a name="emulate-row-count-exceptions-in-select"></a>SELECT의 행 개수 예외 에뮬레이션  
INTO 절이 있는 SELECT 문에서 행을 반환 하지 않으면 DB2는 NO_DATA_FOUND 예외를 발생 시킵니다. 문에서 둘 이상의 행을 반환 하면 TOO_MANY_ROWS 예외가 발생 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]행 개수가 1과 다른 경우의 변환 된 문은 예외를 발생 시 키 지 않습니다.  
  
-   **예**를 선택 하는 경우 ssma는 각 select 문 다음에 db_error_exact_one_row_check sysdb 프로시저에 대 한 호출을 추가 합니다. 이 프로시저는 NO_DATA_FOUND 및 TOO_MANY_ROWS 예외를 에뮬레이트합니다. 이것이 기본값 이며 DB2 동작을 최대한 가깝게 재현할 수 있습니다. 소스 코드에 이러한 오류를 처리 하는 예외 처리기가 있는 경우 항상 **예** 를 선택 해야 합니다. SELECT 문이 사용자 정의 함수 내에서 발생 하는 경우 저장 프로시저 실행 및 예외 발생이 함수 컨텍스트와 호환 되지 않기 때문에이 모듈은 저장 프로시저로 변환 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **아니요**를 선택 하면 예외가 생성 되지 않습니다. 이는 SSMA에서 사용자 정의 함수를 변환 하 고 해당 함수를에서 함수를 유지 하려는 경우에 유용할 수 있습니다.[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 예로  
  
### <a name="generate-error-for-dbms_sqlparse"></a>DBMS_SQL에 대 한 오류를 생성 합니다. 구문 분석  
  
-   **오류**를 선택 하면 변환 DBMS_SQL에서 ssma 오류가 생성 됩니다. 구문 분석.  
  
-   **경고**를 선택 하는 경우 ssma는 변환 DBMS_SQL에서 경고를 생성 합니다. 구문 분석.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 메시지가  
  
### <a name="generate-rowid-column"></a>ROWID 열 생성  
SSMA가에 테이블 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 만들 때 ROWID 열을 만들 수 있습니다. 데이터를 마이그레이션하면 각 행이 newid () 함수에 의해 생성 된 새 UNIQUEIDENTIFIER 값을 얻습니다.  
  
-   **예**를 선택 하면 ROWID 열이 모든 테이블에 생성 되 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 값을 삽입할 때 guid를 생성 합니다. SSMA 테스터를 사용할 계획인 경우 항상 **예** 를 선택 합니다.  
  
-   **아니요**를 선택 하면 ROWID 열이 테이블에 추가 되지 않습니다.  
  
-   **트리거가 있는 테이블에 대해 rowid 열 추가** 트리거를 포함 하는 테이블에 대해 rowid를 추가 합니다.  
  
> [!WARNING]  
> SQL Server 2005의 경우 기본 설정인 SQL Server 2008 및 SQL Server 2012 및 2014은 **트리거가 있는 테이블에 대해 ROWID 열을 추가**합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 트리거가 있는 테이블에 대해 ROWID 열 추가  
  
**전체 모드:** 예로  
  
### <a name="generate-unique-index-on-rowid-column"></a>ROWID 열에 고유 인덱스 생성  
SSMA가 ROWID 생성 열에 고유 인덱스 열을 생성할지 여부를 지정 합니다. 옵션을 "예"로 설정 하면 고유 인덱스가 생성 되 고 "아니요"로 설정 된 경우에는 고유 인덱스가 ROWID 열에 생성 되지 않습니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 예로  
  
### <a name="local-modules-conversion"></a>로컬 모듈 변환  
독립 실행형 저장 프로시저 또는 함수에서 선언 된 DB2 중첩 subprogram의 유형을 정의 합니다.  
  
-   **인라인으로**를 선택 하는 경우 중첩 된 subprogram 호출은 본문으로 대체 됩니다.  
  
-   **저장 프로시저**를 선택 하면 중첩 된 subprogram가 SQL Server 저장 프로시저로 변환 되 고이 프로시저 호출에서 해당 호출이 대체 됩니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 인라인  
  
### <a name="use-isnull-in-string-concatenation"></a>문자열 연결에 ISNULL 사용  
D b 2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 문자열 연결이 NULL 값을 포함 하는 경우 다른 결과를 반환 합니다. DB2는 빈 문자 집합과 같은 NULL 값을 처리 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]NULL을 반환 합니다.  
  
-   **예**를 선택 하면 SSMA에서 DB2 연결 문자 (| |)를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 문자 (+)로 바꿉니다. 또한 SSMA는 NULL 값에 대 한 연결의 양쪽에 있는 식을 확인 합니다.  
  
-   **아니요**를 선택 하면 ssma는 연결 문자를 대체 하지만 NULL 값은 확인 하지 않습니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
### <a name="use-isnull-in-replace-function-calls"></a>REPLACE 함수 호출에서 ISNULL 사용  
ISNULL 문은 DB2 동작을 에뮬레이트하는 함수 호출 바꾸기에 사용 됩니다. 이 설정에 대해 제공 되는 옵션은 다음과 같습니다.  
  
-   YES  
  
-   아니요  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 아니요  
  
**전체 모드:** 예로  
  
### <a name="use-isnull-in-concat-function-calls"></a>CONCAT 함수 호출에서 ISNULL 사용  
ISNULL 문은 DB2 동작을 에뮬레이트하는 함수 호출에 사용 됩니다. 이 설정에 대해 제공 되는 옵션은 다음과 같습니다.  
  
-   YES  
  
-   아니요  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 아니요  
  
**전체 모드:** 예로  
  
### <a name="use-native-convert-function-when-possible"></a>가능 하면 네이티브 convert 함수 사용  
  
-   **예**를 선택 하는 경우 ssma는 가능 하면 TO_CHAR (날짜, 형식)를 네이티브 convert 함수로 변환 합니다.  
  
-   **아니요**를 선택 하는 경우 ssma는 TO_CHAR (날짜, 형식)를 TO_CHAR_DATE 또는 TO_CHAR_DATE_LS으로 변환 합니다 .이는 "TO_CHAR 변환 (날짜, 형식)" 옵션으로 정의 됩니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적 모드:** 예로  
  
**전체 모드:** 아니요  
  
### <a name="use-selectfor-xml-when-converting-selectinto-for-record-variable"></a>SELECT ...를 사용 합니다. SELECT ...를 변환할 때 FOR XML 레코드 변수에 대 한 INTO  
레코드 변수를 선택할 때 XML 결과 집합을 생성할지 여부를 지정 합니다.  
  
-   **예**를 선택 하는 경우 SELECT 문은 XML을 반환 합니다.  
  
-   **아니요**를 선택 하는 경우 select 문은 결과 집합을 반환 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 아니요  
  
## <a name="returning-clause-conversion"></a>절 변환 반환  
  
### <a name="convert-returning-clause-in-delete-statement-to-output"></a>DELETE 문의 반환 절을 출력으로 변환  
DB2는 삭제 된 값을 즉시 가져오는 방법으로 반환 절을 제공 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 OUTPUT 절을 사용 하 여 해당 기능을 제공 합니다.  
  
-   **예**를 선택 하면 DELETE 문의 반환 절이 OUTPUT 절로 변환 됩니다. 테이블의 트리거가 값을 변경할 수 있기 때문에 반환 된 값은 d b 2의 경우와 다를 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **아니요**를 선택 하면 SSMA는 DELETE 문 앞에 select 문을 생성 하 여 반환 된 값을 검색 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 예로  
  
### <a name="convert-returning-clause-in-insert-statement-to-output"></a>INSERT 문의 반환 절을 출력으로 변환  
DB2는 삽입 된 값을 즉시 가져오는 방법으로 반환 절을 제공 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 OUTPUT 절을 사용 하 여 해당 기능을 제공 합니다.  
  
-   **예**를 선택 하면 SSMA가 INSERT 문의 반환 절을 출력으로 변환 합니다. 테이블의 트리거가 값을 변경할 수 있기 때문에 반환 된 값은 d b 2의 경우와 다를 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **아니요**를 선택 하는 경우 ssma는 참조 테이블에서 값을 삽입 한 다음 선택 하 여 DB2 기능을 에뮬레이트합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 예로  
  
### <a name="convert-returning-clause-in-update-statement-to-output"></a>UPDATE 문의 반환 절을 출력으로 변환  
DB2는 업데이트 된 값을 즉시 가져오는 방법으로 반환 절을 제공 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 OUTPUT 절을 사용 하 여 해당 기능을 제공 합니다.  
  
-   **예**를 선택 하면 SSMA가 UPDATE 문의 반환 절을 OUTPUT 절로 변환 합니다. 테이블의 트리거가 값을 변경할 수 있기 때문에 반환 된 값은 d b 2의 경우와 다를 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **아니요**를 선택 하면 SSMA는 UPDATE 문 뒤에 select 문을 생성 하 여 반환 값을 검색 합니다.  
  
**모드** 상자에서 변환 모드를 선택 하면 ssma가 다음 설정을 적용 합니다.  
  
**기본/최적/전체 모드:** 예로  
  
## <a name="sequence-conversion"></a>시퀀스 변환  
  
### <a name="convert-sequence-generator"></a>시퀀스 생성기 변환  
DB2에서는 시퀀스를 사용 하 여 고유 식별자를 생성할 수 있습니다.  
  
SSMA는 시퀀스를 다음으로 변환할 수 있습니다.  
  
-   SQL Server 시퀀스 생성기 사용 (이 옵션은 SQL Server 2012 및 SQL Server 2014)으로 변환 하는 경우에만 사용할 수 있습니다.  
  
-   SSMA 시퀀스 생성기 사용.  
  
-   열 id 사용.  
  
SQL Server 2012 또는 SQL Server 2014로 변환할 때 기본 옵션은 SQL Server 시퀀스 생성기를 사용 하는 것입니다. 그러나 SQL Server 2012 및 SQL Server 2014에서는 현재 시퀀스 값 (예: DB2 sequence al val 메서드의 경우)을 가져올 수 없습니다. DB2 시퀀스 통화를 마이그레이션하는 방법에 대 한 지침은 SSMA 팀 블로그 사이트를 참조 하세요.  
  
또한 SSMA는 DB2 시퀀스를 SSMA 시퀀스 에뮬레이터로 변환 하는 옵션을 제공 합니다. 2012 이전의 SQL Server로 변환할 경우의 기본 옵션입니다.  
  
마지막으로 테이블의 열에 할당 된 시퀀스를 변환 하 여 id 값을 SQL Server 수도 있습니다. DB2 **테이블** 탭의 시퀀스와 id 열 간의 매핑을 지정 해야 합니다.  
  
### <a name="convert-currval-outside-triggers"></a>트리거 외부에서 통화를 변환 합니다.  
변환 시퀀스 생성기가 **열 id를 사용**하도록 설정 된 경우에만 표시 됩니다. DB2 시퀀스는 테이블과 별도의 개체 이므로 시퀀스를 사용 하는 많은 테이블은 트리거를 사용 하 여 새 시퀀스 값을 생성 하 고 삽입 합니다. SSMA는 이러한 문을 주석 처리 하거나 주석 처리 시 오류가 생성 될 때 오류로 표시 합니다.  
  
-   **예**를 선택 하면 ssma는 변환 된 시퀀스의 외부 트리거에 대 한 모든 참조를 경고와 함께 표시 합니다.  
  
-   **아니요**를 선택 하면 ssma는 변환 된 시퀀스의 외부 트리거에 대 한 모든 참조를 오류로 표시 합니다.  
  
## <a name="see-also"></a>참고 항목  
[DB2ToSQL&#41;&#40;사용자 인터페이스 참조](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
