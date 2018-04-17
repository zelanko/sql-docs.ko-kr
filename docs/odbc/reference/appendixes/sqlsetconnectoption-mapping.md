---
title: SQLSetConnectOption 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetConnectOption
ms.assetid: a1b325cf-0c42-41c1-b141-b5a4fee7e708
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f00b06d0a4a64f1c699267020e20f2ca1d74b220
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsetconnectoption-mapping"></a>SQLSetConnectOption 매핑
경우는 ODBC 2. *x* 응용 프로그램 호출 **SQLSetConnectOption** ODBC 3*.x* 드라이버에 대 한 호출  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 다음과 같이 발생 합니다.  
  
-   경우 *fOption* 드라이버 관리자를 호출 하 여 문자열을 필요로 하는 ODBC 정의 연결 특성을 나타냅니다  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   경우 *fOption* 드라이버 관리자를 호출 하 여 32 비트 정수 값을 반환 하는 ODBC 정의 연결 특성을 나타냅니다.  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   경우 *fOption* 드라이버 관리자를 호출 하 여 드라이버에서 정의 된 연결 특성을 나타냅니다.  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 위의 세 가지 경우는 *ConnectionHandle* 인수에 있는 값으로 설정 되어 *hdbc*, *특성* 인수에 있는 값으로 설정 되어 *fOption* , 및 *ValuePtr* 인수는 동일한 값으로 설정 되어 *vParam*합니다.  
  
 에 대 한 유효한 값을 전달 해야 하는 드라이버 관리자 연결 드라이버에서 정의 된 특성 문자열 또는 32 비트 정수 값을 필요한 지 여부를 알지 못하므로 *BufferLength* 의 인수 **SQLSetConnectAttr**. 드라이버가에 대 한 특별 한 의미를 정의 하는 경우 드라이버에서 정의 된 연결 특성 및 사용 하 여 호출 해야 **SQLSetConnectOption**를 지원 해야 합니다 **SQLSetConnectOption**합니다.  
  
 경우에는 ODBC 2입니다. *x* 응용 프로그램 호출 **SQLSetConnectOption** ODBC 3에서 드라이버별 문 옵션을 설정 하려면*.x* 드라이버 및 옵션에에서 정의 되어 있는 ODBC 2. *x* ODBC 3의 옵션에 대 한 버전의 드라이버를 새 매니페스트 상수를 정의 해야*.x* 드라이버입니다. 오래 된 매니페스트 상수에 대 한 호출에 사용 되는 경우 **SQLSetConnectOption**, 드라이버 관리자를 호출 합니다 **SQLSetConnectAttr** 와 **StringLength** 인수는 0으로 설정 합니다.  
  
 ODBC 3에 대 한*.x* 드라이버를 드라이버 관리자는 더 이상 있는지 여부를 확인 *fOption* 사이 SQL_CONN_OPT_MIN 및 SQL_CONN_OPT_MAX, 또는 SQL_CONNECT_OPT_DRVR_START 보다 큽니다.  
  
## <a name="setting-statement-options-on-the-connection-level"></a>연결 수준에서 문 옵션 설정  
 Odbc 2. *x*, 응용 프로그램에서 호출할 수 **SQLSetConnectOption** 문 옵션을 설정 하려면. 드라이버 문 옵션을 기본값으로 설정 완료 되 면 해당 연결에 할당 된 나중에 문의 합니다. 드라이버-정의 된 여부 드라이버 지정된 연결과 관련 된 모든 기존 문 문 옵션을 설정 합니다.  
  
 ODBC 3에는이 기능을 더 이상 사용 되지*.x*합니다. ODBC 3*.x* 드라이버 설정 ODBC 2를 지원만 필요 합니다. *x* ODBC 2를 사용 하는 경우에 연결 수준 문 특성. *x* 이 작업을 수행 하는 응용 프로그램입니다. ODBC 3*.x* 응용 프로그램 연결 수준에서 문 특성을 설정 해서는 안됩니다. ODBC 3*.x* 연결 특성 및 문 특성 모두에 있으며 수 있는 SQL_ATTR_METADATA_ID 및 SQL_ATTR_ASYNC_ENABLE 특성을 제외 하 고 연결 수준에서 문 특성을 설정할 수 없습니다 연결 수준 또는 문 수준에서 설정 합니다.
