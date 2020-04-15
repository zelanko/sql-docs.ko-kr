---
title: SQLSetStmt옵션 매핑 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetStmtOption
- SQLSetStmtOption function [ODBC], mapping
ms.assetid: 6a9921aa-8a53-4668-9b13-87164062f1e5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 91264cee0dfceeb7195e2bad40d1638a88e1e01a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304904"
---
# <a name="sqlsetstmtoption-mapping"></a>SQLSetStmtOption 매핑
응용 프로그램이 ODBC *3.x* 드라이버를 통해 **SQLSetStmtOption을** 호출하면  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 다음과 같이 발생합니다.  
  
-   *fOption문자열인* ODBC 정의 문 특성을 나타내는 경우 드라이버 관리자는  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   *fOption이* 32비트 정수 값을 반환하는 ODBC 정의 문 특성을 나타내는 경우 드라이버 관리자는  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   *fOption이* 드라이버 정의 문 특성을 나타내는 경우 드라이버 관리자는  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 앞의 세 가지 경우에서 **StatementHandle** 인수는 *hstmt의*값으로 설정되고 *특성* 인수는 *fOption의*값으로 설정되고 *ValuePtr* 인수는 *vParam값으로*설정됩니다.  
  
 드라이버 관리자는 드라이버 정의 문 특성에 문자열 또는 32비트 정수 값이 필요한지 여부를 알 수 없으므로 **SQLSetStmtAttr의** *StringLength* 인수에 대해 유효한 값을 전달해야 합니다. 드라이버가 드라이버 정의 문 특성에 대한 특수 의미 체계를 정의하고 **SQLSetStmtOption을**사용하여 호출해야 하는 경우 **SQLSetStmtOption을**지원해야 합니다.  
  
 응용 프로그램이 **SQLSetStmtOption을** 호출하여 ODBC *3.x* 드라이버에서 드라이버 별 명령문 옵션을 설정하고 ODBC *2.x* 버전의 드라이버에 옵션이 정의된 경우 ODBC *3.x* 드라이버의 옵션에 대해 새 매니페스트 상수가 정의되어야 합니다. 이전 매니페스트 상수가 **SQLSetStmtOption**호출에서 사용되는 경우 드라이버 관리자는 *STRINGLength* 인수를 0으로 설정한 **SQLSetStmtAttr을** 호출합니다.  
  
 응용 프로그램이 **SQLSetStmtAttr을** 호출하여 ODBC *3.x* 드라이버에서 SQL_ATTR_USE_BOOKMARKS SQL_UB_ON 설정하면 SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_FIXED 설정됩니다. SQL_UB_ON SQL_UB_FIXED 동일한 상수입니다. 드라이버 관리자는 SQL_UB_FIXED 전달하여 드라이버로 전달합니다. SQL_UB_FIXED ODBC *3.x에서*더 이상 사용되지 않지만 ODBC *3.x* 드라이버는 고정 길이 책갈피를 사용하는 ODBC *2.x* 응용 프로그램과 함께 작동하도록 구현해야 합니다.  
  
 ODBC *3.x* 드라이버의 경우 드라이버 관리자는 더 이상 *옵션이* SQL_STMT_OPT_MIN SQL_STMT_OPT_MAX 사이에 있는지 또는 SQL_CONNECT_OPT_DRVR_START 보다 큰지 확인하지 않습니다.
