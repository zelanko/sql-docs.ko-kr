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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5e50e8128bb80b290e7610d9cc846dd3e148e398
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118625"
---
# <a name="sqlcompleteasync-function"></a>SQLCompleteAsync 함수
**규칙**  
 도입 된 버전: ODBC 3.8  
  
 표준 준수 합니다. 없음  
  
 **요약**  
 **SQLCompleteAsync** 비동기 함수는 두 알림 또는 폴링 기반 처리를 사용 하 여 완료 되 면 확인 하기 위해 사용할 수 있습니다. 비동기 작업에 대 한 자세한 내용은 참조 하세요. [비동기 실행](../../../odbc/reference/develop-app/asynchronous-execution.md)합니다.  
  
 **SQLCompleteAsync** ODBC 드라이버 관리자에만 구현 되었습니다.  
  
 알림 기반 비동기 처리 모드로 **SQLCompleteAsync** the Driver Manager 알림에 사용 되는 이벤트 개체를 발생 한 이후에 호출 해야 합니다. **SQLCompleteAsync** 완료 비동기 처리 및 비동기 함수는 반환 코드를 생성 합니다.  
  
 폴링 기반 비동기 처리 모드로 **SQLCompleteAsync** 원래 비동기 함수 호출에 인수를 지정 하지 않고도 원래 비동기 함수를 호출 하지 않아도 됩니다. **SQLCompleteAsync** ODBC 커서 라이브러리 사용 여부와 상관 없이 사용할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 [입력] 비동기 완료 하는 핸들의 형식을 처리 합니다. 유효한 값은 SQL_HANDLE_DBC 또는 호출 합니다.  
  
 *Handle*  
 [입력] 비동기 완료 하는 핸들을 처리 합니다. 경우 *처리할* 하 여 지정 된 형식의 유효한 핸들이 아닙니다 *HandleType*를 **SQLCompleteAsync** 에서 SQL_INVALID_HANDLE을 반환 합니다.  
  
 경우 *처리할* 하 여 지정 된 형식의 유효한 핸들이 아닙니다 *HandleType*를 **SQLCompleteAsync** 에서 SQL_INVALID_HANDLE을 반환 합니다.  
  
 *AsyncRetCodePtr*  
 [출력] 비동기 API의 반환 코드가 포함 될 버퍼에 대 한 포인터입니다. 하는 경우 *AsyncRetCodePtr* 가 null 인 경우 **SQLCompleteAsync** SQL_ERROR를 반환 합니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_ERROR, SQL_NO_DATA, 또는 SQL_INVALID_HANDLE  
  
## <a name="diagnostics"></a>진단  
 하는 경우 **SQLCompleteAsync** 반환 SQL_SUCCESS, 응용 프로그램에서 가리키는 버퍼에서 비동기 함수의 반환 코드를 가져와야 *AsyncRetCodePtr*합니다. 연결 된 SQLSTATE, 있는 경우 얻을 수 있습니다를 호출 하 여 **SQLGetDiagRec** 사용 하 여를 *HandleType* 호출 하 여 문 핸들을 또는 *HandleType* SQL_의 HANDLE_DBC 및 연결을 처리합니다. 진단 레코드에 해당 되지 않음 비동기 함수를 사용 하 여 연관 **SQLCompleteAsync** 함수입니다.  
  
 **SQLCompleteAsync** 나타내는 SQL_SUCCESS 이외의 코드가 반환 **SQLCompleteAsync** 제대로 호출 되지 않습니다. **SQLCompleteAsync** 진단 레코드를이 예제의 게시 됩니다. 가능한 반환 코드 다음과 같습니다.  
  
-   SQL_INVALID_HANDLE: 핸들에 나타난 *HandleType* 하 고 *처리* 는 유효한 핸들이 아닙니다.  
  
-   SQL_ERROR: *AsyncRetCodePtr* null 않거나 핸들에서 비동기 처리를 지원 하지 않습니다.  
  
-   SQL_NO_DATA: 알림 모드에서 비동기 작업이 진행에서 중이지 또는 드라이버 관리자가 응용 프로그램에 알려지지 않은 합니다. 폴링 모드에서 비동기 작업을 하지 진행 중입니다.  
  
## <a name="comments"></a>주석  
 폴링 기반 비동기 처리 모드에서 *AsyncRetCodePtr* SQL_STILL_EXECUTING 있을 때 **SQLCompleteAsync** 관계 없이 SQL_SUCCESS를 반환 합니다. 응용 프로그램까지 폴링 유지 해야 *AsyncRetCodePtr* SQL_STILL_EXECUTING 아닙니다. 알림 기반 비동기 처리 모드로 *AsyncRetCodePtr* SQL_STILL_EXECUTING 안 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [비동기 실행(폴링 메서드)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
