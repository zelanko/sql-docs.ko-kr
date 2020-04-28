---
title: SQLSetConnectOption 매핑 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287473"
---
# <a name="sqlsetconnectoption-mapping"></a>SQLSetConnectOption 매핑
ODBC 2 인 경우 *x* 응용 프로그램은 ODBC 3.x 드라이버를 통해 **SQLSetConnectOption** 를 호출 합니다 *.*  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 는 다음과 같이 생성 됩니다.  
  
-   *Foption* 은 문자열이 필요한 ODBC 정의 연결 특성을 나타내는 경우 드라이버 관리자는를 호출 합니다.  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   *Foption* 이 32 비트 정수 값을 반환 하는 ODBC 정의 연결 특성을 나타내는 경우 드라이버 관리자는를 호출 합니다.  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   *Foption* 이 드라이버 정의 연결 특성을 나타내는 경우 드라이버 관리자는를 호출 합니다.  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 앞의 세 가지 경우에서 *ConnectionHandle* 인수는 *hdbc*의 값으로 설정 되 고, *특성* 인수는 *foption*의 값으로 설정 되며, 가산 *eptr* 인수는 *vparam*과 동일한 값으로 설정 됩니다.  
  
 드라이버 관리자는 드라이버 정의 연결 특성에 문자열 또는 32 비트 정수 값이 필요한 지 여부를 알 수 없으므로 **SQLSetConnectAttr**의 *bufferlength* 인수에 유효한 값을 전달 해야 합니다. 드라이버가 드라이버 정의 연결 특성에 대 한 특수 한 의미 체계를 정의 하 고 **SQLSetConnectOption**를 사용 하 여 호출 해야 하는 경우 **SQLSetConnectOption**를 지원 해야 합니다.  
  
 ODBC 2 인 경우 *x* 응용 프로그램은 **SQLSetConnectOption** 를 호출 하 여 odbc*3.x 드라이버에서* 드라이버별 문 옵션을 설정 하 고, 옵션은 odbc 2에서 정의 되었습니다. *x* 버전 드라이버의 경우 ODBC*3.x 드라이버의* 옵션에 대해 새 매니페스트 상수를 정의 해야 합니다. **SQLSetConnectOption**에 대 한 호출에서 이전 매니페스트 상수를 사용 하는 경우 드라이버 관리자는 **stringlength** 인수를 0으로 설정 하 여 **SQLSetConnectAttr** 를 호출 합니다.  
  
 ODBC*3.x 드라이버의* 경우 드라이버 관리자는 더 이상 *foption* 이 SQL_CONN_OPT_MIN와 SQL_CONN_OPT_MAX 사이에 있는지 또는 SQL_CONNECT_OPT_DRVR_START 보다 큰지 확인 하지 않습니다.  
  
## <a name="setting-statement-options-on-the-connection-level"></a>연결 수준에서 문 옵션 설정  
 ODBC 2. *x*는 응용 프로그램에서 **SQLSetConnectOption** 를 호출 하 여 문 옵션을 설정할 수 있습니다. 이 작업이 완료 되 면 드라이버는 해당 연결에 대해 나중에 할당 된 모든 문의 기본값으로 문 옵션을 설정 합니다. 드라이버에서 지정 된 연결과 관련 된 기존 문에 대해 문 옵션을 설정 하는지 여부를 드라이버에서 정의 합니다.  
  
 이 기능은 ODBC 3.x에서 더 이상 사용 되지*않습니다.* ODBC 3.x*드라이버는* odbc 2 설정만 지원 하면 됩니다. ODBC 2를 사용 하려는 경우 연결 수준의 *x* 문 특성 이 작업을 수행 하는 *x* 응용 프로그램입니다. ODBC 3.x*응용 프로그램은 연결* 수준에서 문 특성을 설정 하면 안 됩니다. ODBC 3.x 문 특성은 연결 수준에서 설정할 수 없습니다 *.* SQL_ATTR_METADATA_ID 및 SQL_ATTR_ASYNC_ENABLE 특성은 연결 특성과 문 특성 모두 이며 연결 수준 또는 문 수준에서 설정할 수 있습니다.
