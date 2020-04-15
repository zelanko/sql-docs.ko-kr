---
title: SQLCopyDesc 함수 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef1fa5b319e8d72d5b70e6f2010e493eec6f844a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301230"
---
# <a name="sqlcopydesc-function"></a>SQLCopyDesc 함수
**규칙**  
 버전 출시: ODBC 3.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLCopyDesc는** 한 설명자 핸들에서 다른 설명자 핸들로 설명자 정보를 복사합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLCopyDesc(  
     SQLHDESC     SourceDescHandle,  
     SQLHDESC     TargetDescHandle);  
```  
  
## <a name="arguments"></a>인수  
 *소스데스크핸들*  
 [입력] 소스 설명자 핸들입니다.  
  
 *대상데스크핸들*  
 [입력] 대상 설명자 핸들입니다. *TargetDescHandle* 인수는 응용 프로그램 설명자 또는 IPD에 대한 핸들일 수 있습니다. *TargetDescHandle* IRD에 핸들로 설정할 수 없습니다 또는 **SQLCopyDesc SQLSTATE** HY016을 반환 합니다 (구현 행 설명기를 수정할 수 없습니다).  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLCopyDescSQL_ERROR** 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우, SQL_HANDLE_DESC *핸들 유형* 및 *TargetDescHandle의* *핸들을* 사용하는 **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 얻을 수 있습니다. 잘못된 *SourceDescHandle호출에서* 전달된 경우 SQL_INVALID_HANDLE 반환되지만 SQLSTATE는 반환되지 않습니다. 다음 표에서는 **SQLCopyDesc에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
 오류가 반환되면 **SQLCopyDesc에** 대한 호출이 즉시 중단되고 *TargetDescHandle* 설명자의 필드 내용이 정의되지 않습니다.  
  
 **SQLCopyDesc는** **SQLGetDescField** 및 **SQLSetDescField를**호출하여 구현 될 수 있기 때문에 **SQLCDesc는** **SQLGetDescField** 또는 **SQLSetDescField에서**반환된 SQLSTATEs를 반환할 수 있습니다.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY007|관련 문이 준비되지 않았습니다.|*SourceDescHandleIRD와* 연결 되 고 관련 된 문 핸들 준비 또는 실행 된 상태에 있지 않았습니다.|  
|HY010|함수 시퀀스 오류|(DM) *SourceDescHandle* 또는 *TargetDescHandle의* 설명자 핸들은 비동기적으로 실행되는 함수(이 함수가 아님)가 호출되고 이 함수가 호출될 때 여전히 실행 중인 *StatementHandle과* 연결되었습니다.<br /><br /> (DM) *SourceDescHandle* 또는 *TargetDescHandle의* 설명자 핸들은 **SQLExecute,** **SQLExecDirect**, **SQLBulkOperations**또는 **SQLSetPos가** 호출되어 반환된 *문핸들과* SQL_NEED_DATA 연결되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.<br /><br /> (DM) *SourceDescHandle* 또는 *TargetDescHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. 이 비동기 함수는 **SQLCopyDesc** 함수가 호출될 때 계속 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *SourceDescHandle* 또는 *TargetDescHandle과* 연결된 명령문 핸들 중 하나를 호출하고 반환 된 SQL_PARAM_DATA_AVAILABLE. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY016|구현 행 설명자 수정할 수 없습니다.|*TargetDesc핸들은* IRD와 연결되었습니다.|  
|HY021|일관되지 않은 설명자 정보|일관성 검사 중에 확인된 설명자 정보가 일치하지 않았습니다. 자세한 내용은 **SQLSetDescField의**"일관성 검사"를 참조하십시오.|  
|HY092|잘못된 특성/옵션 식별자|**SQLCopyDesc에** 대한 호출은 **SQLSetDescField에**대한 호출을 요청했지만 * \*ValuePtr은* *TargetDescHandle*의 *필드 식별자* 인수에 대해 유효하지 않습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *SourceDescHandle* 또는 *TargetDescHandle과* 연결된 드라이버는 기능을 지원하지 않습니다.|  
  
## <a name="comments"></a>주석  
 **SQLCopyDesc에** 대 한 호출 대상 설명자 핸들에 소스 설명자 핸들의 필드를 복사 합니다. 필드는 응용 프로그램 설명자 또는 IPD에만 복사할 수 있지만 IRD에는 복사할 수 없습니다. 필드는 응용 프로그램 또는 구현 설명자에서 복사할 수 있습니다.  
  
 필드 핸들이 준비되거나 실행된 상태에 있는 경우에만 IRD에서 필드를 복사할 수 있습니다. 그렇지 않으면 함수가 SQLSTATE HY007을 반환합니다(연결된 문은 준비되지 않음).  
  
 명령문이 준비되었는지 여부에 관계없이 IPD에서 필드를 복사할 수 있습니다. 동적 매개 변수가 있는 SQL 문이 준비되고 IPD의 자동 채우기가 지원되고 활성화된 경우 IPD가 드라이버에 의해 채워집니다. **SQLCopyDesc이** *IPD를 소스데스코핸들로*호출하면 채워진 필드가 복사됩니다. IPD가 드라이버에 의해 채워지지 않으면 원래 IPD에 있는 필드의 내용이 복사됩니다.  
  
 SQL_DESC_ALLOC_TYPE(설명자 핸들이 자동으로 할당되었는지 또는 명시적으로 할당되었는지 여부를 지정함)을 제외한 설명자의 모든 필드는 대상 설명자에 대해 필드가 정의되었는지 여부에 관계없이 복사됩니다. 복사된 필드는 기존 필드를 덮어씁니다.  
  
 드라이버는 드라이버가 두 개의 서로 다른 연결 또는 환경에 있는 경우에도 *SourceDescHandle* 및 *TargetDescHandle* 인수가 동일한 드라이버와 연결된 경우 모든 설명자 필드를 복사합니다. *SourceDescHandle* 및 *TargetDescHandle* 인수가 다른 드라이버와 연결되어 있는 경우 드라이버 관리자는 ODBC 정의 필드를 복사하지만 설명자 유형에 대해 ODBC에 의해 정의되지 않은 드라이버 정의 필드 또는 필드를 복사하지 않습니다.  
  
 오류가 발생하면 **SQLCopyDesc** 에 대한 호출이 즉시 중단됩니다.  
  
 SQL_DESC_DATA_PTR 필드가 복사되면 대상 설명자에서 일관성 검사가 수행됩니다. 일관성 검사가 실패하면 SQLSTATE HY021(일관되지 않은 설명자 정보)이 반환되고 **SQLCopyDesc에** 대한 호출이 즉시 중단됩니다. 일관성 검사에 대한 자세한 내용은 [SQLSetDescRec 함수의](../../../odbc/reference/syntax/sqlsetdescrec-function.md)"일관성 검사"를 참조하십시오.  
  
 설명자 핸들은 연결이 서로 다른 환경에 있는 경우에도 연결 간에 복사할 수 있습니다. 드라이버 관리자가 원본 및 대상 설명자 핸들이 동일한 연결에 속하지 않고 두 연결이 별도의 드라이버에 속하는 것을 감지하면 **SQLGetDescField** 및 **SQLSetDescField를**사용하여 필드별 복사본을 수행하여 **SQLCopyDesc을** 구현합니다.  
  
 **SQLCopyDesc가** 한 드라이버의 *SourceDescHandle을* 사용하이고 다른 드라이버의 *TargetDescHandle을* 사용하면 *SourceDescHandle의* 오류 큐가 지워집니다. 이 경우 **SQLCopyDesc은** **SQLGetDescField** 및 **SQLSetDescField**에 대한 호출에 의해 구현되기 때문에 발생합니다.  
  
> [!NOTE]  
>  응용 프로그램은 **SQLCopyDesc을** 호출하여 한 설명자에서 다른 설명자로 필드를 복사하는 대신 명시적으로 할당된 설명자 핸들을 *StatementHandle과*연결할 수 있습니다. 명시적으로 할당된 설명자는 명시적으로 할당된 설명자의 핸들에 SQL_ATTR_APP_ROW_DESC 또는 SQL_ATTR_APP_PARAM_DESC 문 특성을 설정하여 동일한 *ConnectionHandle의* 다른 *StatementHandle과* 연결할 수 있습니다. 이 작업이 완료되면 **SQLCopyDesc은** 설명자 필드 값을 한 설명자에서 다른 설명자로 복사하기 위해 호출할 필요가 없습니다. 그러나 설명자 핸들은 다른 *ConnectionHandle의 StatementHandle과* 연결할 수 없습니다. *ConnectionHandle* 다른 *연결 핸들에* *문 핸들에* 동일한 설명자 필드 값을 사용 하려면 **SQLCopyDesc** 호출 해야 합니다.  
  
 설명자 헤더 또는 레코드의 필드에 대한 설명은 [SQLSetDescField 함수를](../../../odbc/reference/syntax/sqlsetdescfield-function.md)참조하십시오. 설명자에 대한 자세한 내용은 [설명자](../../../odbc/reference/develop-app/descriptors.md)를 참조하십시오.  
  
## <a name="copying-rows-between-tables"></a>테이블 간에 행 복사  
 응용 프로그램은 응용 프로그램 수준에서 데이터를 복사하지 않고 한 테이블에서 다른 테이블로 데이터를 복사할 수 있습니다. 이렇게 하려면 응용 프로그램은 데이터를 가져오는 명령문과 데이터를 복사본에 삽입하는 문에 동일한 데이터 버퍼 및 설명자 정보를 바인딩합니다. 이 작업은 응용 프로그램 설명자를 공유하거나(명시적으로 할당된 설명자를 ARD와 다른 명령문에 ARD로 바인딩) 또는 **SQLCopyDesc를** 사용하여 두 명령문의 ARD와 APD 간의 바인딩을 복사하여 수행할 수 있습니다. 명령문이 다른 연결에 있는 경우 **SQLCopyDesc를** 사용해야 합니다. 또한 **SQLCopyDesc은** 두 명령문의 IRD와 IPD 사이의 바인딩을 복사하기 위해 호출되어야 합니다. 동일한 연결에서 문을 복사할 때 이 작업이 성공하려면 **드라이버가 SQLGetInfo** 를 호출하기 위해 반환하는 SQL_ACTIVE_STATEMENTS 정보 형식이 1보다 커야 합니다. (연결을 가로질러 복사할 때는 그렇지 않습니다.)  
  
### <a name="code-example"></a>코드 예  
 다음 예제에서는 설명자 작업을 사용하여 PartsSource 테이블의 필드를 PartsCopy 테이블에 복사합니다. PartsSource 테이블의 내용은 *hstmt0의*행 집합 버퍼로 가져옵니다. 이러한 값은 partsCopy 테이블의 열을 채우기 위해 *hstmt1에서* INSERT 문의 매개 변수로 사용됩니다. 이렇게 하려면 *hstmt0의* IRD 필드가 *hstmt1의*IPD 필드에 복사되고 *hstmt0의* ARD 필드가 *hstmt1의*APD 필드에 복사됩니다. **SQLSetDescField를** 사용하여 출력 매개 변수가 있는 문에서 입력 매개 변수가 필요한 IPD 필드로 IRD 필드를 복사할 때 IPD의 SQL_DESC_PARAMETER_TYPE 특성을 SQL_PARAM_INPUT 설정합니다.  
  
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
  
|원하는 정보|참조|  
|---------------------------|---------|  
|여러 설명자 필드 얻기|[SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|단일 설명자 필드 설정|[SQLSetDesc필드 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|여러 설명자 필드 설정|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
