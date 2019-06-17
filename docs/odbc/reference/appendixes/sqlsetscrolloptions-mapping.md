---
title: SQLSetScrollOptions 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetScrollOptions
ms.assetid: a0fa4510-8891-4a61-a867-b2555bc35f05
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5520554b509b0c25d62e4a191e16ad3524a02652
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63297456"
---
# <a name="sqlsetscrolloptions-mapping"></a>SQLSetScrollOptions 매핑
응용 프로그램을 호출할 때 **SQLSetScrollOptions** 는 ODBC 3 *.x* 드라이버 및 드라이버 지원 하지 않습니다 **SQLSetScrollOptions**에 대 한 호출  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 다음과 같이 발생 합니다.  
  
-   에 대 한 호출  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     사용 하 여는 *정보 항목* 인수 값에 따라 다음 표의 값 중 하나로 설정 합니다 *KeysetSize* 에서 인수 **SQLSetScrollOptions**합니다.  
  
    |*KeysetSize 인수*|*정보 항목 인수*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |보다 큰 값을 *RowsetSize* 인수|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     경우의 값을 *KeysetSize* 인수 앞의 표에서에 대 한 호출에 나타나지 **SQLSetScrollOptions** SQLSTATE S1107 반환 (행 범위를 벗어났습니다. 값) 및 다음 단계를 모두 수행 합니다.  
  
     드라이버 관리자는 다음 적절 한 비트를 설정할지 여부를 확인 합니다 **InfoValuePtr* 에 대 한 호출에서 반환 된 값 **SQLGetInfo**, 값에 따라는 *동시성* 에 인수 **SQLSetScrollOptions**합니다.  
  
    |*동시성* 인수|*정보 항목* 설정|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     경우는 *동시성* 인수가 위의 테이블에 대 한 호출에서 값 중 하나가 아닙니다 **SQLSetScrollOptions** SQLSTATE S1108를 반환 합니다 (범위를 벗어났습니다. 동시성 옵션) 다음 단계를 하나도 되며 수행 합니다. (앞의 표에 표시 된)으로 적절 한 비트를 설정 하지 않으면 **InfoValuePtr* 해당 하는 값 중 하나에 *동시성* 인수를 호출  **SQLSetScrollOptions** SQLSTATE S1C00 반환 (드라이버를 사용할 수 없습니다.) 및 none 다음 단계를 수행 합니다.  
  
-   에 대 한 호출  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     사용 하 여  *\*ValuePtr* 값에 따라 다음 표의 값 중 하나로 설정 합니다 *KeysetSize* 에서 인수 **SQLSetScrollOptions**합니다.  
  
    |*KeysetSize* 인수|*\*ValuePtr*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |보다 큰 값을 *RowsetSize* 인수|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   에 대 한 호출  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     사용 하 여  *\*ValuePtr* 로 설정 합니다 *동시성* 에서 인수 **SQLSetScrollOptions**합니다.  
  
-   경우는 *KeysetSize* 호출에서 인수 **SQLSetScrollOptions** 이 양수인 경우에 대 한 호출  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     사용 하 여  *\*ValuePtr* 로 설정 합니다 *KeysetSize* 에서 인수 **SQLSetScrollOptions**합니다.  
  
-   에 대 한 호출  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     사용 하 여  *\*ValuePtr* 로 설정 합니다 *RowsetSize* 에서 인수 **SQLSetScrollOptions**합니다.  
  
    > [!NOTE]  
    >  때 드라이버 관리자 매핑합니다 **SQLSetScrollOptions** 는 ODBC 3을 사용 하는 응용 프로그램에 대 한 *.x* 지원 하지 않는 드라이버 **SQLSetScrollOptions**, 드라이버 관리자에 not SQL_ATTR_ROW_ARRAY_SIZE 문 특성 SQL_ROWSET_SIZE 문 옵션을 설정 합니다는 *RowsetSize* 에서 인수 **SQLSetScrollOption**합니다. 따라서 **SQLSetScrollOptions** 를 호출 하 여 여러 행을 인출할 때 응용 프로그램에서 사용할 수 없습니다 **SQLFetch** 하거나 **SQLFetchScroll**합니다. 호출 하 여 행을 가져오는 여러 경우에 사용할 수 있습니다 **SQLExtendedFetch**합니다.
