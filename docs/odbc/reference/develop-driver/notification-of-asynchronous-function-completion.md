---
title: 비동기 기능 완료 알림 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 336565da-4203-4745-bce2-4f011c08e357
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a453967f2ffdda4af2a44429737f700f4a994cf8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287823"
---
# <a name="notification-of-asynchronous-function-completion"></a>비동기 함수 완료 알림
Windows 8 SDK에서 ODBC는 비동기 작업이 완료되면 응용 프로그램에 알리는 메커니즘을 추가했으며, 이 메커니즘은 "완료 시 알림"이라고 합니다. 자세한 내용은 [비동기 실행(알림 메서드)을](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md) 참조하십시오. 이 항목에서는 드라이버 개발자를 위한 몇 가지 문제에 대해 설명합니다.  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>드라이버 관리자와 드라이버 간의 인터페이스  
 드라이버 관리자는 내부적으로 콜백 함수 [SQLAsyncNotificationCallback 기능을](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md)제공합니다. **SQLAsyncNotificationCallback은** 드라이버에서만 호출할 수 있습니다. 드라이버는 마지막으로 반환 SQL_STILL_EXECUTING 후 서버에서 새 데이터를 받을 때마다 **SQLAsyncNotificationCallback을** 호출합니다.  
  
 드라이버 관리자는 해당 함수가 반환된 후 비동기 작업을 실행하는 데 일부 진전이 있을 때 드라이버 관리자에게 알릴 수 있도록 콜백 메커니즘을 SQL_STILL_EXECUTING  
  
 드라이버 관리자는 드라이버가 해당 핸들의 비동기 작업에 대해 알림 모드에서 작동하도록 SQL_ASYNC_NOTIFICATION_CALLBACK 유형인 NULL이 아닌 함수 포인터를 사용하여 드라이버 연결 핸들에 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 특성을 설정합니다. 마찬가지로 드라이버 관리자는 드라이버가 해당 핸들의 비동기 작업에 대해 알림 모드에서 작동하도록 SQL_ASYNC_NOTIFICATION_CALLBACK 형식이기도 한 null이 아닌 함수 포인터를 사용하여 드라이버 문 핸들에 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 특성을 설정합니다.  
  
 드라이버 핸들에서 비동기 작업이 수행되는 경우 비동기 드라이버 함수는 비차단 스타일로 작동해야 합니다. 작업이 즉시 완료되지 않으면 드라이버 함수가 SQL_STILL_EXECUTING 반환해야 합니다. 이 요구 사항은 폴링 모드와 알림 모드 모두에 해당됩니다.  
  
 핸들이 알림 비동기 모드인 경우 드라이버는 SQL_STILL_EXECUTING 반환한 후 주소가 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 또는 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 특성의 값인 알림 콜백 함수를 호출해야 합니다. 즉, 반환 SQL_STILL_EXECUTING 하나의 알림 콜백 함수호출 하나와 쌍을 이루어야 합니다. 드라이버는 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT 또는 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT 핸들 특성의 현재 값을 호출 함수 매개 변수 *pContext의*값으로 사용해야 합니다.  
  
 드라이버는 드라이버 함수를 호출하는 스레드에서 다시 호출해서는 안 됩니다. 함수가 반환되기 전에 진행 상황을 알릴 이유가 없습니다. 드라이버는 자체 스레드를 사용하여 콜백해야 합니다. 드라이버 관리자는 광범위한 처리 논리를 실행하기 위해 드라이버의 콜백 스레드를 사용하지 않습니다.  
  
 드라이버 관리자는 드라이버가 다시 호출한 후 원래 함수를 다시 호출합니다. 드라이버 관리자는 응용 프로그램 스레드도 드라이버 스레드도 없는 스레드를 사용할 수 있습니다. 드라이버가 스레드와 관련된 일부 정보(예: 보안 토큰 또는 사용자 식별자)를 사용하는 경우 드라이버는 초기 비동기 호출에 필요한 정보를 저장하고 전체 비동기 작업이 완료되기 전에 저장된 값을 사용해야 합니다. 일반적으로 **SQLDriverConnect,** **SQLConnect**또는 **SQLBrowseConnect만** 이러한 종류의 정보를 사용해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
