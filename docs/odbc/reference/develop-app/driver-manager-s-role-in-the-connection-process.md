---
title: 연결 프로세스에서 드라이버 관리자&#39;s 역할 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305804"
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>연결 프로세스에서 드라이버 관리자&#39;s 역할
응용 프로그램은 드라이버 함수를 직접 호출 하지 않습니다. 대신 이름이 같은 드라이버 관리자 함수를 호출 합니다. 드라이버 관리자는 드라이버 함수를 호출 합니다. 일반적으로이는 거의 즉시 발생 합니다. 예를 들어 응용 프로그램은 드라이버 관리자에서 **Sqlexecute** 를 호출 하 고 몇 가지 오류 검사 후 드라이버 관리자는 드라이버에서 **sqlexecute** 를 호출 합니다.  
  
 연결 프로세스가 다릅니다. 응용 프로그램이 SQL_HANDLE_ENV 및 SQL_HANDLE_DBC 옵션을 사용 하 여 **SQLAllocHandle** 를 호출 하면 함수는 드라이버 관리자 에서만 핸들을 할당 합니다. 드라이버 관리자는 호출할 드라이버를 인식 하지 못하기 때문에 드라이버에서이 함수를 호출 하지 않습니다. 마찬가지로 응용 프로그램이 연결 되지 않은 연결의 핸들을 **SQLSetConnectAttr** 또는 **SQLGetConnectAttr**에 전달 하는 경우 드라이버 관리자만 함수를 실행 합니다. 이는 설정 되지 않은 특성 값을 가져올 때, 그리고 ODBC에서 기본값을 정의 하지 않는 경우 해당 연결 핸들에서 특성 값을 저장 하거나 가져오고 SQLSTATE 08003 (연결이 열려 있지 않음)를 반환 합니다.  
  
 응용 프로그램에서 **SQLConnect**, **SQLDriverConnect**또는 **SQLBrowseConnect**를 호출 하는 경우 드라이버 관리자는 먼저 사용할 드라이버를 결정 합니다. 그런 다음 드라이버가 현재 연결에 로드 되어 있는지 여부를 확인 합니다.  
  
-   연결에 드라이버가 로드 되지 않은 경우 드라이버 관리자는 지정 된 드라이버가 동일한 환경의 다른 연결에서 로드 되었는지 여부를 확인 합니다. 그렇지 않으면 드라이버 관리자가 연결에서 드라이버를 로드 하 고 SQL_HANDLE_ENV 옵션을 사용 하 여 드라이버에서 **SQLAllocHandle** 를 호출 합니다.  
  
     그런 다음 드라이버 관리자는 방금 로드 되었는지 여부에 관계 없이 SQL_HANDLE_DBC 옵션을 사용 하 여 드라이버에서 **SQLAllocHandle** 를 호출 합니다. 응용 프로그램에서 연결 특성을 설정 하는 경우 드라이버 관리자는 드라이버에서 **SQLSetConnectAttr** 를 호출 합니다. 오류가 발생 하는 경우 드라이버 관리자의 연결 함수는 SQLSTATE IM006 (드라이버의 **SQLSetConnectAttr** 실패)를 반환 합니다. 마지막으로 드라이버 관리자는 드라이버의 connection 함수를 호출 합니다.  
  
-   지정 된 드라이버가 연결에 로드 되 면 드라이버 관리자는 드라이버의 연결 기능만 호출 합니다. 이 경우 드라이버는 연결의 모든 연결 특성이 현재 설정을 유지 하는지 확인 해야 합니다.  
  
-   연결에서 다른 드라이버가 로드 된 경우 드라이버 관리자는 드라이버에서 **Sqlfreehandle** 을 호출 하 여 연결을 해제 합니다. 드라이버를 사용 하는 다른 연결이 없는 경우 드라이버 관리자는 드라이버에서 **Sqlfreehandle** 을 호출 하 여 환경을 해제 하 고 드라이버를 언로드합니다. 그런 다음 드라이버 관리자는 연결에 드라이버가 로드 되지 않은 경우와 동일한 작업을 수행 합니다.  
  
 *HandleType* 가 **SQL_HANDLE_DBC**로 설정 된 경우 드라이버 관리자는 드라이버의 **SQLAllocHandle** 및 **sqlfreehandle** 을 호출 하기 전에 환경 핸들 (*henv*)을 잠급니다.  
  
 응용 프로그램이 **Sqldisconnect**를 호출 하면 드라이버 관리자는 드라이버에서 **sqldisconnect** 를 호출 합니다. 그러나 응용 프로그램이 드라이버에 다시 연결 하는 경우 드라이버는 로드 된 상태로 유지 됩니다. 응용 프로그램이 SQL_HANDLE_DBC 옵션을 사용 하 여 **sqlfreehandle** 을 호출 하면 드라이버 관리자는 드라이버에서 **sqlfreehandle** 을 호출 합니다. 다른 연결에서 드라이버를 사용 하지 않는 경우 드라이버 관리자는 SQL_HANDLE_ENV 옵션을 사용 하 여 드라이버에서 **Sqlfreehandle** 을 호출 하 고 드라이버를 언로드합니다.
