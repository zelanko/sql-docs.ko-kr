---
title: SQLEndTran 함수 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLEndTran
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLEndTran
helpviewer_keywords:
- SQLEndTran function [ODBC]
ms.assetid: ff375ce1-eb50-4693-b1e6-70181a6dbf9f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98a0f072af79c2c6e39d0cfc49e72cbeef1c2193
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344771"
---
# <a name="sqlendtran-function"></a>SQLEndTran 함수(SQLEndTran Function)
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **Sqlendtran** 은 연결과 관련 된 모든 문의 모든 활성 작업에 대 한 커밋 또는 롤백 작업을 요청 합니다. **Sqlendtran** 은 환경에 연결 된 모든 연결에 대해 커밋 또는 롤백 작업을 수행 하도록 요청할 수도 있습니다.  
  
> [!NOTE]  
>  ODBC 3의 경우 드라이버 관리자가이 기능을에 매핑하는 방법에 대 한 자세한 내용을 확인 하십시오. *x* 응용 프로그램에서 ODBC 2를 사용 하 고 있습니다. *x* 드라이버 [응용 프로그램의 이전 버전과의 호환성을 위해 대체 함수 매핑](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)을 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 입력 핸들 유형 식별자입니다. SQL_HANDLE_ENV ( *핸들이* 환경 핸들 인 경우) 또는 SQL_HANDLE_DBC ( *핸들이* 연결 핸들 인 경우)를 포함 합니다.  
  
 *Handle*  
 입력 *HandleType*에 표시 되는 형식의 핸들로, 트랜잭션의 범위를 나타냅니다. 자세한 내용은 "설명"을 참조 하세요.  
  
 *CompletionType*  
 입력 다음 두 값 중 하나입니다.  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE 또는 SQL_STILL_EXECUTING입니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlendtran** 이 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환할 때 적절 한 *HandleType* 및 *핸들*을 사용 하 여 **SQLGETDIAGREC** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 **Sqlendtran** 에서 일반적으로 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목을 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR입니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08003|연결이 열려 있지 않음|(DM) *HandleType* 가 SQL_HANDLE_DBC 되었으며, *핸들이* 연결 된 상태가 아닙니다.|  
|08007|트랜잭션 중 연결 오류|*HandleType* 가 SQL_HANDLE_DBC이 고 *핸들* 에 연결 된 연결이 함수를 실행 하는 동안 실패 했으며 요청 된 **커밋** 또는 **롤백이** 이전에 발생 했는지 여부를 확인할 수 없습니다. 실패로.|  
|25S01|트랜잭션 상태 알 수 없음|*핸들* 에 있는 하나 이상의 연결에서 지정 된 결과를 사용 하 여 트랜잭션을 완료 하지 못했으며 결과가 알려지지 않았습니다.|  
|25S02|트랜잭션이 아직 활성 상태입니다.|드라이버가 전역 트랜잭션의 모든 작업을 원자성으로 완료할 수 없으며 트랜잭션이 여전히 활성 상태 인지를 보장할 수 없습니다.|  
|25S03|트랜잭션을 롤백합니다.|드라이버가 전역 트랜잭션의 모든 작업을 원자성으로 완료할 수 있으며 *핸들* 에서 활성화 된 트랜잭션의 모든 작업이 롤백 되었음을 보장할 수 없습니다.|  
|40001|Serialization 오류|다른 트랜잭션과의 리소스 교착 상태 때문에 트랜잭션이 롤백 되었습니다.|  
|40002|무결성 제약 조건 위반|SQL_COMMIT *형식이* 변경 되어 무결성 제약 조건 위반이 발생 했습니다. 그 결과 트랜잭션이 롤백됩니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. SzMessageText 버퍼에서 **SQLGetDiagRec에** 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.  *\**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소 됨|*ConnectionHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 [Sqlcancelhandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md) 실행이 완료 되기 전에 *ConnectionHandle*에서 호출 되었습니다. 그런 다음 *ConnectionHandle*에서 함수를 다시 호출 했습니다.<br /><br /> 함수가 호출 되었고 **Sqlcancelhandle** 실행이 완료 되기 전에 다중 스레드 응용 프로그램의 다른 스레드에서 *ConnectionHandle* 에 대해 호출 되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *ConnectionHandle* 연결 된 문 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었으며 **sqlendtran** 이 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) *ConnectionHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *ConnectionHandle* 와 연결 된 문 핸들에 대해 호출 되 고 SQL_NEED_DATA를 반환 했습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.<br /><br /> (DM) *HandleType* 가 SQL_HANDLE_DBC로 설정 되 고이 함수가 호출 될 때 여전히 실행 되 고 있는 *핸들* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었습니다.<br /><br /> (DM) **Sqlexecute**, **Sqlexecdirect**또는 **SQLMoreResults** 가 *핸들과* 연결 된 문 핸들 중 하나에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE가 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.|  
|HY012|트랜잭션 작업 코드가 잘못 되었습니다.|(DM) 인수 인수 *형식* 에 지정 된 값이 SQL_COMMIT 또는 SQL_ROLLBACK가 아닙니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY092|특성/옵션 식별자가 잘못 되었습니다.|(DM) 인수 *HandleType* 에 지정 된 값이 SQL_HANDLE_ENV 또는 SQL_HANDLE_DBC가 아닙니다.|  
|HY115|비동기 함수 실행을 사용 하는 연결을 포함 하는 환경에서는 SQLEndTran을 사용할 수 없습니다.|(DM) *HandleType* 는 환경에서 연결에 대 한 비동기 연결 기능 실행이 설정 된 경우 SQL_HANDLE_ENV로 설정할 수 없습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 상태에 대 한 자세한 내용은이 항목의 설명 섹션을 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|드라이버 또는 데이터 원본이 **롤백** 작업을 지원 하지 않습니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *ConnectionHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출에서 SQL_STILL_EXECUTING를 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
## <a name="comments"></a>주석  
 ODBC 3의 경우. *x* 드라이버, *HandleType* 가 SQL_HANDLE_ENV이 고 *handle* 이 유효한 환경 핸들 인 경우 드라이버 관리자는 환경에 연결 된 각 드라이버에서 **sqlendtran** 을 호출 합니다. 드라이버에 대 한 호출에 대 한 *핸들* 인수는 드라이버의 환경 핸들이 됩니다. ODBC 2의 경우. *x* 드라이버, *HandleType* 가 SQL_HANDLE_ENV이 고 *HANDLE* 이 유효한 환경 핸들이 고 해당 환경에 연결 된 상태에 여러 연결이 있는 경우 드라이버 관리자는 드라이버에서 **sqltransact** 을 호출 합니다. 해당 환경에서 연결 된 상태의 각 연결에 대해 한 번 각 호출의 *handle* 인수는 연결의 핸들입니다. 두 경우 모두, 드라이버는 해당 환경에서 연결 된 상태에 있는 모든 연결의 확정 *유형*값에 따라 트랜잭션을 커밋하거나 롤백합니다. 활성 상태가 아닌 연결은 트랜잭션에 영향을 주지 않습니다.  
  
> [!NOTE]  
>  **Sqlendtran** 은 공유 환경에서 트랜잭션을 커밋하거나 롤백하는 데 사용할 수 없습니다. 공유 환경의 핸들 또는 공유 환경의 연결 핸들로 설정 된 *핸들* 을 사용 하 여 **sqlendtran** 을 호출 하는 경우 SQLSTATE HY092 (잘못 된 특성/옵션 식별자)가 반환 됩니다.  
  
 드라이버 관리자는 각 연결에 대해 SQL_SUCCESS를 수신 하는 경우에만 SQL_SUCCESS를 반환 합니다. 드라이버 관리자는 하나 이상의 연결에 대해 SQL_ERROR를 수신 하는 경우 SQL_ERROR를 응용 프로그램에 반환 하 고, 진단 정보는 환경의 진단 데이터 구조에 배치 됩니다. 커밋 또는 롤백 작업 중에 실패 한 연결 또는 연결을 확인 하기 위해 응용 프로그램은 각 연결에 대해 **SQLGetDiagRec** 를 호출할 수 있습니다.  
  
> [!NOTE]  
>  드라이버 관리자는 모든 연결에서 글로벌 트랜잭션을 시뮬레이션 하지 않으므로 2 단계 커밋 프로토콜을 사용 하지 않습니다.  
  
 SQL_COMMIT *형식이* 인 경우 **sqlendtran** 은 영향을 받는 연결과 관련 된 모든 문의 모든 활성 작업에 대해 커밋 요청을 발급 합니다. 지 수 *유형이* SQL_ROLLBACK 인 경우 **sqlendtran** 은 영향을 받는 연결과 관련 된 모든 문에서 모든 활성 작업에 대 한 롤백 요청을 발급 합니다. 활성 트랜잭션이 없는 경우 **Sqlendtran** 은 데이터 원본에 영향을 주지 않고 SQL_SUCCESS를 반환 합니다. 자세한 내용은 [트랜잭션 커밋 및 롤백](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md)을 참조 하세요.  
  
 SQL_ATTR_AUTOCOMMIT 특성이 SQL_AUTOCOMMIT_OFF로 설정 된 **SQLSetConnectAttr** 를 호출 하 여 드라이버가 수동 커밋 모드인 경우 트랜잭션 내에 포함 될 수 있는 SQL 문이 있으면 새 트랜잭션이 암시적으로 시작 됩니다. 현재 데이터 소스에 대해 실행 됩니다. 자세한 내용은 [커밋 모드](../../../odbc/reference/develop-app/commit-mode.md)를 참조 하세요.  
  
 트랜잭션 작업이 커서에 미치는 영향을 확인 하기 위해 응용 프로그램은 SQL_CURSOR_ROLLBACK_BEHAVIOR 및 SQL_CURSOR_COMMIT_BEHAVIOR 옵션을 사용 하 여 **SQLGetInfo** 를 호출 합니다. 자세한 내용은 다음 단락을 참조 하 고 [커서 및 준비 된 문의 트랜잭션 효과](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)를 참조 하세요.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR 또는 SQL_CURSOR_COMMIT_BEHAVIOR 값이 SQL_CB_DELETE와 같은 경우 **Sqlendtran** 은 연결과 관련 된 모든 문에서 열려 있는 모든 커서를 닫고 모든 보류 중인 결과를 삭제 합니다. **Sqlendtran** 은 할당 된 (준비 되지 않음) 상태에 있는 모든 문을 그대로 둡니다. 응용 프로그램은 후속 SQL 요청에 대해 다시 사용 하거나 *HandleType* of SQL_HANDLE_STMT를 사용 하 여 **SQLFreeStmt** 또는 **sqlfreehandle** 을 호출 하 여 할당을 취소할 수 있습니다.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR 또는 SQL_CURSOR_COMMIT_BEHAVIOR 값이 SQL_CB_CLOSE와 같은 경우 **Sqlendtran** 은 연결과 관련 된 모든 문에서 열린 모든 커서를 닫습니다. **Sqlendtran** 은 준비 상태에 있는 모든 문을 그대로 둡니다. 응용 프로그램은 먼저 **Sqlexecute**를 호출 하지 않고 연결과 관련 된 문에 대해 **sqlexecute** 를 호출할 수 있습니다.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR 또는 SQL_CURSOR_COMMIT_BEHAVIOR 값이 SQL_CB_PRESERVE와 같은 경우 **Sqlendtran** 은 연결과 관련 된 열린 커서에 영향을 주지 않습니다. **Sqlendtran**을 호출 하기 전에 커서가 가리키는 행에 커서가 남아 있습니다.  
  
 트랜잭션을 지 원하는 드라이버 및 데이터 원본의 경우 트랜잭션이 활성 상태가 아닌 경우 SQL_COMMIT 또는 SQL_ROLLBACK를 사용 하 여 **Sqlendtran** 을 호출 하면 SQL_SUCCESS (커밋되거나 롤백될 수 없음)가 반환 되 고에는 영향을 주지 않습니다. 데이터 원본입니다.  
  
 드라이버가 자동 커밋 모드인 경우 드라이버 관리자는 드라이버에서 **Sqlendtran** 을 호출 하지 않습니다. **Sqlendtran** 은 SQL_COMMIT 또는 *SQL_ROLLBACK의 SQL_SUCCESS* 를 사용 하 여 호출 되었는지 여부에 관계 없이 항상를 반환 합니다.  
  
 트랜잭션을 지원 하지 않는 드라이버 또는 데이터 원본 (**SQLGetInfo** *옵션* SQL_TXN_CAPABLE is SQL_TC_NONE)은 효과적으로 항상 자동 커밋 모드에 있으므로 항상 **SQLENDTRAN** 에 대해 SQL_SUCCESS를 반환 합니다. SQL_COMMIT 또는 SQL_ROLLBACK의 *형식* 으로 호출 됩니다. 이러한 드라이버 및 데이터 원본은 실제로 트랜잭션을 롤백하지 않습니다.  
  
## <a name="suspended-state"></a>일시 중단 상태  
 Windows 7 이전에 릴리스된 드라이버 관리자의 경우 **Sqlendtran** 이 드라이버에서 SQL_ERROR를 반환 하면 트랜잭션이 활성 상태입니다. 그러나 서버에서 트랜잭션이 성공적으로 커밋될 수 있지만 네트워크 오류가 발생 했기 때문에 클라이언트의 드라이버에 대 한 알림이 제공 되지 않았습니다. 이렇게 하면 연결이 잘못 된 상태로 유지 됩니다. Windows 7부터 **Sqlendtran** 이 SQL_ERROR를 반환 하는 경우 연결이 일시 중단 된 상태일 수 있습니다. 일시 중단 된 상태에서 읽기 전용 함수를 호출할 수 있습니다. 결국 응용 프로그램은 일시 중단 된 연결에서 **Sqldisconnect** 를 호출 하 여 리소스를 해제 해야 합니다.  
  
 다음 조건에 모두 해당 하는 경우 연결이 일시 중단 됨 상태로 전환 됩니다.  
  
-   이 드라이버는 **Sqlendtran**에서 SQL_ERROR를 반환 합니다.  
  
-   드라이버가 ODBC 버전 3.8 이상입니다.  
  
-   응용 프로그램 버전이 3.8 이상입니다. 또는 다시 컴파일된 ODBC 2.x 또는 3(sp3) 응용 프로그램에서 **Sqlendtran**을 통해 **sqlendtran** 함수를 취소 했습니다.  
  
-   드라이버가 다음 메시지 중 하나를 반환 하지 않았으므로 트랜잭션이 완료 되지 않았는지 확인 합니다.  
  
    -   25S03: 트랜잭션을 롤백합니다.  
  
    -   40001: Serialization 오류  
  
    -   40002: 무결성 제약 조건  
  
    -   HYC00: 선택적 기능이 구현 되지 않음  
  
 환경 핸들에 대해 **Sqlendtran** 을 호출 하 고 해당 연결 중 하나가 위의 조건을 충족 하는 경우 동일한 드라이버에 연결 하는 모든 연결은 일시 중단 됨 상태로 전환 됩니다.  
  
 응용 프로그램이 일시 중단 된 연결에서 **Sqldisconnect** 를 호출한 후에는 연결을 사용 하 여 다른 데이터 원본 또는 동일한 데이터 원본에 다시 연결할 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|연결 핸들에서 비동기적으로 실행 되는 함수를 취소 합니다.|[SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|드라이버 또는 데이터 원본에 대 한 정보 반환|[SQLGetInfo 함수](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|핸들 해제|[SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|문 핸들 해제|[SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [비동기 실행(폴링 메서드)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
