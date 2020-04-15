---
title: SQLSetPos (커서 라이브러리) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], Cursor Library
ms.assetid: 574399c3-2bb2-4d19-829c-7c77bd82858d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c46ef88075a5adbd96138d7d1f03c26712f7ea1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300513"
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLSetPos** 함수의 사용에 대해 설명합니다. **SQLSetPos에**대한 일반적인 내용은 [SQLSetPos 함수를](../../../odbc/reference/syntax/sqlsetpos-function.md)참조하십시오.  
  
 커서 라이브러리는 **SQLSetPos의** *작업* 인수에 대해서만 SQL_POSITION 작업을 지원합니다. *LockType* 인수에 대해서만 SQL_LOCK_NO_CHANGE 값을 지원합니다.  
  
 드라이버가 대량 작업을 지원하지 않는 경우 커서 라이브러리는 **SQLSetPos가** *0과* 같을 때 SQLSTATE HYC00(드라이버는 불가능)을 반환합니다. 이 드라이버 동작은 권장되지 않습니다.  
  
 커서 라이브러리는 **SQLSetPos**를 호출할 때 SQL_UPDATE 및 SQL_DELETE 작업을 지원하지 않습니다. 커서 라이브러리는 각 바인딩된 열에 대해 캐시에 저장된 값을 열거하는 WHERE 절을 사용 하 여 검색 된 업데이트 또는 delete 문을 만들어 위치 된 업데이트 또는 삭제 SQL 문을 구현 합니다. 자세한 내용은 [위치 업데이트 처리 및 문 삭제](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)를 참조하십시오.  
  
 드라이버가 정적 커서를 지원하지 않는 경우 커서 라이브러리로 작업하는 응용 프로그램은 **SQLFetch에서** 가져온 행 집합에서만 **SQLFetch** **SQLSetPos를** 호출해야 **합니다.** 커서 라이브러리는 드라이버에서 **SQLFetch(행** 집합 크기가 1)를 반복적으로 호출하여 **SQLExtendedFetch** 및 **SQLFetchScroll을** 구현합니다. 커서 라이브러리는 **SQLFetch에**대한 호출을 전달하는 반면, 드라이버를 통해 전달합니다. **SQLSetPos가** 드라이버가 정적 커서를 지원하지 않을 때 **SQLFetch에서** 가져온 다중 행 행 집합에서 **SQLSetPos가 호출되면 SQLSetPos가** 정방향 전용 커서에서 작동하지 않기 때문에 호출이 실패합니다. 이 문제는 응용 프로그램이 **SQLSetStmtAttr을** 호출하여 SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC 설정하는 경우에도 발생하며, 이 SQL_ATTR_CURSOR_TYPE 드라이버가 정적 커서를 지원하지 않는 경우에도 커서 라이브러리가 지원합니다.
