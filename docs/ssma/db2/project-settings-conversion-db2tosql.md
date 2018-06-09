---
title: 프로젝트 설정 (변환) (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 538c93cf-c5bb-43d5-b758-186d9fb00c19
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 31f00a9fbc779ae0054a04a9890fcca9a0be33a9
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34775609"
---
# <a name="project-settings-conversion-db2tosql"></a>프로젝트 설정 (변환) (DB2ToSQL)
변환 페이지는 **프로젝트 설정** 대화 상자 SSMA를 DB2 구문을 변환 하는 방법을 사용자 지정 하는 설정이 포함 되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구문입니다.  
  
변환에서 제공 되는 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자:  
  
-   에 모든 SSMA 프로젝트에 대 한 설정을 지정 하려면는 **도구** 메뉴 클릭 **기본 프로젝트 설정**, 설정을 보거나에서 변경 하는 데 필요한는 마이그레이션 프로젝트 형식을 선택 **마이그레이션 대상 버전** 드롭다운을 클릭 **일반** 클릭 한 다음 확인 하 고 왼쪽된 창 맨 아래에 **변환**합니다.  
  
-   에 현재 프로젝트에 대 한 설정을 지정 하려면는 **도구** 메뉴 클릭 **프로젝트 설정**, 클릭 **일반** 클릭 한 다음 확인 하 고 왼쪽된 창 맨 아래에 **변환**합니다.  
  
## <a name="conversion-messages"></a>변환 메시지  
  
### <a name="generate-messages-about-issues-applied"></a>적용 되는 문제에 대 한 메시지를 생성 합니다.  
여부를 지정 SSMA 변환 하는 동안 정보 메시지를 생성, 출력 창에 표시 변환된 된 코드에 추가 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적 모드:** 아니요  
  
**전체 모드:** 아니요  
  
## <a name="miscellaneous-options"></a>기타 옵션  
  
### <a name="cast-rownum-expressions-as-integers"></a>정수로 캐스트 ROWNUM 식  
SSMA ROWNUM 식을 변환, 식 옵니다 TOP 절에 식으로 변환 합니다. 다음 예제에서는 DB2 DELETE 문에서 ROWNUM를 보여 줍니다.  
  
`DELETE FROM Table1`  
  
`WHERE ROWNUM < expression and Field1 >= 2`  
  
다음 예제에서는 결과 [!INCLUDE[tsql](../../includes/tsql_md.md)]:  
  
`DELETE TOP (expression-1)`  
  
`FROM Table1`  
  
`WHERE Field1>=2`  
  
위쪽 TOP 절 식이 정수로 필요 합니다. 정수가 음수 이면 명령문에서 오류가 발생 합니다.  
  
-   선택 하는 경우 **예**, SSMA 캐스팅 하는 정수입니다.  
  
-   선택 하는 경우 **아니요**, SSMA를 오류로 변환된 된 코드에서 모든 정수가 아닌 식이 표시 됩니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/전체 모드:** 아니요  
  
**최적 모드:** 예  
  
### <a name="default-schema-mapping"></a>기본 스키마 매핑  
이 설정은 DB2 스키마를 SQL Server 스키마로 매핑되는 방법을 지정 합니다. 두 가지 옵션이이 설정을 사용할 수 있습니다.  
  
1.  **데이터베이스에 스키마:** 이 모드로 DB2 스키마 'sch1' 'dbo' SQL Server 데이터베이스 스키마에 SQL Server 'sch1' 기본적으로 매핑되지 것입니다.  
  
2.  **스키마를 스키마:** 이 모드로 DB2 스키마 'sch1' 'sch1' SQL Server 데이터베이스 스키마에 기본 SQL Server 연결 대화 상자에서 제공 되는 기본적으로 매핑되지 것입니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic/전체 모드:** 데이터베이스에 대 한 스키마  
  
### <a name="conversion-ways-of-merge-statement"></a>MERGE 문의 변환 방법  
  
-   선택 하는 경우 **사용 하 여 삽입, 업데이트, DELETE 문이**, SSMA 변환 합병 문은 INSERT, UPDATE, DELETE 문.  
  
-   선택 하는 경우 **MERGE를 사용 하 여 문은**, SSMA 변환에서 MERGE 문을 합병 문을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
> [!WARNING]  
> 이 프로젝트 설정 옵션은 영어로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic/전체 모드:** MERGE 사용 하 여 문  
  
### <a name="convert-calls-to-subprograms-that-use-default-arguments"></a>기본 인수를 사용 하는 하위 프로그램에 대 한 호출을 변환  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 함수는 함수 호출에 매개 변수는 생략을 지원 하지 않습니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 함수 및 프로시저 식이 기본 매개 변수 값으로 지원 하지 않습니다.  
  
-   선택 하는 경우 **예** 및 매개 변수를 생략 하는 함수 호출, SSMA를 삽입 하는 키워드는 **기본** 함수 및 올바른 위치에 대 한 호출을 합니다. 그런 다음 경고를 사용 하 여 호출 된 것입니다.  
  
-   선택 하는 경우 **아니요**, SSMA를 오류로 함수 호출으로 표시 됩니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적/전체 모드:** 예  
  
### <a name="convert-count-function-to-countbig"></a>COUNT 함수 COUNT_BIG 변환  
즉 2 COUNT 함수는 값, 2147483647 보다 큰 반환 될 경우<sup>31</sup>-1 이면 함수 COUNT_BIG을 변환 해야 합니다.  
  
-   선택 하는 경우 **예**, SSMA COUNT_BIG 개수 사용 되는 모든 변환 됩니다.  
  
-   선택 하는 경우 **아니요**, 기능 수로 유지 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 함수 반환 값 2 보다 큰 경우 오류가 반환 됩니다<sup>31</sup>-1입니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/전체 모드:** 예  
  
**최적 모드:** 아니요  
  
### <a name="convert-forall-statement-to-while-statement"></a>FORALL 문이 WHILE 변환할 문  
SSMA PL/SQL 컬렉션 요소에 대해 FORALL 루프에서 처리 방법을 정의 합니다.  
  
-   선택 하는 경우 **예**, SSMA 컬렉션 요소가 하나씩 검색된 여기서 WHILE 루프를 만듭니다.  
  
-   선택 하는 경우 **아니요**, SSMA 노드 () 메서드를 사용 하 여 컬렉션에서 생성 하는 행 집합으로 사용 하 여 단일 테이블. 더 효율적 이지만 회색조 출력 코드를 만듭니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적 모드:** 아니요  
  
**전체 모드:** 예  
  
### <a name="convert-foreign-keys-with-set-null-referential-action-on-column-that-is-not-null"></a>변환 된 열에 SET NULL 참조 동작으로 외래 키에서 NOT NULL  
DB2 여기서 SET NULL 동작 가능한 수행할 수 없습니다 참조 된 열에 Null이 허용 되지 않는 때문에 foreign key 제약 조건을 만들 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 이러한 외래 키 구성을 허용 하지 않습니다.  
  
-   선택 하는 경우 **예**, SSMA d b 2에서는와 같이 참조 동작 하지만 제약 조건을 로드 하기 전에 수동으로 변경 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 예를 들어, SET NULL 대신 NO ACTION을 선택할 수 있습니다.  
  
-   선택 하는 경우 **아니요**, 제약 조건 오류로 표시 됩니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적/전체 모드:** 아니요  
  
### <a name="convert-function-calls-to-procedure-calls"></a>프로시저 호출에 대 한 함수 호출 변환  
일부 DB2 함수 자치 트랜잭션을으로 정의 된 또는에서 사용할 수 없습니다 하는 문을 포함 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 이러한 경우 SSMA는 프로시저 및 프로시저에 대 한 래퍼 함수를 만듭니다. 변환 된 함수는 구현 프로시저를 호출합니다.  
  
SSMA는 래퍼 함수를 호출 하는 프로시저에 대 한 호출으로 변환할 수 있습니다. 그러면 보다 읽기 쉬운 코드 만들어지고 성능을 향상 시킬 수 있습니다. 그러나 컨텍스트에서 항상 허용 되지 않으면 예를 들어 프로시저 호출으로는 SELECT 목록에서 함수 호출을 바꿀 수 없습니다. SSMA에 일반적인 경우를 처리 하려면 몇 가지 옵션이 있습니다.  
  
-   선택 하는 경우 **항상**, SSMA 래퍼 함수 호출 프로시저 호출으로 변환 하려고 합니다. 현재 컨텍스트는이 변환을 허용 하지 않습니다, 오류 메시지가 생성 됩니다. 이러한 방식으로 더 함수 호출을 생성된 된 코드에 남아 있습니다.  
  
-   선택 하는 경우 **가능 하면**, SSMA를 사용 하면 이동 프로시저 호출에 함수에 매개 변수를 출력 하는 경우에 합니다. 이동 불가능 매개 변수의 출력 특성 제거 됩니다. 다른 모든 경우에 SSMA 함수 호출을 유지합니다.  
  
-   선택 하는 경우 **Never**, SSMA 함수 호출으로 모든 함수 호출을 종료 됩니다. 경우에 따라이 옵션을이 선택 수용 하지 못할 성능상의 이유로 인해 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic/전체 모드:** 가능한 경우  
  
### <a name="convert-lock-table-statements"></a>변환 잠금 테이블 문  
SSMA는 많은 수의 잠금 테이블로 문이 테이블 힌트를 변환할 수 있습니다. SSMA SUBPARTITION, 파티션을 포함 하는 모든 잠금이 테이블 문은 변환할 수 없습니다 @dblink, NOWAIT 절 및 이러한 문의 변환 오류 메시지를 표시 합니다.  
  
-   선택 하는 경우 **예**, SSMA 테이블 힌트로 지원 되는 문의 잠금 테이블을 변환 합니다.  
  
-   선택 하는 경우 **아니요**, SSMA 변환 오류 메시지와 함께 모든 잠금이 TABLE 문을 표시 합니다.  
  
다음 표에서 SSMA DB2 잠금 모드를 변환 하는 방법을 보여 줍니다.  
  
|||  
|-|-|  
|DB2 잠금 모드|SQL Server 테이블 힌트|  
|행 공유|ROWLOCK, HOLDLOCK|  
|단독 행|ROWLOCK, XLOCK, HOLDLOCK|  
|공유 업데이트 = 행 공유|ROWLOCK, HOLDLOCK|  
|공유|TABLOCK, HOLDLOCK|  
|공유 행 제외|TABLOCK, XLOCK, HOLDLOCK|  
|단독|HOLDLOCK, TABLOCKX|  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적/전체 모드:** 예  
  
### <a name="convert-open-for-statements-for-ref-cursor-out-parameters"></a>변환 REF CURSOR OUT 매개 변수에 대해 오픈 FOR 문  
D b 2에서는 오픈 FOR 문을 사용 하 여 결과 하위 프로그램의 출력 형식이 REF CURSOR 매개 변수 집합을 반환할 수 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 저장된 프로시저는 직접 SELECT 문의 결과를 반환 합니다.  
  
SSMA는 여러 오픈 FOR 문에 SELECT 문으로 변환할 수 있습니다.  
  
-   선택 하는 경우 **예**, SSMA 오픈 FOR 문 결과 집합을 클라이언트에 반환 하는 SELECT 문이 변환 합니다.  
  
-   선택 하는 경우 **아니요**, SSMA 변환된 코드 및 출력 창에서 오류 메시지가 생성 됩니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적/전체 모드:** 예  
  
### <a name="convert-record-as-a-list-of-separates-variables"></a>레코드 구분 변수 목록으로 변환  
SSMA는 변수를 구분 하며이 특정 구조를 사용 하 여 XML 변수 DB2 레코드를 변환할 수 있습니다.  
  
-   선택 하는 경우 **예**, SSMA 가능 하면 구분 변수의 목록으로 레코드를 변환 합니다.  
  
-   선택 하는 경우 **아니요**, SSMA 특정 구조를 사용 하 여 XML 변수를 레코드를 변환 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적/전체 모드:** 예  
  
### <a name="convert-substr-function-calls-to-substring-function-calls"></a>SUBSTRING 함수 호출에 대 한 SUBSTR 함수 호출 변환  
SSMA를 DB2 SUBSTR 함수 호출을 변환할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **부분 문자열** 함수 매개 변수 개수에 따라 호출 합니다. SSMA는 SUBSTR 함수 호출을 변환할 수 없습니다 매개 변수 수가 지원 되지 않거나, SSMA 사용자 지정 SSMA 함수 호출에 SUBSTR 함수 호출을 변환 합니다.  
  
-   선택 하는 경우 **예**, SSMA는 세 개의 매개 변수를 사용 하는 SUBSTR 함수 호출 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **부분 문자열**합니다. 다른 SUBSTR 함수를 사용자 지정 SSMA 함수 호출 변환 됩니다.  
  
-   선택 하는 경우 **아니요**, SSMA 사용자 지정 SSMA 함수 호출으로 SUBSTR 함수 호출을 변환 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적 모드:** 예  
  
**전체 모드:** 아니요  
  
### <a name="convert-subtypes"></a>하위 형식 변환  
SSMA는 PL/SQL 하위 두 가지 방법으로 변환할 수 있습니다.  
  
-   선택 하는 경우 **예**, SSMA 만들어집니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 사용자 정의 하위 형식에서 입력 하 고이 하위 유형의 각 변수에 대해 사용 합니다.  
  
-   선택 하는 경우 **아니요**, SSMA를 내부 형식과 하위 형식의 모든 소스 선언을 대체 하 고 결과 정상적으로 변환 됩니다. 이 경우에 추가 형식이 없습니다에 생성 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적/전체 모드:** 아니요  
  
### <a name="convert-synonyms"></a>동의어를 변환 합니다.  
다음 DB2 개체에 대 한 동의어로 마이그레이션할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
-   테이블 및 개체 테이블  
  
-   뷰 및 개체 보기  
  
-   저장된 프로시저 및 함수  
  
-   구체화 된 뷰  
  
개체에 대 한 직접 참조 하 여 다음 DB2 개체에 대 한 동의어를 바꿀 수 있습니다.  
  
-   시퀀스  
  
-   패키지  
  
-   Java 클래스 스키마 개체  
  
-   사용자 정의 개체 유형  
  
다른 동의어를 마이그레이션할 수 없습니다. SSMA는 동의어 및 동의어가 사용 하는 모든 참조에 대 한 오류 메시지가 생성 됩니다.  
  
-   선택 하는 경우 **예**, SSMA 만들어집니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 동의어 및 이전 목록에 따라 직접 개체 참조입니다.  
  
-   선택 하는 경우 **아니요**, SSMA 여기에 나열 된 모든 동의어에 대 한 직접 개체 참조를 생성 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적/전체 모드:** 예  
  
### <a name="convert-tochardate-format"></a>TO_CHAR (날짜, 형식)으로 변환  
SSMA는 DB2 TO_CHAR(date, format) sysdb 데이터베이스에서 절차로 변환할 수 있습니다.  
  
-   선택 하는 경우 **함수를 사용 하 여 TO_CHAR_DATE**, SSMA (날짜, 형식) TO_CHAR TO_CHAR_DATE 함수를 사용 하 여 영어의 변환에 대 한 변환 합니다.  
  
-   선택 하는 경우 **(NLS 주의)를 사용 하 여 TO_CHAR_DATE_LS 함수**, SSMA (날짜, 형식) TO_CHAR TO_CHAR_DATE_LS 함수를 사용 하 여 세션 언어의 변환에 대 한 변환  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드:** Using TO_CHAR_DATE 함수  
  
**전체 모드:** Using TO_CHAR_DATE_LS 함수 (NLS 주의)  
  
### <a name="convert-transaction-processing-statements"></a>트랜잭션 처리 문을 변환합니다  
SSMA는 DB2 트랜잭션 처리 문을 변환할 수 있습니다.  
  
-   선택 하는 경우 **예**, SSMA 변환 DB2 트랜잭션 처리 문을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 문.  
  
-   선택 하는 경우 **아니요**, SSMA 문을 변환 오류로 처리 트랜잭션을 표시 합니다.  
  
> [!NOTE]  
> D b 2는 트랜잭션을 암시적으로 열립니다. 이 동작을 에뮬레이트하는 데 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]를 수동으로 추가 해야는 BEGIN TRANSACTION 문이 시작 하 여 트랜잭션을 저장할 합니다. 또는 세션의 시작 부분에 SET IMPLICIT_TRANSACTIONS ON 명령을 실행할 수 있습니다. SSMA 자치 트랜잭션 사용 하 여 서브루틴을 변환 하는 경우 SET IMPLICIT_TRANSACTIONS ON을 자동으로 추가 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적/전체 모드:** 예  
  
### <a name="emulate-db2-null-behavior-in-order-by-clauses"></a>ORDER BY 절에서 null 동작 DB2 에뮬레이션  
NULL 값에 다르게 정렬 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 및 DB2:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], NULL 값은 정렬 된 목록에서 가장 낮은 값입니다. 오름차순 목록에서 NULL 값이 먼저 표시 됩니다.  
  
-   D b 2에서 NULL 값은 정렬 된 목록에서 가장 높은 값입니다. 기본적으로 NULL 값의 마지막 오름차순 순서 목록에 표시 됩니다.  
  
-   D b 2 d b 2에서 null 값을 정렬 하는 방법을 변경할 수 있도록 NULL 첫 번째 및 마지막 NULL 절에 있습니다.  
  
SSMA는 NULL 값에 대해 확인 하 여 DB2 ORDER BY 동작을 에뮬레이트할 수 있습니다. 다음 먼저 정렬 다른 값으로 지정 된 순서와 다음 주문에서 값이 NULL입니다.  
  
-   선택 하는 경우 **예**, SSMA DB2 문의 ORDER BY DB2 동작을 에뮬레이션 하는 방식으로 변환 됩니다.  
  
-   선택 하는 경우 **아니요**, SSMA는 DB2 규칙을 무시 하 고 NULL 첫 번째 및 마지막 NULL 절에 도달할 때 오류 메시지가 생성 됩니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적 모드:** 아니요  
  
**전체 모드:** 예  
  
### <a name="emulate-row-count-exceptions-in-select"></a>에뮬레이트하 선택에서 행 개수 예외  
INTO 절이 있는 SELECT 명령문이 행을 반환 하지 않으면, DB2 NO_DATA_FOUND 예외를 발생 시킵니다. 문이 두 개 이상의 행이 반환 TOO_MANY_ROWS 예외가 발생 합니다. 변환된 된 문이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 행 수가 하나에서 다른 경우 예외가 발생 하지 않습니다.  
  
-   선택 하는 경우 **예**, SSMA 각 SELECT 문의 후 sysdb 프로시저 db_error_exact_one_row_check 호출을 추가 합니다. 이 절차는 NO_DATA_FOUND 및 TOO_MANY_ROWS 예외를 에뮬레이션합니다. 이것이 기본 설정 및 가능한 DB2 동작을 재현할 수 있습니다. 항상 선택 해야 **예** 소스 코드에 이러한 오류를 처리 하는 예외 처리기를 포함 하는 경우. SELECT 문은 사용자 정의 함수 내 발생 하는 경우 저장된 프로시저를 실행 하기 때문에이 모듈을 저장 프로시저 변환 됩니다 및와 호환 되지 않는 예외를 발생 시키는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 함수 컨텍스트.  
  
-   선택 하는 경우 **아니요**, 예외가 생성 됩니다. SSMA는 사용자 정의 함수를 변환 하 고 함수에 유지 하려는 경우 유용할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적/전체 모드:** 예  
  
### <a name="generate-error-for-dbmssqlparse"></a>DBMS_SQL에 대 한 오류를 생성 합니다. 구문 분석  
  
-   선택 하는 경우 **오류**, SSMA DBMS_SQL 변환에서 오류를 생성 합니다. 구문 분석 합니다.  
  
-   선택 하는 경우 **경고**, SSMA DBMS_SQL 변환에는 경고를 생성 합니다. 구문 분석 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적/전체 모드:** 오류  
  
### <a name="generate-rowid-column"></a>행 ID 열 생성  
SSMA의 테이블을 생성할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 행 ID 열을 만들 수 있습니다. 데이터를 마이그레이션할 때 각 행에 newid () 함수에 의해 생성 된 새 UNIQUEIDENTIFIER 값을 가져옵니다.  
  
-   선택 하는 경우 **예**, 모든 테이블에 행 ID 열은 생성 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 값을 삽입할 때 Guid를 생성 합니다. 항상 선택 **예** SSMA 테스터를 사용 하도록 하려는 경우.  
  
-   선택 하는 경우 **아니요**, ROWID 열 테이블에 추가 되지 않습니다.  
  
-   **트리거가 있는 테이블의 행 ID 열을 추가** ROWID 트리거를 포함 하는 테이블에 대 한 추가 합니다.  
  
> [!WARNING]  
> SQL Server 2005, SQL Server 2008 및 SQL Server 2012 및 2014의 경우 기본 설정은 **트리거가 포함 된 테이블에 대 한 추가 행 ID 열**합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/Optimistic 모드:** 트리거가 있는 테이블의 행 ID 열을 추가 합니다.  
  
**전체 모드:** 예  
  
### <a name="generate-unique-index-on-rowid-column"></a>행 ID 열에 고유 인덱스를 생성 합니다.  
여부 SSMA 생성 하는 행 ID 열에 고유 인덱스 열을 생성 하는지 여부를 지정 합니다. 고유 인덱스 생성 되는 옵션을 "예"로 설정 하 고 행 ID 열에 "아니요"로 설정 된 경우 고유 인덱스가 생성 되지 않습니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적/전체 모드:** 예  
  
### <a name="local-modules-conversion"></a>로컬 모듈 변환  
중첩 된 DB2 (독립 실행형 저장 프로시저 또는 함수에서 선언 됨) 하는 하위 프로그램 변환 형식을 정의합니다.  
  
-   선택 하는 경우 **인라인**, 중첩 된 하위 프로그램 호출 본문으로 대체 됩니다.  
  
-   선택 하는 경우 **저장 프로시저**, SQL Server 저장 프로시저에 중첩 된 하위 프로그램 변환 되 고,이 프로시저 호출에서 해당 호출을 대체 됩니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적/전체 모드:** 인라인  
  
### <a name="use-isnull-in-string-concatenation"></a>문자열 연결의 ISNULL 사용  
DB2 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 문자열 연결 NULL 값을 포함 하는 경우 다른 결과 반환 합니다. D b 2는 NULL 값이 없는 빈 문자 집합 처럼 처리합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] NULL을 반환합니다.  
  
-   선택 하는 경우 **예**, DB2 연결 문자 (|) 바꿉니다. SSMA는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 연결 문자 (+). SSMA는 NULL 값에 대 한 연결의 양쪽 모두에 있는 식을 확인합니다.  
  
-   선택 하는 경우 **아니요**, SSMA 연결 문자를 대체 하지만 NULL 값을 확인 하지 않습니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
### <a name="use-isnull-in-replace-function-calls"></a>REPLACE 함수 호출에서 ISNULL 사용  
ISNULL 문은 d b 2의 동작을 에뮬레이트해야 REPLACE 함수 호출에 사용 됩니다. 다음 옵션은이 설정에 대 한.  
  
-   YES  
  
-   아니요  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적 모드:** 아니요  
  
**전체 모드:** 예  
  
### <a name="use-isnull-in-concat-function-calls"></a>CONCAT 함수 호출에서 ISNULL 사용  
ISNULL 문은 d b 2의 동작을 에뮬레이트해야 CONCAT 함수 호출에 사용 됩니다. 다음 옵션은이 설정에 대 한.  
  
-   YES  
  
-   아니요  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적 모드:** 아니요  
  
**전체 모드:** 예  
  
### <a name="use-native-convert-function-when-possible"></a>가능한 경우 네이티브 convert 함수를 사용 하 여  
  
-   선택 하는 경우 **예**, SSMA TO_CHAR (날짜, 형식) 가능 하면 네이티브 convert 함수로 변환 합니다.  
  
-   선택 하는 경우 **아니요**, SSMA TO_CHAR_DATE 또는 ("TO_CHAR(date, format) 변환" 옵션에 정의 된) TO_CHAR_DATE_LS TO_CHAR (날짜, 형식)을 변환 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적 모드:** 예  
  
**전체 모드:** 아니요  
  
### <a name="use-selectfor-xml-when-converting-selectinto-for-record-variable"></a>SELECT를 사용 하는 중... XML 변환 하는 경우에 대 한 선택... INTO 레코드 변수에 대 한  
레코드 변수로 선택 설정 XML 결과 생성할 것인지 지정 합니다.  
  
-   선택 하는 경우 **예**, SELECT 문은 XML을 반환 합니다.  
  
-   선택 하는 경우 **아니요**, SELECT 문의 결과 집합을 반환 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적/전체 모드:** 아니요  
  
## <a name="returning-clause-conversion"></a>절 변환을 반환합니다.  
  
### <a name="convert-returning-clause-in-delete-statement-to-output"></a>DELETE 문에 RETURNING 절 출력으로 변환  
D b 2는 즉시 삭제 된 값을 검색 하는 방법으로 RETURNING 절을 제공 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] OUTPUT 절에 해당 기능을 제공합니다.  
  
-   선택 하는 경우 **예**, SSMA는 출력 절 RETURNING 절을 DELETE 문 변환 합니다. 반환된 된 값에서 다를 수 있습니다 테이블의 트리거 값을 변경할 수 있으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] d b 2 에서보다 합니다.  
  
-   선택 하는 경우 **아니요**, SSMA DELETE 문 반환 된 값을 검색 하기 전에 SELECT 문을 생성 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적/전체 모드:** 예  
  
### <a name="convert-returning-clause-in-insert-statement-to-output"></a>INSERT 문에서 RETURNING 절을 출력으로 변환  
DB2 즉시 삽입 된 값을 검색 하는 방법으로 RETURNING 절을 제공 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] OUTPUT 절에 해당 기능을 제공합니다.  
  
-   선택 하는 경우 **예**, SSMA는 INSERT 문에서 RETURNING 절 출력 변환 됩니다. 반환된 된 값에서 다를 수 있습니다 테이블의 트리거 값을 변경할 수 있으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] d b 2 에서보다 합니다.  
  
-   선택 하는 경우 **아니요**, SSMA 삽입 한 다음 참조 테이블에서 값을 선택 하 여 DB2 기능을 에뮬레이트합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적/전체 모드:** 예  
  
### <a name="convert-returning-clause-in-update-statement-to-output"></a>UPDATE 문에서 RETURNING 절 출력으로 변환  
D b 2에서는 즉시 업데이트 된 값을 검색 하는 방법으로 RETURNING 절을 제공 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] OUTPUT 절에 해당 기능을 제공합니다.  
  
-   선택 하는 경우 **예**, SSMA는 출력 절 UPDATE 문에서 RETURNING 절 변환 합니다. 반환된 된 값에서 다를 수 있습니다 테이블의 트리거 값을 변경할 수 있으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] d b 2 에서보다 합니다.  
  
-   선택 하는 경우 **아니요**, SSMA SELECT 문이 반환 값을 검색 하는 UPDATE 문을 생성 합니다.  
  
변환 모드를 선택 하면는 **모드** SSMA 상자에서 다음 설정이 적용 됩니다.  
  
**기본/낙관적/전체 모드:** 예  
  
## <a name="sequence-conversion"></a>시퀀스 변환  
  
### <a name="convert-sequence-generator"></a>시퀀스 생성기를 변환 합니다.  
D b 2에서는 고유한 식별자를 생성 하는 순서를 사용할 수 있습니다.  
  
SSMA는 다음에 시퀀스를 변환할 수 있습니다.  
  
-   (이 옵션은만 사용할 수 있는 SQL Server 2012 및 SQL Server 2014를 변환 하는 경우)는 SQL Server 시퀀스 생성기를 사용 합니다.  
  
-   SSMA 시퀀스 생성기를 사용합니다.  
  
-   열 id를 사용 합니다.  
  
SQL Server 2012 또는 SQL Server 2014를 변환할 때 기본 옵션 SQL Server 시퀀스 생성기를 사용 하는 것입니다. 그러나 SQL Server 2012 및 SQL Server 2014 지원 하지 않습니다 (예: DB2 시퀀스 currval 메서드의) 현재 시퀀스 값 가져오기. DB2 순서 currval 방법 마이그레이션에 대 한 지침은 SSMA 팀 블로그 사이트를 참조 하십시오.  
  
SSMA는 또한 DB2 시퀀스 SSMA 시퀀스 에뮬레이터를 변환 하는 옵션을 제공 합니다. SQL server 2012 이전의 변환 하는 경우 기본 옵션입니다.  
  
마지막으로, SQL Server id 값을 테이블의 열에 할당 된 시퀀스를 변환할 수 있습니다. D b 2에 id 열에 시퀀스 간의 매핑을 지정 해야 **테이블** 탭  
  
### <a name="convert-currval-outside-triggers"></a>트리거 밖에 CURRVAL 변환  
변환할 시퀀스 생성기로 설정 된 경우에 표시 **열 id를 사용 하**합니다. DB2 시퀀스는 테이블에서 별도 개체를 생성 하 고 새 시퀀스 값을 삽입 트리거를 사용 하는 시퀀스를 사용 하는 여러 테이블. SSMA는 이러한 문을 주석으로 처리 하거나 주석 달기 아웃 오류를 생성 하는 경우 오류로 표시 합니다.  
  
-   선택 하는 경우 **예**, SSMA 모든 참조의 변환 된 트리거 외부 CURRVAL 경고와 함께 시퀀스를 표시 합니다.  
  
-   선택 하는 경우 **아니요**, SSMA로의 변환 된 트리거 외부 CURRVAL 오류가 발생 하 여 시퀀스에 모든 참조 표시 됩니다.  
  
## <a name="see-also"></a>관련 항목  
[사용자 인터페이스 참조 &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
