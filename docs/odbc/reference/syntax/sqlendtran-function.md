---
title: SQLEndTran 함수 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cce7792e52fce4984f3da41e11d79c34b6b79e53
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302744"
---
# <a name="sqlendtran-function"></a>SQLEndTran 함수(SQLEndTran Function)
**규칙**  
 버전 출시: ODBC 3.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLEndTran연결과** 관련된 모든 명령문에 대한 모든 활성 작업에 대해 커밋 또는 롤백 작업을 요청합니다. **SQLEndTran은** 환경과 연결된 모든 연결에 대해 커밋 또는 롤백 작업을 수행해 달라고 요청할 수도 있습니다.  
  
> [!NOTE]  
>  드라이버 관리자가 이 함수를 ODBC 3에 매핑하는 기능에 대한 자세한 내용을 참조하십시오. *x* 응용 프로그램이 ODBC 2로 작동합니다. *x* 드라이버, [응용 프로그램의 이전 버전과의 호환성에 대한 매핑 교체 함수를](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 [입력] 형식 식별자를 처리합니다. *SQL_HANDLE_ENV(핸들이* 환경 핸들인 경우) 또는 *SQL_HANDLE_DBC(핸들이* 연결 핸들인 경우)이 포함됩니다.  
  
 *Handle*  
 [입력] 트랜잭션 범위를 나타내는 *HandleType으로*표시된 형식의 핸들입니다. 자세한 내용은 "주석"을 참조하십시오.  
  
 *완료 유형*  
 [입력] 다음 두 값 중 하나:  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE 또는 SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>진단  
 **SQLEndTranSQL_ERROR** 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 적절한 *핸들 유형* 및 *핸들을*사용 하 여 **SQLGetDiagRec를** 호출 하 여 관련 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 **SQLEndTran에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08003|연결이 열려 있지 않음|(DM) *핸들 유형이* SQL_HANDLE_DBC *핸들이* 연결된 상태가 아닙니다.|  
|08007|트랜잭션 중 연결 오류|*핸들 유형이* SQL_HANDLE_DBC 함수를 실행하는 동안 *핸들과* 연결된 연결이 실패했으며, 요청된 **COMMIT** 또는 **ROLLBACK이** 실패하기 전에 발생했는지 여부를 확인할 수 없습니다.|  
|25S01|트랜잭션 상태를 알 수 없음|*핸들의* 하나 이상의 연결이 지정된 결과로 트랜잭션을 완료하지 못했으며 결과를 알 수 없습니다.|  
|25S02|트랜잭션이 여전히 활성 상태|드라이버는 글로벌 트랜잭션의 모든 작업을 원자적으로 완료할 수 있으며 트랜잭션이 여전히 활성 상태임을 보장할 수 없습니다.|  
|25S03|트랜잭션이 롤백됩니다.|드라이버는 글로벌 트랜잭션의 모든 작업을 원자적으로 완료할 수 있다고 보장할 수 없으며 *Handle에서* 활성 트랜잭션의 모든 작업이 롤백되었습니다.|  
|40001|직렬화 실패|다른 트랜잭션이 있는 리소스 교착 상태로 인해 트랜잭션이 롤백되었습니다.|  
|40002|무결성 제약 조건 위반|*CompletionType이* SQL_COMMIT 변경 약속으로 인해 무결성 제약 조건 위반이 발생했습니다. 결과적으로 트랜잭션이 롤백되었습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. szMessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류및 그 원인을 설명합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*연결 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 [SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md) 실행이 완료되기 전에 *ConnectionHandle*에서 호출되었습니다. 그런 다음 *연결이*핸들 에서 함수를 다시 호출했습니다.<br /><br /> 함수가 호출되었고 **SQLCancelHandle** 실행이 완료되기 전에 다중 스레드 응용 프로그램의 다른 스레드에서 *ConnectionHandle에서* 호출되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) 비동기적으로 실행 되는 *함수는 연결 핸들과* 관련 된 문 핸들에 대 한 호출 하 고 **SQLEndTran** 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *연결 핸들에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *연결 핸들과* 연결된 명령문 핸들을 호출하고 반환 된 SQL_NEED_DATA. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 SQL_HANDLE_DBC *핸들에* 대 *Handle* 한 호출 되 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults** *핸들과* 연결된 문 핸들 중 하나를 호출하고 반환 된 SQL_PARAM_DATA_AVAILABLE. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.|  
|HY012|잘못된 트랜잭션 작업 코드|(DM) *인수 CompletionType에* 대해 지정된 값이 SQL_COMMIT SQL_ROLLBACK 않았습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY092|잘못된 특성/옵션 식별자|(DM) *인수 HandleType에* 대해 지정된 값은 SQL_HANDLE_ENV SQL_HANDLE_DBC 않았습니다.|  
|HY15|SQLEndTran비동기 함수 실행이 활성화된 연결이 포함된 환경에서는 SQLEndTran이 허용되지 않습니다.|(DM) *핸들 타이는* 환경에서 연결 에 대 한 연결 함수의 비동기 실행이 사용 가능한 경우 SQL_HANDLE_ENV 설정할 수 없습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은이 항목의 코멘트 섹션을 참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|드라이버 또는 데이터 원본은 **ROLLBACK** 작업을 지원하지 않습니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *연결 핸들과* 연결된 드라이버가 기능을 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
 ODBC 3. *x* 드라이버, *핸들 유형이* SQL_HANDLE_ENV *핸들이* 유효한 환경 핸들인 경우 드라이버 관리자는 환경과 연결된 각 드라이버에서 **SQLEndTran을** 호출합니다. 드라이버 호출에 대한 *핸들* 인수는 드라이버의 환경 핸들이 됩니다. ODBC 2. *x* 드라이버, *handleTypeSQL_HANDLE_ENV* *핸들* 은 유효한 환경 핸들 이며 해당 환경에서 연결 된 상태에 여러 연결, 다음 드라이버 관리자는 해당 환경에서 연결 된 상태에서 각 연결에 대 한 드라이버에서 **SQLTransact를** 호출 합니다. 각 호출의 *핸들* 인수는 연결의 핸들이 됩니다. 두 경우 모두 드라이버는 해당 환경에서 연결된 상태에 있는 모든 연결에서 *CompletionType*의 값에 따라 트랜잭션을 커밋하거나 롤백하려고 시도합니다. 활성 상태가 아닌 연결은 트랜잭션에 영향을 주지 않습니다.  
  
> [!NOTE]  
>  **SQLEndTran은** 공유 환경에서 트랜잭션을 커밋하거나 롤백하는 데 사용할 수 없습니다. SQLSTATE HY092(잘못된 특성/옵션 식별자)는 **SQLEndTran이** 공유 환경의 핸들 또는 공유 환경의 연결 핸들로 *핸들* 을 설정하여 호출되는 경우 반환됩니다.  
  
 드라이버 관리자는 각 연결에 대해 SQL_SUCCESS 받는 경우에만 SQL_SUCCESS 반환합니다. 드라이버 관리자가 하나 이상의 연결에서 SQL_ERROR 받는 경우 응용 프로그램에 SQL_ERROR 반환하고 진단 정보가 환경의 진단 데이터 구조에 배치됩니다. 커밋 또는 롤백 작업 중에 실패한 연결 또는 연결을 확인하려면 응용 프로그램에서 각 연결에 대해 **SQLGetDiagRec를** 호출할 수 있습니다.  
  
> [!NOTE]  
>  드라이버 관리자는 모든 연결에서 전역 트랜잭션을 시뮬레이션하지 않으므로 2단계 커밋 프로토콜을 사용하지 않습니다.  
  
 *CompletionType이* SQL_COMMIT 경우 **SQLEndTran은** 영향을 받는 연결과 연결된 모든 명령문에 대한 모든 활성 작업에 대한 커밋 요청을 발행합니다. *CompletionType이* SQL_ROLLBACK **경우 SQLEndTran은** 영향을 받는 연결과 연결된 모든 명령문에 대한 모든 활성 작업에 대한 롤백 요청을 발행합니다. 활성 트랜잭션이 없는 경우 **SQLEndTran은** 데이터 원본에 영향을 주지 않고 SQL_SUCCESS 반환합니다. 자세한 내용은 [트랜잭션 커밋 및 롤백](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md)을 참조하십시오.  
  
 드라이버가 수동 커밋 **모드(sqlSetConnectAttr에** SQL_AUTOCOMMIT_OFF 설정된 SQL_ATTR_AUTOCOMMIT 특성을 호출하여) 트랜잭션 내에 포함될 수 있는 SQL 문이 현재 데이터 원본에 대해 실행될 때 새 트랜잭션이 암시적으로 시작됩니다. 자세한 내용은 [커밋 모드를](../../../odbc/reference/develop-app/commit-mode.md)참조하십시오.  
  
 트랜잭션 작업이 커서에 미치는 영향을 확인하기 위해 응용 프로그램은 SQL_CURSOR_ROLLBACK_BEHAVIOR 및 SQL_CURSOR_COMMIT_BEHAVIOR 옵션을 사용하여 **SQLGetInfo를** 호출합니다. 자세한 내용은 다음 단락을 참조하고 [커서 및 준비된 명령문에 대한 트랜잭션의 효과를](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)참조하십시오.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR 또는 SQL_CURSOR_COMMIT_BEHAVIOR 값이 SQL_CB_DELETE 같으면 **SQLEndTran은** 연결과 연결된 모든 문에서 열려 있는 모든 커서를 닫고 삭제하고 보류 중인 모든 결과를 삭제합니다. **SQLEndTran은** 할당된(준비되지 않은) 상태에 있는 모든 문을 남깁니다. 응용 프로그램은 후속 SQL 요청에 다시 사용할 수 있으며 핸들 *유형* SQL_HANDLE_STMT **사용하여 SQLFreeStmt** 또는 **SQLFreeHandle을** 호출하여 할당 해제할 수 있습니다.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR 값 또는 SQL_CURSOR_COMMIT_BEHAVIOR 값이 SQL_CB_CLOSE 같으면 **SQLEndTran은** 연결과 연결된 모든 문에서 열린 모든 커서를 닫습니다. **SQLEndTran은** 준비된 상태로 있는 모든 문을 남깁니다. 응용 프로그램은 **SQLPrepare를**먼저 호출하지 않고 연결과 연결된 문에 대해 **SQLExecute를** 호출할 수 있습니다.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR 값 또는 SQL_CURSOR_COMMIT_BEHAVIOR 값이 SQL_CB_PRESERVE 같으면 **SQLEndTran은** 연결과 연결된 열린 커서에 영향을 주지 않습니다. **커서는 SQLEndTran을**호출하기 전에 가리키는 행에 남아 있습니다.  
  
 트랜잭션을 지원하는 드라이버 및 데이터 원본의 경우 트랜잭션이 활성 반환SQL_SUCCESS 없을 때 SQL_COMMIT 또는 SQL_ROLLBACK **SQLEndTran을** 호출하고(커밋되거나 롤백할 작업이 없음을 표시) 데이터 원본에 영향을 미치지 않습니다.  
  
 드라이버가 자동 커밋 모드에 있으면 드라이버 관리자는 드라이버에서 **SQLEndTran을** 호출하지 않습니다. **SQLEndTran은** SQL_COMMIT SQL_ROLLBACK *완료 유형으로* 호출되는지 여부에 관계없이 항상 SQL_SUCCESS 반환합니다.  
  
 트랜잭션을 지원하지 않는 드라이버 또는 데이터**원본(SQLGetInfo** *옵션* SQL_TXN_CAPABLE SQL_TC_NONE)은 항상 자동 커밋 모드에 있으므로 SQL_COMMIT 또는 SQL_ROLLBACK *CompletionType으로* 호출되는지 여부에 관계없이 **항상 SQLEndTran에** 대한 SQL_SUCCESS 반환합니다. 이러한 드라이버및데이터원본은 요청시 실제로 트랜잭션을 롤백하지 않습니다.  
  
## <a name="suspended-state"></a>일시 중단된 상태  
 Windows 7 이전에 릴리스된 드라이버 관리자에서 **SQLEndTran이** 드라이버에서 SQL_ERROR 반환하면 트랜잭션이 활성화되었습니다. 그러나 트랜잭션이 서버에서 성공적으로 커밋되었지만 클라이언트의 드라이버에 대한 알림(예: 네트워크 오류가 발생했기 때문에)이 확인되지 않았을 수 있습니다. 이렇게 하면 연결이 잘못된 상태로 남게 됩니다. **SQLEndTran이** SQL_ERROR 반환할 때 Windows 7부터 연결이 일시 중단된 상태일 수 있습니다. 일시 중단된 상태에서읽기 전용 함수를 호출할 수 있습니다. 결국 응용 프로그램은 해제 리소스에 일시 중단된 연결에서 **SQLDisconnect를** 호출해야 합니다.  
  
 다음 조건이 모두 true이면 연결이 일시 중단된 상태로 전환됩니다.  
  
-   드라이버는 **SQLEndTran에서**SQL_ERROR 반환합니다.  
  
-   드라이버는 ODBC 버전 3.8 이상입니다.  
  
-   응용 프로그램 버전은 3.8 이상입니다. 또는 다시 컴파일된 ODBC 2.x 또는 3.x 응용 프로그램은 **SQLCancelHandle**을 통해 **SQLEndTran** 함수를 성공적으로 취소합니다.  
  
-   드라이버가 트랜잭션이 완료되지 않았음을 확인하는 다음 메시지 중 하나를 반환하지 않았습니다.  
  
    -   25S03: 트랜잭션이 롤백됩니다.  
  
    -   40001: 직렬화 실패  
  
    -   40002: 무결성 제약 조건  
  
    -   HYC00: 선택적 기능이 구현되지 않음  
  
 **SQLEndTran환경** 핸들에서 호출되고 해당 연결 중 하나가 위의 조건을 충족하는 경우 동일한 드라이버에 연결하는 모든 연결이 일시 중단된 상태로 전환됩니다.  
  
 응용 프로그램이 일시 중단된 연결에서 **SQLDisconnect를** 호출한 후 연결을 사용하여 다른 데이터 원본 또는 동일한 데이터 원본에 다시 연결할 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|연결 핸들에서 비동기적으로 실행되는 함수를 취소합니다.|[SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|드라이버 또는 데이터 원본에 대한 정보 반환|[SQLGetInfo 함수](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|손잡이 해제|[SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|명령문 핸들 해제|[SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [비동기 실행(폴링 메서드)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
