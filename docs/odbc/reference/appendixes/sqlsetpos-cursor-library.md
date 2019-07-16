---
title: SQLSetPos (커서 라이브러리) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 87ff006e7bead36c2aa6476b99552d1524c213b1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091709"
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는의 사용을 설명 합니다 **SQLSetPos** 커서 라이브러리의 함수입니다. 에 대 한 일반 정보에 대 한 **SQLSetPos**를 참조 하십시오 [SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)합니다.  
  
 커서 라이브러리에 대해서만 SQL_POSITION 작업을 지원 합니다 *작업이* 에서 인수 **SQLSetPos**합니다. SQL_LOCK_NO_CHANGE 값에 대해서만 지원 합니다 *LockType* 인수입니다.  
  
 커서 라이브러리 SQLSTATE HYC00 반환 드라이버 대량 작업을 지원 하지 않습니다 (드라이버를 사용할 수 없습니다.) 때 **SQLSetPos** 사용 하 여 라고 *RowNumber* 0입니다. 이 드라이버 동작은 권장 되지 않습니다.  
  
 커서 라이브러리에 대 한 호출에서 SQL_UPDATE 및 SQL_DELETE 작업을 지원 하지 않습니다 **SQLSetPos**합니다. 커서 라이브러리 구현 하는 위치 지정 업데이트 또는 검색을 만들어 SQL 문을 삭제 업데이트나 바인딩된 각 열에 대 한 해당 캐시에 저장 된 값을 열거 하는 WHERE 절을 사용 하 여 문을 삭제 합니다. 자세한 내용은 [처리 위치 지정 업데이트 및 삭제 문을](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)합니다.  
  
 커서 라이브러리를 사용 하 여 작업 하는 응용 프로그램을 호출 해야 드라이버 정적 커서를 지원 하지 않습니다 **SQLSetPos** 가져온 행 집합 에서만 **SQLExtendedFetch** 또는 **SQLFetchScroll** 가 아니라 **SQLFetch**합니다. 커서 라이브러리를 구현 **SQLExtendedFetch** 하 고 **SQLFetchScroll** 반복된 호출 하 여 **SQLFetch** (사용 하 여 행 집합 크기가 1) 드라이버의 합니다. 커서 라이브러리에 대 한 호출을 전달 **SQLFetch**에, 다른 반면 통해 드라이버입니다. 하는 경우 **SQLSetPos** 인출 하 여 다중 행 집합에서 라고 **SQLFetch** 드라이버는 정적 커서를 지원 하지 않으면, 호출 실패로 인해 **SQLSetPos** 작동 하지 않습니다 정방향 전용 커서입니다. 응용 프로그램에 성공적으로 호출 하는 경우에 전송 됩니다 **SQLSetStmtAttr** SQL_ATTR_CURSOR_TYPE 드라이버 정적 커서를 지원 하지 않는 경우에 커서 라이브러리 지 SQL_CURSOR_STATIC로 설정 합니다.
