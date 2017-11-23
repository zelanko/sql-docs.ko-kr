---
title: "SQLGetConnectOption 매핑 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLGetConnectOption
- SQLGetConnectOption function [ODBC], mapping
ms.assetid: e3792fe4-a955-473a-a297-c1b2403660c4
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 293f6985cd81d92b8de2b264cd69216feaff00cb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlgetconnectoption-mapping"></a>SQLGetConnectOption 매핑
응용 프로그램 호출 하는 경우 **SQLGetConnectOption** ODBC 3*.x* 드라이버에 대 한 호출  
  
```  
SQLGetConnectOption(hdbc, fOption, pvParam)   
```  
  
 다음과 같이 매핑됩니다.  
  
-   경우 *fOption* 드라이버 관리자를 호출 하 여 문자열을 반환 하는 ODBC 정의 된 연결 옵션을 나타냅니다.  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   경우 *fOption* 드라이버 관리자를 호출 하 여 32 비트 정수 값을 반환 하는 ODBC 정의 된 연결 옵션을 나타냅니다.  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   경우 *fOption* 드라이버 관리자를 호출 하 여 드라이버에서 정의 된 문 옵션을 나타냅니다.  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 위의 세 가지 경우는 *ConnectionHandle* 인수에 있는 값으로 설정 되어 *hdbc*, *특성* 인수에 있는 값으로 설정 되어 *fOption* , 및 *ValuePtr* 인수는 동일한 값으로 설정 되어 *pvParam*합니다.  
  
 ODBC 정의 문자열 연결 옵션에 대 한 드라이버 관리자는 다음과 같이 설정 됩니다.는 *BufferLength* 호출에 인수 **SQLGetConnectAttr** 미리 정의 된 최대 길이 (SQL_MAX_OPTION_STRING_LENGTH); 문자열이 아닌 연결 옵션에 대 한 *BufferLength* 0으로 설정 됩니다.  
  
 ODBC 3에 대 한*.x* 드라이버를 드라이버 관리자는 더 이상 있는지 여부를 확인 *옵션* 사이 SQL_CONN_OPT_MIN 및 SQL_CONN_OPT_MAX, 또는 SQL_CONNECT_OPT_DRVR_START 보다 큽니다. 드라이버 옵션 값의 유효성을 검사 해야 합니다.
