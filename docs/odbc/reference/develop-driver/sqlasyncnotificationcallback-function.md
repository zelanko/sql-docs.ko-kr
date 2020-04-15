---
title: SQLAsyncNotification콜백 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c56aedc9-f7f7-4641-b605-f0f98ed4400c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6c182c48b8e5ddb70204ddd3a94d9651f97595d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294540"
---
# <a name="sqlasyncnotificationcallback-function"></a>SQLAsyncNotificationCallback 함수
**규칙**  
 버전 출시: ODBC 3.8  
  
 표준 준수: 없음  
  
 **요약**  
 **SQLAsyncNotificationCallback** 드라이버를 반환 한 후 현재 비동기 작업에 대 한 일부 진행이 있을 때 드라이버 관리자에 다시 호출 할 수 SQL_STILL_EXECUTING 있습니다. **SQLAsyncNotification호출은** 드라이버에서만 호출할 수 있습니다.  
  
 드라이버는 함수 이름 **SQLAsyncNotification호출백으로** **SQLAsyncNotification호출백을**호출하지 않습니다. 대신 드라이버 관리자는 함수 포인터를 해당 연결 핸들 또는 문 핸들의 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 또는 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 특성의 값으로 드라이버에 전달합니다. 다른 핸들은 서로 다른 함수 포인터 값을 할당할 수 있습니다. 함수 포인터의 형식은 SQL_ASYNC_NOTIFICATION_CALLBACK 정의됩니다.  
  
 **SQLAsyncNotification호출은** 스레드에서 안전합니다. 드라이버는 동시에 다른 핸들에 **SQLAsyncNotification호출을** 호출하는 여러 스레드를 사용하도록 선택할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>인수  
 *pContex*  
 드라이버 관리자에 의해 정의된 데이터 구조에 대한 포인터입니다. 이 값은 SQLSetConnectAttr(SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT) 또는 SQLSetStmtAttr(SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT)을 통해 드라이버에 전달됩니다.  드라이버는 값에 액세스할 수 없습니다.  
  
 *fLast*  
 드라이버에서 이 콜백 함수 호출이 현재 비동기 작업에 대한 마지막 호출임을 나타내는 데 사용됩니다. 드라이버 관리자가 함수를 다시 호출할 때 SQL_STILL_EXECUTING 이외의 반환 코드를 반환합니다. 예를 들어 드라이버 관리자는 이 정보를 사용하여 비동기 작업이 완료된다는 것을 응용 프로그램에 미리 알릴 수 있습니다.  
  
 *핸들이* *HandleType에서*지정한 형식의 유효한 핸들이 아닌 경우 **SQLCancelHandle은** SQL_INVALID_HANDLE 반환합니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS 또는 SQL_ERROR.  
  
## <a name="diagnostics"></a>진단  
 **SQLAsyncNotificationCallback은** 다음 두 가지 상황에 대해 SQL_ERROR 반환할 수 있습니다(이는 드라이버 또는 드라이버 관리자의 구현 문제를 나타냅니다.  
  
|Error|설명|  
|-----------|-----------------|  
|연결 또는 명령문이 알림을 요청하지 않았습니다.||  
|잘못된 *핸들*|드라이버가 잘못된 핸들을 전달하여 내부 드라이버 관리자 유효성 검사 테스트에 실패했습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [비동기 실행(폴링 메서드)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
