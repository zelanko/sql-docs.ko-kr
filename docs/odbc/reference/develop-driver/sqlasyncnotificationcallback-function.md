---
title: SQLAsyncNotificationCallback 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c56aedc9-f7f7-4641-b605-f0f98ed4400c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b78764e1dccb7118d43cc967f3b03838366d6eb0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63224518"
---
# <a name="sqlasyncnotificationcallback-function"></a>SQLAsyncNotificationCallback 함수
**규칙**  
 도입 된 버전: ODBC 3.8  
  
 표준 준수 합니다. 없음  
  
 **요약**  
 **SQLAsyncNotificationCallback** 드라이버 SQL_STILL_EXECUTING을 반환 된 후 현재 비동기 작업의 진행률이 어느 정도 있을 때 드라이버 관리자를 다시 호출 하는 드라이버를 허용 합니다. **SQLAsyncNotificationCallback** 드라이버에서 호출할 수 있습니다.  
  
 드라이버를 호출 하지 마십시오 **SQLAsyncNotificationCallback** 함수 이름의 **SQLAsyncNotificationCallback**합니다. 대신 드라이버 관리자 함수 포인터를 전달 하는 드라이버 문 핸들을 해당 연결 핸들의 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 또는 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 특성 값으로 각각. 다른 핸들 다른 함수 포인터 값을 할당할 수 있습니다. 함수 포인터 형식의 SQL_ASYNC_NOTIFICATION_CALLBACK으로 정의 됩니다.  
  
 **SQLAsyncNotificationCallback** 는 스레드로부터 안전 합니다. 드라이버를 호출 하는 여러 스레드를 사용 하도록 선택할 수 **SQLAsyncNotificationCallback** 에서 다른 처리 동시에 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>인수  
 *pContex*  
 드라이버 관리자에 의해 정의 된 데이터 구조에 대 한 포인터입니다. 값은 SQLSetConnectAttr(SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT) 또는 SQLSetStmtAttr(SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT) 통해 드라이버에 전달 됩니다.  드라이버에는 값에 액세스할 수 없습니다.  
  
 *fLast*  
 드라이버에서 사용이 콜백 함수 호출은 현재 비동기 작업의 마지막 항목 임을 나타냅니다. 드라이버 관리자는 함수를 다시 호출 하면 드라이버에서 SQL_STILL_EXECUTING 이외의 반환 코드를 반환 합니다. 드라이버 관리자는 응용 프로그램 미리 비동기 작업은 완료를 알리기 위해 예를 들어이 정보를 사용할 수 있습니다.  
  
 경우 *처리할* 하 여 지정 된 형식의 유효한 핸들이 아닙니다 *HandleType*를 **SQLCancelHandle** 에서 SQL_INVALID_HANDLE을 반환 합니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS 또는 SQL_ERROR 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLAsyncNotificationCallback** (드라이버 또는 드라이버 관리자에서 구현 문제를 나타냅니다 다음 두 가지 상황에서 SQL_ERROR를 반환할 수 있습니다.  
  
|Error|Description|  
|-----------|-----------------|  
|연결 또는 명령문 알림을 요청 하지 않았습니다.||  
|잘못 된 *처리*|드라이버는 내부 드라이버 관리자 유효성 검사 테스트를 하지 못한 잘못 된 핸들을 전달 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [비동기 실행(폴링 메서드)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
