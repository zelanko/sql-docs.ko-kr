---
title: SQLSetStmtAttr 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetStmtAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetStmtAttr
helpviewer_keywords:
- SQLSetStmtAttr function [ODBC]
ms.assetid: 7abc5260-733a-48d4-9974-2d1a6a9ea5f6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dfbd2144e677d053f6154dfb3a1df1f6c25d9da5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287269"
---
# <a name="sqlsetstmtattr-function"></a>SQLSetStmtAttr 함수
**규칙**  
 버전 출시: ODBC 3.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLSetStmtAttr** 는 명령문과 관련된 특성을 설정합니다.  
  
> [!NOTE]
>  ODBC *3.x* 응용 프로그램이 ODBC *2.x* 드라이버로 작업할 때 드라이버 관리자가 이 함수를 매핑하는 작업에 대한 자세한 내용은 [응용 프로그램의 이전 버전과의 호환성에 대한 매핑 교체 함수를](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLSetStmtAttr(  
     SQLHSTMT      StatementHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *특성*  
 [입력] "주석"에 나열된 설정 옵션입니다.  
  
 *ValuePtr*  
 [입력] *속성*에 연결할 값입니다. *속성의*값에 따라 *ValuePtr은* 다음 중 하나가 됩니다.  
  
-   ODBC 설명자 핸들입니다.  
  
-   SQLUINTEGER 값입니다.  
  
-   SQLULEN 값입니다.  
  
-   다음 중 하나에 대한 포인터:  
  
    -   null 종료된 문자 문자열입니다.  
  
    -   이진 버퍼입니다.  
  
    -   SQLLEN, SQLULEN 또는 SQLUSMALLINT 형식의 값 또는 배열입니다.  
  
    -   드라이버 정의 값입니다.  
  
 *특성* 인수가 드라이버 관련 값인 경우 *ValuePtr은* 서명된 정수일 수 있습니다.  
  
 *문자열 길이*  
 [입력] *특성이* ODBC 정의 특성이고 *ValuePtr이* 문자 문자열 또는 이진 버퍼를 가리키는 \*경우 이 인수는 *ValuePtr*의 길이여야 합니다. *특성이* ODBC 정의 특성이고 *ValuePtr이* 정수인 경우 *StringLength는* 무시됩니다.  
  
 *특성이* 드라이버 정의 특성인 경우 응용 프로그램은 *StringLength* 인수를 설정하여 드라이버 관리자에 대한 특성의 특성을 나타냅니다. *StringLength에는* 다음 값이 있을 수 있습니다.  
  
-   *ValuePtr이* 문자열 문자열에 대한 포인터인 경우 *StringLength는* 문자열 또는 SQL_NTS 길이입니다.  
  
-   *ValuePtr이* 이진 버퍼에 대한 포인터인 경우 응용 프로그램은 *stringLength에**SQL_LEN_BINARY_ATTR(길이)* 매크로의 결과를 배치합니다. 그러면 *문자열Length에*음수 값이 배치됩니다.  
  
-   *ValuePtr이* 문자열 또는 이진 문자열 이외 값에 대한 포인터인 경우 *StringLength는* SQL_IS_POINTER 값을 가져야 합니다.  
  
-   *ValuePtr* 고정 길이 값을 포함 하는 경우 *StringLength는* SQL_IS_INTEGER 또는 SQL_IS_UINTEGER 적절 하 게.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLSetStmtAttr** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 관련 된 SQLSTATE 값 SQL_HANDLE_STMT *핸들 유형* 및 *명령문* *핸들* 핸들을 호출 하 여 **SQLGetDiagRec를** 호출 하 여 가져올 수 있습니다. 다음 표에서는 **SQLSetStmtAttr에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01S02|옵션 값이 변경되었습니다.|드라이버는 *ValuePtr에*지정된 값을 지원하지 않거나 *ValuePtr에* 지정된 값이 구현 작업 조건으로 인해 유효하지 않으므로 드라이버가 비슷한 값을 대체했습니다. **(SQLGetStmtAttr** 일시적으로 대체 된 값을 결정 하기 위해 호출할 수 있습니다.) 대체 값은 커서가 닫혀있을 때까지 *StatementHandle에* 대해 유효하며, 이 때 문 특성이 이전 값으로 되돌아갑니다. 변경할 수 있는 문 특성은 다음과 같습니다.<br /><br /> SQL_ SQL_ SQL_ SQL_ SQL_ SQL_ SQL_ SQL_ SQL_ SQL_ SQL_ SQL_ SQL_ SQL_ SQL_ATTR_ROW_ARRAY_SIZE ATTR_QUERY_TIMEOUT ATTR_MAX_ROWS ATTR_MAX_LENGTH SQL_ ATTR_KEYSET_SIZE ATTR_CURSOR_TYPE SQL_ SQL_ SQL_ ATTR_SIMULATE_CURSOR ATTR_CONCURRENCY.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|24000|잘못된 커서 상태|*속성이* SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR 또는 SQL_ATTR_USE_BOOKMARKS 커서가 열려 있습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY09|null 포인터의 잘못된 사용|*특성* 인수는 문자열 특성이 필요한 문 특성을 식별했으며 *ValuePtr* 인수는 null 포인터였습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. **SQLSetStmtAttr** 함수가 호출될 때 이 비동기 함수는 여전히 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 *함수는 StatementHandle에* 대 한 호출 하 고이 함수를 호출 하는 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY011|특성을 지금 설정할 수 없습니다.|*속성은* ATTR_CURSOR_TYPE, SQL_ ATTR_SIMULATE_CURSOR 또는 SQL_ ATTR_USE_BOOKMARKS SQL_ SQL_ATTR_CONCURRENCY, 문작성되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY017|자동으로 할당된 설명자 핸들의 잘못된 사용|(DM) *특성* 인수가 SQL_ATTR_IMP_ROW_DESC 또는 SQL_ATTR_IMP_PARAM_DESC.<br /><br /> (DM) *특성* 인수가 SQL_ATTR_APP_ROW_DESC 또는 SQL_ATTR_APP_PARAM_DESC *값은* ARD 또는 APD에 대해 원래 할당된 핸들이 아닌 암시적으로 할당된 설명자 핸들입니다.|  
|HY024|잘못된 특성 값|지정된 *특성* 값이 주어지면 *값Ptr*에 잘못된 값이 지정되었습니다. 드라이버 관리자는 SQL_ATTR_ACCESS_MODE 또는 SQL_ ATTR_ASYNC_ENABLE 같은 개별 값 집합을 허용하는 연결 및 명령문 특성에 대해서만 이 SQLSTATE를 반환합니다. 다른 모든 연결 및 문 특성의 경우 드라이버는 *ValuePtr에*지정된 값을 확인해야 합니다.)<br /><br /> *특성* 인수가 SQL_ATTR_APP_ROW_DESC SQL_ATTR_APP_PARAM_DESC *값Ptr은* *StatementHandle* 인수와 동일한 연결에 없는 명시적으로 할당된 설명자 핸들입니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) * \*ValuePtr은* 문자 문자열이며 *StringLength* 인수는 0보다 작지만 SQL_NTS 않았습니다.|  
|HY092|잘못된 특성/옵션 식별자|(DM) 인수 *특성에* 대해 지정된 값이 드라이버에서 지원하는 ODBC 버전에 대해 유효하지 않습니다.<br /><br /> (DM) 인수 *특성에* 대해 지정된 값은 읽기 전용 특성입니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|인수 *특성에* 대해 지정된 값은 드라이버에서 지원하는 ODBC 버전에 대한 유효한 ODBC 문 특성이지만 드라이버에서 지원되지 않았습니다.<br /><br /> *특성* 인수가 SQL_ATTR_ASYNC_ENABLE 및 *SQL_ASYNC_MODE SQL_ASYNC_MODE 인* **SQLGetInfo호출이** SQL_AM_CONNECTION 반환합니다.<br /><br /> *특성* 인수가 SQL_ATTR_ENABLE_AUTO_IPD SQL_ATTR_AUTO_IPD 연결 특성의 값은 SQL_FALSE.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
|S1118|드라이버가 비동기 알림을 지원하지 않습니다.|SQL_ATTR_ASYNC_STMT_EVENT 설정하는 **SQLSetStmtAttr을** 호출하는 경우; 비동기 알림은 드라이버에서 지원되지 않습니다.|  
  
## <a name="comments"></a>주석  
 **SQLSetStmtAttr에** 대한 다른 호출에 의해 변경되거나 **SQLFreeHandle**을 호출하여 명령문이 삭제될 때까지 명령문에 대한 명령문 특성은 그대로 유지됩니다. SQL_CLOSE, SQL_UNBIND 또는 SQL_RESET_PARAMS 옵션을 사용 하 여 **SQLFreeStmt를** 호출 하지 않습니다 문 특성을 재설정 하지 않습니다.  
  
 일부 문 특성은 데이터 원본이 *ValuePtr*에 지정된 값을 지원하지 않는 경우 유사한 값의 대체를 지원합니다. 이러한 경우 드라이버는 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01S02(옵션 값이 변경)를 반환합니다. 예를 들어 *특성이* SQL_ATTR_CONCURRENCY 있고 *ValuePtr이* SQL_CONCUR_ROWVER 데이터 원본이 이를 지원하지 않는 경우 드라이버는 SQL_CONCUR_VALUES 대체하고 SQL_SUCCESS_WITH_INFO 반환합니다. 대체 값을 결정하기 위해 응용 프로그램은 **SQLGetStmtAttr**을 호출합니다.  
  
 *ValuePtr을* 사용하면 설정된 정보 형식은 지정된 *특성에*따라 다릅니다. **SQLSetStmtAttr는** 문자 문자열 또는 정수 값의 두 가지 형식 중 하나로 특성 정보를 허용합니다. 각 형식은 특성 설명에 기록됩니다. 이 형식은 **SQLGetStmtAttr**의 각 특성에 대해 반환되는 정보에 적용됩니다. **SQLSetStmtAttr의** *ValuePtr* 인수로 가리키는 문자열 문자열의 길이가 *있습니다.*  
  
> [!NOTE]
>  **SQLSetConnectAttr을** 호출하여 연결 수준에서 문 특성을 설정하는 기능은 ODBC *3.x에서*더 이상 사용되지 않습니다. ODBC *3.x* 응용 프로그램은 연결 수준에서 문 특성을 설정해서는 안 됩니다. ODBC *3.x* 문 특성은 연결 특성과 SQL_ATTR_ASYNC_ENABLE 특성을 제외한 SQL_ATTR_METADATA_ID 연결 수준에서 설정할 수 없으며 연결 특성 및 문 특성모두이며 연결 수준 또는 문 수준에서 설정할 수 있습니다.  
> 
> [!NOTE]
>  ODBC 3.x 드라이버는 연결 수준에서 ODBC *2.x* 문 옵션을 설정하는 ODBC *2.x* 응용 프로그램과 함께 작동해야 하는 경우에만 이 기능을 지원하면 됩니다. *2.x* 자세한 내용은 부록 G의 [SQLSetConnectOption 매핑:](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) 이전 버전과의 호환성을 위한 드라이버 지침에서 "연결 수준에서 문 옵션 설정"을 참조하십시오.  
  
## <a name="statement-attributes-that-set-descriptor-fields"></a>설명자 필드를 설정하는 명령문 특성  
 많은 문 특성은 설명자의 헤더 필드에 해당합니다. 이러한 특성을 설정하면 실제로 설명자 필드가 설정됩니다. **SQLSetDescField가** 아닌 **SQLSetStmtAttr에** 대한 호출로 필드를 설정하면 함수 호출에 대해 설명자 핸들을 가져올 필요가 없다는 장점이 있습니다.  
  
> [!CAUTION]  
>  한 문에 **대해 SQLSetStmtAttr을** 호출하면 다른 문에 영향을 줄 수 있습니다. 이 문제는 명령문과 연결된 APD 또는 ARD가 명시적으로 할당되고 다른 명령문과도 연결될 때 발생합니다. **SQLSetStmtAttr** APD 또는 ARD를 수정하기 때문에 수정 사항은 이 설명자가 연결된 모든 문에 적용됩니다. 필수 동작이 아닌 경우 응용 프로그램은 SQLSetStmtAttr을 다시 호출하기 전에 다른 명령문(SQLSetStmtAttr을 호출하여 **SQL_ATTR_APP_ROW_DESC** 또는 SQL_ATTR_APP_PARAM_DESC **SQLSetStmtAttr** 필드를 다른 설명자 핸들로 설정하도록 호출하여)에서 이 설명기를 분리해야 합니다.  
  
 설명자 필드가 설정된 해당 문 특성의 결과로 설정되면 해당 설명자 필드가 *현재 StatementHandle* 인수에서 식별된 명령문과 연결된 해당 설명자에 대해서만 설정되며 특성 설정은 나중에 해당 명령문과 연관될 수 있는 설명자에는 영향을 주지 않습니다. **SQLSetDescField에**대한 호출에 의해 문 특성이기도 한 설명자 필드가 설정되면 해당 명령문 특성이 설정됩니다. 명시적으로 할당된 설명자가 문에서 분리되면 헤더 필드에 해당하는 문 특성이 암시적으로 할당된 설명자의 필드 값으로 되돌아갑니다.  
  
 명령문이 [할당되면(SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)참조), 네 개의 설명자 핸들이 자동으로 할당되고 명령문과 연결됩니다. 명시적으로 할당된 설명자 핸들은 **sqlAllocHandle을** *SQL_HANDLE_DESC fHandleType을* 호출하여 설명자 핸들을 할당한 다음 **SQLSetStmtAttr을** 호출하여 설명자 핸들을 명령문과 연결하여 명령문과 연결할 수 있습니다.  
  
 다음 표의 문 특성은 설명자 헤더 필드에 해당합니다.  
  
|문 특성|헤더 필드|Desc.|  
|-------------------------|------------------|-----------|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_DESC_BIND_OFFSET_PTR|APD|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_DESC_BIND_TYPE|APD|  
|SQL_ATTR_PARAM_OPERATION_PTR|SQL_DESC_ARRAY_STATUS_PTR|APD|  
|SQL_ATTR_PARAM_STATUS_PTR|SQL_DESC_ARRAY_STATUS_PTR|IPD|  
|SQL_ATTR_PARAMS_PROCESSED_PTR|SQL_DESC_ROWS_PROCESSED_PTR|IPD|  
|SQL_ATTR_PARAMSET_SIZE|SQL_DESC_ARRAY_SIZE|APD|  
|SQL_ATTR_ROW_ARRAY_SIZE|SQL_DESC_ARRAY_SIZE|Ard|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|SQL_DESC_BIND_OFFSET_PTR|Ard|  
|SQL_ATTR_ROW_BIND_TYPE|SQL_DESC_BIND_TYPE|Ard|  
|SQL_ATTR_ROW_OPERATION_PTR|SQL_DESC_ARRAY_STATUS_PTR|Ard|  
|SQL_ATTR_ROW_STATUS_PTR|SQL_DESC_ARRAY_STATUS_PTR|Ird|  
|SQL_ATTR_ROWS_FETCHED_PTR|SQL_DESC_ROWS_PROCESSED_PTR|Ird|  
  
## <a name="statement-attributes"></a>문 특성  
 현재 정의된 특성과 이 특성이 도입된 ODBC 버전은 다음 표에 나와 있습니다. 드라이버가 다른 데이터 원본을 활용하기 위해 더 많은 특성을 정의할 것으로 예상됩니다. 특성의 범위는 ODBC에 의해 예약됩니다. 드라이버 개발자는 Open Group에서 드라이버별 사용을 위해 값을 예약해야 합니다. 자세한 내용은 [드라이버 관련 데이터 유형, 설명자 유형, 정보 유형, 진단 유형 및 특성을](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)참조하십시오.  
  
|특성|*밸류Ptr* 내용|  
|---------------|-------------------------|  
|SQL_ATTR_APP_PARAM_DESC (ODBC 3.0)|명령문 핸들에서 **SQLExecute** 및 **SQLExecDirect에** 대한 후속 호출에 대한 APD핸들입니다. 이 특성의 초기 값은 문이 처음 할당될 때 암시적으로 할당된 설명자입니다. 이 특성의 값이 SQL_NULL_DESC 설정되거나 설명자에 원래 할당된 핸들인 경우 이전에 문 핸들과 연결되었던 명시적으로 할당된 APD 핸들이 해제되고 명령문 핸들이 암시적으로 할당된 APD 핸들로 되돌아갑니다.<br /><br /> 이 특성은 다른 문에 대해 암시적으로 할당된 설명자 핸들또는 동일한 문에 암시적으로 설정된 다른 설명자 핸들로 설정할 수 없습니다. 암시적으로 할당된 설명자 핸들은 두 개 이상의 명령문 또는 설명자 핸들과 연결할 수 없습니다.|  
|SQL_ATTR_APP_ROW_DESC (ODBC 3.0)|명령문 핸들에서 후속 가져오기에 대한 ARD핸들입니다. 이 특성의 초기 값은 문이 처음 할당될 때 암시적으로 할당된 설명자입니다. 이 특성의 값이 SQL_NULL_DESC 설정되거나 설명자에 원래 할당된 핸들인 경우 문 핸들과 이전에 연관된 명시적으로 할당된 ARD 핸들이 해제되고 명령문 핸들이 암시적으로 할당된 ARD 핸들로 되돌아갑니다.<br /><br /> 이 특성은 다른 문에 대해 암시적으로 할당된 설명자 핸들또는 동일한 문에 암시적으로 설정된 다른 설명자 핸들로 설정할 수 없습니다. 암시적으로 할당된 설명자 핸들은 두 개 이상의 명령문 또는 설명자 핸들과 연결할 수 없습니다.|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 1.0)|지정된 문으로 호출된 함수가 비동기적으로 실행되는지 여부를 지정하는 SQLULEN 값은 다음과 같은 것입니다.<br /><br /> SQL_ASYNC_ENABLE_OFF = 문 수준 비동기 실행 지원(기본값)을 사용하지 않도록 설정합니다.<br /><br /> SQL_ASYNC_ENABLE_ON = 문 수준 비동기 실행 지원을 활성화합니다.<br /><br /> 자세한 내용은 [비동기 실행(폴링 메서드)을](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)참조하십시오.<br /><br /> 문 수준 비동기 실행 지원이 있는 드라이버의 경우 SQL_ATTR_ASYNC_ENABLE 문 특성만 읽습니다. 해당 값은 문 핸들이 할당된 시점의 이름이 같은 연결 수준 특성값과 동일합니다.<br /><br /> SQL_ASYNC_MODE *InfoType이* sqlSTATE HYC00을 반환하는 SQL_AM_CONNECTION 때 SQL_ATTR_ASYNC_ENABLE 설정하려면 **SQLSetStmtAttr을** 호출합니다(선택적 기능이 구현되지 않음). 자세한 내용은 자세한 내용은 [SQLSetConnectAttr 함수를](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) 참조하십시오.|  
|SQL_ATTR_ASYNC_STMT_EVENT (ODBC 3.8)|이벤트 핸들인 SQLPOINTER 값입니다.<br /><br /> **sqlSetStmtAttr을** 호출하여 **SQL_ATTR_ASYNC_STMT_EVENT** 특성을 설정하고 이벤트 핸들을 지정하여 비동기 함수완료 알림이 활성화됩니다.|  
|SQL_ATTR_ASYNC_STMT_PCALLBACK (ODBC 3.8)|비동기 콜백 함수에 대한 SQLPOINTER입니다.<br /><br /> 드라이버 관리자만 이 특성을 가진 드라이버의 **SQLSetStmtAttr** 함수를 호출할 수 있습니다.|  
|SQL_ATTR_ASYNC_STMT_PCONTEXT (ODBC 3.8)|컨텍스트 구조에 대한 SQLPOINTER<br /><br /> 드라이버 관리자만 이 특성을 가진 드라이버의 **SQLSetStmtAttr** 함수를 호출할 수 있습니다.|  
|SQL_ATTR_CONCURRENCY (ODBC 2.0)|커서 동시성을 지정하는 SQLULEN 값입니다.<br /><br /> SQL_CONCUR_READ_ONLY = 커서는 읽기 전용입니다. 업데이트는 허용되지 않습니다.<br /><br /> SQL_CONCUR_LOCK = 커서는 행을 업데이트할 수 있도록 충분한 최하위 잠금 수준을 사용합니다.<br /><br /> SQL_CONCUR_ROWVER = 커서는 SQLBase ROWID 또는 Sybase TIMESTAMP와 같은 행 버전을 비교하여 낙관적 동시성 컨트롤을 사용합니다.<br /><br /> SQL_CONCUR_VALUES = 커서는 값을 비교하여 낙관적 동시성 컨트롤을 사용합니다.<br /><br /> SQL_ATTR_CONCURRENCY 기본값은 SQL_CONCUR_READ_ONLY.<br /><br /> 열린 커서에 대해 이 특성을 지정할 수 없습니다. 자세한 내용은 [동시성 유형](../../../odbc/reference/develop-app/concurrency-types.md)을 참조하십시오.<br /><br /> SQL_ATTR_CURSOR_TYPE *특성이* SQL_ATTR_CONCURRENCY 현재 값을 지원하지 않는 유형으로 변경되면 실행 시 SQL_ATTR_CONCURRENCY 값이 변경되고 **SQLExecDirect** 또는 **SQLPrepare가** 호출될 때 경고가 발생합니다.<br /><br /> 드라이버가 SELECT **FOR UPDATE** 문을 지원하고 SQL_ATTR_CONCURRENCY 값이 SQL_CONCUR_READ_ONLY 설정된 상태에서 이러한 문이 실행되면 오류가 반환됩니다. SQL_ATTR_CONCURRENCY 값이 드라이버가 SQL_ATTR_CURSOR_TYPE SQL_ATTR_CURSOR_TYPE 현재 값에 대해 지원하지만 현재 SQL_ATTR_CURSOR_TYPE 값에 대해 지원하는 값으로 변경되면 실행 시 SQL_ATTR_CURSOR_TYPE 값이 변경되고 **SQLExecDirect** 또는 **SQLPrepare가** 호출될 때 SQLSTATE 01S02(옵션 값 변경됨)가 발행됩니다.<br /><br /> 지정된 동시성을 데이터 원본에서 지원하지 않는 경우 드라이버는 다른 동시성을 대체하고 SQLSTATE 01S02(옵션 값이 변경)를 반환합니다. SQL_CONCUR_VALUES 경우 드라이버는 SQL_CONCUR_ROWVER 대체하고 그 반대의 경우도 마찬가지입니다. SQL_CONCUR_LOCK 경우, 드라이버는 순서대로, SQL_CONCUR_ROWVER 또는 SQL_CONCUR_VALUES 대체합니다. 대체 된 값의 유효성은 실행 시간까지 확인 되지 않습니다.<br /><br /> SQL_ATTR_CONCURRENCY 다른 커서 특성 간의 관계에 대한 자세한 내용은 [커서 특성 및 커서 유형을](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)참조하십시오.|  
|SQL_ATTR_CURSOR_SCROLLABLE (ODBC 3.0)|응용 프로그램에 필요한 지원 수준을 지정하는 SQLULEN 값입니다. 이 특성을 설정하면 **SQLExecDirect** 및 **SQLExecute에**대한 후속 호출에 영향을 줍니다.<br /><br /> SQL_NONSCROLLABLE = 문 핸들에는 스크롤 가능한 커서가 필요하지 않습니다. 응용 프로그램에서 이 핸들에서 **SQLFetchScroll를** 호출하는 경우 *FetchOrientation의* 유효한 유일한 값은 SQL_FETCH_NEXT. 이것이 기본값입니다.<br /><br /> SQL_SCROLLABLE = 문 핸들에 스크롤 가능한 커서가 필요합니다. **SQLFetchScroll를**호출할 때 응용 프로그램은 *FetchOrientation의*유효한 값을 지정하여 순차 모드가 아닌 다른 모드에서 커서 위치를 지정할 수 있습니다.<br /><br /> 스크롤 가능한 커서에 대한 자세한 내용은 [스크롤 가능한 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)를 참조하십시오. SQL_ATTR_CURSOR_SCROLLABLE 다른 커서 특성 간의 관계에 대한 자세한 내용은 [커서 특성 및 커서 유형을](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md) 참조하십시오.|  
|SQL_ATTR_CURSOR_SENSITIVITY (ODBC 3.0)|명령문 핸들의 커서가 다른 커서에 의해 설정된 결과에 대한 변경 내용을 표시할지 여부를 지정하는 SQLULEN 값입니다. 이 특성을 설정하면 **SQLExecDirect** 및 **SQLExecute에**대한 후속 호출에 영향을 줍니다. 응용 프로그램은 이 특성의 값을 다시 읽고 응용 프로그램에서 가장 최근에 설정한 대로 초기 상태 또는 상태를 가져올 수 있습니다.<br /><br /> SQL_UNSPECIFIED = 커서 유형이 무엇인지, 명령문 핸들의 커서가 다른 커서에 의해 설정된 결과에 대한 변경 내용을 표시했는지 여부는 지정되지 않습니다. 명령문 핸들의 커서는 보이지 않는 것, 일부 또는 이러한 모든 변경 내용을 표시하지 않을 수 있습니다. 이것이 기본값입니다.<br /><br /> SQL_INSENSITIVE = 명령문 핸들의 모든 커서는 다른 커서에 의해 변경된 내용을 반영하지 않고 결과 집합을 표시합니다. 민감하지 않은 커서는 읽기 전용입니다. 이는 읽기 전용 동시성을 가지는 정적 커서에 해당합니다.<br /><br /> SQL_SENSITIVE = 문 핸들의 모든 커서를 통해 다른 커서가 설정한 결과에 대한 모든 변경 내용을 볼 수 있습니다.<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY 다른 커서 특성 간의 관계에 대한 자세한 내용은 [커서 특성 및 커서 유형을](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)참조하십시오.|  
|SQL_ATTR_CURSOR_TYPE (ODBC 2.0)|커서 형식을 지정하는 SQLULEN 값입니다.<br /><br /> SQL_CURSOR_FORWARD_ONLY = 커서가 앞으로만 스크롤됩니다.<br /><br /> SQL_CURSOR_STATIC = 결과 집합의 데이터가 정적입니다.<br /><br /> SQL_CURSOR_KEYSET_DRIVEN = 드라이버는 SQL_ATTR_KEYSET_SIZE 문 특성에 지정된 행 수에 대한 키를 저장하고 사용합니다.<br /><br /> SQL_CURSOR_DYNAMIC = 드라이버는 행 집합의 행에 대한 키만 저장하고 사용합니다.<br /><br /> 기본값은 SQL_CURSOR_FORWARD_ONLY. SQL 문을 준비한 후에는 이 특성을 지정할 수 없습니다.<br /><br /> 지정된 커서 형식이 데이터 원본에서 지원되지 않는 경우 드라이버는 다른 커서 유형을 대체하고 SQLSTATE 01S02(옵션 값이 변경)를 반환합니다. 혼합 또는 동적 커서의 경우 드라이버는 키집합 기반 또는 정적 커서를 순서대로 대체합니다. 키집합 기반 커서의 경우 드라이버는 정적 커서를 대체합니다.<br /><br /> 스크롤 가능한 커서 유형에 대한 자세한 내용은 [스크롤 가능한 커서 유형을](../../../odbc/reference/develop-app/scrollable-cursor-types.md)참조하십시오. SQL_ATTR_CURSOR_TYPE 다른 커서 특성 간의 관계에 대한 자세한 내용은 [커서 특성 및 커서 유형을](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)참조하십시오.|  
|SQL_ATTR_ENABLE_AUTO_IPD (ODBC 3.0)|IPD의 자동 모집단이 수행되는지 여부를 지정하는 SQLULEN 값은 다음과 같은 것입니다.<br /><br /> SQL_TRUE = **SQLPrepare를**호출한 후 IPD의 자동 채우기를 켭니다. SQL_FALSE = **SQLPrepare를**호출한 후 IPD의 자동 채우기를 끕니다. 응용 프로그램은 여전히 **SQLDescribeParam을**호출하여 IPD 필드 정보를 얻을 수 있습니다. SQL_ATTR_ENABLE_AUTO_IPD 문 특성의 기본값은 SQL_FALSE. 자세한 내용은 [IPD의 자동 채우기 를](../../../odbc/reference/develop-app/automatic-population-of-the-ipd.md)참조하십시오.|  
|SQL_ATTR_FETCH_BOOKMARK_PTR (ODBC 3.0)|이진 \* 책갈피 값을 가리키는 SQLLEN입니다. **SQLFetchScroll** 가 SQL_FETCH_BOOKMARK 것과 동일한 *fFetchOrientation를* 사용하여 호출되면 드라이버는 이 필드에서 책갈피 값을 선택합니다. 이 필드는 기본적으로 null 포인터로 설정됩니다. 자세한 내용은 [책갈피로 스크롤을](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)참조하십시오.<br /><br /> 이 필드에서 가리키는 값은 책갈피로 삭제하거나, 북마크별로 업데이트하거나, 행 집합 버퍼에 캐시된 책갈피를 사용하는 **SQLBulkOperations의**책갈피 작업으로 가져오는 데 사용되지 않습니다.|  
|SQL_ATTR_IMP_PARAM_DESC (ODBC 3.0)|IPD의 핸들입니다. 이 특성의 값은 문이 처음 할당될 때 할당된 설명자입니다. 응용 프로그램에서 이 특성을 설정할 수 없습니다.<br /><br /> 이 특성은 **SQLGetStmtAttr** 에 대한 호출로 검색할 수 있지만 **SQLSetStmtAttr**에 대한 호출로 설정되지 는 않습니다.|  
|SQL_ATTR_IMP_ROW_DESC (ODBC 3.0)|IRD의 핸들입니다. 이 특성의 값은 문이 처음 할당될 때 할당된 설명자입니다. 응용 프로그램에서 이 특성을 설정할 수 없습니다.<br /><br /> 이 특성은 **SQLGetStmtAttr** 에 대한 호출로 검색할 수 있지만 **SQLSetStmtAttr**에 대한 호출로 설정되지 는 않습니다.|  
|SQL_ATTR_KEYSET_SIZE (ODBC 2.0)|키집합 기반 커서의 키 집합의 행 수를 지정하는 SQLULEN입니다. 키 집합 크기가 0(기본값)이면 커서는 완전히 키 집합 기반입니다. 키 집합 크기가 0보다 크면 커서가 혼합됩니다(키 집합 내에서 키 집합 기반 및 키 집합 외부의 동적). 기본 키 집합 크기는 0입니다. 키집합 기반 커서에 대한 자세한 내용은 [키집합 기반 커서를](../../../odbc/reference/develop-app/keyset-driven-cursors.md)참조하십시오.<br /><br /> 지정된 크기가 최대 키 집합 크기를 초과하면 드라이버는 해당 크기를 대체하고 SQLSTATE 01S02(옵션 값이 변경)를 반환합니다.<br /><br /> 키 집합 크기가 0보다 크고 행 집합 크기보다 작은 경우 **SQLFetch** 또는 **SQLFetchScroll에서** 오류를 반환합니다.|  
|SQL_ATTR_MAX_LENGTH (ODBC 1.0)|드라이버가 문자 또는 이진 열에서 반환하는 최대 데이터 양을 지정하는 SQLULEN 값입니다. *ValuePtr가* 사용 가능한 데이터의 길이보다 적으면 **SQLFetch** 또는 **SQLGetData는** 데이터를 트렁킨 다음 SQL_SUCCESS 반환합니다. *ValuePtr이* 0(기본값)이면 드라이버는 사용 가능한 모든 데이터를 반환하려고 시도합니다.<br /><br /> 지정된 길이가 데이터 원본이 반환할 수 있는 최소 데이터 양보다 크거나 데이터 원본이 반환할 수 있는 최대 데이터 양보다 큰 경우 드라이버는 해당 값을 대체하고 SQLSTATE 01S02(옵션 값이 변경)를 반환합니다.<br /><br /> 이 특성의 값은 열린 커서에서 설정할 수 있습니다. 그러나 이 설정은 즉시 적용되지 않을 수 있으며, 이 경우 드라이버는 SQLSTATE 01S02(옵션 값이 변경)를 반환하고 특성을 원래 값으로 재설정합니다.<br /><br /> 이 특성은 네트워크 트래픽을 줄이기 위한 것이며 다중 계층 드라이버의 데이터 원본(드라이버가 아닌)이 이를 구현할 수 있는 경우에만 지원되어야 합니다. 이 메커니즘은 응용 프로그램에서 데이터를 트러커처리하는 데 사용해서는 안 됩니다. 수신된 데이터를 트러클처리하려면 응용 프로그램은 **SQLBindCol** 또는 **SQLGetData**의 *BufferLength* 인수에서 최대 버퍼 길이를 지정해야 합니다.|  
|SQL_ATTR_MAX_ROWS (ODBC 1.0)|**SELECT** 문을 위해 응용 프로그램으로 돌아갈 최대 행 수에 해당하는 SQLULEN 값입니다. \* *ValuePtr이* 0(기본값)이면 드라이버는 모든 행을 반환합니다.<br /><br /> 이 특성은 네트워크 트래픽을 줄이기 위한 것입니다. 개념적으로 결과 집합을 만들 때 적용 되며 결과 집합을 첫 번째 *ValuePtr* 행으로 제한 합니다. 결과 집합의 행 수가 *ValuePtr보다*큰 경우 결과 집합이 잘립니다.<br /><br /> SQL_ATTR_MAX_ROWS 카탈로그 함수에서 반환되는 결과를 포함하여 *명령문의*모든 결과 집합에 적용됩니다. SQL_ATTR_MAX_ROWS 커서 행 수의 값에 대한 최대값을 설정합니다.<br /><br /> SQL_ATTR_MAX_ROWS 제대로 구현될 것이라고 보장할 수 없는 경우 **SQLFetch** 또는 **SQLFetchScroll(데이터** 원본에서 결과 집합 크기 제한을 구현할 수 없는 경우)에 대한 SQL_ATTR_MAX_ROWS 동작을 에뮬레이트해서는 안 됩니다.<br /><br /> SQL_ATTR_MAX_ROWS SELECT 문 이외의 문(예: 카탈로그 함수)에 적용되는지 여부를 드라이버정의입니다.<br /><br /> 이 특성의 값은 열린 커서에서 설정할 수 있습니다. 그러나 이 설정은 즉시 적용되지 않을 수 있으며, 이 경우 드라이버는 SQLSTATE 01S02(옵션 값이 변경)를 반환하고 특성을 원래 값으로 재설정합니다.|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|카탈로그 함수의 문자열 인수를 처리하는 방법을 결정하는 SQLULEN 값입니다.<br /><br /> SQL_TRUE 경우 카탈로그 함수의 문자열 인수는 식별자로 처리됩니다. 이 경우는 중요하지 않습니다. 제한되지 않은 문자열의 경우 드라이버는 후행 공간을 제거하고 문자열을 대문자로 접습니다. 구분된 문자열의 경우 드라이버는 선행 또는 후행 공백을 제거하고 구분 기호 사이에 무엇이든 걸립니다. 이러한 인수 중 하나가 null 포인터로 설정된 경우 함수는 SQL_ERROR 및 SQLSTATE HY009(null 포인터의 잘못된 사용)를 반환합니다.<br /><br /> SQL_FALSE 경우 카탈로그 함수의 문자열 인수는 식별자로 처리되지 않습니다. 이 경우는 중요합니다. 인수에 따라 문자열 검색 패턴을 포함하거나 포함하지 않을 수 있습니다.<br /><br /> 기본값은 SQL_FALSE.<br /><br /> 값 목록을 사용하는 **SQLTable의** *TableType* 인수는 이 특성의 영향을 받지 않습니다.<br /><br /> SQL_ATTR_METADATA_ID 연결 수준에서 설정할 수도 있습니다. 연결 특성인 유일한 문 특성과 SQL_ATTR_ASYNC_ENABLE.)<br /><br /> 자세한 내용은 [카탈로그 함수의 인수를](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)참조하십시오.|  
|SQL_ATTR_NOSCAN (ODBC 1.0)|드라이버가 이스케이프 시퀀스에 대한 SQL 문자열을 검색해야 하는지 여부를 나타내는 SQLULEN 값입니다.<br /><br /> SQL_NOSCAN_OFF = 드라이버는 이스케이프 시퀀스(기본값)에 대해 SQL 문자열을 검사합니다.<br /><br /> SQL_NOSCAN_ON = 드라이버는 이스케이프 시퀀스에 대한 SQL 문자열을 검색하지 않습니다. 대신 드라이버는 명령문을 데이터 원본으로 직접 보냅니다.<br /><br /> 자세한 내용은 [ODBC의 이스케이프 시퀀스를](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)참조하십시오.|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR (ODBC 3.0)|SQLULEN * 동적 매개 변수의 바인딩을 변경 하기 위해 포인터에 추가 된 오프셋을 가리키는 값입니다. 이 필드가 null이 아닌 경우 드라이버는 포인터를 참조하고 설명자 레코드의 각 지연된 필드에 디레반대한 값을 추가합니다(SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR) 바인딩할 때 새 포인터 값을 사용합니다. 기본적으로 null로 설정됩니다.<br /><br /> 바인드 오프셋은 항상 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 필드에 직접 추가됩니다. 오프셋이 다른 값으로 변경된 경우에도 새 값은 설명자 필드의 값에 직접 추가됩니다. 새 오프셋은 필드 값에 이전 오프셋을 더한 값에 추가되지 않습니다.<br /><br /> 자세한 내용은 [매개 변수 바인딩 오프셋을](../../../odbc/reference/develop-app/parameter-binding-offsets.md)참조하십시오.<br /><br /> 이 문 특성을 설정하면 APD 헤더의 SQL_DESC_BIND_OFFSET_PTR 필드가 설정됩니다.|  
|SQL_ATTR_PARAM_BIND_TYPE (ODBC 3.0)|동적 매개 변수에 사용할 바인딩 방향을 나타내는 SQLULEN 값입니다.<br /><br /> 이 필드는 열별 바인딩을 선택하기 위해 기본값(기본값)SQL_PARAM_BIND_BY_COLUMN 설정됩니다.<br /><br /> 행 별 바인딩을 선택하려면 이 필드는 동적 매개 변수 집합에 바인딩되는 버퍼의 구조 길이 또는 인스턴스의 길이로 설정됩니다. 이 길이에는 바인딩된 매개 변수의 주소가 지정된 길이로 증분될 때 결과가 다음 매개변수 집합에서 동일한 매개변수의 시작을 가리키도록 하기 위해 모든 바인딩된 매개변수및 구조 또는 버퍼의 패딩에 대한 공간이 포함되어야 합니다. ANSI C에서 *sizeof* 연산자사용 시 이 동작이 보장됩니다.<br /><br /> 자세한 내용은 [매개 변수 바인딩 배열을](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)참조하십시오.<br /><br /> 이 문 특성을 설정하면 APD 헤더에서 SQL_DESC_ BIND_TYPE 필드가 설정됩니다.|  
|SQL_ATTR_PARAM_OPERATION_PTR (ODBC 3.0)|SQL 문을 실행 \* 하는 동안 매개 변수를 무시 하는 데 사용 하는 SQLUSMALLINT 값의 배열을 가리키는 SQLUSMALLINT 값입니다. 각 값은 SQL_PARAM_PROCEED(매개 변수가 실행될 경우) 또는 SQL_PARAM_IGNORE(매개 변수를 무시할 수 있음)으로 설정됩니다.<br /><br /> APD에서 SQL_DESC_ARRAY_STATUS_PTR 가리키는 배열의 상태 값을 설정하여 처리 중에 매개 변수 집합을 무시하여 SQL_PARAM_IGNORE 수 있습니다. 상태 값이 SQL_PARAM_PROCEED 설정되거나 배열에 요소가 설정되지 않은 경우 매개 변수 집합이 처리됩니다.<br /><br /> 이 문 특성은 null 포인터로 설정할 수 있으며, 이 경우 드라이버는 매개 변수 상태 값을 반환하지 않습니다. 이 특성은 언제든지 설정할 수 있지만 다음에 **SQLExecDirect** 또는 **SQLExecute가** 호출될 때까지 새 값이 사용되지 않습니다.<br /><br /> 바인딩된 매개 변수가 없는 경우 이 특성은 무시됩니다.<br /><br /> 자세한 내용은 [매개 변수 배열 사용을](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)참조하십시오.<br /><br /> 이 문 특성을 설정하면 APD 헤더에 SQL_DESC_ARRAY_STATUS_PTR 필드가 설정됩니다.|  
|SQL_ATTR_PARAM_STATUS_PTR (ODBC 3.0)|SQLExecute 또는 SQLExecDirect 호출 후 매개 변수 값의 각 행에 대 한 상태 정보를 포함 하는 SQLUSMALLINT 값의 배열을 가리키는 \* **SQLUSMALLINT**값입니다. **SQLExecute** 이 필드는 PARAMSET_SIZE 1보다 큰 경우에만 필요합니다.<br /><br /> 상태 값에는 다음 값이 포함될 수 있습니다.<br /><br /> SQL_PARAM_SUCCESS: 이 매개 변수 집합에 대해 SQL 문이 성공적으로 실행되었습니다.<br /><br /> SQL_PARAM_SUCCESS_WITH_INFO: 이 매개 변수 집합에 대해 SQL 문이 성공적으로 실행되었습니다. 그러나 진단 데이터 구조에서 경고 정보를 사용할 수 있습니다.<br /><br /> SQL_PARAM_ERROR: 이 매개 변수 집합을 처리하는 데 오류가 발생했습니다. 추가 오류 정보는 진단 데이터 구조에서 사용할 수 있습니다.<br /><br /> SQL_PARAM_UNUSED: 이 매개 변수 집합은 사용되지 않은 것으로, 일부 이전 매개 변수 집합에서 추가 처리를 중단하거나 SQL_ATTR_PARAM_OPERATION_PTR 지정한 배열의 해당 매개 변수 집합에 대해 SQL_PARAM_IGNORE 설정되었기 때문일 수 있습니다.<br /><br /> SQL_PARAM_DIAG_UNAVAILABLE: 드라이버는 매개 변수 배열을 모놀리식 단위로 처리하므로 이 수준의 오류 정보가 생성되지 않습니다.<br /><br /> 이 문 특성은 null 포인터로 설정할 수 있으며, 이 경우 드라이버는 매개 변수 상태 값을 반환하지 않습니다. 이 특성은 언제든지 설정할 수 있지만 다음에 **SQLExecute** 또는 **SQLExecDirect가** 호출될 때까지 새 값이 사용되지 않습니다. 이 특성을 설정하면 드라이버에서 구현한 출력 매개 변수 동작에 영향을 줄 수 있습니다.<br /><br /> 자세한 내용은 [매개 변수 배열 사용을](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)참조하십시오.<br /><br /> 이 문 특성을 설정하면 IPD 헤더에 SQL_DESC_ARRAY_STATUS_PTR 필드가 설정됩니다.|  
|SQL_ATTR_PARAMS_PROCESSED_PTR (ODBC 3.0)|오류 집합을 \* 포함하여 처리된 매개 변수 집합 수를 반환하는 버퍼를 가리키는 SQLULEN 레코드 필드입니다. null 포인터인 경우 번호가 반환되지 않습니다.<br /><br /> 이 문 특성을 설정하면 IPD 헤더에 SQL_DESC_ROWS_PROCESSED_PTR 필드가 설정됩니다.<br /><br /> 이 특성으로 가리키는 버퍼를 채우는 **SQLExecDirect** 또는 **SQLExecute** 호출이 SQL_SUCCESS 반환되지 않거나 SQL_SUCCESS_WITH_INFO 버퍼의 내용은 정의되지 않습니다.<br /><br /> 자세한 내용은 [매개 변수 배열 사용을](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)참조하십시오.|  
|SQL_ATTR_PARAMSET_SIZE (ODBC 3.0)|각 매개 변수에 대한 값 수를 지정하는 SQLULEN 값입니다. SQL_ATTR_PARAMSET_SIZE 1보다 큰 경우 apd 가리개 배열의 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR. 각 배열의 카디널리티는 이 필드의 값과 같습니다.<br /><br /> 바인딩된 매개 변수가 없는 경우 이 특성은 무시됩니다.<br /><br /> 자세한 내용은 [매개 변수 배열 사용을](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)참조하십시오.<br /><br /> 이 문 특성을 설정하면 APD 헤더에서 SQL_DESC_ARRAY_SIZE 필드가 설정됩니다.|  
|SQL_ATTR_QUERY_TIMEOUT (ODBC 1.0)|SQL 문이 실행될 때까지 기다렸다가 응용 프로그램으로 돌아가기까지 기다리는 시간(초)에 해당하는 SQLULEN 값입니다. *ValuePtr이* 0(기본값)과 같으면 시간 설정이 없습니다.<br /><br /> 지정된 시간 초과가 데이터 원본의 최대 시간 초과를 초과하거나 최소 시간 초과보다 작으면 **SQLSetStmtAttr은** 해당 값을 대체하고 SQLSTATE 01S02(옵션 값이 변경)를 반환합니다.<br /><br /> **SELECT** 문이 시간 만료된 경우 응용 프로그램에서 **SQLCloseCursor를** 호출하여 문을 다시 사용할 필요가 없습니다.<br /><br /> 이 문 특성에 설정된 쿼리 시간 시간은 동기 모드와 비동기 모드 모두에서 유효합니다.|  
|SQL_ATTR_RETRIEVE_DATA (ODBC 2.0)|SQLULEN 값:<br /><br /> SQL_RD_ON = **SQLFetch스크롤** 및 ODBC *3.x에서* **SQLFetch는** 커서를 지정된 위치에 배치한 후 데이터를 검색합니다. 이것이 기본값입니다.<br /><br /> SQL_RD_OFF = **SQLFetch스크롤** 및 ODBC *3.x에서* **SQLFetch는** 커서를 배치한 후 데이터를 검색하지 않습니다.<br /><br /> SQL_RETRIEVE_DATA SQL_RD_OFF 설정하면 응용 프로그램은 행을 검색하는 오버헤드를 발생하지 않고 행이 있는지 확인하거나 행에 대한 책갈피를 검색할 수 있습니다. 자세한 내용은 [행 스크롤 및 가져오기](../../../odbc/reference/develop-app/scrolling-and-fetching-rows-odbc.md)를 참조하십시오.<br /><br /> 이 특성의 값은 열린 커서에서 설정할 수 있습니다. 그러나 이 설정은 즉시 적용되지 않을 수 있으며, 이 경우 드라이버는 SQLSTATE 01S02(옵션 값이 변경)를 반환하고 특성을 원래 값으로 재설정합니다.|  
|SQL_ATTR_ROW_ARRAY_SIZE (ODBC 3.0)|**SQLFetch** 또는 **SQLFetchScroll에**대한 각 호출에서 반환되는 행 수를 지정하는 SQLULEN 값입니다. **또한 SQLBulkOperations의**대량 북마크 작업에 사용되는 책갈피 배열의 행 수이기도 합니다. 기본값은 1입니다.<br /><br /> 지정된 행 집합 크기가 데이터 원본에서 지원하는 최대 행 집합 크기를 초과하면 드라이버는 해당 값을 대체하고 SQLSTATE 01S02(옵션 값이 변경)를 반환합니다.<br /><br /> 자세한 내용은 [행 집합 크기를](../../../odbc/reference/develop-app/rowset-size.md)참조하십시오.<br /><br /> 이 문 특성을 설정하면 ARD 헤더에 SQL_DESC_ARRAY_SIZE 필드가 설정됩니다.|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR (ODBC 3.0)|SQLULEN * 열 데이터의 바인딩을 변경 하기 위해 포인터에 추가 된 오프셋을 가리키는 값입니다. 이 필드가 null이 아닌 경우 드라이버는 포인터를 참조하고 설명자 레코드의 각 지연된 필드에 디레반대한 값을 추가합니다(SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR) 바인딩할 때 새 포인터 값을 사용합니다. 기본적으로 null로 설정됩니다.<br /><br /> 이 문 특성을 설정하면 ARD 헤더의 SQL_DESC_BIND_OFFSET_PTR 필드가 설정됩니다.|  
|SQL_ATTR_ROW_BIND_TYPE (ODBC 1.0)|**SQLFetch** 또는 **SQLFetchScroll** 연결 된 문에 호출 될 때 사용할 바인딩 방향을 설정 하는 SQLULEN 값입니다. SQL_BIND_BY_COLUMN 값을 설정하여 열별 바인딩을 선택합니다. 행별 바인딩은 값을 구조의 길이또는 결과 열이 바인딩되는 버퍼의 인스턴스로 설정하여 선택됩니다.<br /><br /> 길이를 지정하면 바인딩된 열의 주소가 지정된 길이로 증분될 때 결과가 다음 행의 동일한 열의 시작을 가리키도록 하기 위해 모든 바인딩된 열과 구조 또는 버퍼의 패딩에 대한 공백을 포함해야 합니다. ANSI C에서 구조체 또는 공용 구조체와 함께 **sizeof** 연산자사용 시 이 동작이 보장됩니다.<br /><br /> 열별 바인딩은 **SQLFetch** 및 **SQLFetchScroll**에 대한 기본 바인딩 방향입니다.<br /><br /> 자세한 내용은 [블록 커서와 함께 사용할 바인딩 열을](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)참조하십시오.<br /><br /> 이 문 특성을 설정하면 ARD 헤더에 SQL_DESC_BIND_TYPE 필드가 설정됩니다.|  
|SQL_ATTR_ROW_NUMBER (ODBC 2.0)|전체 결과 집합의 현재 행 수인 SQLULEN 값입니다. 현재 행의 수를 확인할 수 없거나 현재 행이 없는 경우 드라이버는 0을 반환합니다.<br /><br /> 이 특성은 **SQLGetStmtAttr** 에 대한 호출로 검색할 수 있지만 **SQLSetStmtAttr**에 대한 호출로 설정되지 는 않습니다.|  
|SQL_ATTR_ROW_OPERATION_PTR (ODBC 3.0)|**SQLSetPos를**사용 하 여 대량 작업 하는 동안 행을 무시 하는 데 사용 하는 SQLUSMALLINT 값의 배열을 가리키는 SQLUSMALLINT \* 값입니다. 각 값은 SQL_ROW_PROCEED(벌크 작업에 포함할 행) 또는 SQL_ROW_IGNORE(행이 벌크 작업에서 제외되려면)으로 설정됩니다. **(SQLBulkOperations를**호출하는 동안이 배열을 사용하여 행을 무시할 수 없습니다.)<br /><br /> 이 문 특성은 null 포인터로 설정할 수 있으며, 이 경우 드라이버는 행 상태 값을 반환하지 않습니다. 이 특성은 언제든지 설정할 수 있지만 다음에 **SQLSetPos가** 호출될 때까지 새 값이 사용되지 않습니다.<br /><br /> 자세한 내용은 [SQLSetPos를 사용할](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md) 수 있는 행 업데이트 및 [SQLSetPos를 통해 행 을 삭제하는 행을](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)참조하십시오.<br /><br /> 이 문 특성을 설정하면 ARD에서 SQL_DESC_ARRAY_STATUS_PTR 필드가 설정됩니다.|  
|SQL_ATTR_ROW_STATUS_PTR (ODBC 3.0)|SQLFetch또는 SQLFetchScroll 에 대한 호출 후 행 상태 값을 포함하는 SQLUSMALLINT 값의 배열을 가리키는 \* **SQLUSMALLINT**값입니다. **SQLFetch** 배열에는 행집합에 행이 있는 만큼의 요소가 있습니다.<br /><br /> 이 문 특성은 null 포인터로 설정할 수 있으며, 이 경우 드라이버는 행 상태 값을 반환하지 않습니다. 이 특성은 언제든지 설정할 수 있지만 다음에 **SQLBulkOperations**, **SQLFetch스크롤** **또는** **SQLSetPos가** 호출될 때까지 새 값이 사용되지 않습니다.<br /><br /> 자세한 내용은 [가져온 행 수 및 상태](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)를 참조하십시오.<br /><br /> 이 문 특성을 설정하면 IRD 헤더에 SQL_DESC_ARRAY_STATUS_PTR 필드가 설정됩니다.<br /><br /> 이 특성은 **SQLExtendedFetch**에 대한 호출에서 *rgbRowStatus* 배열에 ODBC *2.x* 드라이버에 의해 매핑됩니다.|  
|SQL_ATTR_ROWS_FETCHED_PTR (ODBC 3.0)|**SQLFetch** 또는 \* **SQLFetchScroll에**대한 호출 후 가져온 행 수를 반환하는 버퍼를 가리키는 SQLULEN 값입니다. SQL_REFRESH 작업 *인수와* **SQLSetPos에** 대 한 호출에 의해 수행 되는 대량 작업에 의해 영향을 받는 행의 수; 또는 **SQLBulkOperations에서**수행하는 대량 작업의 영향을 받는 행 수입니다. 이 숫자에는 오류 행이 포함됩니다.<br /><br /> 자세한 내용은 [가져온 행 수 및 상태](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)를 참조하십시오.<br /><br /> 이 문 특성을 설정하면 IRD 헤더에 SQL_DESC_ROWS_PROCESSED_PTR 필드가 설정됩니다.<br /><br /> 이 특성으로 가리키는 버퍼를 채우는 **SQLFetch** 또는 **SQLFetchScroll** 호출이 SQL_SUCCESS 반환되지 않거나 SQL_SUCCESS_WITH_INFO 버퍼의 내용은 정의되지 않습니다.|  
|SQL_ATTR_SIMULATE_CURSOR (ODBC 2.0)|위치 업데이트 및 delete 문을 시뮬레이션하는 드라이버가 이러한 명령문이 단일 행에만 영향을 주는지 여부를 지정하는 SQLULEN 값입니다.<br /><br /> 위치 가있는 업데이트를 시뮬레이션하고 문을 삭제하기 위해 대부분의 드라이버는 현재 행의 각 열값을 지정하는 **WHERE** 절을 포함하는 검색된 **UPDATE** 또는 **DELETE** 문을 생성합니다. 이러한 열이 고유 키를 구성하지 않는 한 이러한 문은 두 개 이상의 행에 영향을 줄 수 있습니다.<br /><br /> 이러한 명령문이 한 행에만 영향을 미치도록 하기 위해 드라이버는 고유 키의 열을 결정하고 결과 집합에 이러한 열을 추가합니다. 응용 프로그램에서 결과 집합의 열이 고유한 키를 구성하도록 보장하는 경우 드라이버는 그렇게 할 필요가 없습니다. 이렇게 하면 실행 시간이 단축될 수 있습니다.<br /><br /> SQL_SC_NON_UNIQUE = 드라이버는 시뮬레이션된 위치 업데이트 또는 delete 문이 하나의 행에만 영향을 미치지 않는다는 것을 보장하지 않습니다. 그렇게 하는 것은 응용 프로그램의 책임입니다. 명령문이 두 개 이상의 행에 영향을 주는 경우 **SQLExecute**, **SQLExecDirect**또는 **SQLSetPos는** SQLSTATE 01001(커서 작업 충돌)을 반환합니다.<br /><br /> SQL_SC_TRY_UNIQUE = 드라이버는 시뮬레이션된 위치 업데이트 또는 delete 명령문이 하나의 행에만 영향을 미치도록 보장하려고 시도합니다. 드라이버는 고유 키가 없는 경우와 같이 두 개 이상의 행에 영향을 줄 수 있더라도 항상 이러한 문을 실행합니다. 명령문이 두 개 이상의 행에 영향을 주는 경우 **SQLExecute**, **SQLExecDirect**또는 **SQLSetPos는** SQLSTATE 01001(커서 작업 충돌)을 반환합니다.<br /><br /> SQL_SC_UNIQUE = 드라이버는 시뮬레이트를 시뮬레이션한 위치 업데이트 또는 삭제 문이 하나의 행에만 영향을 미치게 합니다. 드라이버가 지정된 문에 대해 이 것을 보장할 수 없는 경우 **SQLExecDirect** 또는 **SQLPrepare는** 오류를 반환합니다.<br /><br /> 데이터 원본이 위치 업데이트 및 삭제 문에 대한 기본 SQL 지원을 제공하고 드라이버가 커서를 시뮬레이션하지 않는 경우 SQL_SIMULATE_CURSOR SQL_SC_UNIQUE 요청되면 SQL_SUCCESS 반환됩니다. SQL_SC_TRY_UNIQUE 또는 SQL_SC_NON_UNIQUE 요청하면 SQL_SUCCESS_WITH_INFO 반환됩니다. 데이터 원본이 SQL_SC_TRY_UNIQUE 수준의 지원을 제공하고 드라이버가 지원하지 않는 경우 SQL_SUCCESS SQL_SC_TRY_UNIQUE 반환되고 SQL_SUCCESS_WITH_INFO SQL_SC_NON_UNIQUE 반환됩니다.<br /><br /> 지정된 커서 시뮬레이션 유형이 데이터 원본에서 지원되지 않는 경우 드라이버는 다른 시뮬레이션 유형을 대체하고 SQLSTATE 01S02(옵션 값이 변경)를 반환합니다. SQL_SC_UNIQUE 경우, 드라이버는 순서대로 SQL_SC_TRY_UNIQUE 또는 SQL_SC_NON_UNIQUE 대체합니다. SQL_SC_TRY_UNIQUE 경우, 드라이버는 SQL_SC_NON_UNIQUE 대체합니다.<br /><br /> 기본값은 SQL_SC_UNIQUE.<br /><br /> 자세한 내용은 [위치 업데이트 시뮬레이션 및 문 삭제](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)를 참조하십시오.|  
|SQL_ATTR_USE_BOOKMARKS (ODBC 2.0)|응용 프로그램에서 커서와 함께 책갈피를 사용할지 여부를 지정하는 SQLULEN 값입니다.<br /><br /> SQL_UB_OFF = 꺼져(기본값)<br /><br /> SQL_UB_VARIABLE = 응용 프로그램은 커서가 있는 책갈피를 사용하며, 드라이버가 지원되는 경우 가변 길이 책갈피를 제공합니다. SQL_UB_FIXED ODBC *3.x에서*더 이상 사용되지 않습니다. ODBC *3.x* 응용 프로그램은 ODBC *2.x* 드라이버(4바이트, 고정 길이 책갈피만 지원)로 작업하는 경우에도 항상 가변 길이 책갈피를 사용해야 합니다. 고정 길이 책갈피는 가변 길이 책갈피의 특별한 경우일 뿐이기 때문입니다. ODBC *2.x* 드라이버로 작업할 때 드라이버 관리자는 SQL_UB_FIXED SQL_UB_VARIABLE 매핑합니다.<br /><br /> 커서와 함께 책갈피를 사용하려면 응용 프로그램은 커서를 열기 전에 SQL_UB_VARIABLE 값으로 이 특성을 지정해야 합니다.<br /><br /> 자세한 내용은 [책갈피 검색](../../../odbc/reference/develop-app/retrieving-bookmarks.md)을 참조하십시오.|  
  
 [1] 이러한 함수는 설명자가 응용 프로그램 설명자가 아닌 구현 설명자인 경우에만 비동기적으로 호출할 수 있습니다.  
  
 [열 별 바인딩](../../../odbc/reference/develop-app/column-wise-binding.md) 및 행 별 [바인딩](../../../odbc/reference/develop-app/row-wise-binding.md)을 참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|연결 특성의 설정 반환|[SQLGetConnectAttr 함수(SQLGetConnectAttr Function)](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|문 특성의 설정 반환|[SQLGetStmtAttr 함수](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|연결 특성 설정|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|설명자의 단일 필드 설정|[SQLSetDesc필드 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
