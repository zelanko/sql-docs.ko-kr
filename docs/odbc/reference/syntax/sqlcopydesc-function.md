---
title: SQLCopyDesc 함수 | Microsoft Docs
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
- SQLCopyDesc
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCopyDesc
helpviewer_keywords:
- SQLCopyDesc function [ODBC]
ms.assetid: d5450895-3824-44c4-8aa4-d4f9752a9602
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f6afa0af5010989d06b11917c37753825654783f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlcopydesc-function"></a>SQLCopyDesc 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLCopyDesc** 하나의 설명자 핸들에서 설명자 정보 복사 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLCopyDesc(  
     SQLHDESC     SourceDescHandle,  
     SQLHDESC     TargetDescHandle);  
```  
  
## <a name="arguments"></a>인수  
 *SourceDescHandle*  
 [입력] 원본 설명자 핸들입니다.  
  
 *TargetDescHandle*  
 [입력] 대상 설명자 핸들입니다. *TargetDescHandle* 인수는 응용 프로그램 설명자 또는 IPD에 대 한 일 수 있습니다. *TargetDescHandle* IRD에 대 한 핸들을 설정할 수 없습니다 또는 **SQLCopyDesc** SQLSTATE HY016 (구현 행 설명자를 수정할 수 없습니다)를 반환 합니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLCopyDesc** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* SQL_의 HANDLE_DESC 및 *처리* 의 *TargetDescHandle*합니다. 잘못 된 경우 *SourceDescHandle* 전달 된 호출에서 SQL_INVALID_HANDLE 반환 될 하지만 없는 SQLSTATE 반환 됩니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLCopyDesc** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
 오류가 반환 될 때,에 대 한 호출 **SQLCopyDesc** 즉시 중단 됩니다에 있는 필드의 내용과 *TargetDescHandle* 설명자 정의 되지 않습니다.  
  
 때문에 **SQLCopyDesc** 호출 하 여 구현 될 수 있습니다 **SQLGetDescField** 및 **SQLSetDescField**, **SQLCopyDesc** 반환할 수 있습니다 반환 된 Sqlstate **SQLGetDescField** 또는 **SQLSetDescField**합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY007|관련 된 문이 준비 되지 않았습니다.|*SourceDescHandle* IRD, 연관 된 및 관련 된 문 핸들이 준비 또는 실행 된 상태가 아닙니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)에서 처리 된 설명자 *SourceDescHandle* 또는 *TargetDescHandle* 연결 된는 *StatementHandle* 입니다 (not는 비동기적으로 실행 중인 함수 이 중 하나)가 호출 하 고이 함수를 호출할 때 계속 실행 합니다.<br /><br /> (DM)에서 처리 된 설명자 *SourceDescHandle* 또는 *TargetDescHandle* 연결 된 한 *StatementHandle* 를 **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 호출 했으나 SQL_NEED_DATA를 반환 했습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.<br /><br /> DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *SourceDescHandle* 또는 *TargetDescHandle*합니다. 이 비동기 함수 계속 실행 될 때는 **SQLCopyDesc** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 와 관련 된 문 핸들 중 하나에 대해 호출한는 *SourceDescHandle* 또는 *TargetDescHandle* SQL_PARAM_DATA_AVAILABLE를 반환 합니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY016|구현 행 설명자를 수정할 수 없습니다.|*TargetDescHandle* IRD에 연결 되었습니다.|  
|HY021|일관성 없는 설명자 정보|일관성 확인을 하는 동안 체크 설명자 정보 일관 되지 않았습니다. 자세한 내용은 "일관성 검사"의 참조 **SQLSetDescField**합니다.|  
|HY092|잘못 된 특성/옵션 식별자|에 대 한 호출 **SQLCopyDesc** 에 대 한 호출을 묻는 메시지가 표시 **SQLSetDescField**, 하지만  *\*ValuePtr* 에 대해 올바르지 않습니다는 *FieldIdentifier* 인수 *TargetDescHandle*합니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *SourceDescHandle* 또는 *TargetDescHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>설명  
 에 대 한 호출 **SQLCopyDesc** 복사본 원본 설명자 필드 대상 설명자 핸들에 대 한 핸들입니다. 필드는 IPD 또는 응용 프로그램 설명자에만 속하지만 IRD에 복사할 수 있습니다. 응용 프로그램이 나 구현 설명자에서 필드를 복사할 수 있습니다.  
  
 문 핸들 준비 또는 실행 된 상태 이면 있을 경우에 IRD에서 필드를 복사할 수 있습니다. 그렇지 않으면 함수가 반환 SQLSTATE HY007 (관련 된 문이 준비 되지 않았습니다.).  
  
 필드는 문 준비 되었는지 여부는 IPD에서 복사할 수 있습니다. 동적 매개 변수를 포함 하는 SQL 문을 준비 하 고는 IPD의 자동 채우기를 지원 되 고 사용 하는 경우는 IPD은 드라이버에 의해 채워집니다. 때 **SQLCopyDesc** IPD로로 호출 되는 *SourceDescHandle*, 채워진된 필드가 복사 됩니다. IPD의 드라이버에 의해 입력 되지 않으면는 IPD의 원래 필드의 내용은 복사 됩니다.  
  
 대상 설명자에 대해 필드가 정의 되어 있는지 여부 (설명자 핸들이 자동으로 또는 명시적으로 할당 여부를 지정 함)는 SQL_DESC_ALLOC_TYPE 제외 하 고 설명자 필드를 모두 복사 됩니다. 복사한 필드 기존 필드를 덮어씁니다.  
  
 드라이버는 경우 모든 설명자 필드를 복사는 *SourceDescHandle* 및 *TargetDescHandle* 인수는 두 개의 서로 다른 연결에는 드라이버는 경우에 동일한 드라이버와 관련 또는 환경입니다. 경우는 *SourceDescHandle* 및 *TargetDescHandle* 인수는 다른 드라이버와 관련 된, 드라이버 관리자 ODBC 정의 필드를 복사 하지만 드라이버에서 정의 된 필드를 복사 하지 않습니다 또는 필드 설명자의 형식에 대 한 ODBC에는 정의 되지 않습니다.  
  
 에 대 한 호출 **SQLCopyDesc** 오류가 발생 한 경우 즉시 중단 됩니다.  
  
 SQL_DESC_DATA_PTR 필드가 복사 되 면 대상 설명자에서 일관성 확인이 수행 됩니다. 일관성 확인이 실패 하면 SQLSTATE HY021 반환 됩니다 (설명자 정보)에 대 한 호출은 **SQLCopyDesc** 즉시 중단 됩니다. 일관성 검사에 대 한 자세한 내용은 "일관성 검사"의 참조 [SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)합니다.  
  
 다양 한 환경에서 연결을 하는 경우에 설명자 핸들과 연결 전체에서 복사할 수 있습니다. 드라이버 관리자에서 발견 된 원본 서버와 대상 설명자 핸들 두 연결과 동일한 연결에 속하지 않는 드라이버를 별도 속한 구현 하는 경우 **SQLCopyDesc** 는-필드를 수행 하 여 사용 하 여 복사 **SQLGetDescField** 및 **SQLSetDescField**합니다.  
  
 때 **SQLCopyDesc** 로 호출 되는 *SourceDescHandle* 하나의 드라이버에는 및 *TargetDescHandle* 다른 드라이버의 오류 큐에는  *SourceDescHandle* 지워집니다. 이 때문에 발생 **SQLCopyDesc** 이 경우에 대 한 호출에 의해 구현 됩니다 **SQLGetDescField** 및 **SQLSetDescField**합니다.  
  
> [!NOTE]  
>  응용 프로그램 된 명시적으로 할당 된 설명자 핸들에 연결할 수 있습니다는 *StatementHandle*를 호출 하는 대신 **SQLCopyDesc** 한 설명자를 필드 복사 하 합니다. 명시적으로 할당 된 설명자를 다른 연결 될 수 있습니다 *StatementHandle* 동일한 *ConnectionHandle* SQL_ATTR_APP_ROW_DESC 또는 SQL_ATTR_APP_PARAM_DESC 문을 설정 하 여 명시적으로 할당 된 설명자 핸들에 특성입니다. 이 도구를 실행 하는 경우 **SQLCopyDesc** 다른 하나의 설명자의 설명자 필드 값을 복사 하기 위해 호출할 필요는 없습니다. 설명자 핸들와 연결 될 수 없습니다는 *StatementHandle* 다른 *ConnectionHandle*그러나; 설명자 필드 값이 같은에서 사용 하도록 *StatementHandles*다른에 *ConnectionHandles*, **SQLCopyDesc** 을 호출 해야 합니다.  
  
 설명자 헤더 또는 레코드의 필드에 대 한 참조 [SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다. 설명자에 대 한 자세한 내용은 참조 하십시오. [설명자](../../../odbc/reference/develop-app/descriptors.md)합니다.  
  
## <a name="copying-rows-between-tables"></a>테이블 간에 행 복사  
 응용 프로그램 응용 프로그램 수준에서 데이터를 복사 하지 않고 데이터를 한 테이블에서 다른 위치로 복사 될 수 있습니다. 이 위해 응용 프로그램 데이터를 인출 하는 문과 복사본에 데이터를 삽입 하는 문을에 대해 동일한 데이터 버퍼 및 설명자 정보에 바인딩합니다. 응용 프로그램 설명자 (하나의 문으로 카드가 및 다른 APD로 명시적으로 할당 된 설명자 바인딩)을 공유 하 여 또는 사용 하 여이 수행할 수 있습니다 **SQLCopyDesc** 는 카드가 간의 바인딩 복사 하 고 두 개의 문이 APD 합니다. 서로 다른 연결에서 적용 되지만 **SQLCopyDesc** 사용 해야 합니다. 또한 **SQLCopyDesc** 을 IRD 및 IPD 두 개의 문이 사이의 바인딩 복사를 호출 해야 합니다. 에 대 한 호출에 대해 드라이버에서 반환 되는 SQL_ACTIVE_STATEMENTS 정보 형식에 동일한 연결에서 문을 간에 복사할 경우 **SQLGetInfo** 이 작업이 성공 하려면에 대해 1 보다 커야 합니다. (이 아니며 경우 연결을 통해 복사 하는 경우)  
  
### <a name="code-example"></a>코드 예  
 다음 예에서 PartsCopy 테이블로 PartsSource 테이블의 필드를 복사 하는 설명자 작업 사용 됩니다. 행 집합 버퍼로 인출 PartsSource 테이블의 내용을 *hstmt0*합니다. 이러한 값에 INSERT 문의 매개 변수로 사용 *hstmt1* PartsCopy 테이블의 열을 채우기 위해 합니다. 이렇게 하려면의 IRD 필드 *hstmt0* 의 IPD 필드에 복사 됩니다 *hstmt1*, 및의 카드가 필드 *hstmt0* APD의필드에복사*hstmt1*합니다. 사용 하 여 **SQLSetDescField** 특성을 설정 IPD의 DESC_PARAMETER_TYPE을 SQL_PARAM_INPUT IRD 필드에서에서 복사할 출력 매개 변수를 사용 하 여 문을 IPD 필드 입력된 매개 변수 수 있어야 하는 경우.  
  
```  
#define ROWS 100  
#define DESC_LEN 50  
#define SQL_SUCCEEDED(rc) (rc == SQL_SUCCESS || rc == SQL_SUCCESS_WITH_INFO)  
  
// Template for a row  
typedef struct {  
   SQLINTEGER   sPartID;  
   SQLINTEGER   cbPartID;  
   SQLUCHAR     szDescription[DESC_LENGTH];  
   SQLINTEGER   cbDescription;  
   REAL         sPrice;  
   SQLINTEGER   cbPrice;  
} PartsSource;  
  
PartsSource    rget[ROWS];          // rowset buffer  
SQLUSMALLINT   sts_ptr[ROWS];       // status pointer  
SQLHSTMT       hstmt0, hstmt1;  
SQLHDESC       hArd0, hIrd0, hApd1, hIpd1;  
  
// ARD and IRD of hstmt0  
SQLGetStmtAttr(hstmt0, SQL_ATTR_APP_ROW_DESC, &hArd0, 0, NULL);  
SQLGetStmtAttr(hstmt0, SQL_ATTR_IMP_ROW_DESC, &hIrd0, 0, NULL);  
  
// APD and IPD of hstmt1  
SQLGetStmtAttr(hstmt1, SQL_ATTR_APP_PARAM_DESC, &hApd1, 0, NULL);  
SQLGetStmtAttr(hstmt1, SQL_ATTR_IMP_PARAM_DESC, &hIpd1, 0, NULL);  
  
// Use row-wise binding on hstmt0 to fetch rows  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_BIND_TYPE, (SQLPOINTER) sizeof(PartsSource), 0);  
  
// Set rowset size for hstmt0  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER) ROWS, 0);  
  
// Execute a select statement  
SQLExecDirect(hstmt0, "SELECT PARTID, DESCRIPTION, PRICE FROM PARTS ORDER BY 3, 1, 2"",  
               SQL_NTS);  
  
// Bind  
SQLBindCol(hstmt0, 1, SQL_C_SLONG, rget[0].sPartID, 0,   
   &rget[0].cbPartID);  
SQLBindCol(hstmt0, 2, SQL_C_CHAR, &rget[0].szDescription, DESC_LEN,   
   &rget[0].cbDescription);  
SQLBindCol(hstmt0, 3, SQL_C_FLOAT, rget[0].sPrice,   
   0, &rget[0].cbPrice);  
  
// Perform parameter bindings on hstmt1.   
SQLCopyDesc(hArd0, hApd1);  
SQLCopyDesc(hIrd0, hIpd1);  
  
// Set the array status pointer of IRD  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_STATUS_PTR, sts_ptr, SQL_IS_POINTER);  
  
// Set the ARRAY_STATUS_PTR field of APD to be the same  
// as that in IRD.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_PARAM_OPERATION_PTR, sts_ptr, SQL_IS_POINTER);  
  
// Set the hIpd1 records as input parameters  
rc = SQLSetDescField(hIpd1, 1, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
rc = SQLSetDescField(hIpd1, 2, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
rc = SQLSetDescField(hIpd1, 3, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
  
// Prepare an insert statement on hstmt1. PartsCopy is a copy of  
// PartsSource  
SQLPrepare(hstmt1, "INSERT INTO PARTS_COPY VALUES (?, ?, ?)", SQL_NTS);  
  
// In a loop, fetch a rowset, and copy the fetched rowset to PARTS_COPY  
  
rc = SQLFetchScroll(hstmt0, SQL_FETCH_NEXT, 0);  
while (SQL_SUCCEEDED(rc)) {  
  
   // After the call to SQLFetchScroll, the status array has row   
   // statuses. This array is used as input status in the APD  
   // and hence determines which elements of the rowset buffer  
   // are inserted.  
   SQLExecute(hstmt1);  
  
   rc = SQLFetchScroll(hstmt0, SQL_FETCH_NEXT, 0);  
} // while  
```  
  
### <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|여러 설명자 필드 가져오기|[SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|단일 설명자 필드 설정|[SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|여러 설명자 필드 설정|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
