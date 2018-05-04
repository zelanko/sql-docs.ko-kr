---
title: 드라이버 관리자&#39;연결 과정 중에 역할 s | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], role in connection process
- connecting to data source [ODBC], driver manager
- connecting to driver [ODBC], driver manager
- ODBC driver manager [ODBC]
ms.assetid: 77c05630-5a8b-467d-b80e-c705dc06d601
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 85839606036b56f058f6347b57d45ca296e23b96
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>드라이버 관리자&#39;연결 과정에서 s 역할
응용 프로그램 직접 호출 하지 않습니다 드라이버 기능인 기억 합니다. 대신, 동일한 이름 가진 드라이버 관리자 함수를 호출 하 고 드라이버 관리자 드라이버 함수를 호출 합니다. 일반적으로 거의 즉시 전파 됩니다. 예를 들어 응용 프로그램 호출 **SQLExecute** 드라이버 관리자를 호출 하는 드라이버 관리자와 후 몇 가지 오류 검사 **SQLExecute** 드라이버에서입니다.  
  
 연결 프로세스는 다릅니다. 응용 프로그램 호출 하는 경우 **SQLAllocHandle** 함수 SQL_HANDLE_ENV 및 sql_handle_dbc 라는 옵션 드라이버 관리자에만 핸들을 할당 합니다. 드라이버 관리자를 호출 하는 드라이버를 알지 못하므로 드라이버에서이 함수를 호출 하지 않습니다. 마찬가지로, 응용 프로그램에 대 한 연결 되지 않은 연결의 핸들을 전달 하는 경우 **SQLSetConnectAttr** 또는 **SQLGetConnectAttr**함수를 실행 하는 드라이버 관리자만 필요 합니다. 저장 하거나 처리 하 고 특성에 대 한 값을 가져올 설정 되지 않은 경우 및는 odbc SQLSTATE 08003 (열려 있지 않습니다. 연결)를 반환 하는 연결에서 특성 값을 가져옵니다 기본값을 정의 하지 않습니다.  
  
 응용 프로그램 호출 하는 경우 **SQLConnect**, **SQLDriverConnect**, 또는 **SQLBrowseConnect**, 드라이버 관리자는 먼저 드라이버를 사용 하 여 확인 합니다. 그런 다음 드라이버는 연결에 현재 로드 되어 있는지 여부를 확인 하려면 확인:  
  
-   드라이버가 없는 연결에 로드 되 면 드라이버 관리자는 동일한 환경에서 다른 연결에 지정된 된 드라이버 로드 되는지 여부를 확인 합니다. 드라이버 관리자 연결 및 호출의 드라이버를 로드 하지, **SQLAllocHandle** SQL_HANDLE_ENV 옵션을 사용 하 여 드라이버에서 합니다.  
  
     드라이버 관리자는 다음 호출 **SQLAllocHandle** sql_handle_dbc 라는 옵션과 함께 드라이버에서 여부 것 바로 로드 되었습니다. 드라이버 관리자를 호출 하는 응용 프로그램 연결 특성을 설정 하는 경우 **SQLSetConnectAttr** ; 드라이버에서 오류가 발생 하는 경우 드라이버 관리자 연결 함수 반환 SQLSTATE IM006 (드라이버의  **SQLSetConnectAttr** 실패). 마지막으로, 드라이버 관리자는 드라이버에서 연결 함수를 호출합니다.  
  
-   지정된 된 드라이버는 연결에 로드 되 면 드라이버 관리자 드라이버에만 연결 함수를 호출 합니다. 이 경우 드라이버는 연결에서 모든 연결 특성의 현재 설정은 유지 하는 확인 해야 합니다.  
  
-   드라이버 관리자를 호출 하는 다른 드라이버는 연결에 로드 되 면 **SQLFreeHandle** 연결을 해제 하도록 드라이버에 있습니다. 드라이버 관리자를 호출 하는 드라이버를 사용 하 여 연결이 없는 경우 **SQLFreeHandle** 환경을 해제 하도록 드라이버에 하 고 드라이버를 언로드합니다. 드라이버 관리자 연결에는 드라이버가 로드 되지 않은 경우와 동일한 작업을 수행 합니다.  
  
 드라이버 관리자 환경 핸들을 잠가 (*henv*) 드라이버의를 호출 하기 전에 **SQLAllocHandle** 및 **SQLFreeHandle** 때 *HandleType* 로 설정 된 **sql_handle_dbc 라는**합니다.  
  
 응용 프로그램 호출 하는 경우 **SQLDisconnect**, 드라이버 관리자를 호출 하 여 **SQLDisconnect** 드라이버에서입니다. 그러나 응용 프로그램이 드라이버에 다시 연결 하는 경우 로드 된 드라이버를 유지 합니다. 응용 프로그램 호출 하는 경우 **SQLFreeHandle** 드라이버 관리자를 sql_handle_dbc 라는 옵션으로 호출 **SQLFreeHandle** 드라이버에서입니다. 드라이버 관리자는 다음 호출 다른 연결에서 드라이버를 사용 하지 않는 경우 **SQLFreeHandle** 옵션는 SQL_HANDLE_ENV 사용 하 여 드라이버에 선택한 드라이버를 언로드합니다.
