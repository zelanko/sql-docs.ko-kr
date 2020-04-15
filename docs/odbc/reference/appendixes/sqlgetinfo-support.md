---
title: SQLGetInfo 지원 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLGetInfo
- backward compatibility [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], support
ms.assetid: 57326f57-daba-46b6-b0be-6c97213b9ef1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a21c035a14814f51d4344894ef253b2cc844f4c2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307804"
---
# <a name="sqlgetinfo-support"></a>SQLGetInfo 지원
때 ODBC 2. *x* 응용 프로그램은 **SQLGetInfo를** ODBC*3.x* 드라이버로 호출하며 다음 표의 *InfoType* 인수를 지원해야 합니다.  
  
|*정보 입력*|반환|  
|----------------|-------------|  
|SQL_ALTER_TABLE(ODBC 2.0) **참고:** 이 정보 형식은 더 이상 사용되지 않습니다. 오른쪽 열의 비트 마스크는 더 이상 사용되지 않습니다.|데이터 원본에서 지원하는 **ALTER TABLE** 문의 절을 등록하는 SQLINTEGER 비트 마스크입니다.<br /><br /> 다음 비트 마스크는 지원되는 절을 결정하는 데 사용됩니다.<br /><br /> SQL_AT_DROP_COLUMN = 열을 삭제하는 기능이 지원됩니다. 이로 인해 계단식 또는 제한 동작이 발생하든 관계없이 드라이버정의가 정의됩니다. (ODBC 2.0)<br /><br /> SQL_AT_ADD_COLUMN = 단일 ALTER TABLE 문에 여러 열을 추가하는 기능이 지원됩니다. 이 비트는 다른 SQL_AT_ADD_COLUMN_XXX 비트 또는 SQL_AT_CONSTRAINT_XXX 비트와 결합되지 않습니다. (ODBC 2.0)|  
|SQL_FETCH_DIRECTION (ODBC 1.0)<br /><br /> 정보 유형은 ODBC 1.0에 도입되었습니다. 각 비트마스크는 도입된 버전으로 레이블이 지정됩니다.|지원되는 가져오기 방향 옵션을 등록하는 SQLINTEGER 비트 마스크입니다.<br /><br /> 다음 비트마스크는 플래그와 함께 지원되는 옵션을 결정하는 데 사용됩니다.<br /><br /> SQL_FD_FETCH_NEXT (ODBC 1.0) SQL_FD_FETCH_FIRST (ODBC 1.0) SQL_FD_FETCH_LAST (ODBC 1.0) SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_ABSOLUTE (ODBC 1.0) SQL_FD_FETCH_RELATIVE (ODBC 1.0) SQL_FD_FETCH_BOOKMARK (ODBC 2.0)|  
|SQL_LOCK_TYPES (ODBC 2.0)|**SQLSetPos에서** *fLock* 인수에 대 한 지원 되는 잠금 형식을 나열 하는 SQLINTEGER 비트 마스크 .<br /><br /> 다음 비트 마스크는 플래그와 함께 지원되는 잠금 유형을 결정하는 데 사용됩니다.<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1.0)|ODBC 준수 수준을 나타내는 SQLSMALLINT 값입니다.<br /><br /> SQL_OAC_NONE = 없음<br /><br /> SQL_OAC_LEVEL1 = 수준 1 지원<br /><br /> SQL_OAC_LEVEL2 = 수준 2 지원|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1.0)|드라이버에서 지원하는 SQL 문법을 나타내는 SQLSMALLINT 값입니다. SQL 적합성 수준에 대한 정의는 [부록 C: SQL 문법을](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md) 참조하십시오.<br /><br /> SQL_OSC_MINIMUM = 최소 문법 지원<br /><br /> SQL_OSC_CORE = 코어 문법 지원<br /><br /> SQL_OSC_EXTENDED = 확장 된 문법 지원|  
|SQL_POS_OPERATIONS (ODBC 2.0)|**SQLSetPos에서**지원되는 작업을 예인하는 SQLINTEGER 비트 마스크.<br /><br /> 다음 비트마스크는 플래그와 함께 지원되는 옵션을 결정하는 데 사용됩니다.<br /><br /> SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)|  
|SQL_POSITIONED_STATEMENTS (ODBC 2.0)|지원되는 위치가 지정된 SQL 문을 등록하는 SQLINTEGER 비트 마스크입니다.<br /><br /> 다음 비트 마스크는 지원되는 문을 결정하는 데 사용됩니다.<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1.0)|커서에 지원되는 동시성 제어 옵션을 영예하는 SQLINTEGER 비트 마스크입니다.<br /><br /> 다음 비트마스크는 지원되는 옵션을 결정하는 데 사용됩니다.<br /><br /> SQL_SCCO_READ_ONLY = 커서읽기 전용입니다. 업데이트는 허용되지 않습니다.<br /><br /> SQL_SCCO_LOCK = 커서는 행을 업데이트할 수 있도록 충분한 최하위 잠금 수준을 사용합니다.<br /><br /> SQL_SCCO_OPT_ROWVER = 커서는 SQLBase ROWID 또는 Sybase TIMESTAMP와 같은 행 버전을 비교하는 낙관적 동시성 컨트롤을 사용합니다.<br /><br /> SQL_SCCO_OPT_VALUES = 커서는 값을 비교하여 낙관적 동시성 컨트롤을 사용합니다.|  
|SQL_STATIC_SENSITIVITY (ODBC 2.0)|**SQLSetPos** 또는 위치 업데이트 또는 삭제 문을 통해 정적 또는 키 집합 기반 커서에 응용 프로그램에 의해 변경 내용을 열거 하는 SQLINTEGER 비트 마스크 는 해당 응용 프로그램에서 검색할 수 있습니다.<br /><br /> SQL_SS_ADDITIONS = 추가된 행이 커서에 표시됩니다. 커서는 이러한 행으로 스크롤할 수 있습니다. 이러한 행이 커서에 추가되는 위치는 드라이버에 따라 다릅니다.<br /><br /> SQL_SS_DELETIONS = 삭제된 행은 더 이상 커서에서 사용할 수 없으며 결과 집합에 "구멍"을 남기지 않습니다. 커서가 삭제된 행에서 스크롤된 후에는 해당 행으로 돌아갈 수 없습니다.<br /><br /> SQL_SS_UPDATES = 행에 대한 업데이트는 커서에 표시됩니다. 커서가 에서 스크롤되어 업데이트된 행으로 돌아오면 커서에서 반환되는 데이터는 원래 데이터가 아닌 업데이트된 데이터입니다. 이 옵션은 키를 업데이트하지 않는 키 집합 기반 커서의 정적 커서 또는 업데이트에만 적용됩니다. 동적 커서 또는 혼합 커서에서 키가 변경되는 경우에는 이 옵션이 적용되지 않습니다.<br /><br /> 응용 프로그램이 동일한 응용 프로그램의 다른 커서를 포함하여 다른 사용자가 설정한 결과에 대한 변경 내용을 검색할 수 있는지 여부는 커서 유형에 따라 다릅니다.|  
  
 ODBC 3 *.x* 드라이버로 작업하는 ODBC 3 *.x* 응용 프로그램은 다음 단락에 나열된 *ODBC* 3 *.x* *InfoType* 인수를 사용하여 **SQLGetInfo를** 호출하지 않아야 합니다. ODBC 2에 사용되는 *InfoType* 인수 간에는 일대일 대응이 없습니다. *x* 와 ODBC 3 *.x에*사용되는 사람들 . ODBC 2로 작동하는 ODBC*3.x* 응용 프로그램입니다. *반면 x* 드라이버는 앞서 설명한 *InfoType* 인수를 사용해야 합니다.  
  
 이전 테이블의 일부 정보 형식은 커서 특성 정보 형식에 더 이상 사용되지 않습니다. 이러한 사용되지 않는 정보 유형은 SQL_FETCH_DIRECTION, SQL_LOCK_TYPES, SQL_POS_OPERATIONS, SQL_POSITIONED_STATEMENTS, SQL_SCROLL_CONCURRENCY 및 SQL_STATIC_SENSITIVITY. 새 커서 특성 유형은 xxx가 동적, FORWARD_ONLY, KEYSET_DRIVEN 또는 STATIC과 SQL_XXX_CURSOR_ATTRIBUTES1and SQL_XXX_CURSOR_ATTRIBUTES2. 각각의 새 형식은 단일 커서 유형에 대한 드라이버 기능을 나타냅니다. 이러한 옵션에 대한 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명을 참조하십시오.
