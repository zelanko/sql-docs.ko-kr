---
title: 비동기 함수 완료 알림을 | Microsoft Docs
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
ms.assetid: 336565da-4203-4745-bce2-4f011c08e357
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e5b0c8ceb6924171e304f3bc14d3c0438baa3306
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="notification-of-asynchronous-function-completion"></a>비동기 함수 완료
Windows 8 SDK ODBC 비동기 작업이 완료 되는 알림으로"완료" 하는 경우 응용 프로그램에 알리기 위해 하는 메커니즘을 추가 합니다. (참조 [비동기 실행 (알림 방법)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md) 자세한 정보에 대 한 합니다.) 이 항목에서는 드라이버 개발자를 위한 일부의 문제를 설명 합니다.  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>드라이버 관리자와 드라이버 간의 인터페이스  
 콜백 함수를 내부적으로 제공 하는 드라이버 관리자 [SQLAsyncNotificationCallback 함수](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md)합니다. **SQLAsyncNotificationCallback** 에서만 호출할 수는 드라이버-에서 응용 프로그램 직접 호출할 수 없습니다 것입니다. 드라이버 호출 **SQLAsyncNotificationCallback** 마지막 반환 SQL_STILL_EXECUTING 후 서버에서 받은 새 데이터 때마다 합니다.  
  
 드라이버 관리자는 일부 진행 해당 SQL_STILL_EXECUTING 반환 된 후에 비동기 작업을 실행 하는 경우 드라이버를 드라이버 관리자에 게 알릴 수 있도록 콜백 메커니즘을 제공  
  
 형식에 대 한 알림 모드에서 작동 하도록 드라이버에 대 한 SQL_ASYNC_NOTIFICATION_CALLBACK NULL이 아닌 함수 포인터로 드라이버 연결 핸들에 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 특성을 설정 하는 드라이버 관리자는 모든 비동기 이 핸들에 대 한 작업입니다. 드라이버 관리자 이기도 함에 대 한 알림 모드에서 작동 하도록 드라이버에 대 한 SQL_ASYNC_NOTIFICATION_CALLBACK 형식의 NULL이 아닌 함수 포인터로 드라이버 문 핸들에 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 특성을 설정 하는 마찬가지로, 이 핸들에서 비동기 작업입니다.  
  
 드라이버 핸들에는 비동기 작업을 수행 하는 경우 비동기 드라이버 함수는 비 블록 킹 스타일에서 작동 해야 합니다. 작업을 즉시 완료할 수 없으면, 드라이버 함수 SQL_STILL_EXECUTING을 반환 해야 합니다. 이 요구 사항은 폴링 모드와 알림 모드에 적용 됩니다.  
  
 드라이버 주소가 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 또는 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 특성에 대 한 값 이면 알림 콜백 함수를 호출 해야 핸들 알림 비동기 모드인 경우 후 한 번 SQL_STILL_EXECUTING을 반환합니다. 즉, 하나의 반환 SQL_STILL_EXECUTING 알림 콜백 함수가 호출 마다 한 쌍이 되어야 합니다. 드라이버 호출 백 함수 매개 변수 값으로 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT 또는 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT 핸들 특성의 현재 값을 사용 해야 *pContext*합니다.  
  
 드라이버; 드라이버 함수를 호출 하는 스레드에서 다시 호출 해서는 안 함수가 반환 되기 전에 진행률에 알리기 위해 않아도가 됩니다. 드라이버 콜백에 자체 스레드를 사용 해야 합니다. 드라이버 관리자는 광범위 한 처리 논리를 실행 하기 위한 드라이버의 콜백 스레드와 사용 하지 않습니다.  
  
 드라이버 관리자 드라이버를 다시 호출 후 원래 함수를 다시 호출 됩니다. 드라이버 관리자는 응용 프로그램 스레드 또는 드라이버 스레드는 스레드를 사용할 수 있습니다. 드라이버 해야 초기 비동기 호출에 필요한 정보를 저장 하 고 전체 비동기 작업 전에 저장 된 값을 사용 하 여 드라이버 스레드 (예: 보안 토큰 또는 사용자 식별자)와 관련 된 몇 가지 정보를 사용 하는 경우 완료합니다. 일반적으로 **SQLDriverConnect**, **SQLConnect**, 또는 **SQLBrowseConnect** 이러한 종류의 정보를 사용 해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
