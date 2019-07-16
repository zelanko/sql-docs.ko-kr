---
title: SQLSetStmtOption (Visual FoxPro ODBC 드라이버) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a026922cb98fdb520c9eeab223c8b34a231a179e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905335"
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보를 포함합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 ODBC API 규칙: 수준 1  
  
 문 핸들을 관련 된 옵션을 설정 합니다 *hstmt*합니다.  
  
|*fOption*|허용된 값|주석|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|이 설정 하려고 하면 *fOption*, 드라이버에 오류를 반환 합니다. "드라이버 사용할 수 없습니다."입니다. Visual FoxPro 비동기 실행을 지원 하지 않습니다.|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN 또는 결과에 열 바인딩될 버퍼 인스턴스나 구조의 길이 나타내는 32 비트 값입니다.||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|Visual FoxPro에 타임 스탬프에 따라 행 버전 관리 없기 때문에 드라이버 SQL_CONCUR_ROWVER을 허용 하지 않습니다.|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|SQL_CURSOR_KEYSET_DRIVEN 또는 SQL_CURSOR_DYNAMIC; 드라이버 허용 되지 않습니다. 참조 [SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) 자세한 내용은 합니다.|  
|SQL_KEYSET_SIZE|오류: "드라이버를 사용할 수 없습니다."|Visual FoxPro 키 집합 커서 모델을 지원 하지 않습니다.|  
|SQL_MAX_LENGTH|0|이 설정 하려고 하면 *fOption* 값 드라이버 오류를 반환 합니다 "드라이버를 사용할 수 없습니다."입니다.|  
|SQL_MAX_ROWS|0|이 설정 하려고 하면 *fOption* 값 드라이버 오류를 반환 합니다 "드라이버를 사용할 수 없습니다."입니다.|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|이 설정 하려고 하면 *fOption* 값 드라이버 오류를 반환 합니다 "드라이버를 사용할 수 없습니다."입니다.|  
|SQL_RETRIEVE_DATA|SQL_RD_ON, SQL_RD_OFF||  
|SQL_ROWSET_SIZE|4,294,967,296에 1||  
|SQL_SIMULATE_CURSOR|오류: "드라이버를 사용할 수 없습니다."||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 자세한 내용은 [SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md) 에 *ODBC 프로그래머 참조*합니다.
