---
title: SQLCopyDesc 함수 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCopyDesc
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLCopyDesc
helpviewer_keywords:
- SQLCopyDesc function [ODBC]
ms.assetid: d5450895-3824-44c4-8aa4-d4f9752a9602
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8aec6dc776f5fdd84932be089e9503f0083a49c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68345484"
---
# <a name="sqlcopydesc-function"></a>SQLCopyDesc 함수
**규칙**  
 소개 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **Sqlcopydesc** 는 한 설명자 핸들에서 다른 설명자 핸들로 설명자 정보를 복사 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLCopyDesc(  
     SQLHDESC     SourceDescHandle,  
     SQLHDESC     TargetDescHandle);  
```  
  
## <a name="arguments"></a>인수  
 *SourceDescHandle*  
 입력 원본 설명자 핸들입니다.  
  
 *TargetDescHandle*  
 입력 대상 설명자 핸들입니다. *TargetDescHandle* 인수는 응용 프로그램 설명자 또는 IPD에 대 한 핸들 일 수 있습니다. *TargetDescHandle* 는 IRD에 대 한 핸들로 설정할 수 없으며 **SQLCOPYDESC** 는 SQLSTATE HY016를 반환 합니다 (구현 행 설명자를 수정할 수 없음).  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlcopydesc** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 *HandleType* SQL_HANDLE_DESC의 및 *TargetDescHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 가져올 수 있습니다. 호출에 잘못 된 *SourceDescHandle* 이 전달 된 경우 SQL_INVALID_HANDLE가 반환 되지만 SQLSTATE는 반환 되지 않습니다. 다음 표에서는 **Sqlcopydesc** 에서 일반적으로 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
 오류가 반환 되 면 **Sqlcopydesc** 호출이 즉시 중단 되 고 *TargetDescHandle* 설명자의 필드 내용이 정의 되지 않습니다.  
  
 **SQLGetDescField** 및 **SQLSetDescField**를 호출 하 여 **sqlcopydesc** 를 구현할 수 있으므로 **sqlcopydesc** 는 **SQLGetDescField** 또는 **SQLSetDescField**에서 반환 된 sqlstates를 반환할 수 있습니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버가 실행 또는 함수의 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY007|연결 된 문이 준비 되지 않았습니다.|*SourceDescHandle* 가 IRD와 연결 되어 있고 연결 된 문 핸들이 준비 됨 또는 실행 됨 상태가 아닙니다.|  
|HY010|함수 시퀀스 오류|(DM) *SourceDescHandle* 또는 *TargetDescHandle* 의 설명자 핸들이이 함수를 호출 했을 때 비동기적으로 실행 되는 함수 (이 함수는 아님)가 호출 되었으며 아직 실행 중 이었던 *StatementHandle* 와 연결 되었습니다.<br /><br /> (DM) *SourceDescHandle* 또는 *TargetDescHandle* 의 설명자 핸들이 **sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 호출 되 고 SQL_NEED_DATA 반환 된 *StatementHandle* 와 연결 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.<br /><br /> (DM) *SourceDescHandle* 또는 *TargetDescHandle*와 연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. 이 비동기 함수는 **Sqlcopydesc** 함수가 호출 될 때 실행 되 고 있습니다.<br /><br /> (DM) **Sqlexecute**, **Sqlexecdirect**또는 **SQLMoreResults** 가 *SourceDescHandle* 또는 *TargetDescHandle* 와 연결 된 문 핸들 중 하나에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY016|구현 행 설명자를 수정할 수 없습니다.|*TargetDescHandle* 가 IRD와 연결 되었습니다.|  
|HY021|일관 되지 않은 설명자 정보|일관성 확인 중에 확인 된 설명자 정보가 일치 하지 않습니다. 자세한 내용은 **SQLSetDescField**의 "일관성 검사"를 참조 하세요.|  
|HY092|특성/옵션 식별자가 잘못 되었습니다.|**Sqlcopydesc** 호출에서 **SQLSetDescField**을 호출 하 라는 메시지가 * \*표시 되지만,* *TargetDescHandle*의 *FieldIdentifier* 인수에는 인수를 사용할 수 없습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *SourceDescHandle* 또는 *TargetDescHandle* 와 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 **Sqlcopydesc** 호출은 소스 설명자 핸들의 필드를 대상 설명자 핸들에 복사 합니다. 필드는 응용 프로그램 설명자 또는 IPD 복사할 수 있지만 IRD에 복사할 수는 없습니다. 응용 프로그램 또는 구현 설명자에서 필드를 복사할 수 있습니다.  
  
 문 핸들이 준비 됨 또는 실행 됨 상태인 경우에만 IRD에서 필드를 복사할 수 있습니다. 그렇지 않으면이 함수는 SQLSTATE HY007 (연결 된 문은 준비 되지 않음)를 반환 합니다.  
  
 문이 준비 되었는지 여부에 관계 없이 IPD에서 필드를 복사할 수 있습니다. 동적 매개 변수가 있는 SQL 문을 준비 하 고 IPD 자동 채우기를 지원 하 고 사용 하도록 설정 하면 IPD가 드라이버에 의해 채워집니다. IPD를 *SourceDescHandle*로 사용 하 여 **sqlcopydesc** 를 호출 하면 채워진 필드가 복사 됩니다. IPD 드라이버가 채워져 있지 않으면 원래 IPD에 있는 필드의 내용이 복사 됩니다.  
  
 설명자의 모든 필드 (설명자 핸들을 자동 또는 명시적으로 할당 했는지 여부를 지정 하는 SQL_DESC_ALLOC_TYPE 제외)는 대상 설명자에 대해 정의 되어 있는지 여부에 관계 없이 복사 됩니다. 복사 된 필드는 기존 필드를 덮어씁니다.  
  
 드라이버가 서로 다른 두 연결 또는 환경에 있는 경우에도 *SourceDescHandle* 및 *TargetDescHandle* 인수가 동일한 드라이버와 연결 된 경우 드라이버는 모든 설명자 필드를 복사 합니다. *SourceDescHandle* 및 *TargetDescHandle* 인수가 다른 드라이버와 연결 된 경우 드라이버 관리자는 odbc 정의 필드를 복사 하지만 설명자 유형에 대해 odbc에서 정의 되지 않은 필드 또는 드라이버 정의 필드는 복사 하지 않습니다.  
  
 오류가 발생 하면 **Sqlcopydesc** 호출이 즉시 중단 됩니다.  
  
 SQL_DESC_DATA_PTR 필드가 복사 되 면 대상 설명자에 대해 일관성 확인이 수행 됩니다. 일관성 확인이 실패 하면 SQLSTATE HY021 (일치 하지 않는 설명자 정보)가 반환 되 고 **Sqlcopydesc** 호출이 즉시 중단 됩니다. 일관성 확인에 대 한 자세한 내용은 [SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)에서 "일관성 검사"를 참조 하세요.  
  
 연결이 다른 환경에 있는 경우에도 연결 간에 설명자 핸들을 복사할 수 있습니다. 드라이버 관리자에서 원본 및 대상 설명자 핸들이 동일한 연결에 속하지 않고 두 연결이 별도의 드라이버에 속해 있음을 감지 하면 **SQLGetDescField** 및 **SQLSetDescField**를 사용 하 여 필드별 복사를 수행 하 여 **sqlcopydesc** 를 구현 합니다.  
  
 한 드라이버에서 *SourceDescHandle* 를 사용 하 여 **sqlcopydesc** 를 호출 하 고 다른 드라이버의 *TargetDescHandle* 를 호출 하면 *SourceDescHandle* 의 오류 큐가 지워집니다. 이 경우 **Sqlcopydesc** 는 **SQLGetDescField** 및 **SQLSetDescField**를 호출 하 여 구현 되기 때문에 발생 합니다.  
  
> [!NOTE]  
>  응용 프로그램은 **Sqlcopydesc** 를 호출 하 여 한 설명자에서 다른 설명자로 필드를 복사 하는 대신 명시적으로 할당 된 설명자 핸들을 *StatementHandle*와 연결할 수 있습니다. 명시적으로 할당 된 설명자는 SQL_ATTR_APP_ROW_DESC 또는 SQL_ATTR_APP_PARAM_DESC statement 특성을 명시적으로 할당 된 설명자의 핸들로 설정 하 여 동일한 *ConnectionHandle* 에 있는 다른 *StatementHandle* 연결 될 수 있습니다. 이 작업이 완료 되 면 설명자 필드 값을 한 설명자에서 다른 설명자로 복사 하기 위해 **Sqlcopydesc** 를 호출할 필요가 없습니다. 그러나 설명자 핸들을 다른 *ConnectionHandle*의 *StatementHandle* 에 연결할 수는 없습니다. 서로 다른 *Connectionhandles*에서 *StatementHandles* 의 동일한 설명자 필드 값을 사용 하려면 **sqlcopydesc** 를 호출 해야 합니다.  
  
 설명자 헤더 또는 레코드의 필드에 대 한 설명은 [SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)를 참조 하세요. 설명자에 대 한 자세한 내용은 [설명자](../../../odbc/reference/develop-app/descriptors.md)를 참조 하십시오.  
  
## <a name="copying-rows-between-tables"></a>테이블 간 행 복사  
 응용 프로그램은 응용 프로그램 수준에서 데이터를 복사 하지 않고 한 테이블에서 다른 테이블로 데이터를 복사할 수 있습니다. 이렇게 하기 위해 응용 프로그램은 데이터를 인출 하는 문과 데이터를 복사본에 삽입 하는 문에 동일한 데이터 버퍼 및 설명자 정보를 바인딩합니다. 이를 위해서는 응용 프로그램 설명자를 공유 하거나 (명시적으로 할당 된 설명자를 다른 문과 APD에 둘 다로 바인딩) **Sqlcopydesc** 를 사용 하 여 두 문의 고와 apd 사이에 있는 바인딩을 복사 하면 됩니다. 문이 다른 연결에 있으면 **Sqlcopydesc** 를 사용 해야 합니다. 또한 IRD와 두 문의 IPD 간에 바인딩을 복사 하기 위해 **Sqlcopydesc** 를 호출 해야 합니다. 동일한 연결에서 문 간에 복사 하는 경우,이 작업이 성공 하려면 **SQLGetInfo** 호출을 위해 드라이버에서 반환 된 SQL_ACTIVE_STATEMENTS 정보 형식이 1 보다 커야 합니다. 연결 간에 복사 하는 경우는 그렇지 않습니다.  
  
### <a name="code-example"></a>코드 예  
 다음 예에서는 설명자 작업을 사용 하 여 PartsSource 테이블의 필드를 PartsCopy 테이블에 복사 합니다. PartsSource 테이블의 내용은 *hstmt0*의 행 집합 버퍼로 인출 됩니다. 이러한 값은 PartsCopy 테이블의 열을 채우기 위해 *hstmt1* 에 대 한 INSERT 문의 매개 변수로 사용 됩니다. 이렇게 하기 위해 hstmt0의 IRD 필드는 *hstmt1*의 IPD 필드에 복사 되 고 *hstmt0* 의 ** 필드는 *hstmt1*의 apd 필드에 복사 됩니다. **SQLSetDescField** 를 사용 하 여 출력 매개 변수가 있는 문에서 입력 매개 변수가 필요한 IPD 필드로 IRD 필드를 복사할 때 IPD의 SQL_DESC_PARAMETER_TYPE 특성을 SQL_PARAM_INPUT로 설정 합니다.  
  
```cpp  
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
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|여러 설명자 필드 가져오기|[SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|단일 설명자 필드 설정|[SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|여러 설명자 필드 설정|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
