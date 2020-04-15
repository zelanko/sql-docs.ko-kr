---
title: SQLSet스크롤옵션 매핑 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 77050df283b10abd17ba62a48bd366d6c1b3f601
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300503"
---
# <a name="sqlsetscrolloptions-mapping"></a>SQLSetScrollOptions 매핑
응용 프로그램이 ODBC *3.x* 드라이버를 통해 **SQLSetScrollOptions를** 호출하고 드라이버가 **SQLSetScrollOptions를**지원하지 않는 경우  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 다음과 같이 발생합니다.  
  
-   에 대한 호출  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     *INFOType* 인수는 **SQLSetScrollOptions의** *KeysetSize* 인수의 값에 따라 다음 테이블의 값 중 하나로 설정됩니다.  
  
    |*키셋크기 인수*|*인포타이핑 인수*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |*RowsetSize* 인수보다 큰 값|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     *KeysetSize* 인수의 값이 이전 테이블에 나열 되지 않은 경우 **SQLSetScrollOptions** 호출 SQLSTATE S1107 (행 값 범위를 벗어난) 반환 하 고 다음 단계 중 아무 것도 수행 되지 않습니다.  
  
     그런 다음 드라이버 관리자는 **SQLSetScrollOptions의** *동시성* 인수 값에 따라 **SQLGetInfo**호출에서 반환되는 **InfoValuePtr* 값에 적절한 비트가 설정되어 있는지 여부를 확인합니다.  
  
    |*동시성* 인수|*정보 유형* 설정|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     *동시성* 인수가 이전 테이블의 값 중 하나가 아닌 경우 **SQLSetScrollOptions** 호출은 SQLSTATE S1108(동시성 옵션 범위 제외)을 반환하며 다음 단계 중 어느 것도 수행되지 않습니다. 적절한 비트(앞표에 표시된 대로)가 **InfoValuePtr에서* *동시성* 인수에 해당하는 값 중 하나에 설정되지 않은 경우 **SQLSetScrollOptions호출은 SQLSTATE** S1C00(드라이버를 사용할 수 없음)을 반환하며 다음 단계 중 어느 것도 수행되지 않습니다.  
  
-   에 대한 호출  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     **SQLSetScrollOptions에서** *KeysetSize* 인수의 값에 따라 다음 테이블의 값 중 하나에 ValuePtr 설정 . * \**  
  
    |*키셋크기* 인수|*\*밸류Ptr*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |*RowsetSize* 인수보다 큰 값|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   에 대한 호출  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     VALUEPtr **SQLSetScrollOptions에서** *동시성* 인수로 설정 . * \**  
  
-   **SQLSetScrollOptions에** 대한 호출의 *KeysetSize* 인수가 양수인 경우  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     ValuePtr을 *키셋으로* 설정하여 **SQLSetScrollOptions**. * \**  
  
-   에 대한 호출  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     ValuePtr을 **사용하여 SQLSetScrollOptions에서** *RowsetSize* 인수로 설정합니다. * \**  
  
    > [!NOTE]  
    >  드라이버 **관리자가 SQLSetScrollOptions를** 지원하지 않는 ODBC *3.x* 드라이버로 작업하는 응용 프로그램에 대해 **SQLSetScrollOptions를**매핑할 때 드라이버 관리자는 SQL_ATTR_ROW_ARRAY_SIZE 문 특성이 아닌 SQL_ROWSET_SIZE 명령문 옵션을 **SQLSetScrollOption의** *RowsetSize* 인수로 설정합니다. 따라서 SQLFetch스크롤 에 대한 호출로 여러 행을 가져올 때 응용 프로그램에서 **SQLFetchScroll** **SQLSetScroll 옵션을** 사용할 수 없습니다. **SQLFetch** **SQLExtendedFetch**에 대한 호출로 여러 행을 가져올 때만 사용할 수 있습니다.
