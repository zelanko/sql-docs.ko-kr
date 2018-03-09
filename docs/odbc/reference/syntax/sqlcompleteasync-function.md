---
title: "SQLCompleteAsync 함수 | Microsoft Docs"
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
f1_keywords: SQLCompleteAsync
helpviewer_keywords: SQLCompleteAsync function [ODBC]
ms.assetid: 1b97c46a-d2e5-4540-8239-9d975e5321c6
caps.latest.revision: "4"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 91a6449e07ff83fd6bb7478bfc52cb077a76c955
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlcompleteasync-function"></a>SQLCompleteAsync 함수
**규칙**  
 ODBC 3.8 도입 된 버전:  
  
 표준 준수: 없음  
  
 **요약**  
 **SQLCompleteAsync** 알림 또는 폴링 기반 처리 중 하나를 사용 하 여 완료 되는 비동기 함수를 확인 하기 위해 사용할 수 있습니다. 비동기 작업에 대 한 자세한 내용은 참조 [비동기 실행](../../../odbc/reference/develop-app/asynchronous-execution.md)합니다.  
  
 **SQLCompleteAsync** 은 ODBC 드라이버 관리자 에서만 구현 합니다.  
  
 알림 기반 비동기 처리 모드에서 **SQLCompleteAsync** 드라이버 관리자 알림에 사용 되는 이벤트 개체를 발생 한 이후에 호출 해야 합니다. **SQLCompleteAsync** 완료 비동기 처리 및 비동기 함수는 반환 코드를 생성 합니다.  
  
 폴링 기반 비동기 처리 모드에서 **SQLCompleteAsync** 원래 비동기 함수 호출에 인수를 지정 하지 않고도 원래 비동기 함수를 호출 하지 않아도 됩니다. **SQLCompleteAsync** ODBC 커서 라이브러리를 사용할 수 있는지에 관계 없이 사용할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 [입력] 처리 중에 비동기 완료에 대 한 핸들의 유형입니다. 유효한 값은 sql_handle_dbc 라는 또는 여입니다.  
  
 *Handle*  
 [입력] 처리 중에 비동기 완료에 대 한 핸들입니다. 경우 *처리* 하 여 지정 된 형식의 유효한 핸들 않습니다 *HandleType*, **SQLCompleteAsync** 에서 SQL_INVALID_HANDLE을 반환 합니다.  
  
 경우 *처리* 하 여 지정 된 형식의 유효한 핸들 않습니다 *HandleType*, **SQLCompleteAsync** 에서 SQL_INVALID_HANDLE을 반환 합니다.  
  
 *AsyncRetCodePtr*  
 [출력] 비동기 API의 반환 코드가 포함 될 버퍼에 대 한 포인터입니다. 경우 *AsyncRetCodePtr* 이 NULL 이면 **SQLCompleteAsync** SQL_ERROR를 반환 합니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_ERROR, SQL_NO_DATA, 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 경우 **SQLCompleteAsync** 반환 SQL_SUCCESS, 응용 프로그램을 가리키는 버퍼에서 비동기 함수의 반환 코드 얻어야 *AsyncRetCodePtr*합니다. 연결 된 SQLSTATE 있는 경우 얻을 수 있습니다를 호출 하 여 **SQLGetDiagRec** 와 *HandleType* 여 및 문 핸들 또는 *HandleType* SQL_의 HANDLE_DBC 및 연결 핸들입니다. 진단 레코드는 하지이 비동기 함수에 연결 된 **SQLCompleteAsync** 함수입니다.  
  
 **SQLCompleteAsync** 임을 나타내는 SQL_SUCCESS 이외의 코드가 반환 **SQLCompleteAsync** 제대로 호출 되지 않습니다. **SQLCompleteAsync** 진단 레코드를이 예제의 게시 됩니다. 가능한 반환 코드에는  
  
-   SQL_INVALID_HANDLE: 핸들이 표시 *HandleType* 및 *처리* 유효한 핸들 아닙니다.  
  
-   SQL_ERROR: *AsyncRetCodePtr* null 않거나 핸들에서 비동기 처리를 지원 하지 않습니다.  
  
-   SQL_NO_DATA: 알림 모드에서 비동기 작업이 진행 중에서 되었거나 드라이버 관리자가 응용 프로그램 알림을 받지 않습니다. 폴링 모드에서는 비동기 작업이 진행 중에 있지 않습니다.  
  
## <a name="comments"></a>주석  
 폴링 기반 비동기 처리 모드에서 *AsyncRetCodePtr* SQL_STILL_EXECUTING을 수 있습니다 때 **SQLCompleteAsync** 관계 없이 SQL_SUCCESS를 반환 합니다. 응용 프로그램까지 폴링 유지 해야 *AsyncRetCodePtr* SQL_STILL_EXECUTING 않습니다. 알림 기반 비동기 처리 모드에서 *AsyncRetCodePtr* SQL_STILL_EXECUTING 안 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [비동기 실행(폴링 메서드)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
