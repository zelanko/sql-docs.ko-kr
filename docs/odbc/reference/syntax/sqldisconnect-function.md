---
title: SQLDisconnect 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDisconnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDisconnect
helpviewer_keywords:
- SQLDisconnect function [ODBC]
ms.assetid: 9e84a58e-db48-4821-a0cd-5c711fcbe36b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61e32c11aafeaf693188a96b48ddd60728ba5bc4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061461"
---
# <a name="sqldisconnect-function"></a>SQLDisconnect 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLDisconnect** 특정 연결 핸들에 연결 된 연결을 닫습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>인수  
 *ConnectionHandle*  
 [입력] 연결 핸들입니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE, 또는 SQL_STILL_EXECUTING 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLDisconnect** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* SQL_의 HANDLE_DBC와 *처리할* 의 *ConnectionHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLDisconnect** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01002|연결 끊김 오류|연결 해제 하는 동안 오류가 발생 했습니다. 그러나 연결 해제가 했습니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08003|연결이 열려 있지 않습니다.|(DM) 인수에 지정 된 연결이 *ConnectionHandle* 열리지 않았습니다.|  
|25000|잘못된 트랜잭션 상태|프로세스 인수에 의해 지정 된 연결에서 트랜잭션 했습니다 *ConnectionHandle*합니다. 트랜잭션이 활성 상태를 유지 합니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *ConnectionHandle*합니다. 함수 호출 및 완료 했습니다 실행 하기 전에 [SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md) 가 호출 될를 *ConnectionHandle*합니다. 함수에서 다시 호출 된 다음 합니다 *ConnectionHandle*합니다.<br /><br /> 함수 호출 및 실행을 완료 하기 전에 **SQLCancelHandle** 가 호출 된 *ConnectionHandle* 다중 스레드 응용 프로그램에서 다른 스레드에서 합니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수에 대해 호출 된를 *StatementHandle* 연관 합니다 *ConnectionHandle* 경우 계속 실행 하 고 **SQLDisconnect** 되었습니다 호출 됩니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *ConnectionHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된를 *StatementHandle*  연관 된 *ConnectionHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간 만료 됨|연결 제한 시간에는 데이터 원본, 요청에 응답 하 고 연결이 아직 활성 상태인 전에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *ConnectionHandle* 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램을 호출 하는 경우 **SQLDisconnect** 한 후 **SQLBrowseConnect** SQL_NEED_DATA를 반환 합니다, 드라이버는 다른 반환 코드를 반환 하기 전에 프로세스를 검색 하는 연결을 취소 하 고 반환 합니다 연결 된 연결 되지 않은 상태입니다.  
  
 응용 프로그램을 호출 하는 경우 **SQLDisconnect** 연결 핸들에 연결 된 불완전 한 트랜잭션에 인 동안 드라이버 트랜잭션이 변경 중임을 나타내는 SQLSTATE 25000 (잘못 된 트랜잭션 상태)를 반환 합니다 및 연결이 열려 있습니다. 불완전 한 트랜잭션에 하지 커밋 또는 사용 하 여 롤백될 **SQLEndTran**합니다.  
  
 응용 프로그램을 호출 하는 경우 **SQLDisconnect** 연결과 관련 된 모든 문이 해제 하기 전에 드라이버, 데이터 원본에서 성공적으로 연결 해제 후 해제 이러한 문과 되었던 모든 설명자 연결에 명시적으로 할당 합니다. 그러나 하나 이상의 경우 연결과 관련 된 문을 계속 실행 하는 비동기적으로 **SQLDisconnect** HY010 SQLSTATE 값을 사용 하 여 SQL_ERROR를 반환 합니다 (함수 시퀀스 오류). 또한 **SQLDisconnect** 연결 된 모든 문 및 명시적으로 할당 된 연결에서 연결이 일시 중지 된 상태가 아니면 모든 설명자 확보할 **SQLDisconnect** 되었습니다 가 성공적으로 취소 **SQLCancelHandle**합니다.  
  
 응용 프로그램을 사용 하는 방법에 대 한 자세한 **SQLDisconnect**를 참조 하세요 [데이터 원본 또는 드라이버에서 연결 끊기](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)합니다.  
  
## <a name="disconnecting-from-a-pooled-connection"></a>풀링된 연결에서 연결을 끊는 중  
 공유 환경에 대 한 연결 풀링을 사용 하도록 설정 하 고 응용 프로그램 호출 **SQLDisconnect** 해당 환경에서 연결에서 연결 연결 풀으로 반환 되 고 다른 구성 요소를 사용 하 여 계속 사용할 수 동일한 공유 환경입니다.  
  
## <a name="code-example"></a>코드 예  
 참조 [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md)하십시오 [SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md), 및 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|데이터 원본에 연결|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|연결 문자열 또는 대화 상자를 사용 하 여 데이터 원본에 연결|[SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|커밋 또는 롤백 작업을 실행합니다.|[SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|연결 핸들 해제|[SQLFreeConnect 함수](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
