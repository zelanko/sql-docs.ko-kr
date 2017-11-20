---
title: "SQLGetInfo 지원 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], SQLGetInfo
- backward compatibility [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], support
ms.assetid: 57326f57-daba-46b6-b0be-6c97213b9ef1
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fb9afa5b40ffa7628e04ee85e5ddc4f752e98935
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetinfo-support"></a>SQLGetInfo 지원
경우는 ODBC 2. *x* 응용 프로그램 호출 **SQLGetInfo** ODBC 3*.x* 드라이버는 *정보 항목* 인수는 다음 표에 지원 되어야 합니다.  
  
|*정보 항목*|반환 값|  
|----------------|-------------|  
|SQL_ALTER_TABLE (ODBC 2.0) **참고:** 이 정보 유형을 사용 되지 않으면 오른쪽 열에 비트 마스크는 사용 되지 않습니다.|절을 열거 하는 SQLINTEGER 비트 마스크는 **ALTER TABLE** 데이터 소스에서 지 원하는 문입니다.<br /><br /> 다음 비트 마스크는 절이 지원 되는지 확인 하는 데 사용 됩니다.<br /><br /> SQL_AT_DROP_COLUMN =은 열을 삭제 하는 기능을 지원 합니다. 계단식으로 인해이 또는 동작을 제한할 여부는 드라이버 정의입니다. (ODBC 2.0)<br /><br /> SQL_AT_ADD_COLUMN = 단일 ALTER TABLE 문의 여러 열을에서 사용할 수를 추가할 수 있습니다. 이 비트 다른 SQL_AT_ADD_COLUMN_XXX 비트 또는 SQL_AT_CONSTRAINT_XXX 비트와 결합 되지 않습니다. (ODBC 2.0)|  
|SQL_FETCH_DIRECTION (ODBC 1.0)<br /><br /> 정보 유형; ODBC 1.0에 도입 된 각 비트 마스크 도입 된 버전으로 표시 됩니다.|지원 되는 인출 방향 옵션을 열거 SQLINTEGER 비트 마스크입니다.<br /><br /> 다음 비트 마스크 옵션이 지원 되는지 확인 하는 플래그와 함께에서 사용 됩니다.<br /><br /> SQL_FD_FETCH_NEXT (ODBC 1.0) (ODBC 1.0) SQL_FD_FETCH_FIRST SQL_FD_FETCH_LAST (ODBC 1.0) (ODBC 1.0) SQL_FD_FETCH_PRIOR SQL_FD_FETCH_ABSOLUTE (ODBC 1.0) (ODBC 1.0) SQL_FD_FETCH_RELATIVE SQL_FD_FETCH_BOOKMARK (ODBC 2.0)|  
|SQL_LOCK_TYPES (ODBC 2.0)|에 대 한 지원 되는 잠금을 열거 하는 SQLINTEGER 비트 마스크 형식이 고 *떼* 인수에 **SQLSetPos**합니다.<br /><br /> 다음 비트 마스크는 지원 되는 잠금 유형을 결정 하는 플래그와 함께에서 사용 됩니다.<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1.0)|SQLSMALLINT ODBC 규칙 수준을 나타내는 값입니다.<br /><br /> SQL_OAC_NONE = 없음<br /><br /> SQL_OAC_LEVEL1 = 수준 1 지원<br /><br /> SQL_OAC_LEVEL2 지원 수준 2 =|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1.0)|드라이버에서 지 원하는 SQL 문법 나타내는 SQLSMALLINT 값입니다. 참조 [부록 c: SQL 문법을](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md) SQL 받는 규칙 수준에 대 한 정의 대 한 합니다.<br /><br /> Sql_osc_minimum이 합니다 = 최소 문법 지원<br /><br /> SQL_OSC_CORE = 코어 문법 지원<br /><br /> SQL_OSC_EXTENDED = 확장 문법 지원|  
|SQL_POS_OPERATIONS (ODBC 2.0)|지원 되는 작업을 열거 하는 SQLINTEGER 비트 마스크 **SQLSetPos**합니다.<br /><br /> 다음 비트 마스크 옵션이 지원 되는지 확인 하려면를 플래그와 함께에서 사용 됩니다.<br /><br /> SQL_POS_POSITION (ODBC 2.0) (ODBC 2.0) SQL_POS_REFRESH SQL_POS_UPDATE (ODBC 2.0) (ODBC 2.0) SQL_POS_DELETE SQL_POS_ADD (ODBC 2.0)|  
|SQL_POSITIONED_STATEMENTS (ODBC 2.0)|지원 되는 열거 하는 SQLINTEGER 비트 마스크 SQL 문을 배치 합니다.<br /><br /> 다음 비트 마스크 문을 지원 되는지 확인 하는 데 사용 됩니다.<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1.0)|커서에 대해 지원 되는 동시성 제어 옵션을 열거 SQLINTEGER 비트 마스크입니다.<br /><br /> 다음 비트 마스크 옵션이 지원 되는지 확인 하는 데 사용 됩니다.<br /><br /> SQL_SCCO_READ_ONLY = 커서는 읽기 전용입니다. 업데이트할 수 없습니다.<br /><br /> SQL_SCCO_LOCK = 커서 사용 하 여 가장 낮은 수준의 잠금을 행을 업데이트할 수 있는지 확인 하는 데 충분 합니다.<br /><br /> SQL_SCCO_OPT_ROWVER = 커서 사용 하 여 낙관적 동시성 제어를 SQLBase ROWID 또는 Sybase 타임 스탬프와 같은 행 버전을 비교 합니다.<br /><br /> SQL_SCCO_OPT_VALUES = 커서 사용 하 여 낙관적 동시성 제어를 값을 비교 합니다.|  
|SQL_STATIC_SENSITIVITY (ODBC 2.0)|응용 프로그램을 통해 정적 또는 키 집합 커서에 의해 변경 여부을 열거 SQLINTEGER 비트 마스크 **SQLSetPos** 위치 지정된 update 또는 delete 문을 해당 응용 프로그램에서 검색할 수 있습니다.<br /><br /> SQL_SS_ADDITIONS Added = 행; 커서에 표시 됩니다. 이러한 행에 커서를 스크롤할 수 있습니다. 이러한 행이 커서에 추가 하는 위치는 드라이버에 따라 다릅니다.<br /><br /> SQL_SS_DELETIONS = 삭제 된 행이 커서를 사용할 수 있는 더 이상 되 고 결과 집합에 "구멍" 형태로 두지 마십시오 커서가 삭제 된 행을 스크롤하면 후 해당 행을 반환할 수 없습니다.<br /><br /> SQL_SS_UPDATES = 행에 대 한 업데이트는 커서를에 표시 됩니다. 커서를 스크롤 하 고 업데이트 된 행에을 반환 하는 경우 커서에 의해 반환 되는 데이터는 업데이트 된 데이터 원본 데이터가 아닌 합니다. 이 옵션의 키를 업데이트 하지 않으면 키 집합 커서에만 정적 커서 또는 업데이트를 적용 합니다. 이 옵션에는 혼합 된 커서의 키를 변경 하는 경우 또는 동적 커서에 대 한 적용 되지 않습니다.<br /><br /> 응용 프로그램 변경 내용을 다른 사용자가 동일한 응용 프로그램에 다른 커서를 포함 하 여 결과 집합을 검색할 수 있는지 여부를 커서 유형에 따라 다릅니다.|  
  
 ODBC 3*.x* ODBC 3을 사용 하는 응용 프로그램*.x* 드라이버를 호출 하지 않아야 **SQLGetInfo** 와 *정보 항목* 에 설명 된 인수 테이블 위의 있지만 ODBC 3을 사용 해야*.x* *정보 항목* 다음 단락에 인수를 나열 합니다. 간의 한 일 대응 하지는 않습니다 *정보 항목* ODBC 2에서 사용 되는 인수. *x* 고 ODBC 3에서 사용 되는*.x*합니다. ODBC 3*.x* 응용 프로그램을 사용 하는 ODBC 2. *x* 반면에 드라이버를 사용 해야는 *정보 항목* 인수 앞에서 설명한 합니다.  
  
 이전 테이블의 정보 유형 중 일부는 커서 특성 정보 유형이 하기 위해 사용 되지 않습니다. 이러한 유형은 SQL_FETCH_DIRECTION, SQL_LOCK_TYPES, SQL_POS_OPERATIONS, SQL_POSITIONED_STATEMENTS, SQL_SCROLL_CONCURRENCY, 및 SQL_STATIC_SENSITIVITY 정보를 사용 되지 않습니다. 새 커서 특성 유형은 SQL_XXX_CURSOR_ATTRIBUTES1and SQL_XXX_CURSOR_ATTRIBUTES2, 여기서 XXX은 DYNAMIC, FORWARD_ONLY, KEYSET_DRIVEN, 또는 STATIC입니다. 각 새로운 유형의 단일 커서 유형에 대 한 드라이버 기능을 나타냅니다. 이러한 옵션에 대 한 자세한 내용은 참조는 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 합니다.

