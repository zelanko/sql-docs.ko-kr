---
title: 문 전환 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transitioning states [ODBC], statement
- state transitions [ODBC], statement
- statement transitions [ODBC]
ms.assetid: 3d70e0e3-fe83-4b4d-beac-42c82495a05b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55f82e275bfd5bff12544b35a1370cdb31495320
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302854"
---
# <a name="statement-transitions"></a>명령문 전환
ODBC 문에는 다음과 같은 상태가 있습니다.  
  
|시스템 상태|설명|  
|-----------|-----------------|  
|S0|할당되지 않은 명령문입니다. 연결 상태는 C4, C5 또는 C6이어야 합니다. 자세한 내용은 [연결 전환을](../../../odbc/reference/appendixes/connection-transitions.md)참조하십시오.)|  
|S1|할당된 명령문입니다.|  
|S2|준비된 진술. 결과 집합이 생성되지 않습니다.|  
|S3|준비된 진술. (비어 있을 수 있는) 결과 집합이 만들어집니다.|  
|S4|문이 실행되고 결과 집합이 생성되지 않았습니다.|  
|S5|문이 실행되고 (비어 있을 수 있는) 결과 집합이 만들어졌습니다. 커서는 결과 집합의 첫 번째 행 앞에 열리고 배치됩니다.|  
|S6|**커서는 SQLFetch** 또는 **SQLFetch스크롤로**배치됩니다.|  
|S7|**SQLExtendedFetch.**|  
|S8|함수에는 데이터가 필요합니다. **SQLParamData가** 호출되지 않았습니다.|  
|S9|함수에는 데이터가 필요합니다. **SQLPutData가** 호출되지 않았습니다.|  
|S10|함수에는 데이터가 필요합니다. **SQLPutData가** 호출되었습니다.|  
|S11|여전히 실행 중입니다. 비동기적으로 실행되는 함수가 SQL_STILL_EXECUTING 반환한 후에 문이 이 상태로 남아 있습니다. 명령문 핸들을 허용하는 함수가 실행되는 동안 문이 일시적으로 이 상태에 있습니다. 상태 S11의 임시 거주는 **SQLCancel에**대한 상태 테이블을 제외한 모든 상태 테이블에 표시되지 않습니다. 명령문이 일시적으로 상태 S11에 있는 동안 다른 스레드에서 **SQLCancel을** 호출하여 함수를 취소할 수 있습니다.|  
|S12|비동기 실행이 취소되었습니다. S12에서 응용 프로그램은 SQL_STILL_EXECUTING 이외의 값을 반환할 때까지 취소된 함수를 호출해야 합니다. 함수가 SQL_ERROR 및 SQLSTATE HY008(작업이 취소)을 반환하는 경우에만 함수가 성공적으로 취소되었습니다. SQL_SUCCESS 같은 다른 값을 반환하면 취소 작업이 실패하고 함수가 정상적으로 실행됩니다.|  
  
 상태 S2 및 S3는 준비된 상태로 알려져 있으며, S5에서 S7을 커서 상태로, S8에서 S10을 필요로 하는 데이터 상태로 상태하고, S11 및 S12를 비동기 상태로 명시합니다. 이러한 각 그룹에서 전환은 그룹의 각 상태에 대해 서로 다른 경우에만 별도로 표시됩니다. 대부분의 경우 각 그룹의 각 상태에 대한 전환은 동일합니다.  
  
 다음 표는 각 ODBC 함수가 문 상태에 미치는 영향을 보여 줍니다.  
  
## <a name="sqlallochandle"></a>SQLAlloc핸들  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1], [5], [6]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[2], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|S1[3]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[4], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
  
 [1] 이 행은 *핸들타입이* SQL_HANDLE_ENV 때의 전환을 보여 주었습니다.  
  
 [2] 이 행은 *핸들타입이* SQL_HANDLE_DBC 때의 전환을 보여 주었습니다.  
  
 [3] 이 행은 *핸들타입이* SQL_HANDLE_STMT 때의 전환을 보여 주었습니다.  
  
 [4] 이 행은 *핸들타이가* SQL_HANDLE_DESC 때의 전환을 보여줍니다.  
  
 [5] *OutputHandlePtr을* 사용하여 **SQLAllocHandle을** 호출하면 해당 핸들에 대한 이전 내용에 관계없이 핸들을 처리하는 유효한 핸들 덮어쓰기를 가리키며 ODBC 드라이버에 문제가 발생할 수 있습니다. SQLFreeHandle을 호출하지 않고 * \*OutputHandlePtr에* 대해 정의된 동일한 응용 프로그램 변수로 **SQLAllocHandle을** 두 번 호출하는 것은 잘못된 ODBC 응용 프로그램 프로그래밍입니다. **SQLFreeHandle** 이러한 방식으로 ODBC 핸들을 덮어쓰면 ODBC 드라이버부분에서 일관되지 않은 동작이나 오류가 발생할 수 있습니다.  
  
## <a name="sqlbindcol"></a>SQLBindCol  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbindparameter"></a>SQLBindParameter  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbrowseconnect-sqlconnect-and-sqldriverconnect"></a>SQL브라우지커넥트, SQL드라이버커넥트  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|08002|08002|08002|08002|08002|08002|08002|  
  
## <a name="sqlbulkoperations"></a>SQLBulk운영  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24000|다음 표 보기|HY010|NS [c] HY010 o|  
  
## <a name="sqlbulkoperations-cursor-states"></a>SQLBulk연산 (커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetch스크롤|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|-- [s] S8 [d] S11 [x]|-- [s] S8 [d] S11 [x]|HY010|  
  
## <a name="sqlcancel"></a>SQLCancel  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|S1[1] S2[nr]와 [2] S3[r]와 [2] S5[3] 및 [5] S6([3] 또는 [4]) 및 [6] S7[4] 및 [7]|다음 표 보기|  
  
 [1] **SQLExecDirect가** SQL_NEED_DATA 반환했습니다.  
  
 [2] **SQLExecute가** SQL_NEED_DATA 반환했습니다.  
  
 [3] **SQLBulkOperationsSQL_NEED_DATA** 반환되었습니다.  
  
 [4] **SQLSetPos는** SQL_NEED_DATA 반환했습니다.  
  
 [5] **SQLFetch,** **SQLFetch스크롤**또는 **SQLExtendedFetch가** 호출되지 않았습니다.  
  
 [6] **SQLFetch** 또는 **SQLFetchScroll가** 호출되었습니다.  
  
 [7] **SQLExtendedFetch가** 호출되었습니다.  
  
## <a name="sqlcancel-asynchronous-states"></a>SQLCancel(비동기 상태)  
  
|S11<br /><br /> 여전히 실행 중|S12<br /><br /> 아친치 취소|  
|-----------------------------|-----------------------------|  
|NS[1] S12[2]|S12|  
  
 [1] 함수가 실행되는 동안 명령문이 일시적으로 상태 S11에 있었습니다. **SQLCancel은** 다른 스레드에서 호출되었습니다.  
  
 [2] 비동기라고 하는 함수가 SQL_STILL_EXECUTING 반환되었기 때문에 명령문이 S11 상태입니다.  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|24000|24000|24000|S1[np] S3[p]|HY010|HY010|  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|다음 표 보기|24000|-- [s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqlcolattribute-prepared-states"></a>SQLColAttribute(준비된 상태)  
  
|S2<br /><br /> 결과 없음|S3<br /><br /> 결과|  
|-----------------------|--------------------|  
|--[1] 07005[2]|-- [s] S11 x|  
  
 [1] *필드식별자가* SQL_DESC_COUNT.  
  
 [2] *필드식별자가* SQL_DESC_COUNT 않았습니다.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumn특전, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimary키, SQL프로시저열, SQL프로시저, SQL스페셜열, SQLStatistics, SQLStatistics, SQLTablePrivileges 및 SQLTableTable  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S5[s] S11[x]|S1[e] S5[s] S11[x]|S1[e]와 [1] S5[s] 및 [1] S11[x] 및 [1] 24000[2]|다음 표 보기|HY010|NS [c] HY010 o|  
  
 [1] 현재 결과는 마지막 또는 유일한 결과이거나 현재 결과가 없습니다. 여러 결과에 대한 자세한 내용은 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)를 참조하십시오.  
  
 [2] 현재 결과는 마지막 결과가 아닙니다.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables-cursor-states"></a>SQLColumn권한, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimary키, SQL프로시저열, SQL프로시저, SQL특수열, SQLStatistics, SQLTablePrivileges 및 SQLTable 권한 대(커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetch스크롤|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000[1]|24000|  
  
 [1] **SQLFetch** 또는 **SQLFetchScroll가** SQL_NO_DATA 반환되지 않고 **SQLFetch** 또는 **SQLFetchScroll가** SQL_NO_DATA 반환된 경우 드라이버 관리자가 이 오류를 반환합니다.  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH[1]|--|--|--|--|HY010|NS [c] 및 [3] HY010 [o] 또는 [4]|  
|IH[2]|HY010|다음 표 보기|24000|-- [s] S11 x|HY010|NS [c] 및 [3] HY010 [o] 또는 [4]|  
  
 [1] 이 행은 *SourceDescHandle* 인수가 ARD, APD 또는 IPD일 때의 전환을 보여 주었습니다.  
  
 [2] 이 행은 *SourceDescHandle* 인수가 IRD였을 때의 전환을 보여 주었습니다.  
  
 [3] *SourceDescHandle* 및 *TargetDescHandle* 인수는 비동기적으로 실행중인 **SQLCopyDesc** 함수에서와 동일합니다.  
  
 [4] *SourceDescHandle* 인수 또는 *TargetDescHandle* 인수(또는 둘 다)는 비동기적으로 실행중인 **SQLCopyDesc** 함수와 다릅니다.  
  
## <a name="sqlcopydesc-prepared-states"></a>SQLCopyDesc (준비된 상태)  
  
|S2<br /><br /> 결과 없음|S3<br /><br /> 결과|  
|-----------------------|--------------------|  
|24000[1]|-- [s] S11 [x]|  
  
 [1] 이 행은 *SourceDescHandle* 인수가 IRD였을 때의 전환을 보여 주며, 이 행은 전환을 보여 주며,  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSource 및 SQL드라이버  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqldescribecol"></a>SQLDescribeCol  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|다음 표 보기|24000|-- [s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqldescribecol-prepared-states"></a>SQLDescribeCol (준비된 상태)  
  
|S2<br /><br /> 결과 없음|S3<br /><br /> 결과|  
|-----------------------|--------------------|  
|07005|-- [s] S11 [x]|  
  
## <a name="sqldescribeparam"></a>SQLDescribeParam  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|-- [s] S11 [x]|HY010|HY010|HY010|NS [c] HY010 [o]|  
  
## <a name="sqldisconnect"></a>SQL분리  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|S0[1]|S0[1]|S0[1]|S0[1]|(HY010)|(HY010)|  
  
 [1] **SQLDisconnect를** 호출하여 연결과 관련된 모든 문을 해제합니다. 또한 연결 상태를 C2로 반환합니다. 연결 상태는 명령문 상태가 S0이되기 전에 C4여야 합니다.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|-[2] 또는 [3] S1[1]|--[3] S1[np] 및 ([1] 또는 [2]) S1[p]와 [1] S2[p] 및 [2]|--[3] S1[np] 및 ([1] 또는 [2]) S1[p]와 [1] S3[p] 및 [2]|(HY010)|(HY010)|  
  
 [1] *CompletionType* 인수가 SQL_COMMIT **SQLGetInfo는** SQL_CURSOR_COMMIT_BEHAVIOR 정보 형식에 대한 SQL_CB_DELETE 반환하거나 *CompleteType* 인수가 SQL_ROLLBACK **SQLGetInfo는** SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 형식에 대한 SQL_CB_DELETE 반환합니다.  
  
 [2] *CompletionType* 인수가 SQL_COMMIT **SQLGetInfo는** SQL_CURSOR_COMMIT_BEHAVIOR 정보 형식에 대한 SQL_CB_CLOSE 반환하거나 *CompleteType* 인수가 SQL_ROLLBACK **SQLGetInfo는** SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 형식에 대한 SQL_CB_CLOSE 반환합니다.  
  
 [3] *CompletionType* 인수가 SQL_COMMIT **SQLGetInfo는** SQL_CURSOR_COMMIT_BEHAVIOR 정보 형식에 대한 SQL_CB_PRESERVE 반환하거나 *CompleteType* 인수가 SQL_ROLLBACK **SQLGetInfo는** SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 형식에 대해 SQL_CB_PRESERVE 반환합니다.  
  
## <a name="sqlexecdirect"></a>SQLExecDirect  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S4[s] 및 [nr] S5[s] 및 [r] S8[d] S11[x]|-- [e] 및 [1] S1 [e] 및 [2] S4 [s] 및 [nr] S5 [s] 및 [r] S8 [d] S11 [x]|-- [e], [1], [3] S1 [e], [2], [3] S4 [s], [nr], [3] S5 [s], [r], [3] S8 [d]와 [3] S11 [x] 및 [3] 24000 [4]|다음 표 보기|HY010|NS [c] HY010 [o]|  
  
 [1] 드라이버 관리자가 오류를 반환했습니다.  
  
 [2] 드라이버 관리자가 오류를 반환하지 않았습니다.  
  
 [3] 현재 결과는 마지막 또는 유일한 결과이거나 현재 결과가 없습니다. 여러 결과에 대한 자세한 내용은 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)를 참조하십시오.  
  
 [4] 현재 결과는 마지막 결과가 아닙니다.  
  
## <a name="sqlexecdirect-cursor-states"></a>SQLExecDirect (커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetch스크롤|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000 [1]|24000|  
  
 [1] **SQLFetch** 또는 **SQLFetchScroll가** SQL_NO_DATA 반환되지 않은 경우 드라이버 관리자가 이 오류를 반환하고 **SQLFetch** 또는 **SQLFetchScroll가** SQL_NO_DATA 반환한 경우 드라이버에서 반환됩니다.  
  
## <a name="sqlexecute"></a>SQLExecute  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|다음 표 보기|S2 [e], p, [1] S4 [s], [p], [nr], [1] S5 [s], [p], [r], [1] S8 [d], [p], [1] S11 [p], [p], [1] 24000 [p]와 [2] HY0010 [np]|커서 상태 테이블 참조|HY010|NS [c] HY010 [o]|  
  
 [1] 현재 결과는 마지막 또는 유일한 결과이거나 현재 결과가 없습니다. 여러 결과에 대한 자세한 내용은 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)를 참조하십시오.  
  
 [2] 현재 결과는 마지막 결과가 아닙니다.  
  
## <a name="sqlexecute-prepared-states"></a>SQL실행(준비된 상태)  
  
|S2<br /><br /> 결과 없음|S3<br /><br /> 결과|  
|-----------------------|--------------------|  
|S4[s] S8[d] S11[x]|S5[s] S8[d] S11[x]|  
  
## <a name="sqlexecute-cursor-states"></a>SQL실행(커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetch스크롤|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000 [p] HY010 [np]|24000 [p], [1] HY010 [np]|24000 [p] HY010 [np]|  
  
 [1] **SQLFetch** 또는 **SQLFetchScroll가** SQL_NO_DATA 반환되지 않은 경우 드라이버 관리자가 이 오류를 반환하고 **SQLFetch** 또는 **SQLFetchScroll가** SQL_NO_DATA 반환한 경우 드라이버에서 반환됩니다.  
  
## <a name="sqlextendedfetch"></a>SQLExtendedFetch  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|S1010|S1010|24000|다음 표 보기|S1010|NS [c] S1010 [o]|  
  
## <a name="sqlextendedfetch-cursor-states"></a>SQLExtendedFetch(커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetch스크롤|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S7[s] 또는 [nf] S11[x]|S1010|-- [s] 또는 [nf] S11 [x]|  
  
## <a name="sqlfetch-and-sqlfetchscroll"></a>SQLFetch 및 SQLFetch스크롤  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24000|다음 표 보기|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlfetch-and-sqlfetchscroll-cursor-states"></a>SQLFetch 및 SQLFetch스크롤(커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetch스크롤|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S6[s] 또는 [nf] S11[x]|-- [s] 또는 [nf] S11 [x]|HY010|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|-- [1]|HY010|HY010|HY010|HY010|HY010|HY010|  
|IH [2]|S0|S0|S0|S0|HY010|HY010|  
|-- [3]|--|--|--|--|--|--|  
  
 [1] 이 행은 *HandleType이* SQL_HANDLE_ENV 또는 SQL_HANDLE_DBC 때의 전환을 보여 SQL_HANDLE_DBC.  
  
 [2] 이 행은 *핸들타입이* SQL_HANDLE_STMT 때의 전환을 보여 주었습니다.  
  
 [3] 이 행은 *HandleType이* SQL_HANDLE_DESC 설명자가 명시적으로 할당되었을 때의 전환을 보여 주었습니다.  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|S1[np] S2[p]|S1[np] S3[p]|HY010|HY010|  
|IH [2]|--|--|--|--|HY010|HY010|  
  
 [1] 이 행은 *옵션이* SQL_CLOSE 때의 전환을 보여 주었습니다.  
  
 [2] 이 행은 *옵션이* SQL_UNBIND 또는 SQL_RESET_PARAMS 때의 전환을 보여. *옵션* 인수가 SQL_DROP 기본 드라이버가 ODBC 3 *.x* 드라이버인 경우 드라이버 관리자는 *핸들 유형이* SQL_HANDLE_STMT 설정된 **SQLFreeHandle** 호출에 이 드라이버를 매핑합니다. 자세한 내용은 [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)의 전환 테이블을 참조하십시오.  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetcursorname"></a>SQLGetCursorName  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|HY010|HY010|  
  
## <a name="sqlgetdata"></a>SQLGetData  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24000|다음 표 보기|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlgetdata-cursor-states"></a>SQLGetData (커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetch스크롤|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-- [s] 또는 [nf] S11 [x] 24000 [b] HY109 [i]|-- [s] 또는 [nf] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDesc필드 및 SQLGetDescRec  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|-- [1] 또는 [2] HY010 [3]|다음 표 보기|-- [1] 또는 [2] 24000 [3]|-- [1], [2], 또는 [3] S11 [3] 및 [x]|HY010|NS [c] 또는 [4] HY010 [o] 및 [5]|  
  
 [1] *설명자 핸들* 인수는 APD 또는 ARD입니다.  
  
 [2] *설명자 핸들* 인수는 IPD입니다.  
  
 [3] *설명자 핸들* 인수는 IRD였습니다.  
  
 [4] *설명자 핸들* 인수는 비동기적으로 실행중인 **SQLGetDescField** 또는 **SQLGetDescRec** 함수의 *설명자 핸들* 인수와 동일합니다.  
  
 [5] *설명자 핸들* 인수는 비동기적으로 실행중인 **SQLGetDescField** 또는 **SQLGetDescRec** 함수의 *설명자 핸들* 인수와 다릅니다.  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec-prepared-states"></a>SQLGetDesc필드 및 SQLGetDescRec (준비된 상태)  
  
|S2<br /><br /> 결과 없음|S3<br /><br /> 결과|  
|-----------------------|--------------------|  
|-[1], [2], [3] S11[2] 및 [x]|-[1], [2], 또는 [3] S11 [x]|  
  
 [1] *설명자 핸들* 인수는 APD 또는 ARD입니다.  
  
 [2] *설명자 핸들* 인수는 IPD입니다.  
  
 [3] *설명자 핸들* 인수는 IRD였습니다. 이러한 함수는 *설명자 핸들이* IRD인 경우 항상 상태 S2에서 SQL_NO_DATA 반환합니다.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiag필드 및 SQLGetDiagRec  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--|--|--|  
|IH[2]|--[3]|--[3]|--|--|--[3]|--[3]|  
  
 [1] 이 행은 *HandleType이* SQL_HANDLE_ENV, SQL_HANDLE_DBC 또는 SQL_HANDLE_DESC 때의 전환을 보여.  
  
 [2] 이 행은 *핸들타입이* SQL_HANDLE_STMT 때의 전환을 보여 주었습니다.  
  
 [3] **SQLGetDiagField는** *DiagIdentifier가* SQL_DIAG_ROW_COUNT 때 항상 이 상태에서 오류를 반환합니다.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--[1] 24000[2]|--[1] 24000[2]|--[1] 24000[2]|다음 표 보기|HY010|HY010|  
  
 [1] 문 특성이 SQL_ATTR_ROW_NUMBER 않았습니다.  
  
 [2] 문 특성이 SQL_ATTR_ROW_NUMBER.  
  
## <a name="sqlgetstmtattr-cursor-states"></a>SQLGetStmtAttr (커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetch스크롤|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[1] 24000[2]|--[1] 또는 ([v] 및 [2]) 24000 [b] 및 [2] HY109 [i] 및 [2]|-- [i] 또는 [[v] 및 [2]24000 [b] 및 [2] HY109[1] 및 [2]|  
  
 [1] *특성* 인수가 SQL_ATTR_ROW_NUMBER 않았습니다.  
  
 [2] *특성* 인수가 SQL_ATTR_ROW_NUMBER.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|--[1]|--[1]|-- [s] 및 [2] S1 [nf], [np], [4] S2 [nf], [p], [4] S5 [s] 및 [3] S11 [x]|S1[nf], [np], [4] S3[nf], [4] S4[s] 및 [2] S5[s]와 [3] S11 [x]|HY010|NS [c] HY010 [o]|  
  
 [1] 함수는 항상 이 상태에서 SQL_NO_DATA 반환합니다.  
  
 [2] 다음 결과는 행 수입니다.  
  
 [3] 다음 결과는 결과 집합입니다.  
  
 [4] 현재 결과는 마지막 결과입니다.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlnumparams"></a>SQLNumParams  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|-- [s] S11 [x]|-- [s] S11 [x]|-- [s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlnumresultcols"></a>SQLNumResultCols  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|-- [s] S11 [x]|-- [s] S11 [x]|-- [s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata"></a>SQLParamData  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|HY010|HY010|다음 표 보기|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata-need-data-states"></a>SQLParamData(데이터 상태 필요)  
  
|S8<br /><br /> 데이터 필요|S9<br /><br /> 넣어야합니다|S10<br /><br /> 넣을 수 있습니다.|  
|----------------------|---------------------|---------------------|  
|S1[e]와 [1] S2[e], [nr], [2] S3 [e], [r], [2] S5 [e] 및 [4] S6 [e] 및 [5] S7 [e] 및 [3] S9 [d] S11 [x]|HY010|S1[e]와 [1] S2[e], [nr], [2] S3[e], [r], [2] S4[s], [nr], [[[1] 또는 [2]] S5[s], [r], [[]] 또는 [2]) S5([s] 또는 [e]) 및 [4] S6(]s] 또는 [e]) 및 [5] S7(들] 또는 [e]] 및 [3]s1[S1]|  
  
 [1] **SQLExecDirect가** SQL_NEED_DATA 반환했습니다.  
  
 [2] **SQLExecute가** SQL_NEED_DATA 반환했습니다.  
  
 [3] **SQLSetPos는** 상태 S7에서 호출하고 SQL_NEED_DATA 반환했다.  
  
 [4] **SQLBulkOperations는** 상태 S5에서 호출하고 SQL_NEED_DATA 반환했다.  
  
 [5] **SQLSetPos** 또는 **SQLBulkOperations는** 상태 S6에서 호출되고 SQL_NEED_DATA 반환되었습니다.  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S2[s] 및 [nr] S3[s] 및 [r] S11[x]|-- [s] 또는 ([e] 및 [1]) S1 [e] 및 [2] S11 [x]|S1[e]와 [3] S2[s], [nr], [3] S3[s], [r], [3] S11[x] 및 [3] 24000[4]|다음 표 보기|HY010|NS [c] HY010 [o]|  
  
 [1] 명령문을 검증하는 것 이외의 이유로 준비에 실패합니다(SQLSTATE는 HY009 [잘못된 인수 값] 또는 HY090 [잘못된 문자열 또는 버퍼 길이]))  
  
 [2] 명령문을 검증하는 동안 준비에 실패합니다(SQLSTATE가 HY009 [잘못된 인수 값] 또는 HY090 [잘못된 문자열 또는 버퍼 길이])가 아니었습니다).  
  
 [3] 현재 결과는 마지막 또는 유일한 결과이거나 현재 결과가 없습니다. 여러 결과에 대한 자세한 내용은 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)를 참조하십시오.  
  
 [4] 현재 결과는 마지막 결과가 아닙니다.  
  
## <a name="sqlprepare-cursor-states"></a>SQL준비(커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetch스크롤|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000|24000|  
  
## <a name="sqlputdata"></a>SQLPutData  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|HY010|HY010|다음 표 보기|NS [c] HY010 [o]|  
  
## <a name="sqlputdata-need-data-states"></a>SQLPutData(데이터 상태 필요)  
  
|S8<br /><br /> 데이터 필요|S9<br /><br /> 넣어야합니다|S10<br /><br /> 넣을 수 있습니다.|  
|----------------------|---------------------|---------------------|  
|HY010|S1[e]와 [1] S2[e], [nr], [2] S3 [e], [r], [2] S5 [e] 및 [4] S6 [e] 및 [5] S7 [e] 및 [3] S10 [s] S11 [x]|-- [s] S1 [e]와 [1] S2 [e], [nr], [2] S3 [e], [r], [2] S5 [e] 및 [4] S6 [e] 및 [5] S7 [e] 및 [3] S11 [x] HY01[6]|  
  
 [1] **SQLExecDirect가** SQL_NEED_DATA 반환했습니다.  
  
 [2] **SQLExecute가** SQL_NEED_DATA 반환했습니다.  
  
 [3] **SQLSetPos는** 상태 S7에서 호출하고 SQL_NEED_DATA 반환했다.  
  
 [4] **SQLBulkOperations는** 상태 S5에서 호출하고 SQL_NEED_DATA 반환했다.  
  
 [5] **SQLSetPos** 또는 **SQLBulkOperations는** 상태 S6에서 호출되고 SQL_NEED_DATA 반환되었습니다.  
  
 [6] 단일 매개 변수에 대해 하나 이상의 **SQLPutData** 호출이 SQL_SUCCESS 반환된 다음 SQL_NULL_DATA 설정된 *StrLen_or_Ind* 동일한 매개 변수에 대해 **SQLPutData를** 호출했습니다.  
  
## <a name="sqlrowcount"></a>SQLRowCount  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|(HY010)|--|--|(HY010)|(HY010)|  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--[2] 24000[3]|HY010|HY010|  
  
 [1] 이 행은 *특성이* 연결 특성일 때의 전환을 보여 주었습니다. *특성이* 문 특성인 경우 전환의 경우 **SQLSetStmtAttr**에 대한 문 전환 테이블을 참조하십시오.  
  
 [2] *특성* 인수가 SQL_ATTR_CURRENT_CATALOG 않았습니다.  
  
 [3] *특성* 인수가 SQL_ATTR_CURRENT_CATALOG.  
  
## <a name="sqlsetcursorname"></a>SQLSetCursorName  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|24000|24000|HY010|HY010|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDesc필드 및 SQLSetDescRec  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH[1]|--|--|--|--|HY010|HY010|  
  
 [1] 이 행은 *설명자핸들* 인수가 ARD, APD, IPD 또는 **(SQLSetDescField의**경우) *필드 식별자* 인수가 SQL_DESC_ARRAY_STATUS_PTR 또는 SQL_DESC_ROWS_PROCESSED_PTR 경우 IRD인 전환을 보여 SQL_DESC_ROWS_PROCESSED_PTR. *필드 식별자가* 다른 값일 때 IRD에 대해 **SQLSetDescField를** 호출하는 오류입니다.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|HY011|HY011|HY011|HY011|Y011|HY01|HY011|  
  
## <a name="sqlsetpos"></a>SQLSetPos  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24000|다음 표 보기|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlsetpos-cursor-states"></a>SQLSetPos(커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetch스크롤|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-- [s] S8 [d] S11 [x] 24000 [b] HY109 [i]|-- [s] S8 [d] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> Allocated|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|-[1] HY011[2]|--[1] 24000[2]|--[1] 24000[2]|HY010 [np] 또는 [1] HY011 [p] 및 [2]|HY010 [np] 또는 [1] HY011 [p] 및 [2]|  
  
 [1] *특성* 인수가 SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE 또는 SQL_ATTR_CURSOR_SENSITIVITY 않았습니다.  
  
 [2] *속성* 인수는 SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE 또는 SQL_ATTR_CURSOR_SENSITIVITY.
