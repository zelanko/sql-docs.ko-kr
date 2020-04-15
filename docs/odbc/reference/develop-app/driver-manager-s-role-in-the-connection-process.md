---
title: 드라이버 관리자&#39;연결 프로세스에서 역할 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], role in connection process
- connecting to data source [ODBC], driver manager
- connecting to driver [ODBC], driver manager
- ODBC driver manager [ODBC]
ms.assetid: 77c05630-5a8b-467d-b80e-c705dc06d601
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0227a4063573cb05ecaa9434605ba35f2811bd06
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305804"
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>연결 프로세스에서 드라이버 관리자&#39;역할
응용 프로그램은 드라이버 함수를 직접 호출하지 않습니다. 대신 동일한 이름의 Driver Manager 함수를 호출하고 드라이버 관리자는 드라이버 함수를 호출합니다. 보통, 이것은 거의 즉시 발생합니다. 예를 들어 응용 프로그램은 드라이버 관리자에서 **SQLExecute를** 호출하고 몇 가지 오류 검사 후 드라이버 관리자는 드라이버에서 **SQLExecute를** 호출합니다.  
  
 연결 프로세스가 다릅니다. 응용 프로그램이 SQL_HANDLE_ENV 및 SQL_HANDLE_DBC 옵션을 사용하여 **SQLAllocHandle을** 호출하면 함수는 드라이버 관리자에서만 핸들을 할당합니다. 드라이버 관리자는 호출할 드라이버를 알 수 없으므로 드라이버에서 이 함수를 호출하지 않습니다. 마찬가지로 응용 프로그램이 **SQLSetConnectAttr** 또는 **SQLGetConnectAttr에**연결되지 않은 연결의 핸들을 전달하는 경우 드라이버 관리자만 함수를 실행합니다. 설정되지 않은 특성과 ODBC가 기본값을 정의하지 않는 특성에 대한 값을 가져오는 경우 연결 핸들에서 특성 값을 저장하거나 가져옵니다.  
  
 응용 프로그램에서 **SQLConnect,** **SQLDriverConnect**또는 **SQLBrowseConnect를**호출할 때 드라이버 관리자는 먼저 사용할 드라이버를 결정합니다. 그런 다음 드라이버가 현재 연결에 로드되어 있는지 여부를 확인합니다.  
  
-   연결에 로드된 드라이버가 없는 경우 드라이버 관리자는 지정된 드라이버가 동일한 환경에서 다른 연결에 로드되었는지 여부를 확인합니다. 그렇지 않은 경우 드라이버 관리자는 연결에 드라이버를 로드 하 고 SQL_HANDLE_ENV 옵션으로 드라이버에서 **SQLAllocHandle를** 호출 합니다.  
  
     그런 다음 드라이버 관리자는 방금 로드되었는지 여부에 관계없이 SQL_HANDLE_DBC 옵션을 사용 하 고 드라이버에서 **SQLAllocHandle을** 호출 합니다. 응용 프로그램에서 연결 특성을 설정하면 드라이버 관리자는 드라이버에서 **SQLSetConnectAttr을** 호출합니다. 오류가 발생하면 드라이버 관리자의 연결 함수가 SQLSTATE IM006(드라이버의 **SQLSetConnectAttr** 실패)을 반환합니다. 마지막으로 드라이버 관리자는 드라이버의 연결 함수를 호출합니다.  
  
-   지정된 드라이버가 연결에 로드된 경우 드라이버 관리자는 드라이버의 연결 기능만 호출합니다. 이 경우 드라이버는 연결의 모든 연결 특성이 현재 설정을 유지관리해야 합니다.  
  
-   다른 드라이버가 연결에 로드된 경우 드라이버 관리자는 드라이버에서 **SQLFreeHandle을** 호출하여 연결을 해제합니다. 드라이버를 사용하는 다른 연결이 없는 경우 드라이버 관리자는 드라이버에서 **SQLFreeHandle을** 호출하여 환경을 해제하고 드라이버를 언로드합니다. 그런 다음 드라이버 관리자는 드라이버가 연결에 로드되지 않은 경우와 동일한 작업을 수행합니다.  
  
 핸들 *유형이* **SQL_HANDLE_DBC**설정된 경우 드라이버의 **SQLAllocHandle** 및 **SQLFreeHandle을** 호출하기 전에 드라이버 관리자는 환경*핸들(henv)을*잠급니다.  
  
 응용 프로그램에서 **SQLDisconnect를**호출하면 드라이버 관리자는 드라이버에서 **SQLDisconnect를** 호출합니다. 그러나 응용 프로그램이 드라이버에 다시 연결되는 경우 드라이버를 로드합니다. 응용 프로그램이 SQL_HANDLE_DBC 옵션으로 **SQLFreeHandle을** 호출하면 드라이버 관리자는 드라이버에서 **SQLFreeHandle을** 호출합니다. 드라이버가 다른 연결에서 사용되지 않는 경우 드라이버 관리자는 SQL_HANDLE_ENV 옵션을 사용하여 드라이버에서 **SQLFreeHandle을** 호출하고 드라이버를 언로드합니다.
