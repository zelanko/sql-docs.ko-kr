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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091709"
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLSetPos** 함수를 사용 하는 방법을 설명 합니다. **Sqlsetpos**에 대 한 일반적인 내용은 [sqlsetpos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)를 참조 하세요.  
  
 커서 라이브러리는 **SQLSetPos**의 *작업* 인수에 대해서만 SQL_POSITION 작업을 지원 합니다. *LockType* 인수에 대해서만 SQL_LOCK_NO_CHANGE 값을 지원 합니다.  
  
 드라이버가 대량 작업을 지원 하지 않는 경우, *RowNumber* 가 0으로 호출 되 면 커서 라이브러리는 SQLSTATE HYC00 (드라이버 **를 사용할 수** 없음)를 반환 합니다. 이 드라이버 동작은 권장 되지 않습니다.  
  
 커서 라이브러리는 **SQLSetPos**호출의 SQL_UPDATE 및 SQL_DELETE 작업을 지원 하지 않습니다. 커서 라이브러리는 각 바인딩된 열에 대해 해당 캐시에 저장 된 값을 열거 하는 WHERE 절을 사용 하 여 검색 된 update 또는 delete 문을 만들어 위치 지정 update 또는 delete SQL 문을 구현 합니다. 자세한 내용은 [위치 지정 업데이트 및 Delete 문 처리](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)를 참조 하세요.  
  
 드라이버가 정적 커서를 지원 하지 않는 경우 커서 라이브러리를 사용 하 여 작업 하는 응용 프로그램은 **Sqlfetch**가 아니라 **sqlextendedfetch** 또는 **sqlextendedfetch**으로 인출 된 행 집합 에서만 **SQLSetPos** 를 호출 해야 합니다. 커서 라이브러리는 **Sqlextendedfetch** 및 **sqlextendedfetch** 을 구현 합니다 .이는 드라이버에서 **sqlfetch** (행 집합 크기가 1 인)를 반복 해 서 호출 하는 것입니다. 커서 라이브러리는 직접 **Sqlfetch**호출을 드라이버를 통해 전달 합니다. 드라이버가 정적 커서를 지원 하지 않는 경우 **Sqlfetch** 에 의해 인출 된 다중 행 집합에 **sqlsetpos** 를 호출 하면 **sqlsetpos** 가 전방 전용 커서에서 작동 하지 않으므로 호출이 실패 합니다. 이 문제는 응용 프로그램이 **SQLSetStmtAttr** 를 성공적으로 호출 하 여 드라이버에서 정적 커서를 지원 하지 않는 경우에도 커서 라이브러리에서 지 원하는 SQL_CURSOR_STATIC로 SQL_ATTR_CURSOR_TYPE를 호출 하는 경우에도 발생 합니다.
