---
title: SQLSetStmtAttr (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtAttr function [ODBC], Cursor Library
ms.assetid: 6018a733-c2c8-4047-92ec-92cf85031767
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7d4e5bd6ec27891e80933dfcc42beec9056d2d3a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47619792"
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는의 사용을 설명 합니다 **SQLSetStmtAttr** 커서 라이브러리의 함수입니다. 에 대 한 일반 정보에 대 한 **SQLSetStmtAttr**를 참조 하십시오 [SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)합니다.  
  
 커서 라이브러리를 사용 하 여 다음 문 특성을 지 원하는 **SQLSetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 커서 라이브러리 SQL_CURSOR_FORWARD_ONLY 및 SQL_CURSOR_STATIC 값만 SQL_ATTR_CURSOR_TYPE 문 특성을 지원합니다.  
  
 정방향 전용 커서에 대 한 커서 라이브러리는 문 특성 SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY 값을 지원합니다. 정적 커서에 대 한 커서 라이브러리는 문 특성 SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY 및 SQL_CONCUR_VALUES 값을 지원합니다.  
  
 커서 라이브러리 SQL_ATTR_SIMULATE_CURSOR 문 특성 SQL_SC_NON_UNIQUE 값만 지원합니다.  
  
 ODBC 사양에 대 한 호출을 지원 하지만 **SQLSetStmtAttr** 후 SQL_ATTR_PARAM_BIND_TYPE 또는 SQL_ATTR_ROW_BIND_TYPE 특성과 **SQLFetch** 또는 **SQLFetchScroll**  가 호출 된 커서 라이브러리는 하지 않습니다. 커서 라이브러리의 바인딩 유형을 변경할 수 있습니다, 전에 응용 프로그램에 커서를 닫아야 합니다. 커서 라이브러리 SQL_ATTR_ROW_BIND_OFFSET_PTR, SQL_ATTR_PARAM_BIND_OFFSET_PTR SQL_ATTR_ROWS_FETCHED_PTR을 변경 지원 하며 SQL_ATTR_PARAMS_PROCESSED_PTR 문 특성 때 커서를 엽니다.  
  
 응용 프로그램에서 호출할 수 있습니다 **SQLSetStmtAttr** 사용 하 여는 **특성** 커서가 열려 있는 동안에 행 집합 크기를 변경 하려면 sql_attr_row_array_size 라는 합니다. 새 행 집합 크기가 적용 됩니다 나중 **SQLFetchScroll** 하거나 **SQLFetch** 라고 합니다.  
  
 커서 라이브러리 바인딩 오프셋을 사용 하도록 설정 하려면 SQL_ATTR_PARAM_BIND_OFFSET_PTR 또는 SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성 설정을 지원 합니다. 에 대 한 호출에 대 한 바인딩 오프셋 사용 되지 것입니다 **SQLFetch** 커서 라이브러리는 ODBC 2를 사용 하면. *x* 드라이버입니다.  
  
 커서 라이브러리 SQL_UB_VARIABLE SQL_ATTR_USE_BOOKMARKS 문 특성 설정을 지원 합니다.
