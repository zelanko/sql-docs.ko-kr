---
title: "SQLCancelHandle 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQLCancelHandle
helpviewer_keywords:
- SQLCancelHandle function [ODBC]
ms.assetid: 16049b5b-22a7-4640-9897-c25dd0f19d21
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 769f1659436f4325e25f0898c759d25327a795be
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcancelhandle-function"></a>SQLCancelHandle 함수
**규칙**  
 ODBC 3.8 도입 된 버전:  
  
 표준 준수: 없음  
  
 대부분의 ODBC 3.8 (이상) 드라이버가이 함수를 구현 합니다는 사용할 수 있습니다. 드라이버에 대 한 호출 하지 않는 경우 **SQLCancelHandle** 연결에서 처리는 *처리* 매개 변수는 IM001 SQLSTATE 및 메시지는 SQL_ERROR를 반환 합니다 ' 드라이버는이 함수를 지원 하지 않으면 ' 호출 **SQLCancelHandle** 로 처리 하는 문으로 *처리* 에 대 한 호출에 매개 변수가 매핑됩니다 **SQLCancel** 드라이버 관리자에서 경우 처리할 수 있습니다 드라이버 구현 **SQLCancel**합니다. 응용 프로그램 צ ְ ײ **SQLGetFunctions** 드라이버를 지원 하는지 확인 하 **SQLCancelHandle**합니다.  
  
 **요약**  
 **SQLCancelHandle** 연결 또는 명령문에 처리를 취소 합니다. 드라이버 관리자에 대 한 호출을 매핑합니다 **SQLCancelHandle** 한 호출에 **SQLCancel** 때 *HandleType* 여 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 [입력] 형식 cacel 처리에에 대 한 핸들입니다. 유효한 값은 sql_handle_dbc 라는 또는 여입니다.  
  
 *Handle*  
 [입력] 처리를 취소 하려는 핸들입니다.  
  
 경우 *처리* 하 여 지정 된 형식의 유효한 핸들 않습니다 *HandleType*, **SQLCancelHandle** 에서 SQL_INVALID_HANDLE을 반환 합니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLCancelHandle** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* 의 문과 여 처리 *처리* 또는 *HandleType* sql_handle_dbc 라 및 연결 핸들의 *처리*합니다.  
  
 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLCancelHandle** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) 인수에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|와 관련 된 문 핸들 중 하나에 대해 비동기적으로 실행 중인 문을 관련 함수를 호출한는 *처리*, 및 *HandleType* SQL_HANDLE_DBC로 설정 되었습니다. 비동기 함수 계속 실행 될 때 **SQLCancelHandle** 호출 되었습니다.<br /><br /> DM ()는 *HandleType* 인수 여; 관련된 연결 핸들에서 비동기적으로 실행 중인 함수 호출 된 였으며이 함수를 호출할 때 함수 계속 실행 합니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 와 관련 된 문 핸들 중 하나에 대해 호출한는 *처리* 및 *HandleType* 를 SQL_HANDLE_DBC로 설정 하 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.<br /><br /> **SQLBrowseConnect** 위해 호출 된 *ConnectionHandle*, SQL_NEED_DATA를 반환 합니다. 이 함수는 검색 프로세스를 완료 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY092|잘못 된 특성/옵션 식별자|*HandleType* SQL_HANDLE_DESC 또는 SQL_HANDLE_ENV로 설정 되었습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *처리* 함수를 지원 하지 않습니다.|  
  
 경우 **SQLCancelHandle** 사용 하 여 호출 *HandleType* 여로 설정, 반환할 수 있지만 함수에서 반환 될 수 있는 모든 SQLSTATE **SQLCancel**합니다.  
  
## <a name="comments"></a>설명  
 이 함수는 **SQLCancel** 있지만 문 핸들에만 아닌 매개 변수는 연결 또는 명령문 핸들을 걸릴 수 있습니다. 드라이버 관리자에 대 한 호출을 매핑합니다 **SQLCancelHandle** 한 호출에 **SQLCancel** 때 *HandleType* 여 됩니다. 이 통해 사용 하도록 응용 프로그램 **SQLCancelHandle** 드라이버 구현 하지 않는 경우에 문 작업을 취소 하기 **SQLCancelHandle**합니다.  
  
 문 작업을 취소 하는 방법에 대 한 자세한 내용은 참조 [SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)합니다.  
  
 에 진행 중인 작업이 없을 경우 *처리* 호출 **SQLCancelHandle** 영향을 주지 않습니다.  
  
 **SQLCancelHandle** 핸들 연결에서 다음과 같은 유형의 처리를 취소할 수 있습니다.  
  
-   연결에서 비동기적으로 실행 되는 함수입니다.  
  
-   다른 스레드에서 연결 핸들에서 실행 되는 함수입니다.  
  
 때 **SQLCancelHandle** 연결에 의해 게시 되는 진단 레코드에서 비동기적으로 실행 되는 함수를 취소 하기 위해 호출 **SQLCancelHandle** 되는 작업에서 반환한 추가 취소 하지만 **SQLCancelHandle** 반환 하지 않는 진단 레코드 다른 스레드에 대 한 연결에서 실행 되는 함수를 취소 하는 경우.  
  
 사용 하 여 **SQLCancelHandle** 취소 하려면 **SQLEndTran** 일시 중단된 상태에서 연결을 넣을 수 있습니다. 일시 중단 된 상태에 대 한 자세한 내용은 참조 하십시오. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.  
  
> [!NOTE]  
>  사용 하는 방법에 대 한 내용은 **SQLCancelHandle** Windows 7 이전의 Windows 운영 체제에 배포 될 응용 프로그램에서 참조 [호환성 매트릭스](../../../odbc/reference/develop-app/compatibility-matrix.md)합니다.  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>연결 관련 비동기 처리를 취소합니다.  
 함수가 SQL_STILL_EXECUTING을 반환 하는 경우 응용 프로그램 호출 **SQLCancelHandle** 여 작업을 취소 합니다. 취소 요청에 성공 하면 **SQLCancelHandle** 관계 없이 SQL_SUCCESS를 반환 합니다. 원래 함수 취소 된; 아닙니다. 취소 요청을 처리 하는 것을 나타냅니다. 드라이버 및 데이터 원본을 변경 하거나 작업이 취소 되는 경우를 결정 합니다. 응용 프로그램 계속 반환 코드를 SQL_STILL_EXECUTING 없을 때까지 원래 함수를 호출 해야 합니다. 반환 코드는 SQL_ERROR 및 SQLSTATE HY008 원래 함수 취소 된 경우 (작업이 취소 됨). 원래 함수는 일반적으로 처리를 완료 하는 경우 (취소 되지 않은), 반환 코드는 SQL_SUCCESS 또는, SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR 및 HY008 이외의 SQLSTATE (작업을 취소 했습니다), 원래 함수 실패 한 경우.  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>함수에서 다른 스레드로 실행을 취소 합니다.  
 다중 스레드 응용 프로그램에서는 응용 프로그램 다른 스레드에서 실행 중인 작업을 취소할 수 있습니다. 응용 프로그램 호출 작업을 취소 하려면 **SQLCancelHandle** 다른 스레드에서 함수에 의해 사용 된 핸들을 포함 합니다. 드라이버 및 운영 체제 작업이 취소 되는 방식을 결정 합니다. **SQLCancelHandle** 반환 코드 드라이버가 SQL_SUCCESS 또는 SQL_ERROR (진단 정보 없음 반환) 중 하나를 반환 합니다. 요청을 처리 하는지 여부를 나타냅니다. 원래 함수에 대 한 처리를 취소 되 면 원래 함수 반환 SQL_ERROR 및 SQLSTATE HY008 (작업이 취소 됨).  
  
 함수가 되 고 있으면 될 때 실행 되 **SQLCancelHandle** 라고 함수를 취소 하려면 다른 스레드에서 cancel 적용 관계 없이 SQL_SUCCESS를 반환 하는 함수에 대 한 가능한 됩니다. 에 대 한 호출 **SQLCancelHandle** 하기 전에 작업을 완료 하는 경우 아무 효과가 **SQLCancelHandle** 작업을 취소할 수 있었습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|데이터를 필요로 하는 문에 대 한 함수를 취소 하거나 취소 하는 문에서 다른 스레드에서 실행 되는 함수 문 핸들에서 비동기적으로 실행 되는 함수를 취소 합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [비동기 실행(폴링 메서드)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)

