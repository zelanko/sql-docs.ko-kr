---
title: "SQLSetPos (커서 라이브러리) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetPos function [ODBC], Cursor Library
ms.assetid: 574399c3-2bb2-4d19-829c-7c77bd82858d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b195ca1dbb138b21fcf107150832288df8317196
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos (커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목의 사용을 설명는 **SQLSetPos** 커서 라이브러리의 함수가 있습니다. 에 대 한 일반적인 내용은 **SQLSetPos**, 참조 [SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)합니다.  
  
 커서 라이브러리에 대해서만 sql_position과 작업을 지 원하는 *작업* 인수 **SQLSetPos**합니다. SQL_LOCK_NO_CHANGE 값에 대해서만 지원는 *LockType* 인수입니다.  
  
 커서 라이브러리 SQLSTATE HYC00 반환 드라이버 대량 작업을 지원 하지 않으면 (드라이버를 사용할 수 없습니다.) 때 **SQLSetPos** 사용 하 여 호출 *RowNumber* 0입니다. 이 드라이버 동작은 권장 되지 않습니다.  
  
 커서 라이브러리에 대 한 호출에서 SQL_UPDATE 및 SQL_DELETE 작업을 지원 하지 않습니다 **SQLSetPos**합니다. 커서 라이브러리 구현 하는 위치 지정 업데이트 하거나 만들어 검색 결과 SQL 문을 삭제 업데이트 또는 바인딩된 각 열에 대 한 캐시에 저장 된 값을 열거 하는 WHERE 절을 사용 하 여 문을 삭제 합니다. 자세한 내용은 참조 [처리 위치 Update 및 Delete 문이](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)합니다.  
  
 커서 라이브러리를 사용 하는 응용 프로그램을 호출 해야 드라이버는 정적 커서를 지원 하지 않으면, **SQLSetPos** 에 의해 인출 된 행 집합에 대해서만 **SQLExtendedFetch** 또는 **SQLFetchScroll **인식 되지 않습니다 **SQLFetch**합니다. 커서 라이브러리 구현 **SQLExtendedFetch** 및 **SQLFetchScroll** 의 반복 된 호출을 수행 하 여 **SQLFetch** (행 집합 크기가 1)와 드라이버에서 합니다. 커서 라이브러리에 대 한 호출을 전달 **SQLFetch**에서 다른 반면 통해 드라이버에 있습니다. 경우 **SQLSetPos** 다중 행에 의해 인출 된 행 집합에서 호출 **SQLFetch** 때문에 호출이 실패 드라이버는 정적 커서를 지원 하지 않으면, **SQLSetPos** 작동 하지 않습니다 정방향 전용 커서입니다. 응용 프로그램에 성공적으로 호출 하는 경우에이 실시할 **SQLSetStmtAttr** SQL_ATTR_CURSOR_TYPE 커서 라이브러리가 지원 드라이버는 정적 커서를 지원 하지 않는 경우에 있는 SQL_CURSOR_STATIC로 설정 합니다.
