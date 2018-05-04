---
title: SQLAsyncNotificationCallback 함수 | Microsoft Docs
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
ms.assetid: c56aedc9-f7f7-4641-b605-f0f98ed4400c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2dc584145ea87b34ecfa9417cc89135b1fbc98d4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlasyncnotificationcallback-function"></a>SQLAsyncNotificationCallback 함수
**규칙**  
 ODBC 3.8 도입 된 버전:  
  
 표준 준수: 없음  
  
 **요약**  
 **SQLAsyncNotificationCallback** 드라이버를 드라이버 SQL_STILL_EXECUTING을 반환 된 후 현재 비동기 작업에 대 한 몇 가지 진행률 때 드라이버 관리자를 다시 호출할 수 있습니다. **SQLAsyncNotificationCallback** 만 드라이버에서 호출할 수 있습니다.  
  
 드라이버를 호출 하지 마십시오 **SQLAsyncNotificationCallback** 함수 이름으로 **SQLAsyncNotificationCallback**합니다. 대신, 드라이버 관리자 함수 포인터를 전달 하는 드라이버 문 핸들 또는 해당 연결 핸들의 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 또는 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 특성에 대 한 값으로 각각. 다른 핸들 다른 함수 포인터 값을 할당할 수 있습니다. 함수 포인터의 유형은 SQL_ASYNC_NOTIFICATION_CALLBACK으로 정의 됩니다.  
  
 **SQLAsyncNotificationCallback** 는 스레드로부터 안전 합니다. 드라이버를 호출 하는 여러 스레드를 사용 하도록 선택할 수 **SQLAsyncNotificationCallback** 에 서로 다른 처리 동시에 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>인수  
 *pContex*  
 드라이버 관리자에 의해 정의 되는 데이터 구조에 대 한 포인터입니다. 값은 SQLSetConnectAttr(SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT) 또는 SQLSetStmtAttr(SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT)를 통해 드라이버에 전달 됩니다.  드라이버는 값에 액세스할 수는 없습니다.  
  
 *fLast*  
 드라이버 사용이 콜백 함수 호출 현재 비동기 작업에 대 한 마지막 하나 임을 나타냅니다. 드라이버 관리자는 함수를 다시 호출할 때 드라이버 SQL_STILL_EXECUTING 이외의 반환 코드를 반환 합니다. 드라이버 관리자는 응용 프로그램 알리는 사전에 비동기 작업은 완료 하는 예를 들어이 정보를 사용할 수 있습니다.  
  
 경우 *처리* 하 여 지정 된 형식의 유효한 핸들 않습니다 *HandleType*, **SQLCancelHandle** 에서 SQL_INVALID_HANDLE을 반환 합니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS 또는 SQL_ERROR 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLAsyncNotificationCallback** (이러한 드라이버 또는 드라이버 관리자에는 구현 문제를 나타냅니다 다음과 같은 두 가지 상황에서 SQL_ERROR를 반환할 수 있습니다.  
  
|오류|Description|  
|-----------|-----------------|  
|연결 또는 명령문 알림을 요청 하지 않았습니다.||  
|잘못 된 *처리*|드라이버 내부 드라이버 관리자 유효성 검사 테스트를 실패 한 잘못 된 핸들을 전달 합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [비동기 실행(폴링 메서드)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
