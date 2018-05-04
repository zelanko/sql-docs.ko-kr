---
title: SQLEndTran 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLEndTran
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLEndTran
helpviewer_keywords:
- SQLEndTran function [ODBC]
ms.assetid: ff375ce1-eb50-4693-b1e6-70181a6dbf9f
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: af0207a5ccaa11728b0ff67a4acad75577acdca7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlendtran-function"></a>SQLEndTran 함수(SQLEndTran Function)
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLEndTran** 연결과 관련 된 모든 문에 대 한 모든 활성 작업에 대 한 커밋 또는 롤백 작업을 요청 합니다. **SQLEndTran** 커밋 또는 롤백 작업 하는 환경과 관련 된 모든 연결에 대해 수행할 수를 요청할 수도 있습니다.  
  
> [!NOTE]  
>  자세한 내용은 관리자에 대 한 어떤는 드라이버에 대 한 때 ODBC 3이이 함수를를 매핑합니다. *x* 응용 프로그램이 작동 ODBC 2. *x* 드라이버 참조 [이전 버전과 호환성의 응용 프로그램에 대 한 대체 함수 매핑](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 [입력] 유형 식별자를 처리 합니다. SQL_HANDLE_ENV 중 하나를 포함 (경우 *처리* 은 환경 핸들) 또는 sql_handle_dbc 라는 (경우 *처리* 연결 핸들입니다).  
  
 *Handle*  
 [입력] 표시 된 형식의 핸들 *HandleType*, 트랜잭션 범위를 나타내는입니다. 자세한 내용은 "설명"을 참조 하십시오.  
  
 *CompletionType*  
 [입력] 다음 두 값 중 하나입니다.  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE, 또는 SQL_STILL_EXECUTING 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLEndTran** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 는 적절 한 *HandleType*및 *처리*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLEndTran** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08003|연결이 열려 있지 않습니다|DM ()는 *HandleType* sql_handle_dbc 라는, 되었습니다 및 *처리* 가 연결 된 상태가 아닙니다.|  
|08007|트랜잭션 중 연결 오류|*HandleType* sql_handle_dbc 라는, 였으며와 관련 된 연결의 *처리* 함수를 실행 하는 동안 실패 했으며 수 없습니다 되었는지를 확인할 요청 된  **커밋** 또는 **롤백** 실패 하기 전에 발생 했습니다.|  
|25S01|트랜잭션 상태를 알 수 없음된|에 연결 중 하나 이상이 *처리* , 지정 된 결과 함께 트랜잭션을 완료 하지 못하고 결과 알 수 없습니다.|  
|25S02|트랜잭션이 여전히 활성 상태입니다.|드라이버는 전역 트랜잭션의 모든 작업을 개별적으로 완료할 수 없습니다 및 트랜잭션이 여전히 활성 상태인 보장할 수 없습니다.|  
|25S03|트랜잭션이 롤백|전역 트랜잭션의 모든 작업을 개별적으로 완료할 수 없습니다 및에서 활성 상태인 트랜잭션의 모든 작업을 보장할 수 없습니다 *처리* 롤백 되었습니다.|  
|40001|Serialization 오류|트랜잭션이 다른 트랜잭션 사용 하 여 리소스 교착 상태로 인해 롤백 되었습니다.|  
|40002|무결성 제약 조건 위반|*CompletionType* SQL_COMMIT, 였으며 커밋에 변경 내용 무결성 제약 조건 위반이 발생 합니다. 결과적으로, 트랜잭션이 롤백 되었습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*szMessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *ConnectionHandle*합니다. 함수를 호출 하 고 실행을 완료 하기 전에 [SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md) 에서 호출 된는 *ConnectionHandle*합니다. 함수에서 다시 호출 된 후의 *ConnectionHandle*합니다.<br /><br /> 함수를 호출 하 고 실행을 완료 하기 전에 **SQLCancelHandle** 에서 호출 된는 *ConnectionHandle* 다중 스레드 응용 프로그램에서 다른 스레드에서 합니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 비동기적으로 실행 중인 함수를 호출한와 관련 된 문 핸들에는 *ConnectionHandle* 때 계속 실행 하 고 **SQLEndTran** 호출 되었습니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *ConnectionHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 와 관련 된 문 핸들에 대해 호출한는 *ConnectionHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대 한 호출한는 *처리* 와 *HandleType* SQL_HANDLE_DBC로 설정 하 고이 함수를 호출할 때 계속 실행 합니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 와 관련 된 문 핸들 중 하나에 대해 호출한 *처리* 및 반환 된 SQL_PARAM_DATA_AVAILABLE 합니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.|  
|HY012|잘못 된 트랜잭션 작업 코드|인수에 대해 지정 된 값 (DM) *CompletionType* SQL_COMMIT 또는 SQL_ROLLBACK 아닙니다 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY092|잘못 된 특성/옵션 식별자|인수에 대해 지정 된 값 (DM) *HandleType* SQL_HANDLE_ENV 아니고 sql_handle_dbc 라는 되었습니다.|  
|HY115|사용 하도록 설정 하는 비동기 함수 실행에 대 한 연결을 포함 하는 환경을 SQLEndTran 허용 되지 않습니다.|(DM) *HandleType* 연결 함수의 비동기 실행 환경에서 연결에 사용 되 면 SQL_HANDLE_ENV로 설정할 수 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은이 항목의 설명 섹션을 참조 하십시오.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|드라이버 또는 데이터 원본 지원 하지 않습니다는 **롤백** 작업 합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *ConnectionHandle* 함수를 지원 하지 않습니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>설명  
 Odbc 3. *x* 드라이버 경우 *HandleType* SQL_HANDLE_ENV은 및 *처리* 다음 드라이버 관리자가 호출 됩니다는 한 유효한 환경 핸들 **SQLEndTran**는 환경에 연결 된 각 드라이버에 있습니다. *처리* 드라이버에 대 한 호출에 대 한 인수는 드라이버의 환경 핸들 됩니다. Odbc 2. *x* 드라이버 경우 *HandleType* SQL_HANDLE_ENV은 및 *처리* 은 잘못 된 환경 핸들 및 해당 환경에서 연결된 된 상태에 대 한 연결이 여러 개 다음 드라이버 관리자는 호출 **SQLTransact** 해당 환경에서 연결된 된 상태에서 각 연결에 대해 한 번씩 드라이버에서 합니다. *처리* 각 호출의 인수에는 연결의 핸들 수 있습니다. 두 경우 모두 드라이버는 하려고 값에 따라 트랜잭션을 커밋하거나 *CompletionType*, 해당 환경에서 연결된 된 상태에 있는 모든 연결에 대해 합니다. 연결이 활성화 되지 않은 트랜잭션을 영향을 주지 않습니다.  
  
> [!NOTE]  
>  **SQLEndTran** 커밋하거나 공유 환경에서 트랜잭션 롤백에 사용할 수 없습니다. SQLSTATE HY092 (잘못 된 특성/옵션 식별자)는 경우 반환 될 **SQLEndTran** 사용 하 여 호출 *처리* 공유 환경 핸들 또는 공유에 대 한 연결의 핸들을로 설정 환경입니다.  
  
 드라이버 관리자는 각 연결에 대 한 관계 없이 SQL_SUCCESS를 수신 하는 경우에 관계 없이 SQL_SUCCESS를 반환 합니다. 드라이버 관리자는 하나 이상의 연결에서 SQL_ERROR가 받는, 응용 프로그램에서 SQL_ERROR를 반환 하 고 진단 정보는 환경의 진단 데이터 구조에 저장 합니다. 응용 프로그램이 호출할 수 있는 연결 또는 연결에서 커밋 또는 롤백 작업 중 실패를 확인 하려면 **SQLGetDiagRec** 각 연결에 대 한 합니다.  
  
> [!NOTE]  
>  드라이버 관리자는 모든 연결에서 전역 트랜잭션 시뮬레이션 하지 않습니다와 2 단계 커밋 프로토콜을 사용 하지 않습니다.  
  
 경우 *CompletionType* SQL_COMMIT은 **SQLEndTran** 된 문에서 영향을 받는 연결과 관련 된 모든 활성 작업에 대 한 커밋 요청을 실행 합니다. 경우 *CompletionType* SQL_ROLLBACK은 **SQLEndTran** 된 문에서 영향을 받는 연결과 관련 된 모든 활성 작업에 대 한 롤백 요청을 실행 합니다. 트랜잭션이 활성 상태인 경우 **SQLEndTran** 모든 데이터 원본에 영향을 주지 관계 없이 SQL_SUCCESS를 반환 합니다. 자세한 내용은 참조 [Committing 및 트랜잭션을 롤링](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md)합니다.  
  
 드라이버 수동 커밋 모드에 있으면 (호출 하 여 **SQLSetConnectAttr** 는 SQL_ATTR_AUTOCOMMIT을 SQL_AUTOCOMMIT_OFF로 집합 특성) 때 내에 포함 될 수 있는 SQL 문을 암시적으로 새 트랜잭션이 시작 되는 트랜잭션이 현재 데이터 원본에 대해 실행 됩니다. 자세한 내용은 참조 [커밋 모드](../../../odbc/reference/develop-app/commit-mode.md)합니다.  
  
 트랜잭션 작업이 커서에 미치는 영향을 확인 하려면 응용 프로그램이 호출 **SQLGetInfo** SQL_CURSOR_ROLLBACK_BEHAVIOR 및 SQL_CURSOR_COMMIT_BEHAVIOR 옵션입니다. 자세한 내용은 다음 단락을 참조 하십시오. 및 참조도 [커서 및 준비 된 문에서 영향의 트랜잭션을](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)합니다.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR 또는 SQL_CURSOR_COMMIT_BEHAVIOR 값 SQL_CB_DELETE, 절과 같을 경우 **SQLEndTran** 닫습니다 및 연결과 관련 된 모든 문이 열려 있는 모든 커서를 삭제 하 고, 모든 보류 중인 결과 무시 합니다. **SQLEndTran** 할당 된 (준비) 상태 이면에 있는 모든 문을 벗어날 응용 프로그램이 후속 SQL 요청에 다시 사용할 수 나 호출할 수 **SQLFreeStmt** 또는 **SQLFreeHandle** 와 *HandleType* 이러한 할당을 취소 하 여입니다.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR 또는 SQL_CURSOR_COMMIT_BEHAVIOR 값 SQL_CB_CLOSE, 절과 같을 경우 **SQLEndTran** 연결과 관련 된 모든 문에서 열려 있는 모든 커서가 닫힙니다. **SQLEndTran** 준비 된 상태 이면에 있는 모든 문을 벗어날 응용 프로그램에서 호출할 수 **SQLExecute** 먼저 호출 하지 않고 연결과 관련 된 문에 대 한 **SQLPrepare**합니다.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR 또는 SQL_CURSOR_COMMIT_BEHAVIOR 값 SQL_CB_PRESERVE, 절과 같을 경우 **SQLEndTran** 연결과 관련 된 열려 있는 커서에는 영향을 주지 않습니다. 커서는 계속 호출 하기 전에 가리키는 행 **SQLEndTran**합니다.  
  
 호출 트랜잭션을 지 원하는 드라이버와 데이터 원본에 대 한 **SQLEndTran** SQL_COMMIT 또는 SQL_ROLLBACK으로 활성화 된 트랜잭션이 없는 경우 SQL_SUCCESS (커밋 또는 롤백 작업이 있음을 나타내는) 반환 됩니다. 및 데이터 원본에는 아무 효과가 없습니다.  
  
 드라이버 관리자가 호출 하지 않으면 드라이버가 자동 커밋 모드일 때 **SQLEndTran** 드라이버에서입니다. **SQLEndTran** 항상으로 호출 되었는지 여부에 관계 없이 SQL_SUCCESS를 반환 합니다는 *CompletionType* SQL_COMMIT 또는 SQL_ROLLBACK 합니다.  
  
 트랜잭션을 지원 하지 않는 드라이버 또는 데이터 원본 (**SQLGetInfo** *옵션* SQL_TXN_CAPABLE SQL_TC_NONE은)는 항상 효과적으로 자동 커밋 모드 및 따라서 항상에 대 한 관계 없이 SQL_SUCCESS를 반환 **SQLEndTran** 으로 호출 될 지 여부는 *CompletionType* SQL_COMMIT 또는 SQL_ROLLBACK 합니다. 이러한 드라이버와 데이터 원본의 실제로 롤백하지 않습니다 그렇게 하도록 요청 하면 트랜잭션.  
  
## <a name="suspended-state"></a>일시 중단 된 상태  
 Windows 7 보다 먼저 발표 된 드라이버 관리자 트랜잭션이 활성 상태 였던 경우 **SQLEndTran** 드라이버에서 SQL_ERROR를 반환 합니다. 그러나 트랜잭션이 성공적으로 커밋된 서버에 있지만 (예를 들어 네트워크 오류가 발생 했으므로) 클라이언트에서 드라이버에 알림을 받지 수 있었습니다. 연결 상태가 좋지 남을 수 있습니다. Windows 7부터 때 **SQLEndTran** 연결 SQL_ERROR를 반환 일시 중단된 된 상태에 있을 수 있습니다. 일시 중단된 된 상태에서 읽기 전용 함수를 호출 하는 것이 같습니다. 응용 프로그램을 호출 해야 결국 **SQLDisconnect** 일시 중단 된 연결 리소스를 해제 합니다.  
  
 다음 조건이 모두 true 인 경우 연결을 일시 중단 된 상태로 저장 됩니다.  
  
-   드라이버에서 SQL_ERROR를 반환 합니다. **SQLEndTran**합니다.  
  
-   드라이버는 ODBC 3.8, 또는 이후 버전.  
  
-   응용 프로그램 버전은 3.8 이상; 다시 컴파일된 ODBC 2.x 또는 3.x 응용 프로그램을 성공적으로 취소 된 **SQLEndTran** 를 통해 작동할 **SQLCancelHandle**합니다.  
  
-   드라이버는 트랜잭션이 완료 되지 않은 확인 하면 다음 메시지 중 하나를 반환 하지 않았습니다.  
  
    -   25S03: 트랜잭션이 롤백  
  
    -   40001: serialization 오류  
  
    -   40002: 무결성 제약 조건  
  
    -   HYC00: 선택적 기능이 구현 되지 않았습니다  
  
 경우 **SQLEndTran** 호출 된 환경에서 핸들 및 연결 중 하나 위의 조건이 충족 됩니다., 동일한 드라이버에 연결 하는 모든 연결을 일시 중단된 상태에 놓이게 됩니다.  
  
 응용 프로그램이 호출 후 **SQLDisconnect** 일시 중단 된 연결에서 연결 데 사용할 수 있습니다 다른 데이터 원본 또는 동일한 데이터 소스에 다시 연결 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|연결 핸들에서 비동기적으로 실행 되는 함수를 취소 합니다.|[SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|드라이버 또는 데이터 원본에 대 한 정보 반환|[SQLGetInfo 함수](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|핸들을 해제합니다.|[SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|문 핸들 해제|[SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [비동기 실행(폴링 메서드)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
