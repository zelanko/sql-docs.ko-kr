---
title: SQLCompleteAsync 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
f1_keywords:
- SQLCompleteAsync
helpviewer_keywords:
- SQLCompleteAsync function [ODBC]
ms.assetid: 1b97c46a-d2e5-4540-8239-9d975e5321c6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4e09d61ef516e846798dd3af2d07dafa78af4605
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299658"
---
# <a name="sqlcompleteasync-function"></a>SQLCompleteAsync 함수
**규칙**  
 소개 된 버전: ODBC 3.8  
  
 표준 준수: 없음  
  
 **요약**  
 **SQLCompleteAsync** 를 사용 하면 알림 또는 폴링 기반 처리를 사용 하 여 비동기 함수가 완료 되는 시점을 확인할 수 있습니다. 비동기 작업에 대 한 자세한 내용은 [비동기 실행](../../../odbc/reference/develop-app/asynchronous-execution.md)을 참조 하세요.  
  
 **SQLCompleteAsync** 는 ODBC 드라이버 관리자 에서만 구현 됩니다.  
  
 알림 기반 비동기 처리 모드에서 **SQLCompleteAsync** 는 드라이버 관리자가 알림에 사용 되는 이벤트 개체를 발생 시킨 후에 호출 해야 합니다. **SQLCompleteAsync** 는 비동기 처리를 완료 하 고 비동기 함수는 반환 코드를 생성 합니다.  
  
 폴링 기반 비동기 처리 모드에서 **SQLCompleteAsync** 은 원래 비동기 함수 호출에서 인수를 지정할 필요 없이 원래 비동기 함수를 호출 하는 대신 사용할 수 있습니다. **SQLCompleteAsync** 는 ODBC 커서 라이브러리를 사용 하도록 설정할지 여부에 관계 없이 사용할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 입력 비동기 처리를 완료할 핸들의 형식입니다. 유효한 값은 SQL_HANDLE_DBC 또는 SQL_HANDLE_STMT입니다.  
  
 *Handle*  
 입력 비동기 처리를 완료할 핸들입니다. *Handle* 이 *HandleType*에 의해 지정 된 형식의 유효한 핸들이 아닌 경우 **SQLCompleteAsync** 는 SQL_INVALID_HANDLE을 반환 합니다.  
  
 *Handle* 이 *HandleType*에 의해 지정 된 형식의 유효한 핸들이 아닌 경우 **SQLCompleteAsync** 는 SQL_INVALID_HANDLE을 반환 합니다.  
  
 *AsyncRetCodePtr*  
 출력 비동기 API의 반환 코드를 포함 하는 버퍼에 대 한 포인터입니다. *AsyncRetCodePtr* 가 NULL 인 경우 **SQLCompleteAsync** 는 SQL_ERROR을 반환 합니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_ERROR, SQL_NO_DATA 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLCompleteAsync** 가 SQL_SUCCESS을 반환 하는 경우 응용 프로그램은 *AsyncRetCodePtr*가 가리키는 버퍼에서 비동기 함수의 반환 코드를 가져와야 합니다. 연결 된 SQLSTATE (있는 경우)는 SQL_HANDLE_STMT *HandleType* , 문 핸들 또는 HandleType SQL_HANDLE_DBC의 *HandleType* 및 연결 핸들로 **SQLGetDiagRec** 를 호출 하 여 가져올 수 있습니다. 이러한 진단 레코드는이 **SQLCompleteAsync** 함수가 아니라 비동기 함수와 연결 됩니다.  
  
 **SQLCompleteAsync** 는 **SQLCompleteAsync** 가 올바르게 호출 되지 않았음을 나타내는 SQL_SUCCESS 이외의 코드를 반환 합니다. 이 경우 **SQLCompleteAsync** 은 진단 레코드를 게시 하지 않습니다. 가능한 반환 코드는 다음과 같습니다.  
  
-   SQL_INVALID_HANDLE: *HandleType* 및 *handle* 이 나타내는 핸들이 유효한 핸들이 아닙니다.  
  
-   SQL_ERROR: *AsyncRetCodePtr* 가 NULL 이거나 핸들에서 비동기 처리를 사용할 수 없습니다.  
  
-   SQL_NO_DATA: 알림 모드에서 비동기 작업이 진행 되 고 있지 않거나 드라이버 관리자에 게 응용 프로그램에 대 한 알림이 표시 되지 않았습니다. 폴링 모드에서는 비동기 작업이 진행 되 고 있지 않습니다.  
  
## <a name="comments"></a>주석  
 폴링 기반 비동기 처리 모드에서는 **SQLCompleteAsync** 가 SQL_SUCCESS를 반환할 때 *AsyncRetCodePtr* 가 SQL_STILL_EXECUTING 수 있습니다. 응용 프로그램은 *AsyncRetCodePtr* 가 SQL_STILL_EXECUTING 되지 않을 때까지 폴링을 유지 해야 합니다. 알림 기반 비동기 처리 모드에서는 *AsyncRetCodePtr* 가 SQL_STILL_EXECUTING 되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [비동기 실행(폴링 메서드)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
