---
title: SQLSetStmtAttr (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLSetStmtAttr function [ODBC], Cursor Library
ms.assetid: 6018a733-c2c8-4047-92ec-92cf85031767
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d707170f7e321ce41d096da6651c0e825621713
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr (커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목의 사용을 설명는 **SQLSetStmtAttr** 커서 라이브러리의 함수가 있습니다. 에 대 한 일반적인 내용은 **SQLSetStmtAttr**, 참조 [SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)합니다.  
  
 커서 라이브러리는 다음 문 특성과 지원 **SQLSetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 커서 라이브러리 SQL_ATTR_CURSOR_TYPE 문 특성의 SQL_CURSOR_FORWARD_ONLY 및 SQL_CURSOR_STATIC 값을 지원합니다.  
  
 정방향 전용 커서에 대 한 커서 라이브러리는 문 특성 SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY 값을 지원합니다. 정적 커서에 대 한 커서 라이브러리는 문 특성 SQL_ATTR_CONCURRENCY의 SQL_CONCUR_READ_ONLY 및 SQL_CONCUR_VALUES 값을 지원합니다.  
  
 커서 라이브러리 SQL_ATTR_SIMULATE_CURSOR 문 특성의 SQL_SC_NON_UNIQUE 값만 지원합니다.  
  
 ODBC 사양에 대 한 호출을 지원 하지만 **SQLSetStmtAttr** 후 SQL_ATTR_PARAM_BIND_TYPE 또는 SQL_ATTR_ROW_BIND_TYPE 특성을 가진 **SQLFetch** 또는 **SQLFetchScroll**  가 호출 된 커서 라이브러리는 그렇지 않습니다. 커서 라이브러리에서 바인딩 종류를 변경 하기 전에 응용 프로그램이 커서를 닫아야 합니다. 커서 라이브러리가 지원 변경 SQL_ATTR_ROW_BIND_OFFSET_PTR, SQL_ATTR_PARAM_BIND_OFFSET_PTR, SQL_ATTR_ROWS_FETCHED_PTR, 고 때 커서 문 특성을 SQL_ATTR_PARAMS_PROCESSED_PTR 열립니다.  
  
 응용 프로그램에서 호출할 수 **SQLSetStmtAttr** 와 **특성** sql_attr_row_array_size 라는 커서가 열려 있는 동안 행 집합 크기를 변경할 수 있습니다. 새 행 집합 크기가 적용 됩니다 다음에 **SQLFetchScroll** 또는 **SQLFetch** 호출 됩니다.  
  
 커서 라이브러리 지원 바인딩 오프셋을 사용 하도록 설정 하려면 SQL_ATTR_PARAM_BIND_OFFSET_PTR 또는 SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성을 설정 합니다. 바인딩 오프셋에 대 한 호출에 대 한 사용 되지 것입니다 **SQLFetch** ODBC 2 커서 라이브러리 사용 되는 경우. *x* 드라이버입니다.  
  
 커서 라이브러리 SQL_UB_VARIABLE SQL_ATTR_USE_BOOKMARKS 문 특성 설정을 지원 합니다.
