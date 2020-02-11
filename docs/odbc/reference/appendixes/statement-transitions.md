---
title: 문 전환 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b0d46bad2e0b37c5e6751a4895cdf1899aee4b01
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070102"
---
# <a name="statement-transitions"></a>명령문 전환
ODBC 문의 상태는 다음과 같습니다.  
  
|시스템 상태|Description|  
|-----------|-----------------|  
|S0|할당 되지 않은 문입니다. 연결 상태는 C4, C5 또는 C6 이어야 합니다. 자세한 내용은 [연결 전환](../../../odbc/reference/appendixes/connection-transitions.md)을 참조 하세요.|  
|S1|할당 된 문.|  
|S2|준비 된 문. 결과 집합이 생성 되지 않습니다.|  
|S3|준비 된 문. (비어 있을 수 있음) 결과 집합이 생성 됩니다.|  
|S4|문이 실행 되 고 결과 집합이 생성 되지 않았습니다.|  
|S5|문이 실행 되 고 (비어 있을 수 있음) 결과 집합이 생성 되었습니다. 커서가 열리고 결과 집합의 첫 번째 행 앞에 배치 됩니다.|  
|S6|**Sqlfetch** 또는 **sqlfetchscroll**을 사용 하 여 커서 위치를 지정 합니다.|  
|S7|**Sqlextendedfetch**를 사용 하 여 커서가 배치 됩니다.|  
|S8|함수에 데이터가 필요 합니다. **Sqlparamdata** 가 호출 되지 않았습니다.|  
|S9|함수에 데이터가 필요 합니다. **Sqlputdata** 가 호출 되지 않았습니다.|  
|S10|함수에 데이터가 필요 합니다. **Sqlputdata** 가 호출 되었습니다.|  
|S11|계속 실행 중입니다. 비동기 방식으로 실행 되는 함수는 SQL_STILL_EXECUTING을 반환 하 고 나면 문이이 상태로 남아 있습니다. 문 핸들을 수락 하는 함수가 실행 되는 동안 문은 일시적으로이 상태에 있습니다. 상태 S11의 임시 거주지는 **Sqlcancel**의 상태 테이블을 제외한 모든 상태 테이블에 표시 되지 않습니다. 문은 일시적으로 S11 상태에 있지만 다른 스레드에서 **Sqlcancel** 을 호출 하 여 함수를 취소할 수 있습니다.|  
|S12|비동기 실행이 취소 되었습니다. S 12에서 응용 프로그램은 SQL_STILL_EXECUTING 이외의 값을 반환할 때까지 취소 된 함수를 호출 해야 합니다. 함수가 SQL_ERROR 및 SQLSTATE HY008 (작업 취소)를 반환 하는 경우에만 함수를 취소 했습니다. SQL_SUCCESS와 같은 다른 값을 반환 하는 경우에는 취소 작업이 실패 하 고 함수는 정상적으로 실행 됩니다.|  
  
 상태 S2 및 s 3을 준비 상태 라고 하며,이 상태는 S7을 통해 커서 상태로, S8는 S10를 통해 필요한 데이터 상태, S11 및 S 12 상태를 비동기 상태로 명시 합니다. 이러한 각 그룹에서 전환은 그룹의 각 상태 마다 다르게 표시 됩니다. 대부분의 경우 각 그룹의 각 상태에 대 한 전환은 동일 합니다.  
  
 다음 표에서는 각 ODBC 함수가 문 상태에 미치는 영향을 보여 줍니다.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1], [5], [6]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[2], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|S1 [3]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[4], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
  
 [1] *HandleType* 가 SQL_HANDLE_ENV 된 경우이 행은 전환을 표시 합니다.  
  
 [2] *HandleType* 가 SQL_HANDLE_DBC 된 경우이 행은 전환을 표시 합니다.  
  
 [3] *HandleType* 가 SQL_HANDLE_STMT 된 경우이 행은 전환을 표시 합니다.  
  
 [4] *HandleType* 가 SQL_HANDLE_DESC 된 경우이 행은 전환을 표시 합니다.  
  
 [5] 유효한 핸들을 가리키는 *OutputHandlePtr* 를 사용 하 여 **SQLAllocHandle** 를 호출 하면 해당 핸들에 대 한 이전 콘텐츠를 고려 하지 않고 핸들을 덮어쓰므로 ODBC 드라이버에 문제가 발생할 수 있습니다. **Sqlfreehandle** 을 호출 하지 않고 * \*OutputHandlePtr* 에 대해 정의 된 것과 동일한 응용 프로그램 변수를 사용 하 여 **SQLAllocHandle** 를 두 번 호출 하 여 다시 할당 하기 전에 핸들을 해제 합니다. 이러한 방식으로 ODBC 핸들을 덮어쓰면 ODBC 드라이버의 일부에 대해 일관 되지 않은 동작이 나 오류가 발생할 수 있습니다.  
  
## <a name="sqlbindcol"></a>SQLBindCol  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbindparameter"></a>SQLBindParameter  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbrowseconnect-sqlconnect-and-sqldriverconnect"></a>SQLBrowseConnect, SQLConnect 및 SQLDriverConnect  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|08002|08002|08002|08002|08002|08002|08002|  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|HY010|HY010|24000|다음 표 참조|HY010|NS [c] HY010 o|  
  
## <a name="sqlbulkoperations-cursor-states"></a>SQLBulkOperations (커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[s] S8 [d] S11 [x]|--[s] S8 [d] S11 [x]|HY010|  
  
## <a name="sqlcancel"></a>SQLCancel  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|--|--|--|--|S1 [1] S2 [nr] 및 [2] S3 [r] 및 [2] S5 [3] 및 [5] S6 ([3] 또는 [4]) 및 [6] S7 [4] 및 [7]|다음 표 참조|  
  
 [1] **Sqlexecdirect** 가 SQL_NEED_DATA 반환 했습니다.  
  
 [2] **Sqlexecute** 가 SQL_NEED_DATA 반환 했습니다.  
  
 [3] **SQLBulkOperations** 반환 SQL_NEED_DATA.  
  
 [4] **SQLSetPos** 가 SQL_NEED_DATA를 반환 했습니다.  
  
 [5] **Sqlfetch**, **Sqlfetchscroll**또는 **sqlextendedfetch** 가 호출 되지 않았습니다.  
  
 [6] **Sqlfetch** 또는 **sqlfetchscroll** 이 호출 되었습니다.  
  
 [7] **Sqlextendedfetch** 가 호출 되었습니다.  
  
## <a name="sqlcancel-asynchronous-states"></a>SQLCancel (비동기 상태)  
  
|S11<br /><br /> 아직 실행 중|S12<br /><br /> Asynch 취소 됨|  
|-----------------------------|-----------------------------|  
|NS [1] S 12 [2]|S12|  
  
 [1] 함수가 실행 되는 동안 문이 일시적으로 S11 상태 였습니다. **Sqlcancel** 이 다른 스레드에서 호출 되었습니다.  
  
 [2] SQL_STILL_EXECUTING 비동기식으로 호출 된 함수가 상태입니다.  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|24000|24000|24000|S1 [np] S3 [p]|HY010|HY010|  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|HY010|다음 표 참조|24000|--[s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqlcolattribute-prepared-states"></a>SQLColAttribute (준비 된 상태)  
  
|S2<br /><br /> 결과 없음|S3<br /><br /> 결과|  
|-----------------------|--------------------|  
|--[1] 07005 [2]|--[s] S11 x|  
  
 [1] *FieldIdentifier* 가 SQL_DESC_COUNT 되었습니다.  
  
 [2] *FieldIdentifier* 가 SQL_DESC_COUNT 되지 않았습니다.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, Sqlcolumnprivileges, SQLProcedureColumns, Sql프로시저, SQLSpecialColumns, SQLStatistics, Sqlcolumnprivileges 및 SQLTables  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|S5 [s] S11 [x]|S1 [e] S5 [s] S11 [x]|S1 [e] 및 [1] S5 [s] 및 [1] S11 [x] 및 [1] 24000 [2]|다음 표 참조|HY010|NS [c] HY010 o|  
  
 [1] 현재 결과가 마지막 또는 유일한 결과 이거나 현재 결과가 없습니다. 여러 결과에 대 한 자세한 내용은 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)를 참조 하세요.  
  
 [2] 현재 결과가 마지막 결과가 아닙니다.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables-cursor-states"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, Sqlcolumnprivileges, SQLProcedureColumns, Sql프로시저만, SQLSpecialColumns, SQLStatistics, Sqlcolumnprivileges 및 SQLTables (커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000 [1]|24000|  
  
 [1] **sqlfetch 또는** **sqlfetchscroll** 이 SQL_NO_DATA 반환 되지 않은 경우 드라이버 관리자에서이 오류가 반환 됩니다. **Sqlfetch** 또는 **sqlfetchscroll** 에서 SQL_NO_DATA를 반환한 경우 드라이버에서이 오류가 반환 됩니다.  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|--|--|HY010|NS [c] 및 [3] HY010 [o] 또는 [4]|  
|IH [2]|HY010|다음 표 참조|24000|--[s] S11 x|HY010|NS [c] 및 [3] HY010 [o] 또는 [4]|  
  
 [1] *SourceDescHandle* 인수가 IPD 인 경우이 행은 전환을 표시 합니다.  
  
 [2] *SourceDescHandle* 인수가 IRD 인 경우이 행은 전환을 표시 합니다.  
  
 [3] *SourceDescHandle* 및 *TargetDescHandle* 인수는 비동기적으로 실행 되는 **sqlcopydesc** 함수와 동일 합니다.  
  
 [4] *SourceDescHandle* 인수나 *TargetDescHandle* 인수 (또는 둘 다)가 비동기적으로 실행 되는 **sqlcopydesc** 함수와 다릅니다.  
  
## <a name="sqlcopydesc-prepared-states"></a>SQLCopyDesc (준비 상태)  
  
|S2<br /><br /> 결과 없음|S3<br /><br /> 결과|  
|-----------------------|--------------------|  
|24000 [1]|--[s] S11 [x]|  
  
 비슷합니다 *SourceDescHandle* 인수가 IRD 인 경우이 행은 전환을 표시 합니다.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources 원본 및 Sqldatasources  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqldescribecol"></a>SQLDescribeCol  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|HY010|다음 표 참조|24000|--[s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqldescribecol-prepared-states"></a>SQLDescribeCol (준비 상태)  
  
|S2<br /><br /> 결과 없음|S3<br /><br /> 결과|  
|-----------------------|--------------------|  
|07005|--[s] S11 [x]|  
  
## <a name="sqldescribeparam"></a>SQLDescribeParam  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|HY010|--[s] S11 [x]|HY010|HY010|HY010|NS [c] HY010 [o]|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|S0 [1]|S0 [1]|S0 [1]|S0 [1]|HY010|HY010|  
  
 [1] **Sqldisconnect** 를 호출 하면 연결과 관련 된 모든 문이 해제 됩니다. 또한 연결 상태를 C2로 반환 합니다. 문 상태가 S0 인 경우 연결 상태는 C4 여야 합니다.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--[2] 또는 [3] S1 [1]|--[3] s1 [np] 및 ([1] 또는 [2]) S1 [p] 및 [1] S2 [p] 및 [2]|--[3] s1 [np] 및 ([1] 또는 [2]) S1 [p] 및 [1] S3 [p] 및 [2]|HY010|HY010|  
  
 [1] SQL_COMMIT 된 *형식* 인수는이 고 **sqlgetinfo** 는 SQL_CURSOR_COMMIT_BEHAVIOR 정보 형식에 대 한 SQL_CB_DELETE을 반환 하거나, SQL_CB_DELETE *형식* 인수는 SQL_ROLLBACK이 고, **sqlgetinfo** 는 SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 형식에 대 한를 반환 합니다.  
  
 [2] 인수 *형식* 인수가 SQL_COMMIT 이며 **sqlgetinfo** 는 SQL_CURSOR_COMMIT_BEHAVIOR 정보 형식에 대 한 SQL_CB_CLOSE을 반환 하거나, SQL_CB_CLOSE *형식* 인수가 SQL_ROLLBACK이 고, **sqlgetinfo** 는 SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 형식에 대 한를 반환 합니다.  
  
 [3] 인수 *형식* 인수는 SQL_COMMIT이 고 **sqlgetinfo** 는 SQL_CURSOR_COMMIT_BEHAVIOR 정보 형식에 대 한 SQL_CB_PRESERVE을 반환 하거나, SQL_CB_PRESERVE *형식* 인수는 SQL_ROLLBACK이 고, **sqlgetinfo** 는 SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 형식에 대 한를 반환 합니다.  
  
## <a name="sqlexecdirect"></a>SQLExecDirect  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|S4 [s] 및 [nr] S5 [s] 및 [r] S8 [d] S11 [x]|--[e] 및 [1] S1 [e] 및 [2] S4 [s] 및 [nr] S5 [s] 및 [r] S8 [d] S11 [x]|--[e], [1], [3] S1 [e], [2] 및 [3] S4 [s], [nr] 및 [3] S5 [s], [r] 및 [3] S8 [d] 및 [3] S11 [x] 및 [3] 24000 [4]|다음 표 참조|HY010|NS [c] HY010 [o]|  
  
 [1] 드라이버 관리자에서 오류를 반환 했습니다.  
  
 [2] 드라이버 관리자에서 오류를 반환 하지 않았습니다.  
  
 [3] 현재 결과가 마지막 또는 유일한 결과 이거나 현재 결과가 없습니다. 여러 결과에 대 한 자세한 내용은 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)를 참조 하세요.  
  
 [4] 현재 결과가 마지막 결과가 아닙니다.  
  
## <a name="sqlexecdirect-cursor-states"></a>SQLExecDirect (커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000 [1]|24000|  
  
 [1] sqlfetch 또는 **sqlfetchscroll** SQL_NO_DATA 반환 되지 **않은 경우 드라이버** 관리자에서이 오류가 반환 됩니다. **Sqlfetch** 또는 **sqlfetchscroll** 이 SQL_NO_DATA 반환 된 경우 드라이버에서 반환 됩니다.  
  
## <a name="sqlexecute"></a>SQLExecute  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|HY010|다음 표 참조|S2 [e], p, 및 [1] S4 [s], [p], [nr], [1] S5 [s], [p], [r], [1] S8 [d], [p], [1] S11 [x], [p] 및 [1] 24000 [p] 및 [2] HY010 [np]|커서 상태 표를 참조 하세요.|HY010|NS [c] HY010 [o]|  
  
 [1] 현재 결과가 마지막 또는 유일한 결과 이거나 현재 결과가 없습니다. 여러 결과에 대 한 자세한 내용은 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)를 참조 하세요.  
  
 [2] 현재 결과가 마지막 결과가 아닙니다.  
  
## <a name="sqlexecute-prepared-states"></a>SQLExecute (준비 상태)  
  
|S2<br /><br /> 결과 없음|S3<br /><br /> 결과|  
|-----------------------|--------------------|  
|S4 [s] S8 [d] S11 [x]|S5 [s] S8 [d] S11 [x]|  
  
## <a name="sqlexecute-cursor-states"></a>SQLExecute (커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000 [p] HY010 [np]|24000 [p], [1] HY010 [np]|24000 [p] HY010 [np]|  
  
 [1] sqlfetch 또는 **sqlfetchscroll** SQL_NO_DATA 반환 되지 **않은 경우 드라이버** 관리자에서이 오류가 반환 됩니다. **Sqlfetch** 또는 **sqlfetchscroll** 이 SQL_NO_DATA 반환 된 경우 드라이버에서 반환 됩니다.  
  
## <a name="sqlextendedfetch"></a>SQLExtendedFetch  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|S1010|S1010|24000|다음 표 참조|S1010|NS [c] S1010 [o]|  
  
## <a name="sqlextendedfetch-cursor-states"></a>SQLExtendedFetch (커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S7 [s] 또는 [nf] S11 [x]|S1010|--[s] 또는 [nf] S11 [x]|  
  
## <a name="sqlfetch-and-sqlfetchscroll"></a>SQLFetch 및 SQLFetchScroll  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|HY010|HY010|24000|다음 표 참조|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlfetch-and-sqlfetchscroll-cursor-states"></a>SQLFetch 및 SQLFetchScroll (커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S6 [s] 또는 [nf] S11 [x]|--[s] 또는 [nf] S11 [x]|HY010|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|HY010|HY010|HY010|HY010|HY010|HY010|  
|IH [2]|S0|S0|S0|S0|HY010|HY010|  
|--[3]|--|--|--|--|--|--|  
  
 [1] *HandleType* 가 SQL_HANDLE_ENV 또는 SQL_HANDLE_DBC 경우이 행은 전환을 표시 합니다.  
  
 [2] *HandleType* 가 SQL_HANDLE_STMT 된 경우이 행은 전환을 표시 합니다.  
  
 [3] *HandleType* 가 SQL_HANDLE_DESC 되 고 설명자가 명시적으로 할당 된 경우이 행은 전환을 표시 합니다.  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|S1 [np] S2 [p]|S1 [np] S3 [p]|HY010|HY010|  
|IH [2]|--|--|--|--|HY010|HY010|  
  
 [1] *옵션이* SQL_CLOSE 된 경우이 행은 전환을 표시 합니다.  
  
 [2] *옵션* 을 SQL_UNBIND 하거나 SQL_RESET_PARAMS 경우이 행은 전환을 표시 합니다. *Option* 인수가 SQL_DROP 고 기본 드라이버가 ODBC*3.X 드라이버 이면* 드라이버 관리자는이를 *HandleType* 가 SQL_HANDLE_STMT로 설정 된 **sqlfreehandle** 호출에 매핑합니다. 자세한 내용은 [Sqlfreehandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)의 전환 표를 참조 하세요.  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetcursorname"></a>SQLGetCursorName  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|--|--|--|--|HY010|HY010|  
  
## <a name="sqlgetdata"></a>SQLGetData  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|HY010|HY010|24000|다음 표 참조|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlgetdata-cursor-states"></a>SQLGetData (커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|--[s] 또는 [nf] S11 [x] 24000 [b] HY109 [i]|--[s] 또는 [nf] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField 및 SQLGetDescRec  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|--[1] 또는 [2] HY010 [3]|다음 표 참조|--[1] 또는 [2] 24000 [3]|--[1], [2] 또는 [3] S11 [3] 및 [x]|HY010|NS [c] 또는 [4] HY010 [o] 및 [5]|  
  
 [1] *DescriptorHandle* 인수는 apd 또는 이상입니다.  
  
 [2] *DescriptorHandle* 인수는 IPD입니다.  
  
 [3] *DescriptorHandle* 인수는 IRD입니다.  
  
 [4] *DescriptorHandle* 인수가 비동기적으로 실행 되는 **SQLGetDescField** 또는 **SQLGetDescRec** 함수의 *DescriptorHandle* 인수와 동일 합니다.  
  
 [5] *DescriptorHandle* 인수가 비동기적으로 실행 되는 **SQLGetDescField** 또는 **SQLGetDescRec** 함수의 *DescriptorHandle* 인수와 다릅니다.  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec-prepared-states"></a>SQLGetDescField 및 SQLGetDescRec (준비 상태)  
  
|S2<br /><br /> 결과 없음|S3<br /><br /> 결과|  
|-----------------------|--------------------|  
|--[1], [2] 또는 [3] S11 [2] 및 [x]|--[1], [2] 또는 [3] S11 [x]|  
  
 [1] *DescriptorHandle* 인수는 apd 또는 이상입니다.  
  
 [2] *DescriptorHandle* 인수는 IPD입니다.  
  
 [3] *DescriptorHandle* 인수는 IRD입니다. *DescriptorHandle* 가 IRD 인 경우 이러한 함수는 항상 상태 S2의 SQL_NO_DATA을 반환 합니다.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 및 SQLGetDiagRec  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--|--|--|  
|IH [2]|--[3]|--[3]|--|--|--[3]|--[3]|  
  
 [1] *HandleType* 가 SQL_HANDLE_ENV, SQL_HANDLE_DBC 또는 SQL_HANDLE_DESC 된 경우이 행은 전환을 표시 합니다.  
  
 [2] *HandleType* 가 SQL_HANDLE_STMT 된 경우이 행은 전환을 표시 합니다.  
  
 *DiagIdentifier* 가 SQL_DIAG_ROW_COUNT 경우 [3] **SQLGetDiagField** 는 항상이 상태에서 오류를 반환 합니다.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|--[1] 24000 [2]|--[1] 24000 [2]|--[1] 24000 [2]|다음 표 참조|HY010|HY010|  
  
 [1] 문 특성을 SQL_ATTR_ROW_NUMBER 하지 않았습니다.  
  
 [2] 문 특성을 SQL_ATTR_ROW_NUMBER 했습니다.  
  
## <a name="sqlgetstmtattr-cursor-states"></a>SQLGetStmtAttr (커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[1] 24000 [2]|--[1] 또는 ([v] 및 [2]) 24000 [b] 및 [2] HY109 [i] 및 [2]|--[i] 또는 ([v] 및 [2]) 24000 [b] 및 [2] HY109 [1] 및 [2]|  
  
 [1] *특성* 인수가 SQL_ATTR_ROW_NUMBER 되지 않았습니다.  
  
 [2] *특성* 인수가 SQL_ATTR_ROW_NUMBER 되었습니다.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|--[1]|--[1]|--[s] 및 [2] S1 [nf], [np] 및 [4] S2 [nf], [p] 및 [4] S5 [s] 및 [3] S11 [x]|S1 [nf], [np] 및 [4] S3 [nf], [p] 및 [4] S4 [s] 및 [2] S5 [s] 및 [3] S11 [x]|HY010|NS [c] HY010 [o]|  
  
 [1] 함수는 항상이 상태의 SQL_NO_DATA 반환 합니다.  
  
 [2] 다음 결과는 행 개수입니다.  
  
 [3] 다음 결과는 결과 집합입니다.  
  
 [4] 현재 결과가 마지막 결과입니다.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlnumparams"></a>SQLNumParams  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|HY010|--[s] S11 [x]|--[s] S11 [x]|--[s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlnumresultcols"></a>SQLNumResultCols  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|HY010|--[s] S11 [x]|--[s] S11 [x]|--[s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata"></a>SQLParamData  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|HY010|HY010|HY010|HY010|다음 표 참조|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata-need-data-states"></a>SQLParamData (데이터 상태 필요)  
  
|S8<br /><br /> 데이터 필요|S9<br /><br /> 넣어야 함|S10<br /><br /> 넣을 수 있음|  
|----------------------|---------------------|---------------------|  
|S1 [e] 및 [1] S2 [e], [nr] 및 [2] S3 [e], [r] 및 [2] S5 [e] 및 [4] S6 [e] 및 [5] S7 [e] 및 [3] S9 [d] S11 [x]|HY010|S1 [e] 및 [1] S2 [e], [nr] 및 [2] S3 [e], [r] 및 [2] S4 [s], [nr] 및 ([1] 또는 [2]) S5 [s] [r] 및 ([1] 또는 [2]) S5 ([s] 또는 [e]) 및 [4] S6 ([s] 또는 [e]) 및 [5] S7 ([s] 또는 [e]) 및 [3] S9 [d] S11 [x]|  
  
 [1] **Sqlexecdirect** 가 SQL_NEED_DATA 반환 했습니다.  
  
 [2] **Sqlexecute** 가 SQL_NEED_DATA 반환 했습니다.  
  
 [3] **SQLSetPos** 가 S7 상태에서 호출 되 고 SQL_NEED_DATA 반환 되었습니다.  
  
 [4] **SQLBulkOperations** 가 S5 상태에서 호출 되었으며 SQL_NEED_DATA 반환 되었습니다.  
  
 [5] **SQLSetPos** 또는 **SQLBulkOperations** 가 S6 상태에서 호출 되 고 SQL_NEED_DATA 반환 되었습니다.  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|S2 [s] 및 [nr] S3 [s] 및 [r] S11 [x]|--[s] 또는 ([e], [1]) S1 [e] 및 [2] S11 [x]|S1 [e] 및 [3] S2 [s], [nr] 및 [3] S3 [s], [r] 및 [3] S11 [x] 및 [3] 24000 [4]|다음 표 참조|HY010|NS [c] HY010 [o]|  
  
 [1] 문의 유효성을 검사 하는 것 외의 이유로 준비에 실패 했습니다 (SQLSTATE는 HY009 [잘못 된 인수 값] 또는 HY090 [잘못 된 문자열 또는 버퍼 길이]).  
  
 [2] 문의 유효성을 검사 하는 동안 준비에 실패 했습니다 (SQLSTATE가 HY009 [잘못 된 인수 값] 또는 HY090 [잘못 된 문자열 또는 버퍼 길이]).  
  
 [3] 현재 결과가 마지막 또는 유일한 결과 이거나 현재 결과가 없습니다. 여러 결과에 대 한 자세한 내용은 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)를 참조 하세요.  
  
 [4] 현재 결과가 마지막 결과가 아닙니다.  
  
## <a name="sqlprepare-cursor-states"></a>SQLPrepare (커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000|24000|  
  
## <a name="sqlputdata"></a>SQLPutData  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|HY010|HY010|HY010|HY010|다음 표 참조|NS [c] HY010 [o]|  
  
## <a name="sqlputdata-need-data-states"></a>SQLPutData (데이터 상태 필요)  
  
|S8<br /><br /> 데이터 필요|S9<br /><br /> 넣어야 함|S10<br /><br /> 넣을 수 있음|  
|----------------------|---------------------|---------------------|  
|HY010|S1 [e] 및 [1] S2 [e], [nr] 및 [2] S3 [e], [r] 및 [2] S5 [e] 및 [4] S6 [e] 및 [5] S7 [e] 및 [3] S10 [s] S11 [x]|--[s] S1 [e], [1] S2 [e], [nr] 및 [2] S3 [e], [r] 및 [2] S5 [e] 및 [4] S6 [e] 및 [5] S7 [e] 및 [3] S11 [x] HY011 [6]|  
  
 [1] **Sqlexecdirect** 가 SQL_NEED_DATA 반환 했습니다.  
  
 [2] **Sqlexecute** 가 SQL_NEED_DATA 반환 했습니다.  
  
 [3] **SQLSetPos** 가 S7 상태에서 호출 되 고 SQL_NEED_DATA 반환 되었습니다.  
  
 [4] **SQLBulkOperations** 가 S5 상태에서 호출 되었으며 SQL_NEED_DATA 반환 되었습니다.  
  
 [5] **SQLSetPos** 또는 **SQLBulkOperations** 가 S6 상태에서 호출 되 고 SQL_NEED_DATA 반환 되었습니다.  
  
 [6] SQL_SUCCESS 반환 된 단일 매개 변수에 대 한 **Sqlputdata** 에 대 한 하나 이상의 호출에서 *StrLen_or_Ind* SQL_NULL_DATA 설정 된 동일한 매개 변수에 대해 **sqlputdata** 를 호출 했습니다.  
  
## <a name="sqlrowcount"></a>SQLRowCount  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|HY010|HY010|--|--|HY010|HY010|  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--[2] 24000 [3]|HY010|HY010|  
  
 [1] *특성이* 연결 특성인 경우이 행은 전환을 표시 합니다. *특성이* 문 특성인 경우 전환의 경우 **SQLSetStmtAttr**에 대 한 문 전환 표를 참조 하세요.  
  
 [2] *특성* 인수가 SQL_ATTR_CURRENT_CATALOG 되지 않았습니다.  
  
 [3] *특성* 인수가 SQL_ATTR_CURRENT_CATALOG 되었습니다.  
  
## <a name="sqlsetcursorname"></a>SQLSetCursorName  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|--|--|24000|24000|HY010|HY010|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField 및 SQLSetDescRec  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|--|--|HY010|HY010|  
  
 [1]이 행에는 *FieldIdentifier* 인수가 SQL_DESC_ARRAY_STATUS_PTR 되거나 SQL_DESC_ROWS_PROCESSED_PTR 경우 *DescriptorHandle* 인수가 IPD 인 전환이 나 **SQLSetDescField**의 경우 IRD가 표시 됩니다. *FieldIdentifier* 가 다른 값인 경우 IRD에 대해 **SQLSetDescField** 를 호출 하면 오류가 발생 합니다.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|HY011|HY011|HY011|HY011|Y011|HY01|HY011|  
  
## <a name="sqlsetpos"></a>SQLSetPos  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|HY010|HY010|24000|다음 표 참조|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlsetpos-cursor-states"></a>SQLSetPos (커서 상태)  
  
|S5<br /><br /> 열림|S6<br /><br /> SQLFetch 또는 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|--[s] S8 [d] S11 [x] 24000 [b] HY109 [i]|--[s] S8 [d] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
  
|S0<br /><br /> 할당되지 않음|S1<br /><br /> 할당할|S2-S3<br /><br /> Prepared|S4<br /><br /> 될|S5-S7<br /><br /> 커서|S8-S10<br /><br /> 데이터 필요|S11-S 12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|항목|--|--[1] HY011 [2]|--[1] 24000 [2]|--[1] 24000 [2]|HY010 [np] 또는 [1] HY011 [p] 및 [2]|HY010 [np] 또는 [1] HY011 [p] 및 [2]|  
  
 [1] *특성* 인수가 SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE 또는 SQL_ATTR_CURSOR_SENSITIVITY이 아닙니다.  
  
 [2] *특성* 인수가 SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE 또는 SQL_ATTR_CURSOR_SENSITIVITY입니다.
