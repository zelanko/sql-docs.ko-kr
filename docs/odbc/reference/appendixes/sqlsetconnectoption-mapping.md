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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b512a795c3b9e2d1c6aa1c7c9e92fbc42a8c7862
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125585"
---
# <a name="sqlsetconnectoption-mapping"></a>SQLSetConnectOption 매핑
경우는 ODBC 2. *x* 응용 프로그램 호출 **SQLSetConnectOption** ODBC 3를 통해 *.x* 드라이버에 대 한 호출  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 다음과 같이 발생 합니다.  
  
-   하는 경우 *fOption* 드라이버 관리자를 호출 하 여 문자열을 필요로 하는 ODBC 정의한 연결 특성을 나타냅니다  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   하는 경우 *fOption* 드라이버 관리자를 호출 하 여 32 비트 정수 값을 반환 하는 ODBC 정의한 연결 특성을 나타냅니다.  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   하는 경우 *fOption* 드라이버 관리자를 호출 하 여 드라이버에서 정의 된 연결 특성을 나타냅니다.  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 위의 세 가지 경우에 *ConnectionHandle* 인수를 값으로 설정 *hdbc*의 *특성* 인수를 값으로 설정 *fOption* , 및 *ValuePtr* 인수가 동일한 값으로 설정 되어 *갖고*합니다.  
  
 에 대 한 유효한 값을 전달 해야 하는 드라이버 관리자 연결 드라이버에서 정의 된 특성을 문자열 또는 32 비트 정수 값을 필요한 지 여부를 알지 못하므로 합니다 *BufferLength* 인수의 **SQLSetConnectAttr**. 드라이버가에 대 한 특별 한 의미를 정의 하는 경우 드라이버에서 정의 된 연결 특성 및 요구 사항을 사용 하 여 호출할 **SQLSetConnectOption**를 지원 해야 합니다 **SQLSetConnectOption**합니다.  
  
 경우에는 ODBC 2입니다. *x* 응용 프로그램 호출 **SQLSetConnectOption** 는 ODBC 3 드라이버별 문 옵션을 설정 하려면 *.x* 옵션과 드라이버는 ODBC 2에 정의 된. *x* ODBC 3에서 옵션에 대 한 버전의 드라이버를 새 매니페스트 상수를 정의 해야 *.x* 드라이버입니다. 오래 된 매니페스트 상수에 대 한 호출에 사용 되는 경우 **SQLSetConnectOption**, 드라이버 관리자를 호출 합니다 **SQLSetConnectAttr** 사용 하 여 합니다 **StringLength** 인수는 0으로 설정 합니다.  
  
 ODBC 3 *.x* 드라이버를 드라이버 관리자는 더 이상 있는지 확인 합니다 *fOption* SQL_CONN_OPT_MIN 사이의 SQL_CONN_OPT_MAX, 되었거나 SQL_CONNECT_OPT_DRVR_START 보다 큽니다.  
  
## <a name="setting-statement-options-on-the-connection-level"></a>연결 수준에서 문 옵션 설정  
 Odbc 2. *x*, 응용 프로그램이 호출할 수 없습니다 **SQLSetConnectOption** 문 옵션을 설정 합니다. 드라이버 기본값으로 문 옵션을 설정 하는 완료 되 면 해당 연결에 대 한 나중에 할당 된 모든 문에 대 한 합니다. 이 드라이버에서 정의 된 드라이버 지정된 연결과 관련 된 모든 기존 문에 대 한 문 옵션을 설정 하는지 여부를 합니다.  
  
 ODBC 3에서이 기능은 사용 되지 *.x*합니다. ODBC 3 *.x* 드라이버 ODBC 2 설정 지원 해야 합니다. *x* ODBC 2를 사용 하는 경우 연결 수준에서 문 특성. *x* 이 작업을 수행 하는 응용 프로그램입니다. ODBC 3 *.x* 응용 프로그램 연결 수준에서 문 특성을 설정 해서는 안됩니다. ODBC 3 *.x* 문 특성은 연결 특성 및 문 특성을 모두 수 있으며 SQL_ATTR_METADATA_ID 및 SQL_ATTR_ASYNC_ENABLE 특성을 제외 하 고 연결 수준에서 설정할 수 없습니다 연결 수준 또는 문 수준에서 설정 합니다.
