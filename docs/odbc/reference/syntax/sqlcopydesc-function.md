---
title: SQLCopyDesc 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e91febb4b5b94b5a7f9df62347b4db5edcecf975
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259274"
---
# <a name="sqlcopydesc-function"></a>SQLCopyDesc 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLCopyDesc** 다른 하나의 설명자 핸들에서 설명자 정보를 복사 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLCopyDesc(  
     SQLHDESC     SourceDescHandle,  
     SQLHDESC     TargetDescHandle);  
```  
  
## <a name="arguments"></a>인수  
 *SourceDescHandle*  
 [입력] 원본 설명자 핸들입니다.  
  
 *TargetDescHandle*  
 [입력] 대상 설명자 핸들입니다. 합니다 *TargetDescHandle* 인수는 응용 프로그램 설명자 또는 IPD에 대 한 핸들을 사용할 수 있습니다. *TargetDescHandle* IRD에 대 한 핸들을 설정할 수 없습니다 또는 **SQLCopyDesc** SQLSTATE HY016 (구현 행 설명자를 수정할 수 없습니다)를 반환 합니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLCopyDesc** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* SQL_의 HANDLE_DESC와 *처리할* 의 *TargetDescHandle*합니다. 잘못 된 경우 *SourceDescHandle* 전달 된 호출 SQL_INVALID_HANDLE 반환 됩니다 있지만 없습니다 SQLSTATE 반환 됩니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLCopyDesc** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
 오류가 반환 될 때, 호출 **SQLCopyDesc** 즉시 중단 됩니다 및 필드의 콘텐츠를 *TargetDescHandle* 설명자 정의 되지 않습니다.  
  
 때문에 **SQLCopyDesc** 를 호출 하 여 구현 될 수 있습니다 **SQLGetDescField** 하 고 **SQLSetDescField**를 **SQLCopyDesc** 반환할 수 있습니다 반환 된 Sqlstate **SQLGetDescField** 하거나 **SQLSetDescField**합니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY007|연결 된 문이 준비 되지 않았습니다.|*SourceDescHandle* IRD, 연관 된 및 관련된 문 핸들 준비 또는 실행 상태가 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)에서 처리 된 설명자 *SourceDescHandle* 또는 *TargetDescHandle* 연관 된를 *StatementHandle* 입니다는 비동기적으로 실행 중인 함수 (not 이 항목)를 호출한 및이 함수가 호출 되었을 때 계속 실행 합니다.<br /><br /> (DM)에서 처리 된 설명자 *SourceDescHandle* 또는 *TargetDescHandle* 연관 된를 *StatementHandle* 는 **SQLExecute**, **SQLExecDirect**합니다 **SQLBulkOperations**, 또는 **SQLSetPos** 호출 되 고 SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *SourceDescHandle* 하거나 *TargetDescHandle*합니다. 이 비동기 함수가 여전히 실행 시기를 **SQLCopyDesc** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**, 또는 **SQLMoreResults** 관련 된 문 핸들 중 하나에 대해 호출한는 *SourceDescHandle* 나 *TargetDescHandle* SQL_PARAM_DATA_AVAILABLE를 반환 합니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY016|구현 행 설명자를 수정할 수 없습니다.|*TargetDescHandle* IRD와 사용 하 여 연결 합니다.|  
|HY021|일관성이 없는 설명자 정보|일관성 확인 중 선택 설명자 정보를 일관 되지 않았습니다. 자세한 내용은 "일관성 확인"의 참조 **SQLSetDescField**합니다.|  
|HY092|잘못 된 특성/옵션 식별자입니다.|에 대 한 호출 **SQLCopyDesc** 호출 하 라는 메시지가 표시 **SQLSetDescField**, 하지만  *\*ValuePtr* 에 대해 올바르지 않습니다는 *FieldIdentifier* 의 인수 *TargetDescHandle*합니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *SourceDescHandle* 또는 *TargetDescHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 에 대 한 호출 **SQLCopyDesc** 복사 원본 설명자의 필드 대상 설명자 핸들에 대 한 핸들입니다. IRD 아니라 응용 프로그램 설명자를 또는 IPD 필드를 복사할 수 있습니다. 응용 프로그램 또는 구현 설명자 필드를 복사할 수 있습니다.  
  
 문 핸들 준비 또는 실행 상태에 있을 경우에 IRD에서 필드를 복사할 수 있습니다. 그렇지 않으면 함수 반환 SQLSTATE HY007 (관련 된 문이 준비 되지 않았습니다)입니다.  
  
 문이 준비 되었는지 여부는 IPD에서 필드를 복사할 수 있습니다. 동적 매개 변수를 사용 하 여 SQL 문을 준비 하 고 IPD의 자동 채우기를 지원 되 고 사용 하는 경우 IPD은 드라이버에 의해 채워집니다. 때 **SQLCopyDesc** 으로 IPD를 사용 하 여 호출 되는 *SourceDescHandle*, 채워진된 필드가 복사 됩니다. 드라이버에서 IPD 채워져 있지 않으면 IPD의 원래 필드의 내용은 복사 됩니다.  
  
 대상 설명자에 대해 필드가 정의 되어 있는지 여부 (지정 하는 여부를 설명자 핸들을 자동으로 또는 명시적으로 할당 된) SQL_DESC_ALLOC_TYPE 제외 하 고 설명자의 모든 필드가 복사 됩니다. 복사 된 필드는 기존 필드를 덮어씁니다.  
  
 드라이버는 경우 모든 설명자 필드를 복사 합니다 *SourceDescHandle* 하 고 *TargetDescHandle* 인수는 두 개의 서로 다른 연결에서 드라이버는 경우에 동일한 드라이버를 사용 하 여 연결 또는 환경입니다. 경우는 *SourceDescHandle* 하 고 *TargetDescHandle* 인수는 다른 드라이버를 사용 하 여 연결 된, 드라이버 관리자 ODBC 정의 필드를 복사 하지만 드라이버에서 정의 된 필드를 복사 하지 않습니다 또는 필드 형식 설명자에 대해 ODBC에서 정의 되지 않습니다.  
  
 에 대 한 호출 **SQLCopyDesc** 오류가 발생 하면 즉시 중단 됩니다.  
  
 SQL_DESC_DATA_PTR 필드가 복사 되 면 대상 설명자에는 일관성 검사가 수행 됩니다. 일관성 확인이 실패 하면 SQLSTATE HY021 (일관성이 없는 설명자 정보)를 반환 하 고 호출 **SQLCopyDesc** 즉시 중단 됩니다. 일관성 검사에 대 한 자세한 내용은 "일관성 확인"의 참조 [SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)합니다.  
  
 다른 환경에서 연결을 하는 경우에 연결 설명자 핸들을 복사할 수 있습니다. 드라이버 관리자에서 발견 된 원본 및 대상 설명자 핸들 두 연결과 동일한 연결에 속하지 않는 경우이 드라이버를 별도 속한 구현 하는 경우 **SQLCopyDesc** 를-필드를 수행 하 여 사용 하 여 복사할 **SQLGetDescField** 하 고 **SQLSetDescField**합니다.  
  
 때 **SQLCopyDesc** 사용 하 여 호출 되는 *SourceDescHandle* 하나의 드라이버 및 *TargetDescHandle* 오류 큐의 다른 드라이버에서는  *SourceDescHandle* 지워집니다. 이 때문에 발생 **SQLCopyDesc** 를 호출 하 여이 경우에 구현 되 **SQLGetDescField** 및 **SQLSetDescField**합니다.  
  
> [!NOTE]  
>  응용 프로그램을 사용 하 여 명시적으로 할당 된 설명자 핸들을 연결 하는 일을 할 수 있습니다는 *StatementHandle*를 호출 하는 대신 **SQLCopyDesc** 하나의 설명자에서 필드를 다른 컴퓨터로 복사 하려면. 명시적으로 할당 된 설명자를 상호 연결할 수 있습니다 *StatementHandle* 동일한 *ConnectionHandle* SQL_ATTR_APP_ROW_DESC 또는 SQL_ATTR_APP_PARAM_DESC 문을 설정 하 여 특성의 명시적으로 할당 된 설명자 핸들입니다. 이 작업을 마치면 **SQLCopyDesc** 다른 하나의 설명자에서 설명자 필드 값을 복사 하기 위해 호출할 필요가 없습니다. 설명자 핸들을 사용 하 여 연결할 수 없습니다는 *StatementHandle* 다른 *ConnectionHandle*그러나;에서 동일한 설명자 필드 값을 사용 하도록 *StatementHandles*여러 *ConnectionHandles*합니다 **SQLCopyDesc** 을 호출 해야 합니다.  
  
 설명자 헤더 또는 레코드의 필드 설명을 참조 하세요 [SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다. 설명자에 대 한 자세한 내용은 참조 하세요. [설명자](../../../odbc/reference/develop-app/descriptors.md)합니다.  
  
## <a name="copying-rows-between-tables"></a>테이블 간에 행 복사  
 응용 프로그램 응용 프로그램 수준에서 데이터를 복사 하지 않고 데이터를 하나의 테이블에서 다른 위치로 복사할 수 있습니다. 이렇게 하려면 응용 프로그램 데이터를 인출 하는 설명서와 데이터 복사본을 삽입 하는 설명서를 동일한 데이터 버퍼 및 설명자 정보를 바인딩합니다. (하나의 문으로 카드가 및 다른 APD로 명시적으로 할당 된 설명자를 바인딩) 응용 프로그램 설명자를 공유 하 여 또는 사용 하 여 수행할 수 있습니다 **SQLCopyDesc** 는 카드가 간의 바인딩에 복사 하 고 두 개의 문이 APD 합니다. 다른 연결에 적용 되지만 **SQLCopyDesc** 사용 해야 합니다. 또한 **SQLCopyDesc** IRD 및 IPD 두 개의 문이 간의 바인딩에 복사할 호출 되어야 합니다. 에 대 한 호출에 대 한 드라이버에 의해 반환 되는 SQL_ACTIVE_STATEMENTS 정보 형식에서 같은 연결에서 문을 복사 하는 경우 **SQLGetInfo** 이 작업을 수행 하려면 1 보다 커야 합니다. (이 경우 되지 경우 연결을 통해 복사 하는 경우)  
  
### <a name="code-example"></a>코드 예  
 다음 예에서 설명자 작업 PartsSource 테이블의 필드 PartsCopy 테이블로 복사할 사용 됩니다. PartsSource 테이블의 내용에서 행 집합 버퍼로 인출 *hstmt0*합니다. 이러한 값에 INSERT 문의 매개 변수로 사용 됩니다 *hstmt1* PartsCopy 테이블의 열을 채우기 위해. 이렇게 하려면의 IRD 필드 *hstmt0* 의 IPD 필드에 복사 됩니다 *hstmt1*, 및의 카드가 필드 *hstmt0* APD의필드에복사됩니다*hstmt1*합니다. 사용 하 여 **SQLSetDescField** 특성을 설정 IPD의 DESC_PARAMETER_TYPE을 SQL_PARAM_INPUT IRD 필드에서에서 복사할 출력 매개 변수를 사용 하 여 문을 IPD 필드 입력된 매개 변수를 해야 하는 경우.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
