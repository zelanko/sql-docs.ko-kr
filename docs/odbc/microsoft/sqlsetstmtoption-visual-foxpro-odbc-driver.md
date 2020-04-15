---
title: SQLSetStmt옵션 (비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 76b813e3-c7dc-4bb2-a710-d2aa9dcfdc36
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb9677a9ccf307be847089c657964d96904eb20b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299403"
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함되어 있습니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 지원: 전체  
  
 ODBC API 적합성: 레벨 1  
  
 명령문 핸들, *hstmt와*관련된 옵션을 설정합니다.  
  
|*f옵션*|허용되는 값|주석|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|이 *fOption을*설정하려고 하면 드라이버가 "드라이버를 사용할 수 없습니다"라는 오류를 반환합니다. Visual FoxPro는 비동기 실행을 지원하지 않습니다.|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN 또는 구조의 길이 또는 결과 열이 바인딩될 버퍼의 인스턴스를 나타내는 32비트 값입니다.||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|Visual FoxPro에는 타임스탬프를 기반으로 한 행 버전 전환이 없기 때문에 드라이버는 SQL_CONCUR_ROWVER 허용하지 않습니다.|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|운전자는 SQL_CURSOR_KEYSET_DRIVEN 또는 SQL_CURSOR_DYNAMIC 허용하지 않습니다. 자세한 내용은 [SQLSetScroll옵션을](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) 참조하십시오.|  
|SQL_KEYSET_SIZE|오류: "드라이버를 수행할 수 없습니다."|Visual FoxPro는 키집합 커서 모델을 지원하지 않습니다.|  
|SQL_MAX_LENGTH|0|이 *fOption* 값을 설정하려고 하면 드라이버가 "드라이버를 사용할 수 없음"이라는 오류를 반환합니다.|  
|SQL_MAX_ROWS|0|이 *fOption* 값을 설정하려고 하면 드라이버가 "드라이버를 사용할 수 없음"이라는 오류를 반환합니다.|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|이 *fOption* 값을 설정하려고 하면 드라이버가 "드라이버를 사용할 수 없음"이라는 오류를 반환합니다.|  
|SQL_RETRIEVE_DATA|SQL_RD_ON, SQL_RD_OFF||  
|SQL_ROWSET_SIZE|1 ~ 4,294,967,296||  
|SQL_SIMULATE_CURSOR|오류: "드라이버를 수행할 수 없습니다."||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 자세한 내용은 *ODBC 프로그래머의 참조에서* [SQLSetStmtOption을](../../odbc/reference/syntax/sqlsetstmtoption-function.md) 참조하십시오.
