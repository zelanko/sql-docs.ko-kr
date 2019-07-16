---
title: SQLGetStmtOption 매핑 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2973455ff4ee7e8dc51b2cd07a6423c9b1c36346
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073809"
---
# <a name="sqlgetstmtoption-mapping"></a>SQLGetStmtOption 매핑
응용 프로그램을 호출할 때 **SQLGetStmtOption** 는 odbc *3.x* 것에 대 한 호출을 지원 하지 않는 드라이버  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 다음과 같이 발생 합니다.  
  
-   하는 경우 *fOption* 드라이버 관리자를 호출 하 여 문자열을 반환 하는 ODBC 정의 문 옵션을 나타냅니다.  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   하는 경우 *fOption* 드라이버 관리자를 호출 하 여 32 비트 정수 값을 반환 하는 ODBC 정의 문 옵션을 나타냅니다.  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   하는 경우 *fOption* 드라이버 관리자를 호출 하 여 드라이버에서 정의 된 문 옵션을 나타냅니다.  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 위의 세 가지 경우에 *StatementHandle* 인수를 값으로 설정 *hstmt*의 *특성* 인수를 값으로 설정 *fOption* , 및 *ValuePtr* 인수가 동일한 값으로 설정 되어 *pvParam*합니다.  
  
 드라이버 관리자 ODBC 정의 문자열 연결 옵션을 설정 합니다 *BufferLength* 호출에 인수 **SQLGetConnectAttr** 미리 정의 된 최대 길이 (SQL_MAX_OPTION_STRING_LENGTH); 문자열이 아닌 연결 옵션의 경우 *BufferLength* 0으로 설정 됩니다.  
  
 ODBC의 SQL_GET_BOOKMARK 문 옵션을 사용 되지 *3.x*합니다. ODBC에 대 한 *3.x* ODBC를 사용 하는 드라이버 *2.x* SQL_GET_BOOKMARK를 사용 하는 응용 프로그램 SQL_GET_BOOKMARK 지원 해야 합니다. ODBC에 대 한 *3.x* ODBC를 사용 하는 드라이버 *2.x* 응용 프로그램을 지원 해야 SQL_USE_BOOKMARKS SQL_UB_ON을 설정 하 고 고정 길이 책갈피를 노출 해야 합니다. 경우 ODBC *3.x* 만 가변 길이 책갈피를 고정 길이 없습니다 책갈피를 지 원하는 드라이버, SQLSTATE HYC00 반환 해야 합니다 (선택적 기능이 구현 되지 않음) 하는 경우 ODBC *2.x* 응용 프로그램 시도 SQL_USE_BOOKMARKS SQL_UB_ON 설정 합니다.  
  
 ODBC에 대 한 *3.x* 드라이버를 드라이버 관리자를 더 이상 확인 여부 *옵션* SQL_STMT_OPT_MIN 사이의 SQL_STMT_OPT_MAX, 되었거나 SQL_CONNECT_OPT_DRVR_START 보다 큽니다. 드라이버는이 확인 해야 합니다.
