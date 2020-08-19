---
description: SQLSetStmtAttr(커서 라이브러리)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96466e354875224c05bef4c94d72249bad9a4cff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429496"
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLSetStmtAttr** 함수를 사용 하는 방법을 설명 합니다. **SQLSetStmtAttr**에 대 한 일반 정보는 [SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)를 참조 하세요.  
  
 커서 라이브러리는 **SQLSetStmtAttr**을 사용 하는 다음과 같은 문 특성을 지원 합니다.  

:::row:::
    :::column:::
        SQL_ATTR_CONCURRENCY  
        SQL_ATTR_CURSOR_TYPE  
        SQL_ATTR_FETCH_BOOKMARK_PTR  
        SQL_ATTR_PARAM_BIND_OFFSET_PTR  
        SQL_ATTR_PARAM_BIND_TYPE  
    :::column-end:::
    :::column:::
        SQL_ATTR_ROW_BIND_OFFSET_PTR  
        SQL_ATTR_ROW_BIND_TYPE  
        SQL_ATTR_ROWSET_ARRAY_SIZE  
        SQL_ATTR_SIMULATE_CURSOR  
        SQL_ATTR_USE_BOOKMARKS  
    :::column-end:::
:::row-end:::

 커서 라이브러리는 SQL_ATTR_CURSOR_TYPE statement 특성의 SQL_CURSOR_FORWARD_ONLY 및 SQL_CURSOR_STATIC 값만 지원 합니다.  
  
 전방 전용 커서의 경우 커서 라이브러리는 SQL_ATTR_CONCURRENCY statement 특성의 SQL_CONCUR_READ_ONLY 값을 지원 합니다. 정적 커서의 경우 커서 라이브러리는 SQL_ATTR_CONCURRENCY statement 특성의 SQL_CONCUR_READ_ONLY 및 SQL_CONCUR_VALUES 값을 지원 합니다.  
  
 커서 라이브러리는 SQL_ATTR_SIMULATE_CURSOR statement 특성의 SQL_SC_NON_UNIQUE 값만 지원 합니다.  
  
 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출한 후에 SQL_ATTR_PARAM_BIND_TYPE 또는 SQL_ATTR_ROW_BIND_TYPE 특성을 사용 하 여 **SQLSetStmtAttr** 에 대 한 호출을 지원 하지만 커서 라이브러리는 그렇지 않습니다. 커서 라이브러리의 바인딩 유형을 변경 하려면 응용 프로그램에서 커서를 닫아야 합니다. 커서 라이브러리는 커서가 열려 있을 때 SQL_ATTR_ROW_BIND_OFFSET_PTR, SQL_ATTR_PARAM_BIND_OFFSET_PTR, SQL_ATTR_ROWS_FETCHED_PTR 및 SQL_ATTR_PARAMS_PROCESSED_PTR 문 특성의 변경을 지원 합니다.  
  
 응용 프로그램은 SQL_ATTR_ROW_ARRAY_SIZE **특성** 을 사용 하 여 **SQLSetStmtAttr** 를 호출 하 여 커서가 열려 있는 동안 행 집합 크기를 변경할 수 있습니다. 새 행 집합 크기는 다음에 **Sqlfetchscroll** 또는 **sqlfetch** 를 호출할 때 적용 됩니다.  
  
 커서 라이브러리는 SQL_ATTR_PARAM_BIND_OFFSET_PTR 또는 SQL_ATTR_ROW_BIND_OFFSET_PTR statement 특성을 설정 하 여 바인딩 오프셋을 사용할 수 있도록 지원 합니다. 커서 라이브러리를 ODBC 2와 함께 사용할 경우에는 **Sqlfetch** 호출에 바인딩 오프셋이 사용 되지 않습니다. *x* 드라이버.  
  
 커서 라이브러리는 SQL_ATTR_USE_BOOKMARKS statement 특성을 SQL_UB_VARIABLE로 설정 하는 것을 지원 합니다.
