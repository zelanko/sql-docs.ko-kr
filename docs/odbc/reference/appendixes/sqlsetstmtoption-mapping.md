---
title: SQLSetStmtOption 매핑 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc4ed430b301f2b191c0586c0a54af19a2d2d526
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091675"
---
# <a name="sqlsetstmtoption-mapping"></a>SQLSetStmtOption 매핑
응용 프로그램을 호출할 때 **SQLSetStmtOption** 는 ODBC를 통한 *3.x* 드라이버에 대 한 호출  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 다음과 같이 발생 합니다.  
  
-   하는 경우 *fOption* ODBC 정의 문 특성 드라이버 관리자를 호출 하 여 문자열을 나타냅니다.  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   하는 경우 *fOption* 드라이버 관리자를 호출 하 여 32 비트 정수 값을 반환 하는 ODBC 정의 문 특성을 나타냅니다.  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   하는 경우 *fOption* 드라이버 관리자를 호출 하 여 드라이버에서 정의 된 문 특성을 나타냅니다.  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 위의 세 가지 경우에 **StatementHandle** 인수를 값으로 설정 *hstmt*의 *특성* 인수를 값으로 설정 *fOption* , 및 *ValuePtr* 인수를 값으로 설정 됩니다 *갖고*합니다.  
  
 에 대 한 유효한 값을 전달 해야 하는 드라이버 관리자가 드라이버에서 정의 된 문 특성 문자열 또는 32 비트 정수 값을 필요한 지 여부를 알지 못하므로, 합니다 *StringLength* 인수의 **SQLSetStmtAttr**. 드라이버가 드라이버에서 정의 된 문 특성에 대 한 특별 한 의미를 정의 하 고 사용 하 여 호출 해야 하는 경우 **SQLSetStmtOption**를 지원 해야 **SQLSetStmtOption**합니다.  
  
 응용 프로그램을 호출 하는 경우 **SQLSetStmtOption** ODBC에서 드라이버별 문 옵션을 설정 하려면 *3.x* 옵션과 드라이버는 ODBC에 정의 된 *2.x* 의 버전을 드라이버는 ODBC의 옵션에 대 한 새 매니페스트 상수를 정의 해야 *3.x* 드라이버입니다. 오래 된 매니페스트 상수에 대 한 호출에 사용 되는 경우 **SQLSetStmtOption**, 드라이버 관리자를 호출 합니다 **SQLSetStmtAttr** 사용 하 여 합니다 *StringLength* 인수는 0으로 설정 합니다.  
  
 응용 프로그램을 호출할 때 **SQLSetStmtAttr** SQL_ATTR_USE_BOOKMARKS SQL_UB_ON ODBC에서 설정 하려면 *3.x* 드라이버 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_FIXED로 설정 됩니다. SQL_UB_ON는 SQL_UB_FIXED로 동일한 상수입니다. 드라이버 관리자는 드라이버를 통해 SQL_UB_FIXED를 전달합니다. SQL_UB_FIXED ODBC 되지 *3.x*, 있지만 ODBC *3.x* 드라이버는 ODBC를 사용 하도록 구현 해야 *2.x* 고정 길이 책갈피를 사용 하는 응용 프로그램입니다.  
  
 ODBC에 대 한 *3.x* 드라이버를 드라이버 관리자는 더 이상 있는지 확인 합니다 *옵션* SQL_STMT_OPT_MIN 사이의 SQL_STMT_OPT_MAX, 되었거나 SQL_CONNECT_OPT_DRVR_START 보다 큽니다.
