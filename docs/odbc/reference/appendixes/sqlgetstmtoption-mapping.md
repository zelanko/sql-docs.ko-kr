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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68819269d41407f2ce9dee172c889f7d7f286793
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300603"
---
# <a name="sqlgetstmtoption-mapping"></a>SQLGetStmtOption 매핑
응용 프로그램에서 **SQLGetStmtOption** 를 호출 하는 경우이를 지원 하지 *않는 ODBC 2.x* 드라이버에 대 한 호출은  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 는 다음과 같이 생성 됩니다.  
  
-   *Foption* 이 문자열을 반환 하는 ODBC 정의 문 옵션을 나타내는 경우 드라이버 관리자는를 호출 합니다.  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   *Foption* 이 32 비트 정수 값을 반환 하는 ODBC 정의 문 옵션을 나타내는 경우 드라이버 관리자는를 호출 합니다.  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   *Foption* 이 드라이버 정의 문 옵션을 나타내는 경우 드라이버 관리자는를 호출 합니다.  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 앞의 세 가지 경우에서 *StatementHandle* 인수는 *hstmt*의 값으로 설정 되 고, *특성* 인수는 *foption*의 값으로 설정 되며, 값 *eptr* 인수는 *pvParam*와 동일한 값으로 설정 됩니다.  
  
 ODBC 정의 문자열 연결 옵션의 경우 드라이버 관리자는 **SQLGetConnectAttr** 호출에서 *bufferlength* 인수를 미리 정의 된 최대 길이 (SQL_MAX_OPTION_STRING_LENGTH)로 설정 합니다. 문자열이 아닌 연결 옵션의 경우 *Bufferlength* 는 0으로 설정 됩니다.  
  
 SQL_GET_BOOKMARK 문 옵션 *은 ODBC 3.x*에서 더 이상 사용 되지 않습니다. ODBC *2.x 드라이버가 SQL_GET_BOOKMARK* 를 사용 하는 odbc *2.x 응용 프로그램* 에서 작동 하려면 SQL_GET_BOOKMARK를 지원 해야 합니다. *Odbc 2.x 드라이버에서* odbc *2.x 응용 프로그램* 을 사용 하려면 SQL_UB_ON에 대 한 SQL_USE_BOOKMARKS 설정을 지원 하 고 고정 길이 책갈피를 노출 해야 합니다. *Odbc 2.x 드라이버가 고정* 길이 책갈피가 아닌 가변 길이 책갈피만 지 원하는 경우 odbc *2.x 응용 프로그램이* SQL_USE_BOOKMARKS를 SQL_UB_ON로 설정 하려고 하면 SQLSTATE HYC00 (선택적 기능이 구현 되지 않음)를 반환 해야 합니다.  
  
 ODBC 3.x 드라이버의 경우 드라이버 관리자는 *옵션이* SQL_STMT_OPT_MIN와 SQL_STMT_OPT_MAX 사이에 있는지 여부를 더 이상 확인 하지 않으며 SQL_CONNECT_OPT_DRVR_START 보다 큰지 확인 *합니다.* 드라이버에서이를 확인 해야 합니다.
