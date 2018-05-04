---
title: SQLDisconnect 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 658b6cdddf1cbf66d7216c7fcdaa1b011c134345
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqldisconnect-function"></a>SQLDisconnect 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLDisconnect** 특정 연결 핸들에 연결 된 연결을 닫습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>인수  
 *ConnectionHandle*  
 [입력] 연결 핸들입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE, 또는 SQL_STILL_EXECUTING 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLDisconnect** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* SQL_의 HANDLE_DBC 및 *처리* 의 *ConnectionHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLDisconnect** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01002|오류 연결 끊기|연결 해제 하는 동안 오류가 발생 했습니다. 그러나 연결 해제가 했습니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08003|연결이 열려 있지 않습니다|(DM) 인수에 지정 된 연결 *ConnectionHandle* 를 열 수 없습니다.|  
|25000|잘못된 트랜잭션 상태|인수에 의해 지정 된 연결의 프로세스에서 트랜잭션 했습니다 *ConnectionHandle*합니다. 트랜잭션이 활성 상태로 유지 합니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *ConnectionHandle*합니다. 함수가 호출 된 및를 완료 했습니다 실행 하기 전에 [SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md) 에서 호출 된는 *ConnectionHandle*합니다. 함수에서 다시 호출 된 후의 *ConnectionHandle*합니다.<br /><br /> 함수를 호출 하 고 실행을 완료 하기 전에 **SQLCancelHandle** 에서 호출 된는 *ConnectionHandle* 다중 스레드 응용 프로그램에서 다른 스레드에서 합니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()를 비동기적으로 실행 중인 함수에 대해 호출 되었습니다는 *StatementHandle* 연관는 *ConnectionHandle* 때 계속 실행 하 고 **SQLDisconnect** 되었습니다 호출 됩니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *ConnectionHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 되었으며 한 *StatementHandle*  연관는 *ConnectionHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하 고 연결이 아직 사용 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *ConnectionHandle* 함수를 지원 하지 않습니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>설명  
 응용 프로그램을 호출 하는 경우 **SQLDisconnect** 후 **SQLBrowseConnect** sql_need_data가 반환 하 고는 다른 반환 코드를 반환 하기 전에 드라이버 프로세스를 검색 하는 연결을 취소 하 고이 반환 하는 연결 된 연결 되지 않은 상태입니다.  
  
 응용 프로그램을 호출 하는 경우 **SQLDisconnect** 불완전 한 트랜잭션에 연결 핸들에 연결 된 상태인 동안 드라이버 SQLSTATE 25000 (잘못 된 트랜잭션 상태) 트랜잭션이 변경 중임을 나타내는 반환 및 연결이 열려 있습니다. 불완전 한 트랜잭션에 하지 커밋 또는 사용 하 여 롤백될 **SQLEndTran**합니다.  
  
 응용 프로그램을 호출 하는 경우 **SQLDisconnect** 전에 연결과 관련 된 모든 문을 해제 되 고, 드라이버를 성공적으로 데이터 원본에서 테이블을 후 해제 이러한 문 및 되었던 모든 설명자 연결에 명시적으로 할당 합니다. 그러나 하나 이상의 경우 연결과 관련 된 문을 여전히 비동기적으로 실행, **SQLDisconnect** SQLSTATE HY010 값 인 SQL_ERROR를 반환 합니다. (함수 시퀀스 오류). 또한 **SQLDisconnect** 관련 된 모든 문 및 명시적으로 할당 된 연결에서 연결이 일시 중단된 된 상태 또는 경우 모든 설명자를 해제 합니다 **SQLDisconnect** 되었습니다 가 성공적으로 취소 **SQLCancelHandle**합니다.  
  
 응용 프로그램 사용 하는 방법에 대 한 내용은 **SQLDisconnect**, 참조 [데이터 원본이 나 드라이버에서 연결 끊기](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)합니다.  
  
## <a name="disconnecting-from-a-pooled-connection"></a>풀링된 연결에서 연결 끊기  
 공유 환경에 대 한 연결 풀링이 사용 되 고 응용 프로그램이 호출 **SQLDisconnect** 해당 환경에서 해당 연결에서 연결이 연결 풀으로 반환 되 고 계속 사용 하 여 다른 구성 요소에 사용할 수 동일한 공유 환경입니다.  
  
## <a name="code-example"></a>코드 예  
 참조 [ODBC 프로그램 샘플](../../../odbc/reference/sample-odbc-program.md), [SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md), 및 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|데이터 원본에 연결|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|연결 문자열 또는 대화 상자를 사용 하 여 데이터 원본에 연결|[SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|커밋 또는 롤백 작업 실행|[SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|연결 핸들 해제|[SQLFreeConnect 함수](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
