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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb9677a9ccf307be847089c657964d96904eb20b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299403"
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함 되어 있습니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 지원: 전체  
  
 ODBC API 규칙: 수준 1  
  
 문 핸들 *hstmt*와 관련 된 옵션을 설정 합니다.  
  
|*fOption*|허용되는 값|주석|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|이 *Foption*을 설정 하려고 하면 "드라이버를 사용할 수 없음" 오류가 반환 됩니다. Visual FoxPro는 비동기 실행을 지원 하지 않습니다.|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN 또는 결과 열이 바인딩될 버퍼의 인스턴스 또는 구조의 길이를 나타내는 32 비트 값입니다.||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|Visual FoxPro에는 타임 스탬프를 기반으로 하는 행 버전 관리가 없으므로 드라이버는 SQL_CONCUR_ROWVER을 허용 하지 않습니다.|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|드라이버가 SQL_CURSOR_KEYSET_DRIVEN 또는 SQL_CURSOR_DYNAMIC을 허용 하지 않습니다. 자세한 내용은 [SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) 를 참조 하세요.|  
|SQL_KEYSET_SIZE|오류: "드라이버를 사용할 수 없음"|Visual FoxPro는 키 집합 커서 모델을 지원 하지 않습니다.|  
|SQL_MAX_LENGTH|0|이 *Foption* 값을 설정 하려고 하면 드라이버가 "드라이버를 사용할 수 없음" 오류를 반환 합니다.|  
|SQL_MAX_ROWS|0|이 *Foption* 값을 설정 하려고 하면 드라이버가 "드라이버를 사용할 수 없음" 오류를 반환 합니다.|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|이 *Foption* 값을 설정 하려고 하면 드라이버가 "드라이버를 사용할 수 없음" 오류를 반환 합니다.|  
|SQL_RETRIEVE_DATA|SQL_RD_ON, SQL_RD_OFF||  
|SQL_ROWSET_SIZE|1 ~ 4294967296||  
|SQL_SIMULATE_CURSOR|오류: "드라이버를 사용할 수 없음"||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 자세한 내용은 *ODBC 프로그래머 참조*에서 [SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md) 를 참조 하세요.
