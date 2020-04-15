---
title: SQLCompleteAsync 기능 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299658"
---
# <a name="sqlcompleteasync-function"></a>SQLCompleteAsync 함수
**규칙**  
 버전 출시: ODBC 3.8  
  
 표준 준수: 없음  
  
 **요약**  
 **SQLCompleteAsync는** 알림 또는 폴링 기반 처리를 사용하여 비동기 함수가 완료되는 시기를 결정하는 데 사용할 수 있습니다. 비동기 작업에 대한 자세한 내용은 [비동기 실행](../../../odbc/reference/develop-app/asynchronous-execution.md)을 참조하십시오.  
  
 **SQLCompleteAsync는** ODBC 드라이버 관리자에서만 구현됩니다.  
  
 알림 기반 비동기 처리 **모드에서는** 드라이버 관리자가 알림에 사용되는 이벤트 개체를 발생시켜야 합니다. **SQLCompleteAsync비동기** 처리를 완료 하 고 비동기 함수 반환 코드를 생성 합니다.  
  
 폴링 기반 비동기 처리 모드에서 **SQLCompleteAsync는** 원래 비동기 함수 호출에서 인수를 지정할 필요 없이 원래 비동기 함수를 호출하는 대신 사용됩니다. **SQLCompleteAsync는** ODBC 커서 라이브러리가 활성화되어 있는지 여부에 관계없이 사용할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 [입력] 비동기 처리를 완료할 핸들의 유형입니다. 유효한 값은 SQL_HANDLE_DBC 또는 SQL_HANDLE_STMT.  
  
 *Handle*  
 [입력] 비동기 처리를 완료할 핸들입니다. *핸들이* *핸들 Type에서*지정한 형식의 유효한 핸들이 아닌 경우 **SQLCompleteAsync는** SQL_INVALID_HANDLE 반환합니다.  
  
 *핸들이* *핸들 Type에서*지정한 형식의 유효한 핸들이 아닌 경우 **SQLCompleteAsync는** SQL_INVALID_HANDLE 반환합니다.  
  
 *비동기레트코드Ptr*  
 [출력] 비동기 API의 반환 코드를 포함하는 버퍼에 대한 포인터입니다. *비동기RetCodePtr이* NULL이면 **SQLCompleteAsync는** SQL_ERROR 반환합니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_ERROR, SQL_NO_DATA 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLCompleteAsync가** SQL_SUCCESS 반환하는 경우 응용 프로그램은 *AsyncRetCodePtr에*의해 가리키는 버퍼에서 비동기 함수의 반환 코드를 받아야 합니다. 연결된 SQLSTATE(있는 경우)는 *핸들 유형* SQL_HANDLE_STMT 및 명령문 핸들 또는 핸들 *유형* SQL_HANDLE_DBC 및 연결 핸들을 사용하는 **SQLGetDiagRec를** 호출하여 가져올 수 있습니다. 이러한 진단 레코드는 이 **SQLCompleteAsync** 함수가 아니라 비동기 함수와 연결됩니다.  
  
 **SQLCompleteAsync 는 SQLCompleteAsync가** **SQLCompleteAsync** 올바르게 호출되지 않음을 나타내기 위해 SQL_SUCCESS 이외의 코드를 반환합니다. **SQLCompleteAsync는** 이 경우 진단 레코드를 게시하지 않습니다. 가능한 반환 코드는 다음과 같습니다.  
  
-   SQL_INVALID_HANDLE: HandleType *및* *Handle으로* 표시된 핸들이 올바른 핸들이 아닙니다.  
  
-   SQL_ERROR: *비동기코드Ptr이* NULL이거나 비동기 처리가 핸들에서 활성화되지 않습니다.  
  
-   SQL_NO_DATA: 알림 모드에서비동기 작업이 진행중이 아니거나 드라이버 관리자가 응용 프로그램에 알리지 않았습니다. 폴링 모드에서는 비동기 작업이 진행되지 않습니다.  
  
## <a name="comments"></a>주석  
 폴링 기반 비동기 처리 모드에서 **는 SQLCompleteAsync가** SQL_SUCCESS 반환할 때 *비동기 코드Ptr이* SQL_STILL_EXECUTING 수 있습니다. 응용 프로그램은 *비동기RetCodePtr이* SQL_STILL_EXECUTING 않을 때까지 폴링을 유지해야합니다. 알림 기반 비동기 처리 모드에서는 *AsyncRetCodePtr이* SQL_STILL_EXECUTING 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [비동기 실행(폴링 메서드)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
