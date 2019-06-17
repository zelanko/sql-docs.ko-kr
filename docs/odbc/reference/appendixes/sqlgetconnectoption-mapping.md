---
title: SQLGetConnectOption 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLGetConnectOption
- SQLGetConnectOption function [ODBC], mapping
ms.assetid: e3792fe4-a955-473a-a297-c1b2403660c4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8504709cb2cedb36c62bb9be74ffc8d12a4c811d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188792"
---
# <a name="sqlgetconnectoption-mapping"></a>SQLGetConnectOption 매핑
응용 프로그램을 호출할 때 **SQLGetConnectOption** 는 ODBC 3 *.x* 드라이버에 대 한 호출  
  
```  
SQLGetConnectOption(hdbc, fOption, pvParam)   
```  
  
 다음과 같이 매핑됩니다.  
  
-   하는 경우 *fOption* 드라이버 관리자를 호출 하 여 문자열을 반환 하는 ODBC 정의한 연결 옵션을 나타냅니다.  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   하는 경우 *fOption* 드라이버 관리자를 호출 하 여 32 비트 정수 값을 반환 하는 ODBC 정의한 연결 옵션을 나타냅니다.  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   하는 경우 *fOption* 드라이버 관리자를 호출 하 여 드라이버에서 정의 된 문 옵션을 나타냅니다.  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 위의 세 가지 경우에 *ConnectionHandle* 인수를 값으로 설정 *hdbc*의 *특성* 인수를 값으로 설정 *fOption* , 및 *ValuePtr* 인수가 동일한 값으로 설정 되어 *pvParam*합니다.  
  
 드라이버 관리자 ODBC 정의 문자열 연결 옵션을 설정 합니다 *BufferLength* 호출에 인수 **SQLGetConnectAttr** 미리 정의 된 최대 길이 (SQL_MAX_OPTION_STRING_LENGTH); 문자열이 아닌 연결 옵션의 경우 *BufferLength* 0으로 설정 됩니다.  
  
 ODBC 3 *.x* 드라이버를 드라이버 관리자는 더 이상 있는지 확인 합니다 *옵션* SQL_CONN_OPT_MIN 사이의 SQL_CONN_OPT_MAX, 되었거나 SQL_CONNECT_OPT_DRVR_START 보다 큽니다. 드라이버 옵션 값의 유효성을 검사 해야 합니다.
