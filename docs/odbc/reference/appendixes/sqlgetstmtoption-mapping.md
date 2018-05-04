---
title: SQLGetStmtOption 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLGetStmtOption
ms.assetid: fa599517-3f3e-4dad-a65a-b8596ae3f330
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 02eaacbe3503b5d93677633aa0e98326b14e304f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetstmtoption-mapping"></a>SQLGetStmtOption 매핑
응용 프로그램 호출 하는 경우 **SQLGetStmtOption** ODBC 3 *.x* 것에 대 한 호출을 지원 하지 않는 드라이버  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 다음과 같이 발생 합니다.  
  
-   경우 *fOption* 드라이버 관리자를 호출 하 여 문자열을 반환 하는 ODBC 정의 문 옵션을 나타냅니다.  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   경우 *fOption* 드라이버 관리자를 호출 하 여 32 비트 정수 값을 반환 하는 ODBC 정의 문 옵션을 나타냅니다.  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   경우 *fOption* 드라이버 관리자를 호출 하 여 드라이버에서 정의 된 문 옵션을 나타냅니다.  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 위의 세 가지 경우는 *StatementHandle* 인수에 있는 값으로 설정 되어 *hstmt*, *특성* 인수에 있는 값으로 설정 되어 *fOption* , 및 *ValuePtr* 인수는 동일한 값으로 설정 되어 *pvParam*합니다.  
  
 ODBC 정의 문자열 연결 옵션에 대 한 드라이버 관리자는 다음과 같이 설정 됩니다.는 *BufferLength* 호출에 인수 **SQLGetConnectAttr** 미리 정의 된 최대 길이 (SQL_MAX_OPTION_STRING_LENGTH); 문자열이 아닌 연결 옵션에 대 한 *BufferLength* 0으로 설정 됩니다.  
  
 ODBC 3에서 SQL_GET_BOOKMARK 문 옵션은 사용 되지 *.x*합니다. ODBC 3에 대 한 *.x* ODBC 2에서 실행 되도록 드라이버. *x* SQL_GET_BOOKMARK를 사용 하는 응용 프로그램 SQL_GET_BOOKMARK를 지원 해야 합니다. ODBC 3에 대 한 *.x* ODBC 2에서 실행 되도록 드라이버. *x* 응용 프로그램을 지원 해야 SQL_USE_BOOKMARKS SQL_UB_ON을 설정 하 고 고정 길이의 책갈피를 노출 해야 합니다. ODBC 3 경우 *.x* 드라이버 지원만 가변 길이 책갈피, 고정 길이 하지 책갈피, SQLSTATE HYC00 반환 해야 합니다 (선택적 기능이 구현 되지 않았습니다) 경우 ODBC 2. *x* 응용 프로그램이 SQL_USE_BOOKMARKS SQL_UB_ON로 설정 하려고 합니다.  
  
 ODBC 3에 대 한 *.x* 드라이버를 드라이버 관리자를 더 이상 확인 여부를 *옵션* 사이 SQL_STMT_OPT_MIN 및 SQL_STMT_OPT_MAX, 또는 SQL_CONNECT_OPT_DRVR_START 보다 큽니다. 드라이버는이 확인란을 선택 해야 합니다.
