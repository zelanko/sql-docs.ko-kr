---
description: SQLSetScrollOptions 매핑
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 111fb84cd584e23b18d889634893556de86311a2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476925"
---
# <a name="sqlsetscrolloptions-mapping"></a>SQLSetScrollOptions 매핑
응용 *프로그램이 ODBC 3.x* 드라이버를 통해 **SQLSetScrollOptions** 를 호출 하 고 드라이버가 **SQLSetScrollOptions**을 지원 하지 않는 경우  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 는 다음과 같이 생성 됩니다.  
  
-   호출입니다.  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     *InfoType* 인수를 다음 표에 있는 값 중 하나로 설정 하 여 **SQLSetScrollOptions**의 *KeysetSize* 인수 값에 따라 설정 합니다.  
  
    |*KeysetSize 인수*|*InfoType 인수*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |*RowsetSize* 인수 보다 큰 값입니다.|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     *KeysetSize* 인수의 값이 앞의 표에 나열 되지 않은 경우 **SQLSetScrollOptions** 에 대 한 호출은 SQLSTATE S1107를 반환 하 고 (행 값이 범위를 벗어남) 다음 단계가 수행 되지 않습니다.  
  
     그런 다음 드라이버 관리자는 **SQLSetScrollOptions**의 *동시성* 인수 값에 따라 **SQLGetInfo**호출에서 반환 된 **infovalueptr* 값에 적절 한 비트가 설정 되어 있는지 여부를 확인 합니다.  
  
    |*Concurrency* 인수|*InfoType* 설정|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     *동시성* 인수가 앞의 표에 있는 값 중 하나가 아닌 경우 **SQLSetScrollOptions** 에 대 한 호출은 SQLSTATE S1108 (동시성 옵션 범위를 벗어남)를 반환 하 고 다음 단계는 수행 하지 않습니다. 위의 표에 나와 있는 것과 같은 적절 한*비트를* *동시성* 인수에 해당 하는 값 중 하나로 설정 하지 않은 경우 **SQLSETSCROLLOPTIONS** 에 대 한 호출은 SQLSTATE S1C00 (드라이버를 사용할 수 없음)를 반환 하 고 다음 단계를 수행 하지 않습니다.  
  
-   호출입니다.  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     **SQLSetScrollOptions**의 *KeysetSize* 인수 값에 따라 다음 표에 있는 값 중 하나로 값 * \* 을 설정 합니다* .  
  
    |*KeysetSize* 인수|*\*ValuePtr*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |*RowsetSize* 인수 보다 큰 값입니다.|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   호출입니다.  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     **SQLSetScrollOptions**의 *동시성* * \* 인수를 이상으로 설정 합니다* .  
  
-   **SQLSetScrollOptions** 에 대 한 호출의 *KeysetSize* 인수가 양수인 경우를 호출 합니다.  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     **SQLSetScrollOptions**의 *KeysetSize* 인수 *를 사용 하 여 인수 \* * 를 설정 합니다.  
  
-   호출입니다.  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     **SQLSetScrollOptions**의 *RowsetSize* 인수 *를 사용 하 여 인수 \* * 를 설정 합니다.  
  
    > [!NOTE]  
    >  드라이버 관리자가 **SQLSetScrollOptions**을 지원 하지 *않는 ODBC 2.x* 드라이버를 사용 하 여 작동 하는 응용 프로그램에 대해 **SQLSetScrollOptions** 를 매핑하는 경우 드라이버 관리자는 SQL_ATTR_ROW_ARRAY_SIZE statement 특성이 아닌 SQL_ROWSET_SIZE 문 옵션을 **SQLSetScrollOption**의 *RowsetSize* 인수로 설정 합니다. 결과적으로 **Sqlfetch** 또는 **sqlfetchscroll**을 호출 하 여 여러 행을 인출 하는 경우 응용 프로그램에서 **SQLSetScrollOptions** 를 사용할 수 없습니다. **Sqlextendedfetch**를 호출 하 여 여러 행을 인출 하는 경우에만 사용할 수 있습니다.
