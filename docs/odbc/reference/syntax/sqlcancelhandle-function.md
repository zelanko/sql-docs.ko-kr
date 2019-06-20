---
title: SQLCancelHandle 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
f1_keywords:
- SQLCancelHandle
helpviewer_keywords:
- SQLCancelHandle function [ODBC]
ms.assetid: 16049b5b-22a7-4640-9897-c25dd0f19d21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9f572e9e76f77b0c535cd57ff4ed6cd091aec0f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537568"
---
# <a name="sqlcancelhandle-function"></a>SQLCancelHandle 함수
**규칙**  
 도입 된 버전: ODBC 3.8  
  
 표준 준수 합니다. 없음  
  
 대부분의 ODBC 3.8 이상 드라이버가이 함수를 구현 합니다 예상 됩니다. 드라이버에 대 한 호출 하지 않는 경우 **SQLCancelHandle** 연결을 사용 하 여 처리 합니다 *처리* 매개 변수에서 IM001의 SQLSTATE 및 메시지를 사용 하 여 SQL_ERROR를 반환 하는 ' 드라이버는이 함수를 지원 하지 않습니다 ' 호출 **SQLCancelHandle** 문을 사용 하 여로 처리 합니다 *처리* 매개 변수에 대 한 호출으로 매핑될 **SQLCancel** 드라이버 관리자에 의해 경우에 처리 될 수 있습니다 드라이버 구현 **SQLCancel**합니다. 응용 프로그램에서 사용할 수 있습니다 **SQLGetFunctions** 드라이버를 지원 하는지 확인할 **SQLCancelHandle**합니다.  
  
 **요약**  
 **SQLCancelHandle** 연결 또는 명령문에서 처리를 취소 합니다. 드라이버 관리자에 대 한 호출을 매핑합니다 **SQLCancelHandle** 대 한 호출으로 **SQLCancel** 때 *HandleType* 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 [입력] Cacel 처리 하는 핸들의 형식입니다. 유효한 값은 SQL_HANDLE_DBC 또는 호출 합니다.  
  
 *Handle*  
 [입력] 처리를 취소 하는 핸들입니다.  
  
 경우 *처리할* 하 여 지정 된 형식의 유효한 핸들이 아닙니다 *HandleType*를 **SQLCancelHandle** 에서 SQL_INVALID_HANDLE을 반환 합니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLCancelHandle** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* 의 호출 하 여 문 핸들 *처리할* 또는 *HandleType* SQL_HANDLE_DBC 및 연결 핸들 *처리*.  
  
 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLCancelHandle** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) 인수의  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|와 관련 된 문 핸들 중 하나에 대해 비동기적으로 실행 중인 문을 관련 함수를 호출한 합니다 *처리할*, 및 *HandleType* SQL_HANDLE_DBC로 설정 되었습니다. 비동기 함수 계속 실행 될 때 **SQLCancelHandle** 호출 되었습니다.<br /><br /> (DM)는 *HandleType* 인수가 호출 하 여 연결 핸들에서 비동기적으로 실행 중인 함수를 호출한 하 고이 함수가 호출 되었을 때 함수를 계속 실행 합니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 관련 된 문 핸들 중 하나에 대해 호출한 합니다 *처리* 및 *HandleType* 를 SQL_HANDLE_DBC로 설정 되었으며 SQL_PARAM_DATA_AVAILABLE를 반환 합니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> **SQLBrowseConnect** 에 대 한 호출한 *ConnectionHandle*, SQL_NEED_DATA를 반환 합니다. 이 함수는 검색 프로세스를 완료 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY092|잘못 된 특성/옵션 식별자입니다.|*HandleType* SQL_HANDLE_ENV 또는 SQL_HANDLE_DESC로 설정 되었습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *처리* 함수를 지원 하지 않습니다.|  
  
 하는 경우 **SQLCancelHandle** 사용 하 여 라고 *HandleType* 호출 하 여로 함수에 의해 반환 될 수 있는 모든 SQLSTATE를 반환할 수 있습니다 **SQLCancel**합니다.  
  
## <a name="comments"></a>주석  
 이 함수는 비슷합니다 **SQLCancel** 있지만로 문 핸들만이 아닌 매개 변수 연결 또는 문 핸들을 걸릴 수 있습니다. 드라이버 관리자에 대 한 호출을 매핑합니다 **SQLCancelHandle** 대 한 호출으로 **SQLCancel** 때 *HandleType* 호출 됩니다. 이렇게 하면 응용 프로그램을 사용 하 여 **SQLCancelHandle** 드라이버를 구현 하지 않는 경우에 문 작업을 취소 하려면 **SQLCancelHandle**합니다.  
  
 문 작업을 취소 하는 방법에 대 한 자세한 내용은 참조 하세요. [SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)합니다.  
  
 진행 중인 작업이 없을 경우 *처리할* 에 대 한 호출 **SQLCancelHandle** 영향을 주지 않습니다.  
  
 **SQLCancelHandle** 핸들 연결에서 다음 유형의 처리를 취소할 수 있습니다.  
  
-   연결에서 비동기적으로 실행 되는 함수입니다.  
  
-   다른 스레드에서 연결 핸들에서 실행 되는 함수입니다.  
  
 때 **SQLCancelHandle** 연결 하 여 게시 하는 진단 레코드에서에서 비동기적으로 실행 하는 함수를 취소 하 라고 **SQLCancelHandle** 되 고 있는 작업에서 반환 하는 추가 취소 그러나 **SQLCancelHandle** 반환 하지 않는 진단 레코드, 다른 스레드에서 연결에서 실행 중인 함수를 취소 하는 경우.  
  
 사용 하 여 **SQLCancelHandle** 취소할 **SQLEndTran** 일시 중단 된 상태에서 연결을 넣을 수 있습니다. 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.  
  
> [!NOTE]  
>  사용 하는 방법에 대 한 자세한 **SQLCancelHandle** Windows 7 이전 Windows 운영 체제에 배포 되는 응용 프로그램에서 참조 [호환성 매트릭스](../../../odbc/reference/develop-app/compatibility-matrix.md)합니다.  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>연결 관련 비동기 처리를 취소합니다.  
 응용 프로그램 함수가 SQL_STILL_EXECUTING을 반환 하는 경우 호출할 수 있습니다 **SQLCancelHandle** 작업을 취소할 수 있습니다. 취소 요청에 성공 하면 **SQLCancelHandle** 관계 없이 SQL_SUCCESS를 반환 합니다. 이 의미 하지는 원래 함수 취소 되었습니다. 취소 요청이 처리 된 것을 나타냅니다. 드라이버 및 데이터 원본을 변경 하거나 작업이 취소 되는 경우를 결정 합니다. 응용 프로그램 계속 반환 코드를 SQL_STILL_EXECUTING 없을 때까지 원래 함수를 호출 해야 합니다. 반환 코드는 SQL_ERROR 및 SQLSTATE HY008 원래 함수 취소 된 경우 (작업이 취소 됨). 원래 함수는 일반적으로 처리를 완료 하는 경우 (취소 되지 않은), 반환 코드는 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 또는 SQL_ERROR와 HY008 이외의 SQLSTATE (작업 취소 됨), 원래 함수 실패 한 경우.  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>다른 스레드에서 실행 하는 함수를 취소 합니다.  
 다중 스레드 응용 프로그램에서 응용 프로그램 다른 스레드에서 실행 하는 작업을 취소할 수 있습니다. 응용 프로그램이 호출 작업을 취소 하려면 **SQLCancelHandle** 함수를 통해 다른 스레드에서 사용 하는 핸들을 포함 합니다. 드라이버 및 운영 체제에는 작업을 취소 하는 방법을 결정 합니다. 합니다 **SQLCancelHandle** 반환 코드는 드라이버가 SQL_SUCCESS 또는 SQL_ERROR (진단 정보가 반환 되지 않은)를 반환 합니다. 요청을 처리 하는지 여부를 나타냅니다. 원래 원본 함수에서 처리 취소 되 면 반환 SQL_ERROR 및 SQLSTATE HY008 (작업이 취소 됨).  
  
 함수 되 면 실행 될 때 **SQLCancelHandle** 라고 함수를 취소 하려면 다른 스레드에서 취소를 적용 하려면 먼저 관계 없이 SQL_SUCCESS를 반환 하는 함수에 대 한 가능한 것입니다. 에 대 한 호출 **SQLCancelHandle** 하기 전에 작업을 완료 하는 경우 효과가 없습니다 **SQLCancelHandle** 작업을 취소할 수 있었습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|문은 데이터에 대해 함수를 취소 하거나 취소 하는 다른 스레드에서 문을 실행 하는 함수 문 핸들에서 비동기적으로 실행 되는 함수를 취소 합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [비동기 실행(폴링 메서드)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
