---
title: 문 전환 | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- transitioning states [ODBC], statement
- state transitions [ODBC], statement
- statement transitions [ODBC]
ms.assetid: 3d70e0e3-fe83-4b4d-beac-42c82495a05b
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a0566a32a2c34efca52391aea656c6908a7f8906
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="statement-transitions"></a>문 전환
ODBC 문 상태를 갖습니다.  
  
|State|Description|  
|-----------|-----------------|  
|S0|할당 되지 않은 문입니다. (연결 상태는 c 4, c, 5 또는 c 6 이어야 합니다. 자세한 내용은 참조 [연결 전환](../../../odbc/reference/appendixes/connection-transitions.md).)|  
|S1|할당 된 문입니다.|  
|S2|준비 된 문입니다. 결과 집합이 생성 됩니다.|  
|S3|준비 된 문입니다. (비어 있을 수 있음) 결과 집합이 생성 됩니다.|  
|S4|실행 된 문 및 결과 집합이 만들어졌습니다.|  
|S5|문이 실행 되 고 (비어 있을 수 있음) 결과 집합을 만들었습니다. 커서를 열어 결과 집합의 첫 번째 행 앞에 둡니다.|  
|S6|커서를 배치 하는 **SQLFetch** 또는 **SQLFetchScroll**합니다.|  
|S7|커서를 배치 하는 **SQLExtendedFetch**합니다.|  
|S8|함수는 데이터가 필요 합니다. **SQLParamData** 호출 되지 않았습니다.|  
|S9|함수는 데이터가 필요 합니다. **SQLPutData** 호출 되지 않았습니다.|  
|S10|함수는 데이터가 필요 합니다. **SQLPutData** 가 호출 되었습니다.|  
|S11|계속 실행 합니다. 문은이 상태로 남아 비동기적으로 실행 되는 함수가 SQL_STILL_EXECUTING을 반환 합니다. 문을 일시적으로 실행 하는 문 핸들을 허용 하는 함수는 동안이 상태에서입니다. 임시 거주 S11 상태 테이블을 제외한 모든 상태 테이블에 표시 되지 않으면 상태에서 **SQLCancel**합니다. 함수를 호출 하 여 취소할 수는 문이 일시적으로 S11 상태인 동안 **SQLCancel** 다른 스레드에서 합니다.|  
|S12|비동기 실행이 취소 되었습니다. S12, SQL_STILL_EXECUTING 이외의 값을 반환 될 때까지 응용 프로그램은 취소 된 함수를 호출 해야 합니다. 함수는 SQL_ERROR 및 SQLSTATE HY008 함수에서 반환 하는 경우에 성공적으로 취소 되었습니다 (작업이 취소 됨). 관계 없이 SQL_SUCCESS 취소 하지 못했습니다. 및 정상적으로 실행 하는 함수 같은 다른 값을 반환 합니다.|  
  
 커서 상태 S10 통해 S8 필요 데이터 상태를 설명 하 고 비동기 상태로 S11 및 S12 상태 대로 S7 통해 S5 상태 상태 S2, S3 준비 된 상태 라고 합니다. 이러한 그룹의 각 전환 별도로 표시; 그룹의 각 상태에 대 한 다른 경우에 대부분의 경우 각각에 대 한 전환 상태에서 각 그룹은 동일 합니다.  
  
 다음 표에서 각 ODBC 함수 문 상태에 미치는 영향을 보여 줍니다.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1], [5], [6]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[2], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|S1 [3]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[4], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
  
 [1]이이 행 표시 전환 때 *HandleType* SQL_HANDLE_ENV 되었습니다.  
  
 [2]이이 행 표시 전환 때 *HandleType* sql_handle_dbc 라는 되었습니다.  
  
 [3]이이 행 표시 전환 때 *HandleType* 여 되었습니다.  
  
 [이 행 4]이 표시 되며 여기 전환 때 *HandleType* SQL_HANDLE_DESC 되었습니다.  
  
 [5] 호출 **SQLAllocHandle** 와 *OutputHandlePtr* 유효한 핸들을 가리키는 된 이전 내용을 처리 하 고 ODBC 드라이버에 대 한 문제를 일으킬 수에 대 한 관계 없이 해당 핸들을 덮어씁니다. 잘못 된 ODBC 응용 프로그램 프로그래밍 호출 하는 **SQLAllocHandle** 에 대해 정의 된 동일한 응용 프로그램 변수로 두 번  *\*OutputHandlePtr* 호출 하지 않고  **SQLFreeHandle** 를 재할당 하기 전에 핸들을 해제 합니다. ODBC를 덮어쓰지 핸들 방식으로 일관 되지 않은 동작이 또는 ODBC 드라이버 안되며 오류 발생할 수 있습니다.  
  
## <a name="sqlbindcol"></a>SQLBindCol  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbindparameter"></a>SQLBindParameter  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbrowseconnect-sqlconnect-and-sqldriverconnect"></a>SQLBrowseConnect, SQLConnect, 및 SQLDriverConnect  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|08002|08002|08002|08002|08002|08002|08002|  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|HY010|HY010|24000|다음 표를 참조 하십시오.|HY010|HY010 o NS [c + +]|  
  
## <a name="sqlbulkoperations-cursor-states"></a>SQLBulkOperations (커서 상태)  
  
|S5<br /><br /> 열|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|-[s] S8 S11 [d] [x]|-[s] S8 S11 [d] [x]|HY010|  
  
## <a name="sqlcancel"></a>SQLCancel  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|--|--|--|--|S1 [1] S2 [nr] [2] S3 [r] 및 [2] S5 [3] 및 [5] S6 ([3] 또는 [4]) 및 S7 [6] [4] [7] 및|다음 표를 참조 하십시오.|  
  
 [1] **SQLExecDirect** SQL_NEED_DATA를 반환 합니다.  
  
 [2] **SQLExecute** SQL_NEED_DATA를 반환 합니다.  
  
 [3] **SQLBulkOperations** SQL_NEED_DATA를 반환 합니다.  
  
 [4] **SQLSetPos** SQL_NEED_DATA를 반환 합니다.  
  
 [5] **SQLFetch**, **SQLFetchScroll**, 또는 **SQLExtendedFetch** 마치 호출 합니다.  
  
 [6] **SQLFetch** 또는 **SQLFetchScroll** 호출한 합니다.  
  
 [7] **SQLExtendedFetch** 호출한 합니다.  
  
## <a name="sqlcancel-asynchronous-states"></a>SQLCancel (비동기 상태)  
  
|S11<br /><br /> 아직 실행|S12<br /><br /> 비동기 취소|  
|-----------------------------|-----------------------------|  
|[1] NS S12 [2]|S12|  
  
 [1] 문을 함수를 실행 하는 동안 S11 상태의 일시적으로 되었습니다. **SQLCancel** 다른 스레드에서 호출 되었습니다.  
  
 [2]에서 문을 비동기적으로 호출 하는 함수 SQL_STILL_EXECUTING을 반환 했기 때문에 S11 상태 였습니다.  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|24000|24000|24000|S1 S3 [np] [p]|HY010|HY010|  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|HY010|다음 표를 참조 하십시오.|24000|-[s] S11 [x]|HY010|HY010 o NS [c + +]|  
  
## <a name="sqlcolattribute-prepared-states"></a>SQLColAttribute (준비 상태)  
  
|S2<br /><br /> 결과 없음|S3<br /><br /> 결과|  
|-----------------------|--------------------|  
|--[1] 07005[2]|-[s] S11 x|  
  
 [1] *FieldIdentifier* SQL_DESC_COUNT 되었습니다.  
  
 [2] *FieldIdentifier* SQL_DESC_COUNT 없습니다.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges, 및 SQLTables  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(면)|S5 [s] S11 [x]|S1 S5 [e] [s] S11 [x]|S1 [e] 및 [1] S5 [s]와 [1] S11 [x] 및 [1] 24000 [2]|다음 표를 참조 하십시오.|HY010|HY010 o NS [c + +]|  
  
 [1] 현재 결과 마지막 또는 결과만 또는 현재 결과가 없습니다. 여러 결과 대 한 자세한 내용은 참조 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)합니다.  
  
 [2]에 현재 결과 마지막 결과가 않습니다.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables-cursor-states"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges, 및 SQLTables (커서 상태)  
  
|S5<br /><br /> 열|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000[1]|24000|  
  
 [1]이이 오류는 경우 드라이버 관리자에서 반환은 **SQLFetch** 또는 **SQLFetchScroll** sql_no_data가 반환 되지 않은 경우 드라이버에서 반환 되 고 **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA를 반환 했습니다.  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면 [1]|--|--|--|--|HY010|NS [c + +] 및 [3] HY010 [o] 또는 [4]|  
|[2] 면|HY010|다음 표를 참조 하십시오.|24000|-[s] S11 x|HY010|NS [c + +] 및 [3] HY010 [o] 또는 [4]|  
  
 [1]이이 행 표시 전환 때는 *SourceDescHandle* 인수는 카드가, APD, 또는 IPD 했습니다.  
  
 [2]이이 행 표시 전환 때는 *SourceDescHandle* IRD 되었습니다.  
  
 [3]는 *SourceDescHandle* 및 *TargetDescHandle* 인수가에서 같이 동일한는 **SQLCopyDesc** 비동기적으로 실행 되는 함수입니다.  
  
 [4] 중 하나는 *SourceDescHandle* 인수 또는 *TargetDescHandle* 인수 (또는 둘 다) 된 다른는 **SQLCopyDesc** 실행 중인 함수 비동기적으로 합니다.  
  
## <a name="sqlcopydesc-prepared-states"></a>SQLCopyDesc (준비 상태)  
  
|S2<br /><br /> 결과 없음|S3<br /><br /> 결과|  
|-----------------------|--------------------|  
|24000[1]|-[s] S11 [x]|  
  
 [1] 이 행 표시 전환 때는 *SourceDescHandle* IRD 되었습니다.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources 및 SQLDrivers  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqldescribecol"></a>SQLDescribeCol  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|HY010|다음 표를 참조 하십시오.|24000|-[s] S11 [x]|HY010|HY010 o NS [c + +]|  
  
## <a name="sqldescribecol-prepared-states"></a>SQLDescribeCol (준비 상태)  
  
|S2<br /><br /> 결과 없음|S3<br /><br /> 결과|  
|-----------------------|--------------------|  
|07005|-[s] S11 [x]|  
  
## <a name="sqldescribeparam"></a>SQLDescribeParam  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|HY010|-[s] S11 [x]|HY010|HY010|HY010|[C + +] NS HY010 [o]|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|S0 [1]|S0 [1]|S0 [1]|S0 [1]|(HY010)|(HY010)|  
  
 [1] 호출 **SQLDisconnect** 연결과 연관 된 모든 문을 해제 합니다. 또한 c 2; 연결 상태를 반환이 연결 상태 문 상태가 S0 전에 c 4 이어야 합니다.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|-[2] 또는 [3] S1 [1]|-[3] S1 [np] 및 ([1] 또는 [2]) S1 [p] 및 [1] S2 [p] 및 [2]|-[3] S1 [np] 및 ([1] 또는 [2]) S1 [p] 및 [1] S3 [p] 및 [2]|(HY010)|(HY010)|  
  
 [1]는 *CompletionType* 인수가 SQL_COMMIT 및 **SQLGetInfo** SQL_CURSOR_COMMIT_BEHAVIOR 정보 유형에 대해 SQL_CB_DELETE 반환 또는 *CompletionType*인수가 SQL_ROLLBACK 및 **SQLGetInfo** SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 유형에 대해 SQL_CB_DELETE를 반환 합니다.  
  
 [2]는 *CompletionType* 인수가 SQL_COMMIT 및 **SQLGetInfo** SQL_CURSOR_COMMIT_BEHAVIOR 정보 유형에 대해 SQL_CB_CLOSE 반환 또는 *CompletionType*인수가 SQL_ROLLBACK 및 **SQLGetInfo** SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 유형에 대해 SQL_CB_CLOSE를 반환 합니다.  
  
 [3]는 *CompletionType* 인수가 SQL_COMMIT 및 **SQLGetInfo** SQL_CURSOR_COMMIT_BEHAVIOR 정보 유형에 대해 SQL_CB_PRESERVE 반환 또는 *CompletionType*인수가 SQL_ROLLBACK 및 **SQLGetInfo** SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 유형에 대해 SQL_CB_PRESERVE를 반환 합니다.  
  
## <a name="sqlexecdirect"></a>SQLExecDirect  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(면)|S4 [s] 및 [nr] S5 [s] 및 [r] [d] S8 S11 [x]|-[1] S1 [e] 및 [2] S4 [s] 및 [nr] S5 [e] 및 [s] 및 [r] [d] S8 S11 [x]|-[e], [1] 및 [3] S1 [e], [2] 및 [3] S4 [s] [nr] 및 [3] S5 [s] [r] 및 [3] S8 [d] 및 [3] S11 [x]과 [3] 24000 [4]|다음 표를 참조 하십시오.|HY010|[C + +] NS HY010 [o]|  
  
 [1] 오류 드라이버 관리자에서 반환 되었습니다.  
  
 [2] 오류 드라이버 관리자에서 반환 되지 않았습니다.  
  
 [3] 현재 결과 마지막 또는 결과만 또는 현재 결과가 없습니다. 여러 결과 대 한 자세한 내용은 참조 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)합니다.  
  
 [4] 현재 결과 마지막 결과가 않습니다.  
  
## <a name="sqlexecdirect-cursor-states"></a>SQLExecDirect (커서 상태)  
  
|S5<br /><br /> 열|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000 [1]|24000|  
  
 [1]이이 오류는 경우 드라이버 관리자에서 반환은 **SQLFetch** 또는 **SQLFetchScroll** 에서 SQL_NO_DATA를 반환 되지 않은 경우 드라이버에서 반환 되 고 **SQLFetch** 또는  **SQLFetchScroll** SQL_NO_DATA를 반환 했습니다.  
  
## <a name="sqlexecute"></a>SQLExecute  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(면)|(HY010)|다음 표를 참조 하십시오.|S2 [e], p, 및 [1] S4 [s] [p] [nr] 및 [1] S5 [s] [p] [r] 및 S8 [d] [p] [1] 및 [1] S11 [x], [p] 및 [1] 24000 [p]에서 [2] HY010 [np]|커서 상태 표를 참조 하십시오.|HY010|[C + +] NS HY010 [o]|  
  
 [1] 현재 결과 마지막 또는 결과만 또는 현재 결과가 없습니다. 여러 결과 대 한 자세한 내용은 참조 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)합니다.  
  
 [2]에 현재 결과 마지막 결과가 않습니다.  
  
## <a name="sqlexecute-prepared-states"></a>SQLExecute (준비 상태)  
  
|S2<br /><br /> 결과 없음|S3<br /><br /> 결과|  
|-----------------------|--------------------|  
|S4 [s] [d] S8 S11 [x]|S5 [s] [d] S8 S11 [x]|  
  
## <a name="sqlexecute-cursor-states"></a>SQLExecute (커서 상태)  
  
|S5<br /><br /> 열|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000 [p] HY010 [np]|24000 [p], [1] HY010 [np]|24000 [p] HY010 [np]|  
  
 [1]이이 오류는 경우 드라이버 관리자에서 반환은 **SQLFetch** 또는 **SQLFetchScroll** 에서 SQL_NO_DATA를 반환 되지 않은 경우 드라이버에서 반환 되 고 **SQLFetch** 또는  **SQLFetchScroll** SQL_NO_DATA를 반환 했습니다.  
  
## <a name="sqlextendedfetch"></a>SQLExtendedFetch  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|S1010|S1010|24000|다음 표를 참조 하십시오.|S1010|[C + +] NS S1010 [o]|  
  
## <a name="sqlextendedfetch-cursor-states"></a>SQLExtendedFetch (커서 상태)  
  
|S5<br /><br /> 열|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S7 [s] 또는 [nf] S11 [x]|S1010|-[s] 또는 [nf] S11 [x]|  
  
## <a name="sqlfetch-and-sqlfetchscroll"></a>SQLFetch 및 SQLFetchScroll  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|HY010|HY010|24000|다음 표를 참조 하십시오.|HY010|[C + +] NS HY010 [o]|  
  
## <a name="sqlfetch-and-sqlfetchscroll-cursor-states"></a>SQLFetch 및 SQLFetchScroll (커서 상태)  
  
|S5<br /><br /> 열|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S6 [s] 또는 [nf] S11 [x]|-[s] 또는 [nf] S11 [x]|HY010|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|-- [1]|HY010|HY010|HY010|HY010|HY010|HY010|  
|[2] 면|S0|S0|S0|S0|HY010|HY010|  
|-- [3]|--|--|--|--|--|--|  
  
 [1]이이 행 표시 전환 때 *HandleType* SQL_HANDLE_ENV 되었거나 sql_handle_dbc 라는 합니다.  
  
 [2]이이 행 표시 전환 때 *HandleType* 여 되었습니다.  
  
 [3]이이 행 표시 전환 때 *HandleType* SQL_HANDLE_DESC 였으며 설명자가 명시적으로 할당 합니다.  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면 [1]|--|--|S1 S2 [np] [p]|S1 S3 [np] [p]|HY010|HY010|  
|[2] 면|--|--|--|--|HY010|HY010|  
  
 [1]이이 행 표시 전환 때 *옵션* SQL_CLOSE 되었습니다.  
  
 [2]이이 행 표시 전환 때 *옵션* SQL_UNBIND 되었거나 SQL_RESET_PARAMS 합니다. 경우는 *옵션* 인수 SQL_DROP 였으며 기본 드라이버는 ODBC 3*.x* 드라이버, 드라이버 관리자 매핑합니다이에 대 한 호출을 **SQLFreeHandle** 와  *HandleType* 여로 설정 합니다. 자세한 내용은 전환 표를 참조 하십시오. [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)합니다.  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetcursorname"></a>SQLGetCursorName  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|--|--|--|--|HY010|HY010|  
  
## <a name="sqlgetdata"></a>SQLGetData  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|HY010|HY010|24000|다음 표를 참조 하십시오.|HY010|[C + +] NS HY010 [o]|  
  
## <a name="sqlgetdata-cursor-states"></a>SQLGetData (커서 상태)  
  
|S5<br /><br /> 열|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-[s] 또는 [nf] [x] [b] HY109 24000 S11 [i]|-[s] 또는 [nf] [x] [b] HY109 24000 S11 [i]|  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField 및 SQLGetDescRec  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|-[1] 또는 [2] HY010 [3]|다음 표를 참조 하십시오.|-[1] 또는 [2] 24000 [3]|-[1], [2] 또는 [3] S11 [3] 및 [x]|HY010|NS [c + +] 또는 [4] HY010 [o] 및 [5]|  
  
 [1]는 *DescriptorHandle* APD 또는 인수 했습니다.  
  
 [2]는 *DescriptorHandle* 인수는 IPD 했습니다.  
  
 [3]는 *DescriptorHandle* IRD 되었습니다.  
  
 [4]는 *DescriptorHandle* 인수 같았습니다는 *DescriptorHandle* 인수에는 **SQLGetDescField** 또는 **SQLGetDescRec** 비동기적으로 실행 되는 함수입니다.  
  
 [5]는 *DescriptorHandle* 인수가 고 *DescriptorHandle* 인수에는 **SQLGetDescField** 또는 **SQLGetDescRec**비동기적으로 실행 되는 함수입니다.  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec-prepared-states"></a>SQLGetDescField 및 SQLGetDescRec (준비 상태)  
  
|S2<br /><br /> 결과 없음|S3<br /><br /> 결과|  
|-----------------------|--------------------|  
|-[1], [2] 또는 [3] S11 [2] 및 [x]|-[1], [2] 또는 [3] S11 [x]|  
  
 [1]는 *DescriptorHandle* APD 또는 인수 했습니다.  
  
 [2]는 *DescriptorHandle* 인수는 IPD 했습니다.  
  
 [3]는 *DescriptorHandle* IRD 되었습니다. 이러한 함수 항상 반환 SQL_NO_DATA S2 상태의 경우 *DescriptorHandle* IRD 했습니다.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 및 SQLGetDiagRec  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--|--|--|  
|[2] 면|--[3]|--[3]|--|--|--[3]|--[3]|  
  
 [1]이이 행 표시 전환 때 *HandleType* SQL_HANDLE_ENV, sql_handle_dbc 라는, 또는 SQL_HANDLE_DESC 합니다.  
  
 [2]이이 행 표시 전환 때 *HandleType* 여 되었습니다.  
  
 [3] **SQLGetDiagField** 에서 오류를 반환 하면 상태로 항상 *DiagIdentifier* SQL_DIAG_ROW_COUNT 됩니다.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|--[1] 24000[2]|--[1] 24000[2]|--[1] 24000[2]|다음 표를 참조 하십시오.|HY010|HY010|  
  
 [1] 문 특성 SQL_ATTR_ROW_NUMBER 없습니다.  
  
 [2]에서 문 특성 SQL_ATTR_ROW_NUMBER 했습니다.  
  
## <a name="sqlgetstmtattr-cursor-states"></a>SQLGetStmtAttr (커서 상태)  
  
|S5<br /><br /> 열|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[1] 24000[2]|-[1] 또는 ([v] 및 [2]) 24000 [b] 및 [2] HY109 [i] 및 [2]|-[i] 또는 ([v] 및 [2]) 24000 [b] 및 [2] HY109 [1] 및 [2]|  
  
 [1]는 *특성* 인수 SQL_ATTR_ROW_NUMBER 없습니다.  
  
 [2]는 *특성* SQL_ATTR_ROW_NUMBER 되었습니다.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(면)|--[1]|--[1]|-[s], [2] S1 [nf] [np] 및 [4] S2 [nf] [p] 및 [4] S5 [s] 및 [3] S11 [x]|S1 [nf] [np] 및 [4] S3 [nf] [p] 및 [4] S4 [s] 및 [2] S5 [s] 및 [3] S11 [x]|HY010|[C + +] NS HY010 [o]|  
  
 [1] 함수는 항상이 상태에서 SQL_NO_DATA를 반환합니다.  
  
 [2]에서 다음 결과 행 수입니다.  
  
 [3]에서 다음 결과 결과 집합입니다.  
  
 [4] 현재 결과는 마지막 결과가입니다.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlnumparams"></a>SQLNumParams  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|HY010|-[s] S11 [x]|-[s] S11 [x]|-[s] S11 [x]|HY010|[C + +] NS HY010 [o]|  
  
## <a name="sqlnumresultcols"></a>SQLNumResultCols  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|HY010|-[s] S11 [x]|-[s] S11 [x]|-[s] S11 [x]|HY010|[C + +] NS HY010 [o]|  
  
## <a name="sqlparamdata"></a>SQLParamData  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|HY010|HY010|HY010|HY010|다음 표를 참조 하십시오.|[C + +] NS HY010 [o]|  
  
## <a name="sqlparamdata-need-data-states"></a>SQLParamData (필요 데이터 상태)  
  
|S8<br /><br /> 데이터가 필요|S9<br /><br /> 넣으십시오|S10<br /><br /> 넣을 수합니다 있습니다.|  
|----------------------|---------------------|---------------------|  
|S1 [e] 및 [1] S2 [e] [nr], [2] S3 [e] [r] 및 [2] S5 [e] [4] S6 및 [e] 및 [5] S7 [e] 및 [x] [3] S9 [d] S11|HY010|S1 [e] 및 [1] S2 [e] [nr], [2] S3 [e] [r] 및 S4 [2] [s] [nr] 및 ([1] 또는 [2]) S5 [s] [r] 및 ([1] 또는 [2]) S5 ([s] 또는 [e]) 및 S6 [4] \([s] 또는 [e]) 및 [5] S7 ([s] 또는 [e]) 및 [x] [3] S9 [d] S11|  
  
 [1] **SQLExecDirect** SQL_NEED_DATA를 반환 합니다.  
  
 [2] **SQLExecute** SQL_NEED_DATA를 반환 합니다.  
  
 [3] **SQLSetPos** S7 상태에서 호출 되었으며 SQL_NEED_DATA를 반환 했습니다.  
  
 [4] **SQLBulkOperations** S5 상태에서 호출 되었으며 SQL_NEED_DATA를 반환 했습니다.  
  
 [5] **SQLSetPos** 또는 **SQLBulkOperations** S6 상태에서 호출 되었으며 SQL_NEED_DATA를 반환 했습니다.  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(면)|S2 [s] 및 [nr] S3 [s] 및 [r] S11 [x]|-[s] 또는 ([e] 및 [1]) S1 [e] 및 [2] S11 [x]|S1 [e] 및 [3] S2 [s] [nr] 및 [3] S3 [s] [r] 및 [3] S11 [x] [3] 및 24000 [4]|다음 표를 참조 하십시오.|HY010|[C + +] NS HY010 [o]|  
  
 [유효성을 검사 하는 문 외의 다른 이유로 실패 하는 1]는 준비 (SQLSTATE가 HY009 [잘못 된 인수 값] 또는 HY090 [잘못 된 문자열 또는 버퍼 길이가]).  
  
 [2]에서 준비 문을 확인 하는 동안 실패 (SQLSTATE HY009 없습니다 [잘못 된 인수 값] 또는 HY090 [잘못 된 문자열 또는 버퍼 길이가]).  
  
 [3] 현재 결과 마지막 또는 결과만 또는 현재 결과가 없습니다. 여러 결과 대 한 자세한 내용은 참조 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)합니다.  
  
 [4] 현재 결과 마지막 결과가 않습니다.  
  
## <a name="sqlprepare-cursor-states"></a>SQLPrepare (커서 상태)  
  
|S5<br /><br /> 열|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000|24000|  
  
## <a name="sqlputdata"></a>SQLPutData  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|HY010|HY010|HY010|HY010|다음 표를 참조 하십시오.|[C + +] NS HY010 [o]|  
  
## <a name="sqlputdata-need-data-states"></a>SQLPutData (필요 데이터 상태)  
  
|S8<br /><br /> 데이터가 필요|S9<br /><br /> 넣으십시오|S10<br /><br /> 넣을 수합니다 있습니다.|  
|----------------------|---------------------|---------------------|  
|HY010|S1 [e] 및 [1] S2 [e] [nr], [2] S3 [e] [r] 및 [2] S5 [e] [4] S6 및 [e] 및 [5] S7 [e] 및 [3] S10 [s] S11 [x]|-[s] S1 [e] 및 [1] S2 [e] [nr], [2] S3 [e] [r] 및 [2] S5 [e] [4] S6 및 [e] 및 [5] S7 [e] 및 [3] S11 [x] HY011 [6]|  
  
 [1] **SQLExecDirect** SQL_NEED_DATA를 반환 합니다.  
  
 [2] **SQLExecute** SQL_NEED_DATA를 반환 합니다.  
  
 [3] **SQLSetPos** S7 상태에서 호출 되었으며 SQL_NEED_DATA를 반환 했습니다.  
  
 [4] **SQLBulkOperations** S5 상태에서 호출 되었으며 SQL_NEED_DATA를 반환 했습니다.  
  
 [5] **SQLSetPos** 또는 **SQLBulkOperations** S6 상태에서 호출 되었으며 SQL_NEED_DATA를 반환 했습니다.  
  
 [6] 하나 이상의 호출을 **SQLPutData** 단일 매개 변수 관계 없이 SQL_SUCCESS를 반환 된 다음 반환에 대 한 호출에 대 한 **SQLPutData** 와 동일한 매개 변수에 만들어진 *StrLen_or_Ind* 설정 sql_null_data로 합니다.  
  
## <a name="sqlrowcount"></a>SQLRowCount  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(면)|(HY010)|(HY010)|--|--|(HY010)|(HY010)|  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--[2] 24000[3]|HY010|HY010|  
  
 [1]이이 행 표시 전환 때 *특성* 연결 특성이 있습니다. 에 대 한 전환 될 때 *특성* 된 문인 특성에 대 한 문 전환 테이블을 참조 하십시오 **SQLSetStmtAttr**합니다.  
  
 [2]는 *특성* 인수 SQL_ATTR_CURRENT_CATALOG 없습니다.  
  
 [3]는 *특성* SQL_ATTR_CURRENT_CATALOG 되었습니다.  
  
## <a name="sqlsetcursorname"></a>SQLSetCursorName  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|--|--|24000|24000|HY010|HY010|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField 및 SQLSetDescRec  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면 [1]|--|--|--|--|HY010|HY010|  
  
 [1]이이 행 전이 보여 줍니다. 여기서는 *DescriptorHandle* 인수가 카드가, APD, IPD, 또는 (에 대 한 **SQLSetDescField**) IRD 때는 *FieldIdentifier* 인수가 SQL_ DESC_ARRAY_STATUS_PTR 또는 SQL_DESC_ROWS_PROCESSED_PTR 합니다. 호출 하면 오류가 발생 **SQLSetDescField** IRD에 대 한 때 *FieldIdentifier* 다른 값이 있습니다.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|HY011|HY011|HY011|HY011|Y011|HY01|HY011|  
  
## <a name="sqlsetpos"></a>SQLSetPos  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|HY010|HY010|24000|다음 표를 참조 하십시오.|HY010|[C + +] NS HY010 [o]|  
  
## <a name="sqlsetpos-cursor-states"></a>SQLSetPos (커서 상태)  
  
|S5<br /><br /> 열|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-[s] S8 [d] [x] [b] HY109 24000 S11 [i]|-[s] S8 [d] [x] [b] HY109 24000 S11 [i]|  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당 된|S2-S3<br /><br /> Prepared|S4<br /><br /> 실행|S5 – S7<br /><br /> 커서|S8 – S10<br /><br /> 데이터가 필요|S11 – S12<br /><br /> 비동기|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|면|--|-[1] HY011 [2]|--[1] 24000[2]|--[1] 24000[2]|HY010 [np] 또는 [1] HY011 [p] 및 [2]|HY010 [np] 또는 [1] HY011 [p] 및 [2]|  
  
 [1]는 *특성* 인수 SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE 및 SQL_ATTR_CURSOR_SENSITIVITY 없습니다.  
  
 [2]는 *특성* SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE 및 SQL_ATTR_CURSOR_SENSITIVITY 되었습니다.
