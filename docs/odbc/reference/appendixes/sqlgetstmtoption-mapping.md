---
title: SQLGetStmt옵션 매핑 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLGetStmtOption
ms.assetid: fa599517-3f3e-4dad-a65a-b8596ae3f330
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68819269d41407f2ce9dee172c889f7d7f286793
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300603"
---
# <a name="sqlgetstmtoption-mapping"></a>SQLGetStmtOption 매핑
응용 프로그램이 **SQLGetStmtOption을** 지원하지 않는 ODBC *3.x* 드라이버로 호출하면  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 다음과 같이 발생합니다.  
  
-   *fOption* 문자열을 반환 하는 ODBC 정의 된 문 옵션을 나타내는 경우 드라이버 관리자 호출  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   *fOption이* 32비트 정수 값을 반환하는 ODBC 정의 문 옵션을 나타내는 경우 드라이버 관리자는  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   *fOption이* 드라이버 정의 문 옵션을 나타내는 경우 드라이버 관리자는  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 앞의 세 가지 경우에서 *StatementHandle* 인수는 *hstmt의*값으로 설정되고 *특성* 인수는 *fOption의*값으로 설정되고 *ValuePtr* 인수는 *pvParam과*동일한 값으로 설정됩니다.  
  
 ODBC 정의 문자열 연결 옵션의 경우 드라이버 관리자는 **SQLGetConnectAttr** 호출에서 *bufferLength* 인수를 미리 정의된 최대 길이(SQL_MAX_OPTION_STRING_LENGTH)로 설정합니다. 비문자열 연결 옵션의 경우 *BufferLength가* 0으로 설정됩니다.  
  
 SQL_GET_BOOKMARK 명령문 옵션은 ODBC *3.x에서*더 이상 사용되지 않습니다. ODBC *3.x* 드라이버가 SQL_GET_BOOKMARK 사용하는 ODBC *2.x* 응용 프로그램과 함께 작동하려면 SQL_GET_BOOKMARK 지원해야 합니다. ODBC *3.x* 드라이버가 ODBC *2.x* 응용 프로그램과 함께 작동하려면 SQL_USE_BOOKMARKS 설정을 지원하여 SQL_UB_ON 고정 길이 책갈피를 노출해야 합니다. ODBC *3.x* 드라이버가 고정 길이 책갈피가 아닌 가변 길이 책갈피만 지원하는 경우 ODBC *2.x* 응용 프로그램이 SQL_UB_ON SQL_USE_BOOKMARKS 설정하려고 하면 SQLSTATE HYC00(선택적 기능이 구현되지 않음)을 반환해야 합니다.  
  
 ODBC *3.x* 드라이버의 경우 드라이버 관리자는 더 이상 *옵션이* SQL_STMT_OPT_MIN SQL_STMT_OPT_MAX 사이에 있는지 또는 SQL_CONNECT_OPT_DRVR_START 보다 큰지 확인하지 않습니다. 드라이버는 이것을 확인해야 합니다.
