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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091675"
---
# <a name="sqlsetstmtoption-mapping"></a>SQLSetStmtOption 매핑
응용 *프로그램이 ODBC 3.x* 드라이버를 통해 **SQLSetStmtOption** 를 호출 하는 경우에 대 한 호출이  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 는 다음과 같이 생성 됩니다.  
  
-   *Foption* 이 문자열인 ODBC 정의 문 특성을 나타내는 경우 드라이버 관리자는를 호출 합니다.  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   *Foption* 이 32 비트 정수 값을 반환 하는 ODBC 정의 문 특성을 나타내는 경우 드라이버 관리자는를 호출 합니다.  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   *Foption* 이 드라이버 정의 문 특성을 나타내는 경우 드라이버 관리자는를 호출 합니다.  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 앞의 세 가지 경우에서 **StatementHandle** 인수는 *hstmt*의 값으로 설정 되 고, *특성* 인수는 *foption*의 값으로 설정 되며, *값은* *vparam*로 값으로 설정 됩니다.  
  
 드라이버 관리자는 드라이버 정의 문 특성에 문자열 또는 32 비트 정수 값이 필요한 지 여부를 알 수 없으므로 **SQLSetStmtAttr**의 *stringlength* 인수에 유효한 값을 전달 해야 합니다. 드라이버가 드라이버 정의 문 특성에 대 한 특수 한 의미 체계를 정의 하 고 **SQLSetStmtOption**를 사용 하 여 호출 해야 하는 경우 **SQLSetStmtOption**를 지원 해야 합니다.  
  
 응용 프로그램에서 **SQLSetStmtOption** 를 호출 하 여 odbc 2.x 드라이버에서 드라이버별 문 옵션을 설정 하 고 해당 *옵션이 odbc 2.x* 버전의 드라이버에서 정의 된 *경우 odbc 3.x* 드라이버의 옵션에 대해 새 매니페스트 상수를 정의 해야 *합니다.* **SQLSetStmtOption**에 대 한 호출에서 이전 매니페스트 상수를 사용 하는 경우 드라이버 관리자는 *stringlength* 인수를 0으로 설정 하 여 **SQLSetStmtAttr** 를 호출 합니다.  
  
 응용 프로그램에서 **SQLSetStmtAttr** 를 호출 하 여 ODBC *3.x 드라이버에서* SQL_ATTR_USE_BOOKMARKS를 SQL_UB_ON로 설정 하면 SQL_ATTR_USE_BOOKMARKS statement 특성이 SQL_UB_FIXED로 설정 됩니다. SQL_UB_ON은 SQL_UB_FIXED와 동일한 상수입니다. 드라이버 관리자는 드라이버에 SQL_UB_FIXED를 전달 합니다. SQL_UB_FIXED ODBC 3.x에서 더 이상 사용 되지 *않지만 odbc 2.x 드라이버는* 고정 길이 *책갈피를 사용*하는 odbc *2.x 응용 프로그램* 에서 작동 하도록 구현 해야 합니다.  
  
 ODBC 3.x 드라이버의 경우 드라이버 관리자는 더 이상 *옵션이* SQL_STMT_OPT_MIN와 SQL_STMT_OPT_MAX 사이에 있는지 또는 SQL_CONNECT_OPT_DRVR_START 보다 큰지 확인 하지 *않습니다.*
