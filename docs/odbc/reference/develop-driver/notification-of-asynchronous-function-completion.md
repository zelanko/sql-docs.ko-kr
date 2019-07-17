---
title: 비동기 함수 완료 알림 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 336565da-4203-4745-bce2-4f011c08e357
author: MightyPen
ms.author: genemi
ms.openlocfilehash: de3496661f2ab329e5bf662a9cb8fa749cb81bfc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129315"
---
# <a name="notification-of-asynchronous-function-completion"></a>비동기 함수 완료 알림
Windows 8 SDK, ODBC는 비동기 작업이 완료 되 면 알림으로"완료" 이라고 하는 응용 프로그램에 알릴 수 있는 메커니즘을 추가 합니다. (참조 [비동기 실행 (알림 메서드)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md) 자세한.) 이 항목에서는 드라이버 개발자를 위한 일부의 문제를 설명합니다.  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>드라이버 관리자와 드라이버 인터페이스  
 콜백 함수를 내부적으로 제공 하는 the Driver Manager [SQLAsyncNotificationCallback 함수](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md)합니다. **SQLAsyncNotificationCallback** 만 호출할 수 있습니다-드라이버에서 응용 프로그램 직접 호출할 수 없습니다 것입니다. 드라이버 **SQLAsyncNotificationCallback** 때마다 마지막 반환 SQL_STILL_EXECUTING 후 서버에서 받은 새 데이터입니다.  
  
 드라이버 관리자는 해당 함수의 SQL_STILL_EXECUTING을 반환 된 후 비동기 작업을 실행에 진행률이 어느 정도 이루어졌을 때 드라이버를 드라이버 관리자를 알릴 수 있도록 콜백 메커니즘을 제공  
  
 드라이버 관리자 특성을 설정 합니다 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 형식에 대 한 알림 모드로 작동 하도록 드라이버에 대 한 SQL_ASYNC_NOTIFICATION_CALLBACK입니다는 NULL이 아닌 함수 포인터를 사용 하 여 드라이버 연결 핸들의 모든 비동기 이 핸들에 대 한 작업입니다. 드라이버 관리자가 형식에 대 한 알림 모드로 작동 하도록 드라이버에 대 한 SQL_ASYNC_NOTIFICATION_CALLBACK 이기도 하는 NULL이 아닌 함수 포인터를 사용 하 여 드라이버 문 핸들에 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 특성을 설정 하는 마찬가지로 해당 핸들의 모든 비동기 작업입니다.  
  
 드라이버 핸들에는 비동기 작업을 수행 하는 경우 비동기 드라이버 함수 비차단 스타일 작동 합니다. 작업을 즉시 완료할 수 없습니다, 하는 경우 드라이버는 SQL_STILL_EXECUTING을 반환 해야 합니다. 이 요구 사항은 폴링 모드 및 알림 모드를 둘 다에 대해 적용 됩니다.  
  
 드라이버 주소의 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 또는 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 특성 값을 더 알림 콜백 함수를 호출 해야 핸들을 알림 비동기 모드에 있으면 후 한 번 SQL_STILL_EXECUTING을 반환합니다. 즉, 하나의 알림 콜백 함수 호출을 사용 하 여 하나의 반환 SQL_STILL_EXECUTING 이루어야 합니다. 드라이버 호출 백 함수 매개 변수 값으로 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT 또는 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT 핸들 특성의 현재 값을 사용 해야 *pContext*합니다.  
  
 드라이버 함수를 호출 하는 스레드 드라이버를 다시 호출 해야 합니다. 함수가 반환 되기 전에 진행 상태를 알릴 필요가 없습니다 있습니다. 드라이버는 콜백에 자체 스레드를 사용 해야 합니다. 드라이버 관리자는 광범위 한 처리 논리를 실행 하는 것에 대 한 드라이버의 콜백 스레드를 사용 하지 않습니다.  
  
 드라이버 관리자 드라이버를 다시 호출 후 원래 함수를 다시 호출 됩니다. 드라이버 관리자는 응용 프로그램 스레드 아니고 드라이버 스레드는 스레드를 사용할 수 있습니다. 드라이버 초기 비동기 호출에 필요한 정보를 저장 하며 전체 비동기 작업 전에 저장된 된 값을 사용 하 여 스레드 (예: 보안 토큰 또는 사용자 식별자)와 관련 된 일부 정보를 사용 하는 드라이버 완료합니다. 일반적으로 **SQLDriverConnect**를 **SQLConnect**, 또는 **SQLBrowseConnect** 해당 종류의 정보를 사용 해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
