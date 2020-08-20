---
description: 비동기 함수 완료 알림
title: 비동기 함수 완료 알림 | Microsoft Docs
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
ms.openlocfilehash: d6e762e6b144e6a713f22429dccf43e1d27d8b24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476262"
---
# <a name="notification-of-asynchronous-function-completion"></a>비동기 함수 완료 알림
Windows 8 SDK에서 ODBC는 비동기 작업이 완료 될 때 응용 프로그램에 알리는 메커니즘을 추가 했습니다 .이 메커니즘은 "완료 시 알림" 이라고 지칭 합니다. 자세한 내용은 [비동기 실행 (알림 방법)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md) 을 참조 하세요. 이 항목에서는 드라이버 개발자를 위한 몇 가지 문제에 대해 설명 합니다.  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>드라이버 관리자와 드라이버 간의 인터페이스  
 드라이버 관리자는 내부적으로 콜백 함수 [Sqlasyncnotificationcallback 함수](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md)를 제공 합니다. **Sqlasyncnotificationcallback** 은 드라이버 에서만 호출할 수 있으며 응용 프로그램에서 직접 호출할 수는 없습니다. 드라이버는 마지막으로 SQL_STILL_EXECUTING 반환한 후 서버에서 새 데이터가 수신 될 때마다 **Sqlasyncnotificationcallback** 을 호출 합니다.  
  
 드라이버 관리자는 콜백 메커니즘을 제공 하므로 해당 함수가 반환 된 후 비동기 작업을 실행 하는 동안 몇 가지 진행률이 발생 했을 때 드라이버가 드라이버 관리자에 게 알릴 수 있습니다 SQL_STILL_EXECUTING  
  
 드라이버 관리자는 SQL_ASYNC_NOTIFICATION_CALLBACK 형식인 NULL이 아닌 함수 포인터를 사용 하 여 드라이버 연결 핸들에 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 특성을 설정 하 여 해당 핸들의 모든 비동기 작업에 대 한 알림 모드에서 드라이버를 사용할 수 있도록 합니다. 마찬가지로 드라이버 관리자는 SQL_ASYNC_NOTIFICATION_CALLBACK 형식 이기도 한 NULL이 아닌 함수 포인터를 사용 하 여 드라이버 문 핸들에 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 특성을 설정 하 여 해당 핸들의 비동기 작업에 대 한 알림 모드에서 드라이버를 사용할 수 있습니다.  
  
 드라이버 핸들에 대해 비동기 작업을 수행 하는 경우 비동기 드라이버 함수는 비 블로킹 스타일로 작동 해야 합니다. 작업을 즉시 완료할 수 없는 경우 드라이버 함수는 SQL_STILL_EXECUTING을 반환 해야 합니다. 이 요구 사항은 폴링 모드와 알림 모드 모두에 적용 됩니다.  
  
 핸들이 알림 비동기 모드에 있으면 드라이버는 알림 콜백 함수를 호출 해야 합니다 .이 함수는 주소가 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 또는 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 특성의 값이 SQL_STILL_EXECUTING 반환 된 후에 한 번입니다. 즉, 한 번의 반환 SQL_STILL_EXECUTING 알림 콜백 함수의 한 호출과 쌍을 이루어야 합니다. 드라이버는 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT 또는 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT 핸들 특성의 현재 값을 콜백 함수 매개 변수 *pContext*값으로 사용 해야 합니다.  
  
 드라이버는 드라이버 함수를 호출 하는 스레드에서 콜백 해서는 안 됩니다. 함수가 반환 되기 전에 진행률을 알릴 이유가 없습니다. 드라이버는 자체 스레드를 사용 하 여 콜백을 해야 합니다. 드라이버 관리자는 광범위 한 처리 논리를 실행 하기 위해 드라이버의 콜백 스레드를 사용 하지 않습니다.  
  
 드라이버 관리자는 드라이버가 다시 호출 된 후 원래 기능을 다시 호출 합니다. 드라이버 관리자는 응용 프로그램 스레드나 드라이버 스레드가 아닌 스레드를 사용할 수 있습니다. 드라이버에서 스레드와 연결 된 일부 정보 (예: 보안 토큰 또는 사용자 식별자)를 사용 하는 경우 드라이버는 초기 비동기 호출에 필요한 정보를 저장 하 고 전체 비동기 작업을 완료 하기 전에 저장 된 값을 사용 해야 합니다. 일반적으로 **SQLDriverConnect**, **SQLConnect**또는 **SQLBrowseConnect** 만 해당 종류의 정보를 사용 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
