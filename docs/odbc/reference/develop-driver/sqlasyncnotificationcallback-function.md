---
description: SQLAsyncNotificationCallback 함수
title: SQLAsyncNotificationCallback 함수 | Microsoft Docs
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
ms.openlocfilehash: b9d03e8a3fa7e62c19dd09a210dca3a56348c692
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476232"
---
# <a name="sqlasyncnotificationcallback-function"></a>SQLAsyncNotificationCallback 함수
**규칙**  
 소개 된 버전: ODBC 3.8  
  
 표준 준수: 없음  
  
 **요약**  
 **Sqlasyncnotificationcallback** 은 드라이버가 SQL_STILL_EXECUTING 반환 된 후 현재 비동기 작업에 대 한 진행률이 있는 경우 드라이버에서 드라이버 관리자에 게 콜백할 수 있도록 허용 합니다. **Sqlasyncnotificationcallback** 은 드라이버에 의해서만 호출 될 수 있습니다.  
  
 드라이버는 Sqlasyncnotificationcallback 함수 이름을 사용 하 여 **SQLAsyncNotificationCallback** **sqlasyncnotificationcallback** 을 호출 하지 않습니다. 대신 드라이버 관리자는 해당 하는 연결 핸들이 나 문 핸들의 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 또는 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 특성에 대 한 값으로 함수 포인터를 드라이버에 전달 합니다. 여러 핸들에 다른 함수 포인터 값을 할당할 수 있습니다. 함수 포인터의 형식은 SQL_ASYNC_NOTIFICATION_CALLBACK로 정의 됩니다.  
  
 **Sqlasyncnotificationcallback** 은 스레드로부터 안전 합니다. 드라이버는 서로 다른 핸들에서 **Sqlasyncnotificationcallback** 을 동시에 호출 하는 여러 스레드를 사용 하도록 선택할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>인수  
 *pContex*  
 드라이버 관리자가 정의 하는 데이터 구조에 대 한 포인터입니다. 이 값은 SQLSetConnectAttr (SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT) 또는 SQLSetStmtAttr (SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT)를 통해 드라이버에 전달 됩니다.  드라이버에서 값에 액세스할 수 없습니다.  
  
 *fLast*  
 드라이버가 현재 비동기 작업에 대 한 마지막 콜백 함수 호출을 나타내는 데 사용 됩니다. 드라이버 관리자가 함수를 다시 호출 하는 경우 드라이버는 SQL_STILL_EXECUTING 이외의 반환 코드를 반환 합니다. 예를 들어 드라이버 관리자는이 정보를 사용 하 여 비동기 작업이 완료 될 때까지 응용 프로그램을 미리 알릴 수 있습니다.  
  
 *Handle* 이 *HandleType*에 의해 지정 된 형식의 유효한 핸들이 아닌 경우 **sqlcancelhandle** 은 SQL_INVALID_HANDLE를 반환 합니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS 또는 SQL_ERROR.  
  
## <a name="diagnostics"></a>진단  
 **Sqlasyncnotificationcallback** 은 다음 두 가지 상황에 대 한 SQL_ERROR를 반환할 수 있습니다 .이는 드라이버 또는 드라이버 관리자의 구현 문제를 의미 합니다.  
  
|오류|설명|  
|-----------|-----------------|  
|연결 또는 문이 알림을 요청 하지 않았습니다.||  
|잘못 된 *핸들*|드라이버가 잘못 된 핸들을 전달 하 여 내부 드라이버 관리자 유효성 검사 테스트에 실패 했습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [비동기 실행 (폴링 방법)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
