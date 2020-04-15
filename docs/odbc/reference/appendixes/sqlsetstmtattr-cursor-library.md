---
title: SQLSetStmtAttr (커서 라이브러리) | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1bdd9b3b559d5cc78a0d44f5280aae347bc8996a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300493"
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLSetStmtAttr** 함수의 사용에 대해 설명합니다. **SQLSetStmtAttr에**대한 일반 정보는 [SQLSetStmtAttr 함수를](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)참조하십시오.  
  
 커서 라이브러리는 **SQLSetStmtAttr에서**다음 문 특성을 지원합니다.  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 커서 라이브러리는 SQL_ATTR_CURSOR_TYPE 문 특성의 SQL_CURSOR_FORWARD_ONLY 및 SQL_CURSOR_STATIC 값만 지원합니다.  
  
 정방향 전용 커서의 경우 커서 라이브러리는 SQL_ATTR_CONCURRENCY 문 특성의 SQL_CONCUR_READ_ONLY 값을 지원합니다. 정적 커서의 경우 커서 라이브러리는 SQL_ATTR_CONCURRENCY 문 특성의 SQL_CONCUR_READ_ONLY 및 SQL_CONCUR_VALUES 값을 지원합니다.  
  
 커서 라이브러리는 SQL_ATTR_SIMULATE_CURSOR 문 특성의 SQL_SC_NON_UNIQUE 값만 지원합니다.  
  
 ODBC 규격은 **SQLFetch** 또는 **SQLFetchScroll가** 호출된 후 SQL_ATTR_PARAM_BIND_TYPE 또는 SQL_ATTR_ROW_BIND_TYPE 특성을 사용하여 **SQLSetStmtAttr에** 대한 호출을 지원하지만 커서 라이브러리는 지원하지 않습니다. 커서 라이브러리에서 바인딩 형식을 변경하려면 응용 프로그램이 커서를 닫아야 합니다. 커서 라이브러리는 커서가 열려 있을 때 SQL_ATTR_ROW_BIND_OFFSET_PTR, SQL_ATTR_PARAM_BIND_OFFSET_PTR, SQL_ATTR_ROWS_FETCHED_PTR 및 SQL_ATTR_PARAMS_PROCESSED_PTR 문 특성을 변경하는 데 지원됩니다.  
  
 응용 프로그램은 커서가 열려 있는 동안 행 집합 크기를 변경하기 위해 SQL_ATTR_ROW_ARRAY_SIZE **특성을** 사용하여 **SQLSetStmtAttr을** 호출할 수 있습니다. 새 행 집합 크기는 다음에 **SQLFetchScroll** 또는 **SQLFetch가** 호출될 때 적용됩니다.  
  
 커서 라이브러리는 바인딩 오프셋을 사용하도록 SQL_ATTR_PARAM_BIND_OFFSET_PTR 또는 SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성 설정을 지원합니다. 커서 라이브러리가 ODBC 2와 함께 사용될 때 **SQLFetch** 호출에는 바인딩 오프셋이 사용되지 않습니다. *x* 드라이버.  
  
 커서 라이브러리는 SQL_ATTR_USE_BOOKMARKS 문 특성을 SQL_UB_VARIABLE 설정하는 데 지원됩니다.
