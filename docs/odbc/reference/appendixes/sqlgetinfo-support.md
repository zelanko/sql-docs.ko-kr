---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6eb6bedb20e1f61c48776d03df59aa6865cfb2a3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62751213"
---
# <a name="sqlgetinfo-support"></a>SQLGetInfo 지원
경우는 ODBC 2. *x* 응용 프로그램 호출 **SQLGetInfo** 는 ODBC 3 *.x* 드라이버를 *정보 항목* 다음 표에 인수를 지원 해야 합니다.  
  
|*InfoType*|반환 값|  
|----------------|-------------|  
|(ODBC 2.0) SQL_ALTER_TABLE **참고 합니다.**  이 정보 유형은 되지; 열 오른쪽에 있는 비트 마스크가 사용 되지 않습니다.|절을 열거 하는 SQLINTEGER 비트 마스크를 **ALTER TABLE** 데이터 원본에서 지 원하는 문입니다.<br /><br /> 다음 비트 마스크는 절이 지원 되는지 확인 하는 데 사용 됩니다.<br /><br /> SQL_AT_DROP_COLUMN = 열을 삭제 하는 기능이 지원 됩니다. Cascade 결과 또는 동작을 제한할이 있는지 여부를 드라이버 정의 됩니다. (ODBC 2.0)<br /><br /> SQL_AT_ADD_COLUMN = 단일 ALTER TABLE 문에서 여러 열에는 추가할 수 있습니다. 이 비트 다른 SQL_AT_ADD_COLUMN_XXX 비트 또는 SQL_AT_CONSTRAINT_XXX 비트를 사용 하 여 결합 되지 않습니다. (ODBC 2.0)|  
|SQL_FETCH_DIRECTION (ODBC 1.0)<br /><br /> 정보 유형 ODBC 1.0;에 도입 합니다. 각 비트 마스크는 이전에 도입 된 버전을 사용 하 여 레이블이 지정 됩니다.|지원 되는 인출 방향 옵션을 열거 SQLINTEGER 비트 마스크입니다.<br /><br /> 다음 비트 마스크는 어떤 옵션이 지원 되는지 확인 하려면 플래그와 함께에서 사용 됩니다.<br /><br /> (ODBC 1.0) SQL_FD_FETCH_NEXT SQL_FD_FETCH_FIRST (ODBC 1.0) SQL_FD_FETCH_LAST (ODBC 1.0) SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_ABSOLUTE (ODBC 1.0) SQL_FD_FETCH_RELATIVE (ODBC 1.0) SQL_FD_FETCH_BOOKMARK (ODBC 2.0)|  
|SQL_LOCK_TYPES (ODBC 2.0)|지원 되는 잠금 열거 하는 SQLINTEGER 비트 마스크 형식에 대 한 합니다 *떼* 에서 인수 **SQLSetPos**합니다.<br /><br /> 다음 비트 마스크는 잠금 유형을 지원 되는지 확인 하는 플래그와 함께에서 사용 됩니다.<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1.0)|ODBC 규칙 수준을 나타내는 SQLSMALLINT 값입니다.<br /><br /> SQL_OAC_NONE = 없음<br /><br /> SQL_OAC_LEVEL1 = 수준 1 지원<br /><br /> SQL_OAC_LEVEL2 = 수준 2 지원|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1.0)|드라이버에서 지 원하는 SQL 문법 나타내는 SQLSMALLINT 값입니다. 참조 [부록 c: SQL 문법을](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md) SQL 적합성 수준의 정의 합니다.<br /><br /> SQL_OSC_MINIMUM 지원 되는 최소 문법 =<br /><br /> SQL_OSC_CORE 지원 되는 핵심 문법 =<br /><br /> SQL_OSC_EXTENDED 지원 되는 확장 문법 =|  
|SQL_POS_OPERATIONS (ODBC 2.0)|지원 되는 작업을 열거 하는 SQLINTEGER 비트 마스크 **SQLSetPos**합니다.<br /><br /> 다음 비트 마스크는 어떤 옵션이 지원 되는지 확인 하려면 플래그와 함께에서 사용 됩니다.<br /><br /> SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH   (ODBC 2.0) SQL_POS_UPDATE     (ODBC 2.0) SQL_POS_DELETE     (ODBC 2.0) SQL_POS_ADD          (ODBC 2.0)|  
|SQL_POSITIONED_STATEMENTS (ODBC 2.0)|지원 되는 열거 하는 SQLINTEGER 비트 마스크에는 SQL 문을 배치 합니다.<br /><br /> 다음 비트 마스크는 문을 지원 되는지 확인 하는 데 사용 됩니다.<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1.0)|커서에 대해 지원 되는 동시성 제어 옵션을 열거 SQLINTEGER 비트 마스크입니다.<br /><br /> 다음 비트 마스크는 어떤 옵션이 지원 되는지 확인 하는 데 사용 됩니다.<br /><br /> SQL_SCCO_READ_ONLY = 읽기 전용 커서입니다. 업데이트할 수 없습니다.<br /><br /> SQL_SCCO_LOCK = 커서 사용 하 여 가장 낮은 수준의 잠금을 행을 업데이트할 수 있는지 확인 하는 데 충분 합니다.<br /><br /> SQL_SCCO_OPT_ROWVER = 커서 사용 하 여 낙관적 동시성 제어를 SQLBase ROWID 또는 Sybase 타임 스탬프와 같은 행 버전을 비교 합니다.<br /><br /> SQL_SCCO_OPT_VALUES = 커서 사용 하 여 낙관적 동시성 제어, 값을 비교 합니다.|  
|SQL_STATIC_SENSITIVITY (ODBC 2.0)|응용 프로그램을 통해 정적 또는 키 집합 커서에 의해 변경 여부를 열거 SQLINTEGER 비트 마스크 **SQLSetPos** 또는 해당 응용 프로그램에서 위치 지정된 update 또는 delete 문을 검색할 수 있습니다.<br /><br /> SQL_SS_ADDITIONS Added = 행은 커서에 표시 됩니다. 커서는 이러한 행을 스크롤할 수 있습니다. 이러한 행이 커서에 추가 하는 위치는 드라이버에 따라 다릅니다.<br /><br /> SQL_SS_DELETIONS = 삭제 된 행에 커서를 사용할 수 없게 됩니다 및 결과 집합에 "구멍" 두지 마십시오 커서가 삭제 된 행을 스크롤하면 후에 해당 행을 반환할 수 없습니다.<br /><br /> SQL_SS_UPDATES = 행에 대 한 업데이트는 커서에 표시 됩니다. 커서에서 스크롤 하는 업데이트 된 행을 반환 하는 경우 커서에 의해 반환 되는 데이터는 업데이트 된 데이터를 원래 데이터가 아니라입니다. 이 옵션의 키를 업데이트 하려면 키 집합 커서에만 정적 커서 또는 업데이트를 적용 합니다. 혼합된 커서에서 키를 변경 하는 경우 또는 동적 커서에이 옵션이 적용 되지 않습니다.<br /><br /> 응용 프로그램 다른 사용자가 동일한 응용 프로그램에 다른 커서를 포함 하 여 결과 집합에 대 한 변경 내용을 감지할 수 있는지 여부를 커서 유형에 따라 다릅니다.|  
  
 ODBC 3 *.x* 는 ODBC 3을 사용 하는 응용 프로그램 *.x* 드라이버를 호출 하지 않아야 **SQLGetInfo** 사용 하 여 합니다 *정보 항목* 에 설명 된 인수 위의 테이블에 있지만 ODBC 3 사용할지 *.x* *정보 항목* 다음 단락에 나열 된 인수입니다. 한 일 대응 되지 *정보 항목* ODBC 2에서 사용 되는 인수입니다. *x* 고 ODBC 3에서 사용 되는 *.x*합니다. ODBC 3 *.x* 응용 프로그램을 사용 하는 ODBC 2. *x* 반면에 드라이버를 사용 해야 합니다 *정보 항목* 인수 앞에서 설명한 합니다.  
  
 이전 테이블의 정보 유형 중 일부는 커서 특성 정보 형식을 대신 사용 되지 않습니다. 이러한 유형은 SQL_FETCH_DIRECTION, SQL_LOCK_TYPES, SQL_POS_OPERATIONS, SQL_POSITIONED_STATEMENTS, SQL_SCROLL_CONCURRENCY, 및 SQL_STATIC_SENSITIVITY 정보를 사용 되지 않습니다. 새 커서 특성 유형은 SQL_XXX_CURSOR_ATTRIBUTES1and SQL_XXX_CURSOR_ATTRIBUTES2, 여기서 XXX은 DYNAMIC, FORWARD_ONLY, KEYSET_DRIVEN, 또는 STATIC입니다. 새 형식의 각 단일 커서 유형에 대해 드라이버 기능을 나타냅니다. 이러한 옵션에 대 한 자세한 내용은 참조는 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 합니다.
