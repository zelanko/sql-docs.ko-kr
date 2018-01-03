---
title: "환경이 전환 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- environment transitions [ODBC]
- transitioning states [ODBC], environment
- state transitions [ODBC], environment
ms.assetid: 9d11b1ab-f4c8-48ca-9812-8c04303f939d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a47acf216ef707600fad3fd28a8d94603052be6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="environment-transitions"></a>환경이 전환
ODBC 환경은 다음 세 가지 상태입니다.  
  
|State|Description|  
|-----------|-----------------|  
|E0|할당 되지 않은 환경|  
|E1|연결 할당 되지 않은 할당 된 환경|  
|E2|환경 연결에 할당 된 할당|  
  
 다음 표에서 각 ODBC 함수 환경 상태에 미치는 영향을 보여 줍니다.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> 할당 된|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|E1 [1]|--[4]|--[4]|  
|(면) [2]|E2 [5]<br />(HY010) [6]|--[4]|  
|(면) [3]|(면)|--[4]|  
  
 [1]이이 행 표시 전환 때 *HandleType* SQL_HANDLE_ENV 되었습니다.  
  
 [2]이이 행 표시 전환 때 *HandleType* sql_handle_dbc 라는 되었습니다.  
  
 [3]이이 행 표시 전환 때 *HandleType* 여 되었거나 SQL_HANDLE_DESC 합니다.  
  
 [4] 호출 **SQLAllocHandle** 와 *OutputHandlePtr* 유효한 핸들을 가리키는 해당 핸들을 덮어씁니다. 이 응용 프로그램 프로그래밍 오류일 수 있습니다.  
  
 [환경에 설정 된 5] SQL_ATTR_ODBC_VERSION 환경 특성입니다.  
  
 [6] SQL_ATTR_ODBC_VERSION 환경 특성 환경에 설정 된 되지 않습니다.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources 및 SQLDrivers  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> 할당 된|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(면)|--[1]<br />(HY010) [2]|--[1]<br />(HY010) [2]|  
  
 [환경에 설정 된 1] SQL_ATTR_ODBC_VERSION 환경 특성입니다.  
  
 [2] SQL_ATTR_ODBC_VERSION 환경 특성 환경에서 설정 되지 했습니다.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> 할당 된|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(면) [1]|--[3]<br />(HY010) [4]|--[3]<br />(HY010) [4]|  
|(면) [2]|(면)|--|  
  
 [1]이이 행 표시 전환 때 *HandleType* SQL_HANDLE_ENV 되었습니다.  
  
 [2]이이 행 표시 전환 때 *HandleType* sql_handle_dbc 라는 되었습니다.  
  
 [환경에 설정 된 3] SQL_ATTR_ODBC_VERSION 환경 특성입니다.  
  
 [SQL_ATTR_ODBC_VERSION 환경 특성 4]에서 환경에 설정 된 되지 않습니다.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> 할당 된|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(면) [1]|E0|(HY010)|  
|(면) [2]|(면)|--[4]<br />E1 [5]|  
|(면) [3]|(면)|--|  
  
 [1]이이 행 표시 전환 때 *HandleType* SQL_HANDLE_ENV 되었습니다.  
  
 [2]이이 행 표시 전환 때 *HandleType* sql_handle_dbc 라는 되었습니다.  
  
 [3]이이 행 표시 전환 때 *HandleType* 여 되었거나 SQL_HANDLE_DESC 합니다.  
  
 [다른 할당 된 연결 핸들 4] 발생 했습니다.  
  
 [5]에 지정 된 연결 핸들 *처리* 만 할당 된 연결 핸들을 했습니다.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 및 SQLGetDiagRec  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> 할당 된|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(면) [1]|--|--|  
|(면) [2]|(면)|--|  
  
 [1]이이 행 표시 전환 때 *HandleType* SQL_HANDLE_ENV 되었습니다.  
  
 [2]이이 행 표시 전환 때 *HandleType* sql_handle_dbc 라는, 여, 또는 SQL_HANDLE_DESC 합니다.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> 할당 된|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(면)|--[1]<br />(HY010) [2]|--|  
  
 [환경에 설정 된 1] SQL_ATTR_ODBC_VERSION 환경 특성입니다.  
  
 [2] SQL_ATTR_ODBC_VERSION 환경 특성 환경에서 설정 되지 했습니다.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> 할당 된|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(면)|--[1]<br />(HY010) [2]|(HY011)|  
  
 [환경에 설정 된 1] SQL_ATTR_ODBC_VERSION 환경 특성입니다.  
  
 [2]는 *특성* 인수 SQL_ATTR_ODBC_VERSION, 되었으며 SQL_ATTR_ODBC_VERSION 환경 특성 환경에 설정 된 되지 않습니다.  
  
## <a name="all-other-odbc-functions"></a>다른 모든 ODBC 함수  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> 할당 된|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(면)|(면)|--|
