---
title: SQLSetConnect옵션 매핑 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetConnectOption
ms.assetid: a1b325cf-0c42-41c1-b141-b5a4fee7e708
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 757b50c7e18133e02b4cf6addaa327b2053f5439
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287473"
---
# <a name="sqlsetconnectoption-mapping"></a>SQLSetConnectOption 매핑
때 ODBC 2. *x* 응용 프로그램은 ODBC 3 *.x* 드라이버를 통해 **SQLSetConnectOption을** 호출합니다.  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 다음과 같이 발생합니다.  
  
-   *fOption* 문자열이 필요한 ODBC 정의 연결 특성을 나타내는 경우 드라이버 관리자는  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   *fOption이* 32비트 정수 값을 반환하는 ODBC 정의 연결 특성을 나타내는 경우 드라이버 관리자는  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   *fOption이* 드라이버 정의 연결 특성을 나타내는 경우 드라이버 관리자는  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 앞의 세 가지 경우에서 *ConnectionHandle* 인수는 *hdbc의*값으로 설정되고 *특성* 인수는 *fOption의*값으로 설정되고 *ValuePtr* 인수는 *vParam과*동일한 값으로 설정됩니다.  
  
 드라이버 관리자는 드라이버 정의 연결 특성에 문자열 또는 32비트 정수 값이 필요한지 여부를 알 수 없으므로 **SQLSetConnectAttr**의 *BufferLength* 인수에 대해 유효한 값을 전달해야 합니다. 드라이버가 드라이버 정의 연결 특성에 대한 특수 의미 체계를 정의하고 **SQLSetConnectOption을**사용하여 호출해야 하는 경우 **SQLSetConnectOption**을 지원해야 합니다.  
  
 ODBC 2의 경우. *x* 응용 프로그램은 **SQLSetConnectOption을** 호출하여 ODBC*3.x* 드라이버에서 드라이버별 명령문 옵션을 설정하고 이 옵션은 ODBC 2에 정의되었습니다. *x* 버전의 드라이버에는 ODBC*3.x* 드라이버의 옵션에 대해 새 매니페스트 상수가 정의되어야 합니다. 이전 매니페스트 상수가 **SQLSetConnectOption**호출에서 사용되는 경우 드라이버 관리자는 **SQLSetConnectAttr을** **문자열 길이** 인수를 0으로 설정하여 호출합니다.  
  
 ODBC*3.x* 드라이버의 경우 드라이버 관리자는 더 이상 *fOption이* SQL_CONN_OPT_MIN SQL_CONN_OPT_MAX 사이에 있는지 또는 SQL_CONNECT_OPT_DRVR_START 보다 큰지 확인하지 않습니다.  
  
## <a name="setting-statement-options-on-the-connection-level"></a>연결 수준에서 문 옵션 설정  
 ODBC 2. *x,* 응용 프로그램은 **SQLSetConnectOption을** 호출하여 명령문 옵션을 설정할 수 있습니다. 이 작업이 완료되면 드라이버는 나중에 해당 연결에 할당된 모든 문에 대해 명령문 옵션을 기본값으로 설정합니다. 드라이버가 지정된 연결과 연결된 기존 문에 대해 명령문 옵션을 설정하는지 여부를 드라이버 정의합니다.  
  
 이 기능은 ODBC 3 *.x에서*더 이상 사용되지 않습니다. ODBC 3 *.x* 드라이버는 ODBC 2 설정만 지원하면 됩니다. *그들은* ODBC 2와 함께 작업하려는 경우 연결 수준에서 x 문 특성. *이* 작업을 수행하는 x 응용 프로그램. ODBC 3 *.x* 응용 프로그램은 연결 수준에서 문 특성을 설정해서는 안 됩니다. ODBC 3 *.x* 문 특성은 연결 특성과 SQL_ATTR_ASYNC_ENABLE 특성을 SQL_ATTR_METADATA_ID 제외하고 연결 수준에서 설정할 수 없으며 연결 특성 및 문 특성모두이며 연결 수준 또는 문 수준에서 설정할 수 있습니다.
