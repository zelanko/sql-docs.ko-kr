---
title: "SQLSetScrollOptions 매핑 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetScrollOptions
ms.assetid: a0fa4510-8891-4a61-a867-b2555bc35f05
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e6774f99f1a9596964a965e34f800141fd58e9fb
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetscrolloptions-mapping"></a>SQLSetScrollOptions 매핑
응용 프로그램 호출 하는 경우 **SQLSetScrollOptions** ODBC 3*.x* 드라이버 및 드라이버를 지원 하지 않습니다 **SQLSetScrollOptions**에 대 한 호출  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 다음과 같이 발생 합니다.  
  
-   에 대 한 호출  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     와 *정보 항목* 인수 값에 따라 다음 표의 값 중 하나로 설정 된 *KeysetSize* 인수에 **SQLSetScrollOptions**합니다.  
  
    |*KeysetSize 인수*|*정보 항목 인수*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |보다 큰 값은 *RowsetSize* 인수|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     하는 경우의 값은 *KeysetSize* 앞의 표에서에 대 한 호출에 인수 나타나지 **SQLSetScrollOptions** SQLSTATE S1107 반환 (행 범위를 벗어났습니다. 값) 있고 없는 다음 단계 중 수행 됩니다.  
  
     드라이버 관리자에 적절 한 비트가 설정 여부를 확인 합니다는 **InfoValuePtr* 에 대 한 호출에서 반환 된 값 **SQLGetInfo**, 값에 따라는 *동시성* 인수 **SQLSetScrollOptions**합니다.  
  
    |*동시성* 인수|*정보 항목* 설정|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     경우는 *동시성* 인수 앞의 표에서에 대 한 호출에서 값 중 하나는 **SQLSetScrollOptions** SQLSTATE S1108 반환 (범위를 벗어났습니다. 동시성 옵션) 다음 단계를 수행 됩니다. 적절 한 비트 (앞의 표에 표시 된)으로 설정 되지 않은 경우 **InfoValuePtr* 해당 하는 값 중 하나에 *동시성* 인수에 대 한 호출 ** SQLSetScrollOptions** SQLSTATE S1C00 반환 (드라이버를 사용할 수 없습니다.) 및 없음 다음 단계를 수행 합니다.  
  
-   에 대 한 호출  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     와 * \*ValuePtr* 값에 따라 다음 표의 값 중 하나로 설정 된 *KeysetSize* 인수에 **SQLSetScrollOptions**합니다.  
  
    |*KeysetSize* 인수|*\*ValuePtr*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |보다 큰 값은 *RowsetSize* 인수|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   에 대 한 호출  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     와 * \*ValuePtr* 로 설정 된 *동시성* 인수 **SQLSetScrollOptions**합니다.  
  
-   경우는 *KeysetSize* 호출에 인수 **SQLSetScrollOptions** 이 양수인 경우에 대 한 호출  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     와 * \*ValuePtr* 로 설정 된 *KeysetSize* 인수 **SQLSetScrollOptions**합니다.  
  
-   에 대 한 호출  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     와 * \*ValuePtr* 로 설정 된 *RowsetSize* 인수 **SQLSetScrollOptions**합니다.  
  
    > [!NOTE]  
    >  드라이버 관리자에 매핑합니다 **SQLSetScrollOptions** ODBC 3을 사용 하는 응용 프로그램에 대 한*.x* 지원 하지 않는 드라이버 **SQLSetScrollOptions**, 드라이버 관리자 설정 SQL_ROWSET_SIZE 문 옵션 not SQL_ATTR_ROW_ARRAY_SIZE 문 특성에는 *RowsetSize* 인수 **SQLSetScrollOption**합니다. 결과적으로, **SQLSetScrollOptions** 를 호출 하 여 여러 행을 인출할 때 응용 프로그램에서 사용할 수 없습니다 **SQLFetch** 또는 **SQLFetchScroll**합니다. 호출 하 여 행을 가져오는 여러 경우에 사용할 수 있습니다 **SQLExtendedFetch**합니다.
