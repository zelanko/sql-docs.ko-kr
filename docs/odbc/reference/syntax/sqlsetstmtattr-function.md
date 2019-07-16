---
title: SQLSetStmtAttr 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 583639a5cd4680bf6cfcf03bbaf6ee9eb63adba8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039653"
---
# <a name="sqlsetstmtattr-function"></a>SQLSetStmtAttr 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLSetStmtAttr** 문에 관련 된 특성을 설정 합니다.  
  
> [!NOTE]
>  새로운 드라이버 관리자는이 함수를 경우 맵을 ODBC에 대 한 자세한 *3.x* ODBC를 사용 하 여 응용 프로그램이 작동 *2.x* 드라이버를 참조 하세요. [뒤로 대 한 대체 함수 매핑 응용 프로그램의 호환성](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLSetStmtAttr(  
     SQLHSTMT      StatementHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *특성*  
 [입력] 옵션을 설정 하려면 "주석입니다."에 나열 된  
  
 *ValuePtr*  
 [입력] 와 연결할 값 *특성*합니다. 값에 따라 *특성*를 *ValuePtr* 다음 중 하나로 설정 됩니다.  
  
-   ODBC 설명자 핸들입니다.  
  
-   SQLUINTEGER 값입니다.  
  
-   SQLULEN 값입니다.  
  
-   다음 중 하나에 대 한 포인터:  
  
    -   Null로 끝나는 문자열입니다.  
  
    -   이진 버퍼입니다.  
  
    -   값 또는 SQLLEN, SQLULEN, 또는 SQLUSMALLINT 형식의 배열입니다.  
  
    -   드라이버에서 정의 된 값입니다.  
  
 경우는 *특성* 인수 드라이버별 값인 *ValuePtr* 부호 있는 정수를 수 있습니다.  
  
 *StringLength*  
 [입력] 하는 경우 *특성* 은 ODBC 정의 특성 및 *ValuePtr* 문자열 또는 이진 버퍼를 가리키는,이 인수 길이 여야 \* *ValuePtr*. 하는 경우 *특성* 은 ODBC 정의 특성 및 *ValuePtr* 정수 이면 *StringLength* 무시 됩니다.  
  
 하는 경우 *특성* 은 드라이버에서 정의 된 특성을 응용 프로그램을 설정 하 여 드라이버 관리자에 특성의 특성을 나타내는 합니다 *StringLength* 인수. *StringLength* 다음 값을 가질 수 있습니다.  
  
-   하는 경우 *ValuePtr* 문자열에 대 한 포인터 이면 *StringLength* SQL_NTS 또는 문자열의 길이입니다.  
  
-   하는 경우 *ValuePtr* 이진 버퍼에 대 한 포인터 이면 응용 프로그램을 SQL_LEN_BINARY_ATTR의 결과 배치 (*길이*)에서 매크로 *StringLength*합니다. 에 음수 값이 배치 *StringLength*합니다.  
  
-   하는 경우 *ValuePtr* 이 아닌 문자열 또는 이진 문자열 값에 대 한 포인터 이면 *StringLength* SQL_IS_POINTER 값이 있어야 합니다.  
  
-   하는 경우 *ValuePtr* 다음을 고정 길이 값이 포함 되어 *StringLength* SQL_IS_INTEGER 또는 SQL_IS_UINTEGER를 적절 하 게 됩니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLSetStmtAttr** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* sql _HANDLE_STMT와 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLSetStmtAttr** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S02|옵션 값이 변경 됨|드라이버에서 지정 된 값을 지원 하지 않았습니다 *ValuePtr*, 또는 지정 된 값 *ValuePtr* 드라이버 유사한 값을 대체 하도록 구현 작업 조건으로 인해 잘못 되었습니다. (**SQLGetStmtAttr** 일시적으로 대체 값을 확인 하기 위해 호출할 수 있습니다.) 대체 값이 적합 합니다 *StatementHandle* 커서를 닫을 때까지 시점에서 문 특성 값으로 되돌리는 경우 해당 이전 합니다. 변경할 수 있는 문 특성은 다음과 같습니다.<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT SQL_ATTR_ROW_ARRAY_SIZE SQL_ ATTR_SIMULATE_CURSOR<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|24000|잘못된 커서 상태|합니다 *특성* SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, 또는 SQL_ATTR_USE_BOOKMARKS, 및 커서를 엽니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|합니다 *특성* 인수는 필수 문자열 특성에는 문 특성을 식별 하며 *ValuePtr* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수가 여전히 실행 시기를 **SQLSetStmtAttr** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY011|특성을 지금 설정할 수 없습니다.|합니다 *특성* SQL_ATTR_CONCURRENCY, SQL_ ATTR_CURSOR_TYPE, SQL_ ATTR_SIMULATE_CURSOR 또는 SQL_ ATTR_USE_BOOKMARKS 및 문이 준비 되어 있습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY017|자동으로 할당 된 설명자 핸들을 잘못 사용|(DM)는 *특성* SQL_ATTR_IMP_ROW_DESC 또는 SQL_ATTR_IMP_PARAM_DESC 인수 했습니다.<br /><br /> (DM)는 *특성* 인수가 SQL_ATTR_APP_ROW_DESC SQL_ATTR_APP_PARAM_DESC, 및에 값 *ValuePtr* 원래 핸들 이외의 암시적으로 할당 된 설명자 핸들 APD 카드가에 할당 합니다.|  
|HY024|잘못 된 특성 값|지정 된 주어진 *특성* 값을 잘못 된 값에 지정 된 *ValuePtr*합니다. (드라이버 관리자 연결 및 문 특성 SQL_ATTR_ACCESS_MODE 또는 SQL_ ATTR_ASYNC_ENABLE 같은 값의 불연속 집합을 허용 하는 경우에이 SQLSTATE를 반환 하는 데 사용 합니다. 다른 모든 연결 및 문 특성에 대 한 드라이버에 지정 된 값을 확인 해야 합니다 *ValuePtr*.)<br /><br /> *특성* 인수가 SQL_ATTR_APP_ROW_DESC 또는 SQL_ATTR_APP_PARAM_DESC, 및 *ValuePtr* 와 동일한 연결에 없는 명시적으로 할당 된 설명자 핸들을가  *StatementHandle* 인수입니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM)  *\*ValuePtr* 는 문자 문자열인 하며 *StringLength* 인수가 0 보다 작은 하지만 SQL_NTS 없습니다.|  
|HY092|잘못 된 특성/옵션 식별자입니다.|인수에 지정 된 값 (DM) *특성* ODBC 드라이버에서 지 원하는 버전에 올바르지 않습니다.<br /><br /> 인수에 지정 된 값 (DM) *특성* 읽기 전용 특성을 했습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|인수에 지정 된 값 *특성* ODBC의 버전 드라이버에서 지원 되지만 드라이버에서 지원 되지에 대 한 유효한 ODBC 문 특성 되었습니다.<br /><br /> 합니다 *특성* 인수가 SQL_ATTR_ASYNC_ENABLE, 및에 대 한 호출 **SQLGetInfo** 사용 하 여는 *정보 항목* SQL_ASYNC_MODE의 SQL_AM_CONNECTION를 반환 합니다.<br /><br /> 합니다 *특성* 인수가 SQL_ATTR_ENABLE_AUTO_IPD, 및 SQL_ATTR_AUTO_IPD 연결 특성의 값이 SQL_FALSE입니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
|S1118|드라이버 비동기 알림을 지원 하지 않습니다.|호출 하는 경우 **SQLSetStmtAttr** SQL_ATTR_ASYNC_STMT_EVENT;를 설정 하는 드라이버에서 비동기 알림을 지원 되지 않습니다.|  
  
## <a name="comments"></a>주석  
 문 특성 문에 대 한 다른 호출에 의해 변경 될 때까지 계속 적용 **SQLSetStmtAttr** 문을 호출 하 여 삭제 될 때까지 또는 **SQLFreeHandle**합니다. 호출 **SQLFreeStmt** 옵션은 SQL_CLOSE, SQL_UNBIND, 또는 SQL_RESET_PARAMS로 문 특성을 설정 하지 않습니다.  
  
 데이터 원본에 지정 된 값을 지원 하지 않는 경우 일부 문 특성 유사한 값의 대체를 지원 *ValuePtr*합니다. 이러한 경우 드라이버는 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01S02를 반환 합니다. (옵션 값이 변경 됨). 예를 들어 경우 *특성* SQL_ATTR_CONCURRENCY 됩니다 및 *ValuePtr* SQL_CONCUR_ROWVER, 이므로 데이터 소스가 지원 하지 않는 경우 드라이버 SQL_CONCUR_VALUES 대체 고 SQL_를 반환 합니다. SUCCESS_WITH_INFO 합니다. 대체 값을 확인 하려면 응용 프로그램 호출 **SQLGetStmtAttr**합니다.  
  
 정보의 형식을 집합과 *ValuePtr* 된 종속 *특성*합니다. **SQLSetStmtAttr** 두 가지 형식 중 하나에 대 한 특성 정보를 허용 합니다: 문자열 또는 정수 값입니다. 형식에 대해 특성의 설명에 표시 됩니다. 이 형식은 각 특성에 대해 반환 되는 정보에 적용 됩니다 **SQLGetStmtAttr**합니다. 가리키는 문자열을 *ValuePtr* 인수의 **SQLSetStmtAttr** 길이 *StringLength*합니다.  
  
> [!NOTE]
>  연결 수준에서 호출 하 여 문 특성을 설정 하는 기능 **SQLSetConnectAttr** ODBC 되지 *3.x*합니다. ODBC *3.x* 응용 프로그램 연결 수준에서 문 특성을 설정 해서는 안됩니다. ODBC *3.x* 문 특성은 연결 특성 및 문 특성을 모두 수 있으며 SQL_ATTR_METADATA_ID 및 SQL_ATTR_ASYNC_ENABLE 특성을 제외 하 고 연결 수준에서 설정할 수 없습니다 연결 수준 또는 문 수준에서 설정 합니다.  
> 
> [!NOTE]
>  ODBC *3.x* 드라이버 ODBC를 사용 하 여 작동 해야 하는 경우이 기능을 지원만 필요한 *2.x* ODBC를 설정 하는 응용 프로그램 *2.x* 연결 수준에서 문 옵션입니다. 자세한 내용은 "설정 문 옵션에는 연결 수준"를 참조 하세요 [SQLSetConnectOption 매핑](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) 부록 g:에서 이전 버전과 호환성에 대 한 드라이버 지침입니다.  
  
## <a name="statement-attributes-that-set-descriptor-fields"></a>설명자 필드를 설정 하는 문 특성  
 여러 문 특성 설명자 헤더 필드에 해당합니다. 설명자 필드의 설정에서 이러한 특성 실제로 결과 설정 합니다. 호출 하 여 필드를 설정 **SQLSetStmtAttr** 아닌 **SQLSetDescField** 설명자 핸들을 함수 호출에서 얻은 없는 장점이 있습니다.  
  
> [!CAUTION]  
>  호출 **SQLSetStmtAttr** 하나의 문으로 다른 문의 영향을 줄 수에 대 한 합니다. 이런 APD 또는 카드가 문과 사용 하 여 연결을 명시적으로 할당 되 고 있을 때 다른 문과 사용 하 여 연결 합니다. 때문에 **SQLSetStmtAttr** APD 또는 카드가, 수정이 설명자와 연결 된 모든 문이에 수정 내용을 적용 합니다. 응용 프로그램에서 다른 문에서이 설명자를 분리 해야 필요한 동작은 없는 경우 (호출한 **SQLSetStmtAttr** 다른 SQL_ATTR_APP_ROW_DESC 또는 SQL_ATTR_APP_PARAM_DESC 필드를 설정 하려면 설명자 핸들) 호출 하기 전에 **SQLSetStmtAttr** 다시 합니다.  
  
 필드에서 식별 된 문을 사용 하 여 현재 연결 된 해당 설명자에만 설정 됩니다는 설명자 필드 설정 되 고 해당 문 특성의 결과로 설정 된 경우는 *StatementHandle* 인수 및 특성 설정을 나중에 해당 문과 사용 하 여 연결할 수 있는 모든 설명자 영향을 주지 않습니다. 문 특성 이기도 하는 설명자 필드를 호출 하 여 설정 된 경우 **SQLSetDescField**, 해당 문 특성 설정 됩니다. 문에서 명시적으로 할당 된 설명자를 분리 됩니다, 경우에 헤더 필드에 해당 하는 문 특성 암시적으로 할당 된 설명자 필드의 값으로 되돌아갑니다.  
  
 문을 할당 되는 경우 (참조 [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)), 4 개의 설명자 핸들이 자동으로 할당 되 고 문과 사용 하 여 연결 합니다. 호출 하 여 명시적으로 할당 된 설명자 핸들 문과 사용 하 여 연결할 수 있습니다 **SQLAllocHandle** 사용 하 여는 *fHandleType* 설명자 핸들 및 호출 할당할SQL_HANDLE_DESC의 **SQLSetStmtAttr** 설명자 핸들 문을 사용 하 여 연결 합니다.  
  
 다음 표에서에서 문 특성 설명자 헤더 필드에 해당합니다.  
  
|문 특성|헤더 필드|Desc입니다.|  
|-------------------------|------------------|-----------|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_DESC_BIND_OFFSET_PTR|APD|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_DESC_BIND_TYPE|APD|  
|SQL_ATTR_PARAM_OPERATION_PTR|SQL_DESC_ARRAY_STATUS_PTR|APD|  
|SQL_ATTR_PARAM_STATUS_PTR|SQL_DESC_ARRAY_STATUS_PTR|IPD|  
|SQL_ATTR_PARAMS_PROCESSED_PTR|SQL_DESC_ROWS_PROCESSED_PTR|IPD|  
|SQL_ATTR_PARAMSET_SIZE|SQL_DESC_ARRAY_SIZE|APD|  
|SQL_ATTR_ROW_ARRAY_SIZE|SQL_DESC_ARRAY_SIZE|카드가|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|SQL_DESC_BIND_OFFSET_PTR|카드가|  
|SQL_ATTR_ROW_BIND_TYPE|SQL_DESC_BIND_TYPE|카드가|  
|SQL_ATTR_ROW_OPERATION_PTR|SQL_DESC_ARRAY_STATUS_PTR|카드가|  
|SQL_ATTR_ROW_STATUS_PTR|SQL_DESC_ARRAY_STATUS_PTR|IRD|  
|SQL_ATTR_ROWS_FETCHED_PTR|SQL_DESC_ROWS_PROCESSED_PTR|IRD|  
  
## <a name="statement-attributes"></a>문 특성  
 현재 정의 된 특성 및 도입 된 ODBC 버전입니다; 다음 표에 표시 됩니다. 다양 한 데이터 소스를 활용 하는 드라이버에서 더 많은 특성을 정의할는 예상 됩니다. 특성의 범위는 ODBC;에 예약 되어 있습니다. 드라이버 개발자는 Open Group에서 자신의 드라이버별 사용에 대 한 값을 예약 해야 합니다. 자세한 내용은 [드라이버별 데이터 형식, 설명자 유형, 정보 유형, 진단 유형 및 특성](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)합니다.  
  
|attribute|*ValuePtr* 내용|  
|---------------|-------------------------|  
|SQL_ATTR_APP_PARAM_DESC (ODBC 3.0)|APD에 대 한 후속 호출에 대 한 핸들 **SQLExecute** 하 고 **SQLExecDirect** 문 핸들에서 합니다. 이 특성의 초기 값은 암시적으로 문을 처음에 할당 된 경우 할당 된 설명자입니다. 이 특성의 값을 SQL_NULL_DESC 또는 설명자에 대 한 원래 할당 된 핸들을 설정 하는 경우 문 핸들을 사용 하 여 이전에 연결 하는 명시적으로 할당 된 APD 핸들에서 분리 되 고 문 핸들으로 돌아갑니다 합니다 암시적으로 APD 핸들을 할당 합니다.<br /><br /> 같은 문에서; 암시적으로 설정 된 다른 설명자 핸들 또는 다른 문에 대 한 암시적으로 할당 된 설명자 핸들에이 특성을 설정할 수 없습니다. 암시적으로 할당 된 설명자 핸들은 둘 이상의 문 또는 설명자 핸들을 사용 하 여 연결할 수 없습니다.|  
|SQL_ATTR_APP_ROW_DESC (ODBC 3.0)|문 핸들에서 후속 인출에 대 한 카드가에 대 한 핸들입니다. 이 특성의 초기 값은 암시적으로 문을 처음에 할당 된 경우 할당 된 설명자입니다. 이 특성의 값을 SQL_NULL_DESC 또는 설명자에 대 한 원래 할당 된 핸들을 설정 하는 경우 문 핸들을 사용 하 여 이전에 연결 하는 명시적으로 할당 된 카드가 핸들에서 분리 되 고 문 핸들으로 돌아갑니다 합니다 암시적으로 카드가 핸들을 할당 합니다.<br /><br /> 같은 문에서; 암시적으로 설정 된 다른 설명자 핸들 또는 다른 문에 대 한 암시적으로 할당 된 설명자 핸들에이 특성을 설정할 수 없습니다. 암시적으로 할당 된 설명자 핸들은 둘 이상의 문 또는 설명자 핸들을 사용 하 여 연결할 수 없습니다.|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 1.0)|지정 된 문과 호출 된 함수를 비동기적으로 실행 되는지 여부를 지정 하는 SQLULEN 값:<br /><br /> SQL_ASYNC_ENABLE_OFF = 사용 안 함 문을 수준 비동기 실행 지원 (기본값).<br /><br /> Sql_async_enable_on으로 = 문 수준 비동기 실행 지원 사용 합니다.<br /><br /> 자세한 내용은 [비동기 실행 (폴링 메서드)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)합니다.<br /><br /> 문 수준 비동기 실행 지원 드라이버에서는 문 특성 SQL_ATTR_ASYNC_ENABLE 읽기 전용입니다. 해당 값 문 핸들 할당 된 시간을 동일한 이름의 연결 수준 특성의 값과 동일 합니다.<br /><br /> 호출 **SQLSetStmtAttr** SQL_ATTR_ASYNC_ENABLE을 설정할 때를 SQL_ASYNC_MODE *정보 항목* SQL_AM_CONNECTION 반환 SQLSTATE HYC00 (선택적 기능이 구현 되지 않음). 자세한 내용은 [SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) 자세한 내용은 합니다.|  
|SQL_ATTR_ASYNC_STMT_EVENT (ODBC 3.8)|이벤트 핸들에 해당 하는 대 SQLPOINTER 값입니다.<br /><br /> 호출 하 여 비동기 함수 완료 알림 가능 **SQLSetStmtAttr** 설정 하는 **SQL_ATTR_ASYNC_STMT_EVENT** 특성 및 이벤트 핸들을 지정 합니다.|  
|SQL_ATTR_ASYNC_STMT_PCALLBACK (ODBC 3.8)|비동기 콜백 함수에 대 한 SQLPOINTER입니다.<br /><br /> 드라이버 관리자는 드라이버를 호출할 수 있습니다만 **SQLSetStmtAttr** 이 특성을 사용 하 여 함수입니다.|  
|SQL_ATTR_ASYNC_STMT_PCONTEXT (ODBC 3.8)|상황에 맞는 구조에 대 한 SQLPOINTER<br /><br /> 드라이버 관리자는 드라이버를 호출할 수 있습니다만 **SQLSetStmtAttr** 이 특성을 사용 하 여 함수입니다.|  
|SQL_ATTR_CONCURRENCY (ODBC 2.0)|커서 동시성을 지정 하는 SQLULEN 값:<br /><br /> SQL_CONCUR_READ_ONLY = 읽기 전용 커서입니다. 업데이트할 수 없습니다.<br /><br /> SQL_CONCUR_LOCK = 커서 사용 하 여 가장 낮은 수준의 잠금을 행을 업데이트할 수 있는지 확인 하는 데 충분 합니다.<br /><br /> SQL_CONCUR_ROWVER = 커서 사용 하 여 낙관적 동시성 제어를 SQLBase ROWID 또는 Sybase 타임 스탬프와 같은 행 버전을 비교 합니다.<br /><br /> SQL_CONCUR_VALUES = 커서 사용 하 여 낙관적 동시성 제어, 값을 비교 합니다.<br /><br /> SQL_ATTR_CONCURRENCY 기본 값 SQL_CONCUR_READ_ONLY 됩니다.<br /><br /> 열린 커서에 대 한이 특성을 지정할 수 없습니다. 자세한 내용은 [동시성 유형은](../../../odbc/reference/develop-app/concurrency-types.md)합니다.<br /><br /> 경우는 SQL_ATTR_CURSOR_TYPE *특성* 변경 SQL_ATTR_CONCURRENCY의 현재 값을 지원 하지 않는 형식에 SQL_ATTR_CONCURRENCY은 실행 시간 및 경고 메시지를 표시 하면 변경됩니다**SQLExecDirect** 나 **SQLPrepare** 라고 합니다.<br /><br /> 드라이버에서 지 원하는 경우 합니다 **SELECT FOR UPDATE** SQL_ATTR_CONCURRENCY 값 SQL_CONCUR_READ_ONLY로 설정 되는 동안 문 및 이러한 문이 실행 되는 오류가 반환 됩니다. 실행 시간 및 SQLSTATE 01S02 SQL_ATTR_CURSOR_TYPE의 값을 변경할 수는 SQL_ATTR_CONCURRENCY의 값은 드라이버에서 지 원하는 SQL_ATTR_CURSOR_TYPE의 현재 값을 아니라 SQL_ATTR_CURSOR_TYPE의 일부 값에 대 한 값으로 변경 되 면 (옵션 값이 변경 됨)가 실행 될 **SQLExecDirect** 하거나 **SQLPrepare** 라고 합니다.<br /><br /> 동시성은 지정 된 데이터 원본에서 지원 되지 않는 경우 드라이버 다른 동시성을 대체 하 고 SQLSTATE 01S02를 반환 합니다 (옵션 값이 변경 됨). SQL_CONCUR_VALUES에 대 한 드라이버 대체 SQL_CONCUR_ROWVER, 그 반대로 가능 합니다. SQL_CONCUR_LOCK에 대 한 드라이버 대체, SQL_CONCUR_ROWVER 또는 SQL_CONCUR_VALUES 순서로 합니다. 실행 시간까지 대체 값의 유효성을 확인 하지 않습니다.<br /><br /> SQL_ATTR_CONCURRENCY과 다른 커서 특성 간의 관계에 대 한 자세한 내용은 참조 하세요. [커서 특징 및 커서 유형](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)합니다.|  
|SQL_ATTR_CURSOR_SCROLLABLE (ODBC 3.0)|응용 프로그램에서 필요한 지원 수준을 지정 하는 SQLULEN 값입니다. 이 특성에 대 한 후속 호출에 영향을 줍니다 **SQLExecDirect** 하 고 **SQLExecute**합니다.<br /><br /> SQL_NONSCROLLABLE = Scrollable 커서 문 핸들에서 필요 하지 않습니다. 응용 프로그램을 호출 하는 경우 **SQLFetchScroll** 의 유일한 유효 값이 핸들 *FetchOrientation* SQL_FETCH_NEXT 됩니다. 기본값입니다.<br /><br /> SQL_SCROLLABLE = Scrollable 커서 문 핸들에 필요 합니다. 호출할 때 **SQLFetchScroll**, 응용 프로그램의 유효한 값을 지정할 수 있습니다 *FetchOrientation*, 순차 모드 이외의 모드로 커서 위치 지정을 달성 합니다.<br /><br /> 스크롤 가능 커서에 대 한 자세한 내용은 참조 하세요. [스크롤 가능 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)합니다. SQL_ATTR_CURSOR_SCROLLABLE 및 다른 커서 특성 간의 관계에 대 한 자세한 내용은 참조 하세요. [커서 특징 및 커서 유형](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)|  
|SQL_ATTR_CURSOR_SENSITIVITY (ODBC 3.0)|커서 문 핸들에서 확인 표시 여부를 지정 하는 SQLULEN 값 결과에 대 한 변경 내용을 다른 커서에서 설정 합니다. 이 특성에 대 한 후속 호출에 영향을 줍니다 **SQLExecDirect** 하 고 **SQLExecute**합니다. 응용 프로그램에서 초기 상태로 또는 가져올 상태로으로 가장 최근에이 특성의 값이 설정 된 응용 프로그램 다시 읽을 수 있습니다.<br /><br /> SQL_UNSPECIFIED = 커서 유형이 이란 무엇 이며 문 핸들에서 커서를 변경 하는지 여부 표시를 다른 커서에 의해 결과 집합에 대 한 지정 됩니다. 문 핸들 커서 수 표시 되도록 none, 일부 또는 모든 변경. 기본값입니다.<br /><br /> SQL_INSENSITIVE = 다른 커서에서 모든 커서 결과 집합에 한 변경 내용을 반영 하지 않고 문 핸들 표시 합니다. Insensitive 커서는 읽기 전용입니다. 이 읽기 전용 동시성에는 정적 커서에 해당 합니다.<br /><br /> SQL_SENSITIVE = 모든 커서 문 핸들 make 표시 결과에 대 한 모든 변경 내용을 다른 커서에서 설정 합니다.<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY과 다른 커서 특성 간의 관계에 대 한 자세한 내용은 참조 하세요. [커서 특징 및 커서 유형](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)합니다.|  
|SQL_ATTR_CURSOR_TYPE (ODBC 2.0)|커서 유형을 지정 하는 SQLULEN 값:<br /><br /> SQL_CURSOR_FORWARD_ONLY = 앞으로 커서만 스크롤합니다.<br /><br /> SQL_CURSOR_STATIC 데이터 = 결과 집합은 정적입니다.<br /><br /> SQL_CURSOR_KEYSET_DRIVEN SQL_ATTR_KEYSET_SIZE 문 특성에 지정 된 행 수에 대 한 키를 사용 하 여 = 드라이버 저장 합니다.<br /><br /> SQL_CURSOR_DYNAMIC 드라이버 저장 = 및 행 집합의 행에 대 한 키만 사용 합니다.<br /><br /> 기본값은 SQL_CURSOR_FORWARD_ONLY 합니다. SQL 문의 준비 된 후에이 특성을 지정할 수 없습니다.<br /><br /> 데이터 원본에서 지정 된 커서 유형이 지원 되지 않는 경우 드라이버 다른 커서 유형을 대체 하 고 SQLSTATE 01S02를 반환 합니다 (옵션 값이 변경 됨). 혼합 또는 동적 커서에 대 한 드라이버 대체, 순서로 키 집합 커서 또는 정적 커서입니다. 키 집합 커서에 대 한 드라이버는 정적 커서를 대체합니다.<br /><br /> 스크롤 가능 커서 유형에 대 한 자세한 내용은 참조 하세요. [스크롤 가능 커서 유형](../../../odbc/reference/develop-app/scrollable-cursor-types.md)합니다. SQL_ATTR_CURSOR_TYPE 및 다른 커서 특성 간의 관계에 대 한 자세한 내용은 참조 하세요. [커서 특징 및 커서 유형](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)합니다.|  
|SQL_ATTR_ENABLE_AUTO_IPD (ODBC 3.0)|IPD의 자동 채우기가 수행 여부를 지정 하는 SQLULEN 값:<br /><br /> SQL_TRUE = 설정에 대 한 호출 후 IPD의 자동 채우기를 on **SQLPrepare**합니다. SQL_FALSE를 호출한 후 IPD의 자동 채우기를 설정 = **SQLPrepare**합니다. (호출 하 여 응용 프로그램 IPD 필드 정보를 여전히 가져올 수 있습니다 **SQLDescribeParam**이면 지원 합니다.) SQL_ATTR_ENABLE_AUTO_IPD 문 특성의 기본값은 SQL_FALSE입니다. 자세한 내용은 [IPD의 자동 채우기](../../../odbc/reference/develop-app/automatic-population-of-the-ipd.md)합니다.|  
|SQL_ATTR_FETCH_BOOKMARK_PTR (ODBC 3.0)|SQLLEN \* 는 이진 책갈피 값을 가리킵니다. 때 **SQLFetchScroll** 사용 하 여 라고 *fFetchOrientation* 이 필드의 책갈피 값 같음 SQL_FETCH_BOOKMARK, 드라이버를 선택 합니다. 이 필드는 기본적으로 null 포인터입니다. 자세한 내용은 [책갈피로 스크롤](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)합니다.<br /><br /> 이 필드에서 가리키는 값을 사용 되지 않습니다 삭제 하면 책갈피, 책갈피에서 업데이트 또는 책갈피 작업으로 인해 인출 **SQLBulkOperations**, 행 집합 버퍼에 캐시 하는 책갈피를 사용 하는 합니다.|  
|SQL_ATTR_IMP_PARAM_DESC (ODBC 3.0)|IPD에 대 한 핸들입니다. 이 특성의 값은 문이 처음에 할당 된 경우 할당 된 설명자입니다. 응용 프로그램이이 특성을 설정할 수 없습니다.<br /><br /> 호출 하 여이 특성을 검색할 수 있습니다 **SQLGetStmtAttr** 를 호출 하 여 설정 되지 않지만 **SQLSetStmtAttr**합니다.|  
|SQL_ATTR_IMP_ROW_DESC (ODBC 3.0)|IRD에 대 한 핸들입니다. 이 특성의 값은 문이 처음에 할당 된 경우 할당 된 설명자입니다. 응용 프로그램이이 특성을 설정할 수 없습니다.<br /><br /> 호출 하 여이 특성을 검색할 수 있습니다 **SQLGetStmtAttr** 를 호출 하 여 설정 되지 않지만 **SQLSetStmtAttr**합니다.|  
|SQL_ATTR_KEYSET_SIZE (ODBC 2.0)|키 집합 커서에 대 한 키 집합에 있는 행의 수를 지정 하는 SQLULEN입니다. 키 집합 크기를 0 (기본값) 이면 커서는 키 집합 커서를 완벽 하 게 되었습니다. 키 집합 크기를 0 보다 큰 경우 키 집합 내에서 키 집합 커서와 키 집합 외부에서 동적 커서는 mixed입니다. 기본 키 집합 크기는 0입니다. 키 집합 커서에 대 한 자세한 내용은 참조 하세요. [키 집합 커서](../../../odbc/reference/develop-app/keyset-driven-cursors.md)합니다.<br /><br /> 지정된 된 크기는 최대 키 집합 크기를 초과 하면 드라이버 해당 크기를 대체 하 고 SQLSTATE 01S02를 반환 합니다 (옵션 값이 변경 됨).<br /><br /> **SQLFetch** 나 **SQLFetchScroll** 키 집합 크기는 0 보다 크고 행 집합 크기 보다 작은 경우에 오류를 반환 합니다.|  
|SQL_ATTR_MAX_LENGTH (ODBC 1.0)|드라이버 문자 또는 이진 열에서 반환 되는 데이터의 최대 크기를 지정 하는 SQLULEN 값입니다. 하는 경우 *ValuePtr* 사용 가능한 데이터의 길이 보다 작으면 **SQLFetch** 또는 **SQLGetData** 관계 없이 SQL_SUCCESS를 반환 하 고 데이터를 자릅니다. 하는 경우 *ValuePtr* 가 0 (기본값) 이면 드라이버에서 사용 가능한 모든 데이터를 반환 하려고 합니다.<br /><br /> 지정된 된 길이 사용 하면 데이터 원본에서 반환할 수 있는 데이터의 최소 크기 보다 작으면 값 SQLSTATE 01S02를 반환 하는 드라이버 대체 데이터 소스를 반환할 수 있는 데이터의 최대 크기 보다 크거나 (옵션 값이 변경 됨).<br /><br /> 열린 커서;에서이 특성의 값을 설정할 수 있습니다. 그러나 설정 수에 적용 되지 즉시 경우 드라이버는 SQLSTATE 01S02 반환 됩니다 (옵션 값 변경) 원래 값을 특성으로 다시 설정 합니다.<br /><br /> 이 특성은 네트워크 트래픽을 줄이기 위해 되며 여러 계층 드라이버에서 (드라이버)와 달리 데이터 원본에서 구현할 수 있습니다 하는 경우에 지원 합니다. 이 메커니즘 해서는 안 응용 프로그램에서 데이터를 잘라내려면 응용 프로그램을 받은 데이터를 자르는, 최대 버퍼 길이 지정 해야 합니다 *BufferLength* 에서 인수 **SQLBindCol** 또는 **SQLGetData**합니다.|  
|SQL_ATTR_MAX_ROWS (ODBC 1.0)|에 대 한 응용 프로그램에 반환할 행의 최대 수에 해당 하는 SQLULEN 값을 **선택** 문입니다. 하는 경우 \* *ValuePtr* 0 (기본값) 이면 드라이버는 모든 행을 반환 합니다.<br /><br /> 이 특성은 네트워크 트래픽을 줄이기 위해 것입니다. 결과 집합 생성 되 고 첫 번째 결과 집합을 제한 하는 경우 적용 되는 개념상 *ValuePtr* 행. 결과 집합의 행 개수 보다 크면 *ValuePtr*, 결과 집합 잘립니다.<br /><br /> SQL_ATTR_MAX_ROWS에 모든 결과 집합에 적용 됩니다는 *문을*, 카탈로그 함수에서 반환 된 포함 합니다. SQL_ATTR_MAX_ROWS 커서 행 개수에 대 한 값에 대 한 최대값을 설정합니다.<br /><br /> 드라이버는 SQL_ATTR_MAX_ROWS 동작을 에뮬레이트하 지 않습니다 **SQLFetch** 하거나 **SQLFetchScroll** (하는 경우 결과 집합 크기 제한을 구현할 수 없습니다 데이터 소스의) 보장할 수 없습니다 하는 경우 해당 SQL_ATTR_ MAX_ROWS 제대로 구현 됩니다.<br /><br /> 드라이버에서 정의 된 SELECT 문 (예: 카탈로그 함수) 이외의 문에 SQL_ATTR_MAX_ROWS 적용 되는지 여부<br /><br /> 열린 커서;에서이 특성의 값을 설정할 수 있습니다. 그러나 설정 수에 적용 되지 즉시 경우 드라이버는 SQLSTATE 01S02 반환 됩니다 (옵션 값 변경) 원래 값을 특성으로 다시 설정 합니다.|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|카탈로그 함수의 문자열 인수를 처리 하는 방법을 결정 하는 SQLULEN 값입니다.<br /><br /> 면 SQL_TRUE를 카탈로그 함수의 문자열 인수는 식별자로 처리 됩니다. 대/소문자는 중요 하지 않습니다. Nondelimited 문자열에 대 한 드라이버 후행 공백을 제거한 문자열을 대문자로 정리 됩니다. 구분 기호로 분리 된 문자열에 대 한 드라이버 선행 또는 후행 공백을 제거 하 고 무엇이 구분 기호 간 문자 그대로 사용 합니다. 함수 반환 SQL_ERROR 및 SQLSTATE HY009 null 포인터로 설정 되어 이러한 인수 중 하나 (null 포인터를 잘못 사용).<br /><br /> 경우 SQL_FALSE를 카탈로그 함수의 문자열 인수를 사용 하는 식별자로 처리 되지 됩니다. 대/소문자는 중요 합니다. 포함할 수 있습니다 하거나 문자열 검색 패턴으로 인수에 따라.<br /><br /> 기본값은 SQL_FALSE입니다.<br /><br /> *TableType* 인수의 **SQLTables**,이 특성에 의해 영향을 받지 않습니다 값 목록을 사용 합니다.<br /><br /> SQL_ATTR_METADATA_ID 연결 수준에서 설정할 수도 있습니다. (고 SQL_ATTR_ASYNC_ENABLE는 연결 특성 이기도 문만 특성.)<br /><br /> 자세한 내용은 [카탈로그 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)합니다.|  
|SQL_ATTR_NOSCAN (ODBC 1.0)|드라이버 이스케이프 시퀀스에 대 한 SQL 문자열을 검색 해야 하는지 여부를 지정 하는 SQLULEN 값:<br /><br /> SQL_NOSCAN_OFF = 드라이버 검색 이스케이프 시퀀스 (기본값)에 대 한 SQL 문자열입니다.<br /><br /> SQL_NOSCAN_ON = 드라이버에서는 이스케이프 시퀀스에 대 한 SQL 문자열을 검색 하지 않습니다. 대신 드라이버는 데이터 원본에 직접 문의 보냅니다.<br /><br /> 자세한 내용은 [ODBC의 이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)합니다.|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR (ODBC 3.0)|SQLULEN * 동적 매개 변수 바인딩을 변경에 대 한 포인터를 추가 하는 오프셋 지점입니다. 이 필드가 null이 아닌 경우 드라이버는 포인터를 역참조, 각 설명자 레코드 (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, 및 SQL_DESC_OCTET_LENGTH_PTR)의 지연 된 필드에 역참조 된 값을 추가 및 새 포인터 값을 사용 하 여 바인딩하는 경우. 설정은 기본적으로 null로 합니다.<br /><br /> 바인딩 오프셋은 항상 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, 및 SQL_DESC_OCTET_LENGTH_PTR 필드에 직접 추가 됩니다. 오프셋을 다른 값으로 변경 되 면 설명자 필드의 값에 직접 새 값 추가 계속 됩니다. 새 오프셋 된 필드 값과 모든 이전 오프셋에 추가 되지 않습니다.<br /><br /> 자세한 내용은 [매개 변수 바인딩 오프셋](../../../odbc/reference/develop-app/parameter-binding-offsets.md)합니다.<br /><br /> 이 문 특성 설정 SQL_DESC_BIND_OFFSET_PTR 필드 APD 헤더를 설정 합니다.|  
|SQL_ATTR_PARAM_BIND_TYPE (ODBC 3.0)|동적 매개 변수에 대해 사용할 바인딩 방향을 나타내는 SQLULEN 값입니다.<br /><br /> 이 필드는 열 단위 바인딩을 선택 하려면 SQL_PARAM_BIND_BY_COLUMN (기본값)에 설정 됩니다.<br /><br /> 행 단위 바인딩은 선택 하려면이 필드는 동적 매개 변수 집합에 바인딩될 버퍼 인스턴스나 구조 길이 설정 됩니다. 이 길이 바인딩된 매개 변수 및 구조 또는 바인딩된 매개 변수의 주소를 지정된 된 길이 사용 하 여 증가 하는 경우 결과를 가리키는지 확인 시작 부분에에서 동일한 매개 변수 버퍼의 패딩에 대 한 공간이 있어야 합니다. 매개 변수 집합입니다. 사용 하는 경우는 *sizeof* ANSI c에서 연산자를이 동작이 유지 됩니다.<br /><br /> 자세한 내용은 [Binding Parameters 배열](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)합니다.<br /><br /> 이 문 특성 설정 SQL_DESC_ BIND_TYPE 필드 APD 헤더를 설정 합니다.|  
|SQL_ATTR_PARAM_OPERATION_PTR (ODBC 3.0)|SQLUSMALLINT \* SQLUSMALLINT 값의 배열을 가리키는 값은 SQL 문 실행 하는 동안 매개 변수를 무시 하는 데 사용 합니다. 각 값 (실행할 매개 변수)에 대 한 SQL_PARAM_PROCEED 또는 SQL_PARAM_IGNORE (용를 무시할 매개 변수)으로 설정 됩니다.<br /><br /> SQL_PARAM_IGNORE APD의 SQL_DESC_ARRAY_STATUS_PTR 가리키는 배열에서 상태 값을 설정 하 여 매개 변수 집합을 처리 하는 동안 무시 됩니다. 해당 상태 값 SQL_PARAM_PROCEED로 설정 된 경우 또는 배열에 요소가 설정 된 경우 매개 변수 집합이 처리 됩니다.<br /><br /> 없는 경우 드라이버는 반환 하지 않는 매개 변수 상태 값을 null 포인터로이 문 특성을 설정할 수 있습니다. 언제 든 지가이 특성을 설정할 수 있습니다 되지만 새 값을 다음 시간까지 사용 되지 않습니다 **SQLExecDirect** 하거나 **SQLExecute** 라고 합니다.<br /><br /> 바인딩된 매개 변수가 없는 경우이 특성이 무시 됩니다.<br /><br /> 자세한 내용은 [매개 변수의 배열을 사용 하 여](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)입니다.<br /><br /> 이 문 특성 설정 SQL_DESC_ARRAY_STATUS_PTR 필드 APD 헤더를 설정 합니다.|  
|SQL_ATTR_PARAM_STATUS_PTR (ODBC 3.0)|SQLUSMALLINT \* SQLUSMALLINT 배열을 가리키는 값 값을 호출한 후에 매개 변수 값의 각 행에 대 한 상태 정보를 포함 하 **SQLExecute** 하거나 **SQLExecDirect**합니다. 이 필드는 PARAMSET_SIZE 1 보다 큰 경우에 필요 합니다.<br /><br /> 상태 값은 다음 값을 포함할 수 있습니다.<br /><br /> SQL_PARAM_SUCCESS: 이 매개 변수이 집합에 대 한 SQL 문이 성공적으로 실행 합니다.<br /><br /> SQL_PARAM_SUCCESS_WITH_INFO: 이 매개 변수이 집합에 대 한 SQL 문이 성공적으로 실행 그러나 경고 정보는 진단 데이터 구조에서 사용할 수 있습니다.<br /><br /> SQL_PARAM_ERROR: 이 매개 변수이 집합을 처리에서 오류가 발생 했습니다. 추가 오류 정보를 진단 데이터 구조에서 사용할 수 있습니다.<br /><br /> SQL_PARAM_UNUSED: 이 매개 변수 집합 되지 않았거나 사용 가능한 경우 때문에 일부 이전 매개 변수 집합 추가 처리를 중단 하는 오류가 발생 한 SQL_PARAM_IGNORE는 SQL_ATTR_PARAM_OPERATION_PTR 하 여 지정 된 배열에 매개 변수 집합에 대 한 설정 되었기 때문에 합니다.<br /><br /> SQL_PARAM_DIAG_UNAVAILABLE: 드라이버 모놀리식 단위로 배열 매개 변수를 처리 하며 따라서이 수준의 오류 정보를 생성 하지 않습니다.<br /><br /> 없는 경우 드라이버는 반환 하지 않는 매개 변수 상태 값을 null 포인터로이 문 특성을 설정할 수 있습니다. 언제 든 지가이 특성을 설정할 수 있습니다 되지만 새 값을 다음 시간까지 사용 되지 않습니다 **SQLExecute** 하거나 **SQLExecDirect** 라고 합니다. 이 특성을 설정 합니다. 영향을 줄 수 드라이버에 의해 구현 된 출력 매개 변수 동작을 참고 합니다.<br /><br /> 자세한 내용은 [매개 변수의 배열을 사용 하 여](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)입니다.<br /><br /> 이 문 특성 설정 SQL_DESC_ARRAY_STATUS_PTR 필드 IPD 헤더를 설정 합니다.|  
|SQL_ATTR_PARAMS_PROCESSED_PTR (ODBC 3.0)|SQLULEN \* 처리 된 경우 오류 집합을 포함 하는 매개 변수 집합의 수를 반환 하는 버퍼를 가리키는 레코드 필드입니다. 이 null 포인터인 경우 번호가 없으면 반환 됩니다.<br /><br /> 이 문 특성 설정 SQL_DESC_ROWS_PROCESSED_PTR 필드 IPD 헤더를 설정 합니다.<br /><br /> 경우에 대 한 호출 **SQLExecDirect** 하거나 **SQLExecute** 는 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 입력 한 후가이 특성에서 가리키는 버퍼에 반환 하지 않습니다, 버퍼의 내용을 정의 되지 않습니다.<br /><br /> 자세한 내용은 [매개 변수의 배열을 사용 하 여](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)입니다.|  
|SQL_ATTR_PARAMSET_SIZE (ODBC 3.0)|각 매개 변수에 대해 값의 수를 지정 하는 SQLULEN 값입니다. SQL_ATTR_PARAMSET_SIZE 1 보다 큰 경우 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, 및 APD의 SQL_DESC_OCTET_LENGTH_PTR 배열을 가리킵니다. 각 배열의 카디널리티가이 필드의 값과 동일합니다.<br /><br /> 바인딩된 매개 변수가 없는 경우이 특성이 무시 됩니다.<br /><br /> 자세한 내용은 [매개 변수의 배열을 사용 하 여](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)입니다.<br /><br /> 이 문 특성 설정 SQL_DESC_ARRAY_SIZE 필드 APD 헤더를 설정 합니다.|  
|SQL_ATTR_QUERY_TIMEOUT (ODBC 1.0)|응용 프로그램에 반환 하기 전에 실행할 SQL 문에 대 한 대기 시간 (초) 수에 해당 하는 SQLULEN 값입니다. 하는 경우 *ValuePtr* 은 0 (기본값) 일 제한 시간은 없습니다.<br /><br /> 지정된 된 시간 제한 데이터 원본에 대 한 최대 제한 시간을 초과 하거나 최소 제한 시간 보다 작습니다 **SQLSetStmtAttr** 해당 값을 대체 하 고 SQLSTATE 01S02를 반환 합니다 (옵션 값이 변경 됨).<br /><br /> 응용 프로그램을 호출 하지 않아도 **SQLCloseCursor** 경우 명령문을 재사용 하는 **선택** 문을 시간이 초과 되었습니다.<br /><br /> 이 문 특성에 설정 하는 쿼리 제한 시간 동기 및 비동기 모드에서 유효 합니다.|  
|SQL_ATTR_RETRIEVE_DATA (ODBC 2.0)|SQLULEN 값:<br /><br /> SQL_RD_ON = **SQLFetchScroll** 및 ODBC *3.x*합니다 **SQLFetch** 커서 지정된 된 위치에 배치 된 후 데이터를 검색 합니다. 기본값입니다.<br /><br /> SQL_RD_OFF = **SQLFetchScroll** 및 ODBC *3.x*를 **SQLFetch** 커서 위치에 배치 된 후 데이터를 검색 하지 않습니다.<br /><br /> SQL_RETRIEVE_DATA SQL_RD_OFF을로 설정 하면 응용 프로그램에는 행이 없거나 행을 검색 하는 오버 헤드 없이 행에 대 한 책갈피를 검색 합니다. 확인할 수 있습니다. 자세한 내용은 [스크롤 및 페치 행](../../../odbc/reference/develop-app/scrolling-and-fetching-rows-odbc.md)합니다.<br /><br /> 열린 커서;에서이 특성의 값을 설정할 수 있습니다. 그러나 설정 수에 적용 되지 즉시 경우 드라이버는 SQLSTATE 01S02 반환 됩니다 (옵션 값 변경) 원래 값을 특성으로 다시 설정 합니다.|  
|SQL_ATTR_ROW_ARRAY_SIZE (ODBC 3.0)|각 호출에서 반환한 행 수를 지정 하는 SQLULEN 값 **SQLFetch** 하거나 **SQLFetchScroll**합니다. 대량 책갈피 작업에 사용 되는 책갈피 배열의 행 수 이기도 **SQLBulkOperations**합니다. 기본값은 1입니다.<br /><br /> 지정 된 행 집합 크기를 데이터 원본에서 지원 되는 최대 행 집합 크기를 초과 하면 드라이버 해당 값을 대체 하 고 SQLSTATE 01S02를 반환 합니다 (옵션 값이 변경 됨).<br /><br /> 자세한 내용은 [행 집합 크기](../../../odbc/reference/develop-app/rowset-size.md)합니다.<br /><br /> 이 문 특성 설정 SQL_DESC_ARRAY_SIZE 필드 카드가 헤더를 설정 합니다.|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR (ODBC 3.0)|SQLULEN * 열 데이터의 바인딩을 변경에 대 한 포인터를 추가 하는 오프셋을 가리키는 값입니다. 이 필드가 null이 아닌 경우 드라이버는 포인터를 역참조, 각 설명자 레코드 (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, 및 SQL_DESC_OCTET_LENGTH_PTR)의 지연 된 필드에 역참조 된 값을 추가 및 새 포인터 값을 사용 하 여 바인딩하는 경우. 설정은 기본적으로 null로 합니다.<br /><br /> 이 문 특성 설정 SQL_DESC_BIND_OFFSET_PTR 필드 카드가 헤더를 설정 합니다.|  
|SQL_ATTR_ROW_BIND_TYPE (ODBC 1.0)|바인딩 방향을 설정 하는 SQLULEN 값 때 사용할 수 있도록 **SQLFetch** 하거나 **SQLFetchScroll** 연결 문에서 호출 됩니다. 열 단위 바인딩은을 sql_bind_by_column으로 설정 된 값을 설정 하 여 선택 됩니다. 행 단위 바인딩은 넣을 결과 열 바인딩될 버퍼 인스턴스나 구조체의 길이 값을 설정 하 여 선택 됩니다.<br /><br /> 길이 지정 하면 모든 바인딩된 열 및 구조 또는 바인딩된 열의 주소가 지정된 된 길이 사용 하 여 증가 하는 경우 결과를 가리키는지 확인에서 동일한 열의 시작 부분에는 버퍼의 패딩에 대 한 공간을 포함 해야 합니다. e 다음 행입니다. 사용 하는 경우는 **sizeof** 연산자 구조 또는 ANSI c에서 공용 구조체를 사용 하 여이 동작이 유지 됩니다.<br /><br /> 기본 바인딩 방향을 열 단위 바인딩은 **SQLFetch** 하 고 **SQLFetchScroll**합니다.<br /><br /> 자세한 내용은 [블록 커서와 함께 사용 하기 위해 열 바인딩](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)합니다.<br /><br /> 이 문 특성 설정 SQL_DESC_BIND_TYPE 필드 카드가 헤더를 설정 합니다.|  
|SQL_ATTR_ROW_NUMBER (ODBC 2.0)|전체 결과의 현재 행의 수 SQLULEN 값을 설정 합니다. 현재 행의 수를 확인할 수 없는 경우 현재 행이 드라이버는 0을 반환 합니다.<br /><br /> 호출 하 여이 특성을 검색할 수 있습니다 **SQLGetStmtAttr** 를 호출 하 여 설정 되지 않지만 **SQLSetStmtAttr**합니다.|  
|SQL_ATTR_ROW_OPERATION_PTR (ODBC 3.0)|SQLUSMALLINT \* SQLUSMALLINT 값의 배열을 가리키는 값을 사용 하 여 대량 작업 중에 행을 무시 하는 데 **SQLSetPos**합니다. 각 값 (예: 대량 작업에 포함 시킬 행) SQL_ROW_PROCEED 또는 SQL_ROW_IGNORE (행에 대해 대량 작업에서 제외)으로 설정 됩니다. (호출 하는 동안이 배열을 사용 하 여 행을 무시할 수 없는 **SQLBulkOperations**.)<br /><br /> Null 포인터인 경우 드라이버는 행 상태 값을 반환 하지 않습니다 하이 문 특성을 설정할 수 있습니다. 언제 든 지가이 특성을 설정할 수 있습니다 되지만 새 값을 다음 시간까지 사용 되지 않습니다 **SQLSetPos** 라고 합니다.<br /><br /> 자세한 내용은 [SQLSetPos 사용 하 여 행 집합의 행 업데이트](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md) 하 고 [SQLSetPos 사용 하 여 행 집합에서 행 삭제](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)합니다.<br /><br /> 이 문 특성 설정 SQL_DESC_ARRAY_STATUS_PTR 필드는를 설정 합니다.|  
|SQL_ATTR_ROW_STATUS_PTR (ODBC 3.0)|SQLUSMALLINT \* SQLUSMALLINT 배열을 가리키는 값을 호출한 후에 포함 된 행 상태 값 값 **SQLFetch** 하거나 **SQLFetchScroll**합니다. 배열에 행 집합의 행이 있는 만큼의 요소가 있습니다.<br /><br /> Null 포인터인 경우 드라이버는 행 상태 값을 반환 하지 않습니다 하이 문 특성을 설정할 수 있습니다. 언제 든 지가이 특성을 설정할 수 있습니다 되지만 새 값을 다음 시간까지 사용 되지 않습니다 **SQLBulkOperations**, **SQLFetch**하십시오 **SQLFetchScroll**, 또는  **SQLSetPos** 라고 합니다.<br /><br /> 자세한 내용은 [수의 행 인출 및 상태](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)합니다.<br /><br /> 이 문 특성 설정 SQL_DESC_ARRAY_STATUS_PTR 필드 IRD 헤더를 설정 합니다.<br /><br /> 이 특성은 ODBC에서 매핑된 *2.x* 드라이버를 합니다 *rgbRowStatus* 배열에 대 한 호출에서 **SQLExtendedFetch**합니다.|  
|SQL_ATTR_ROWS_FETCHED_PTR을 설정 (ODBC 3.0)|SQLULEN \* 값에 대 한 호출 후 가져온 행 수를 반환 하는 버퍼를 가리키는 **SQLFetch** 하거나 **SQLFetchScroll**; 수행 된 대량 작업에 의해 영향을 받는 행 수 호출한 **SQLSetPos** 사용 하 여는 *작업이* SQL_REFRESH; 또는 수행한 대량 작업에 의해 영향을 받는 행 수의 인수 **SQLBulkOperations**. 이 숫자는 오류 행을 포함합니다.<br /><br /> 자세한 내용은 [수의 행 인출 및 상태](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)합니다.<br /><br /> 이 문 특성 설정 SQL_DESC_ROWS_PROCESSED_PTR 필드 IRD 헤더를 설정 합니다.<br /><br /> 경우에 대 한 호출 **SQLFetch** 하거나 **SQLFetchScroll** 는 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 입력 한 후가이 특성에서 가리키는 버퍼에 반환 하지 않습니다, 버퍼의 내용을 정의 되지 않습니다.|  
|SQL_ATTR_SIMULATE_CURSOR (ODBC 2.0)|배치를 시뮬레이션 하는 드라이버 업데이트 및 delete 문을 지 여부를 지정 하는 SQLULEN 값 이러한 문을 하나만 단일 행에 영향을 줄 것을 보장 합니다.<br /><br /> 하려면 위치 지정된 업데이트를 시뮬레이션 및 delete 문, 대부분의 드라이버를 생성 하는 검색 **업데이트** 또는 **삭제** 문을 포함 하는 **여기서** 지정 하는 절을 현재 행에서 각 열의 값입니다. 이러한 열을 고유 키를 구성 하지 않는 한 이러한 문을 둘 이상의 행을 발생할 수 있습니다.<br /><br /> 이러한 문이 하나의 행에 영향을 줄을 보장 하기 위해 드라이버 고유 키에 열을 결정 하 고 결과 집합에 이러한 열을 추가 합니다. 결과 집합의 열이 고유 키를 구성 하는 보장 하는 응용 프로그램, 드라이버에서 이렇게 않아도 됩니다. 실행 시간이 줄어들 수 있습니다.<br /><br /> SQL_SC_NON_UNIQUE 드라이버 = 것을 보장 하지는 시뮬레이션 된 업데이트 위치 또는 delete 문이 하나의 행에 영향 을지 것입니다 이렇게 해야 하는 응용 프로그램의 경우 문을 둘 이상의 행에 영향을 주 면 **SQLExecute**를 **SQLExecDirect**, 또는 **SQLSetPos** SQLSTATE 01001 (커서 작업이 충돌)를 반환 합니다.<br /><br /> SQL_SC_TRY_UNIQUE 보장 하기 위해 시뮬레이션 된 업데이트에 배치 되는 드라이버 시도 = 또는 문의 영향을 하나의 행을 삭제 합니다. 드라이버는 항상 이러한 문에서 실행 때와 같이 둘 이상의 행에 영향을 줄 수 있습니다 하는 경우에 고유 키가 있습니다. 문을 둘 이상의 행에 영향을 주 면 **SQLExecute**를 **SQLExecDirect**, 또는 **SQLSetPos** SQLSTATE 01001 (커서 작업이 충돌)를 반환 합니다.<br /><br /> SQL_SC_UNIQUE 위치 지정된 업데이트를 시뮬레이션 하는 드라이버 보장 = 또는 문의 영향을 하나의 행을 삭제 합니다. 드라이버는이 지정 된 문에서 보장할 수 없습니다 하는 경우 **SQLExecDirect** 하거나 **SQLPrepare** 오류를 반환 합니다.<br /><br /> 데이터 원본 드라이버 커서를 시뮬레이션 하지 않습니다 및 네이티브 SQL 위치 지정된 업데이트에 대 한 지원 및 delete 문의 하면 SQL_SC_UNIQUE SQL_SIMULATE_CURSOR에 대 한 요청 된 경우 SQL_SUCCESS가 반환 됩니다. SQL_SC_TRY_UNIQUE 또는 SQL_SC_NON_UNIQUE 요청 되 면 SQL_SUCCESS_WITH_INFO가 반환 됩니다. 데이터 원본 SQL_SC_TRY_UNIQUE 수준의 지원 제공 하 고 드라이버 않습니다 SQL_SC_TRY_UNIQUE 및 SQL_SUCCESS_WITH_INFO가 반환 되는 SQL_SC_NON_UNIQUE SQL_SUCCESS 반환 됩니다.<br /><br /> 데이터 원본에서 지정 된 커서 시뮬레이션 유형이 지원 되지 않는 경우 드라이버 대신 다른 시뮬레이션 형식을 사용 하 고 SQLSTATE 01S02를 반환 합니다 (옵션 값이 변경 됨). SQL_SC_UNIQUE에 대 한 드라이버 대체, SQL_SC_TRY_UNIQUE 또는 SQL_SC_NON_UNIQUE 순서로 합니다. SQL_SC_TRY_UNIQUE에 대 한 드라이버 SQL_SC_NON_UNIQUE를 대체합니다.<br /><br /> 기본값은 SQL_SC_UNIQUE 합니다.<br /><br /> 자세한 내용은 [시뮬레이션 배치 업데이트 및 삭제 문을](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)합니다.|  
|SQL_ATTR_USE_BOOKMARKS (ODBC 2.0)|커서를 사용 하 여 응용 프로그램에서 책갈피를 사용할지 여부를 지정 하는 SQLULEN 값:<br /><br /> SQL_UB_OFF = Off (기본값)<br /><br /> SQL_UB_VARIABLE = 응용 프로그램은 커서를 사용 하 여 책갈피를 사용 하며 드라이버에서는 지원 되는 경우 가변 길이 책갈피를 제공 합니다. SQL_UB_FIXED ODBC에서 사용 되지 않습니다 *3.x*합니다. ODBC *3.x* ODBC를 사용 하는 경우에 응용 프로그램에서 가변 길이 책갈피를 항상 사용 해야 *2.x* 드라이버 (4 바이트, 고정 길이 책갈피 지원 됨). 고정 길이 책갈피는 가변 길이 책갈피의 특별 한 경우 방금 때문입니다. ODBC를 사용 하 여 작업 하는 경우 *2.x* 드라이버를 드라이버 관리자 SQL_UB_VARIABLE SQL_UB_FIXED에 매핑됩니다.<br /><br /> 커서를 사용 하 여 책갈피를 사용 하려면 응용 프로그램 커서를 열기 전에 SQL_UB_VARIABLE 값을 사용 하 여이 특성을 지정 해야 합니다.<br /><br /> 자세한 내용은 [책갈피 검색](../../../odbc/reference/develop-app/retrieving-bookmarks.md)합니다.|  
  
 [설명자가 응용 프로그램 설명자를 하지 설명자를 구현 하는 경우에 1] 이러한 함수를 비동기적으로 호출할 수 있습니다.  
  
 참조 [열 단위 바인딩을](../../../odbc/reference/develop-app/column-wise-binding.md) 하 고 [행 단위 바인딩은](../../../odbc/reference/develop-app/row-wise-binding.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|연결 특성의 설정을 반환합니다.|[SQLGetConnectAttr 함수](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|반환 문 특성 설정|[SQLGetStmtAttr 함수](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|연결 특성을 설정합니다.|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|설명자의 단일 필드를 설정합니다.|[SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
