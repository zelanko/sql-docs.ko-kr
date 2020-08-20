---
description: SQLGetInfo 지원
title: SQLGetInfo 지원 | Microsoft Docs
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
ms.openlocfilehash: cff18a23c7d8c4526fc86904d75375ed5aaaf5a7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471234"
---
# <a name="sqlgetinfo-support"></a>SQLGetInfo 지원
ODBC 2 인 경우 *x* 응용 프로그램은 **SQLGetInfo** 를 ODBC 3.x*드라이버에* 호출 하 고 다음 표에 있는 *InfoType* 인수를 지원 해야 합니다.  
  
|*InfoType*|반환|  
|----------------|-------------|  
|SQL_ALTER_TABLE (ODBC 2.0) **참고:**  이 정보 형식은 더 이상 사용 되지 않습니다. 오른쪽에 있는 열의 비트 마스크는 사용 되지 않습니다.|데이터 원본에서 지 원하는 **ALTER TABLE** 문의 절을 열거 하는 sqlinteger 비트 마스크입니다.<br /><br /> 지원 되는 절을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br /><br /> SQL_AT_DROP_COLUMN = 열을 삭제 하는 기능이 지원 됩니다. 이로 인해 cascade 또는 restrict 동작이 적용 되는지 여부는 드라이버에 의해 정의 됩니다. (ODBC 2.0)<br /><br /> SQL_AT_ADD_COLUMN = 단일 ALTER TABLE 문에 여러 열을 추가 하는 기능이 지원 됩니다. 이 비트는 다른 SQL_AT_ADD_COLUMN_XXX 비트 또는 SQL_AT_CONSTRAINT_XXX 비트와 함께 사용 되지 않습니다. (ODBC 2.0)|  
|SQL_FETCH_DIRECTION (ODBC 1.0)<br /><br /> 정보 유형은 ODBC 1.0에서 도입 되었습니다. 각 비트 마스크는 도입 된 버전으로 레이블이 지정 됩니다.|지원 되는 fetch 방향 옵션을 열거 하는 SQLINTEGER 비트 마스크입니다.<br /><br /> 다음 비트 마스크는 플래그와 함께 사용 되어 지원 되는 옵션을 결정 합니다.<br /><br /> SQL_FD_FETCH_NEXT (ODBC 1.0) SQL_FD_FETCH_FIRST (ODBC 1.0) SQL_FD_FETCH_LAST (ODBC 1.0) SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_ABSOLUTE (ODBC 1.0) SQL_FD_FETCH_RELATIVE (ODBC 1.0) SQL_FD_FETCH_BOOKMARK (ODBC 2.0) (ODBC)|  
|SQL_LOCK_TYPES (ODBC 2.0)|**SQLSetPos**의 *fLock* 인수에 대해 지원 되는 잠금 유형을 열거 하는 sqlinteger 비트 마스크입니다.<br /><br /> 다음 비트 마스크는 플래그와 함께 사용 되어 지원 되는 잠금 유형을 결정 합니다.<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1.0)|ODBC 규칙의 수준을 나타내는 SQLSMALLINT 값입니다.<br /><br /> SQL_OAC_NONE = 없음<br /><br /> SQL_OAC_LEVEL1 = 수준 1 지원 됨<br /><br /> SQL_OAC_LEVEL2 = 수준 2 지원 됨|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1.0)|드라이버에서 지 원하는 SQL 문법을 나타내는 SQLSMALLINT 값입니다. SQL 규칙 수준 정의는 [부록 C: Sql 문법](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md) 을 참조 하세요.<br /><br /> SQL_OSC_MINIMUM = 지원 되는 최소 문법<br /><br /> SQL_OSC_CORE = 코어 문법이 지원 됨<br /><br /> SQL_OSC_EXTENDED = 확장 된 문법이 지원 됨|  
|SQL_POS_OPERATIONS (ODBC 2.0)|**SQLSetPos**에서 지원 되는 작업을 열거 하는 sqlinteger 비트 마스크입니다.<br /><br /> 다음 비트 마스크는 플래그와 함께 지원 되는 옵션을 결정 하는 데 사용 됩니다.<br /><br /> SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)|  
|SQL_POSITIONED_STATEMENTS (ODBC 2.0)|지원 되는 위치 지정 SQL 문을 열거 하는 SQLINTEGER 비트 마스크입니다.<br /><br /> 다음 비트 마스크는 지원 되는 문을 결정 하는 데 사용 됩니다.<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1.0)|커서에 대해 지원 되는 동시성 제어 옵션을 열거 하는 SQLINTEGER 비트 마스크입니다.<br /><br /> 지원 되는 옵션을 결정 하는 데 사용 되는 비트 마스크는 다음과 같습니다.<br /><br /> SQL_SCCO_READ_ONLY = 커서가 읽기 전용입니다. 업데이트는 허용 되지 않습니다.<br /><br /> SQL_SCCO_LOCK = 커서는 행이 업데이트 될 수 있도록 가장 낮은 수준의 잠금을 사용 합니다.<br /><br /> SQL_SCCO_OPT_ROWVER = 커서는 SQLBase ROWID 또는 Sybase TIMESTAMP와 같은 행 버전을 비교 하 여 낙관적 동시성 제어를 사용 합니다.<br /><br /> SQL_SCCO_OPT_VALUES = 커서는 낙관적 동시성 제어를 사용 하 여 값을 비교 합니다.|  
|SQL_STATIC_SENSITIVITY (ODBC 2.0)|응용 프로그램에서 **SQLSetPos** 또는 배치 된 update 또는 delete 문을 통해 정적 또는 키 집합 커서에 대 한 응용 프로그램의 변경 내용을 검색할 수 있는지 여부를 열거 하는 sqlinteger 비트 마스크입니다.<br /><br /> SQL_SS_ADDITIONS = 추가 된 행이 커서에 표시 됩니다. 커서는 이러한 행으로 스크롤할 수 있습니다. 이러한 행이 커서에 추가 되는 위치는 드라이버에 따라 다릅니다.<br /><br /> SQL_SS_DELETIONS = 삭제 된 행은 커서에서 더 이상 사용할 수 없으며 결과 집합에 "hole"을 두지 않습니다. 삭제 된 행에서 커서를 스크롤한 후에는 해당 행으로 돌아갈 수 없습니다.<br /><br /> SQL_SS_UPDATES = 행에 대 한 업데이트가 커서에 표시 됩니다. 커서가에서 스크롤하고 업데이트 된 행으로 반환 되는 경우 커서가 반환한 데이터는 원래 데이터가 아닌 업데이트 된 데이터입니다. 이 옵션은 키를 업데이트 하지 않는 키 집합 커서에 대 한 정적 커서 또는 업데이트에만 적용 됩니다. 이 옵션은 동적 커서에는 적용 되지 않으며 혼합 커서에서 키가 변경 된 경우에는 적용 되지 않습니다.<br /><br /> 응용 프로그램이 같은 응용 프로그램의 다른 커서를 비롯 하 여 다른 사용자가 결과 집합에 적용 한 변경 내용을 검색할 수 있는지 여부는 커서 유형에 따라 달라 집니다.|  
  
 Odbc*3.x 드라이버를* 사용 하 여 작업 하는 odbc*2.x 응용 프로그램* 은 위의 표에 설명 된 *InfoType* 인수를 사용 하 여 **SQLGetInfo** 를 호출 해서는 안 되지만, 다음 단락에 나열 된*odbc 3(sp3)* *InfoType* 인수를 사용 해야 합니다. ODBC 2에서 사용 되는 *InfoType* 인수 간에는 일대일 대응이 없습니다. *x* 및 ODBC 3.x에서 사용 되는*것입니다.* Odbc 3 *. x* 응용 프로그램은 odbc 2를 사용 하 여 작동 합니다. 반면 *x* 드라이버는 앞에서 설명한 *InfoType* 인수를 사용 해야 합니다.  
  
 위의 표에 나와 있는 일부 정보 유형은 커서 특성 정보 유형을 위해 더 이상 사용 되지 않습니다. 이러한 사용 되지 않는 정보 유형은 SQL_FETCH_DIRECTION, SQL_LOCK_TYPES, SQL_POS_OPERATIONS, SQL_POSITIONED_STATEMENTS, SQL_SCROLL_CONCURRENCY, SQL_STATIC_SENSITIVITY입니다. 새 커서 특성 유형은 SQL_XXX_CURSOR_ATTRIBUTES2 SQL_XXX_CURSOR_ATTRIBUTES1and 됩니다. 여기서 XXX는 DYNAMIC, FORWARD_ONLY, KEYSET_DRIVEN 또는 STATIC입니다. 각 새 형식은 단일 커서 유형에 대 한 드라이버 기능을 나타냅니다. 이러한 옵션에 대 한 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명을 참조 하세요.
