---
title: SQLSetStmtOption (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 76b813e3-c7dc-4bb2-a710-d2aa9dcfdc36
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5ff8c2b1d58e3cd9f309290ed7f86acb15521d89
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption (Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보입니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 수준 1 ODBC API 적용:  
  
 문 핸들에 관련 된 옵션 설정 *hstmt*합니다.  
  
|*fOption*|허용된 값|설명|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|이 설정 하려고 하면 *fOption*, 드라이버는 오류를 반환 합니다.: "드라이버를 사용할 수 없습니다."입니다. Visual FoxPro 비동기 실행을 지원 하지 않습니다.|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN 또는 결과에 열이 바인딩될 버퍼 인스턴스나 구조의 길이 나타내는 32 비트 값입니다.||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|Visual FoxPro에 타임 스탬프에 따라 행 버전 관리 없기 때문에 드라이버가 SQL_CONCUR_ROWVER을 허용 하지 않습니다.|  
|에서는 SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|드라이버는 SQL_CURSOR_KEYSET_DRIVEN 또는 SQL_CURSOR_DYNAMIC; 수 없습니다. 참조 [SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) 자세한 정보에 대 한 합니다.|  
|SQL_KEYSET_SIZE|오류: "드라이버 사용할 수 없습니다.|Visual FoxPro 키 집합 커서 모델을 지원 하지 않습니다.|  
|SQL_MAX_LENGTH|0|이 설정 하려고 하면 *fOption* 값 이면 드라이버 반환 오류 "드라이버를 사용할 수 없습니다."입니다.|  
|SQL_MAX_ROWS|0|이 설정 하려고 하면 *fOption* 값 이면 드라이버 반환 오류 "드라이버를 사용할 수 없습니다."입니다.|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|이 설정 하려고 하면 *fOption* 값 이면 드라이버 반환 오류 "드라이버를 사용할 수 없습니다."입니다.|  
|SQL_RETRIEVE_DATA|SQL_RD_ON, SQL_RD_OFF||  
|SQL_ROWSET_SIZE|1을 4294967296||  
|SQL_SIMULATE_CURSOR|오류: "드라이버 사용할 수 없습니다.||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 자세한 내용은 참조 [SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md) 에 *ODBC Programmer's Reference*합니다.
