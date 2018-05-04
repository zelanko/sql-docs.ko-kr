---
title: SQLSetStmtOption 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetStmtOption
- SQLSetStmtOption function [ODBC], mapping
ms.assetid: 6a9921aa-8a53-4668-9b13-87164062f1e5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b5b1fd1295586e69f9db0f4084f74540163f45ed
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetstmtoption-mapping"></a>SQLSetStmtOption 매핑
응용 프로그램 호출 하는 경우 **SQLSetStmtOption** ODBC 3 *.x* 드라이버에 대 한 호출  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 다음과 같이 발생 합니다.  
  
-   경우 *fOption* 드라이버 관리자를 호출 하 여 문자열 정의 ODBC 문 특성을 나타냅니다  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   경우 *fOption* 드라이버 관리자를 호출 하 여 32 비트 정수 값을 반환 하는 ODBC 정의 문 특성을 나타냅니다.  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   경우 *fOption* 는 드라이버에서 정의 된 문 특성을 호출 하 여 드라이버 관리자를 나타냅니다  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 위의 세 가지 경우는 **StatementHandle** 인수에 있는 값으로 설정 되어 *hstmt*, *특성* 인수에 있는 값으로 설정 되어 *fOption* , 및 *ValuePtr* 인수 값으로 설정 되어 *vParam*합니다.  
  
 에 대 한 유효한 값을 전달 해야 하는 드라이버 관리자 드라이버에서 정의 된 문 특성 문자열 또는 32 비트 정수 값을 필요한 지 여부를 알지 못하므로 *StringLength* 의 인수 **SQLSetStmtAttr**. 드라이버가 드라이버에서 정의 된 문 특성에 대 한 특별 한 의미를 정의 하 고 사용 하 여 호출 해야 하는 경우 **SQLSetStmtOption**를 지원 해야 **SQLSetStmtOption**합니다.  
  
 응용 프로그램을 호출 하는 경우 **SQLSetStmtOption** ODBC 3에서 드라이버별 문 옵션을 설정 하려면 *.x* 드라이버 및 옵션에에서 정의 되어 있는 ODBC 2. *x* ODBC 3의 옵션에 대 한 버전의 드라이버를 새 매니페스트 상수를 정의 해야 *.x* 드라이버입니다. 오래 된 매니페스트 상수에 대 한 호출에 사용 되는 경우 **SQLSetStmtOption**, 드라이버 관리자를 호출 합니다 **SQLSetStmtAttr** 와 *StringLength* 인수는 0으로 설정 합니다.  
  
 응용 프로그램 호출 하는 경우 **SQLSetStmtAttr** SQL_ATTR_USE_BOOKMARKS SQL_UB_ON ODBC 3에서으로 설정 하려면 *.x* 드라이버 SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_FIXED로 설정 되어 있습니다. SQL_UB_ON은 SQL_UB_FIXED로 동일한 상수입니다. 드라이버 관리자를 통해 SQL_UB_FIXED 드라이버에 전달 합니다. ODBC 3에서 SQL_UB_FIXED를 더 이상 사용 되지 *.x*, 하지만 ODBC 3 *.x* 드라이버는 ODBC 2와 작동 하도록 구현 해야 합니다. *x* 고정 길이의 책갈피를 사용 하는 응용 프로그램입니다.  
  
 ODBC 3에 대 한 *.x* 드라이버를 드라이버 관리자는 더 이상 있는지 여부를 확인 *옵션* 사이 SQL_STMT_OPT_MIN 및 SQL_STMT_OPT_MAX, 또는 SQL_CONNECT_OPT_DRVR_START 보다 큽니다.
