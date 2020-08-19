---
description: SQLSetStmtAttr 함수
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7572a907a1111e1c6aa96a2761e8551d3265b2d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421097"
---
# <a name="sqlsetstmtattr-function"></a>SQLSetStmtAttr 함수
**규칙**  
 소개 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLSetStmtAttr** 는 문과 관련 된 특성을 설정 합니다.  
  
> [!NOTE]
>  ODBC *2.x 응용 프로그램이 odbc 2.x* *드라이버를* 사용할 때 드라이버 관리자가이 기능을에 매핑하는 방법에 대 한 자세한 내용은 [응용 프로그램의 이전 버전과의 호환성을 위한 대체 함수 매핑](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)을 참조 하세요.  
  
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
 입력 문 핸들입니다.  
  
 *Attribute*  
 입력 "설명"에 나열 된 설정 옵션입니다.  
  
 *ValuePtr*  
 입력 *특성과*연결할 값입니다. *특성*의 값에 따라 결정 되는 값은 다음 중 *하나가 됩니다.*  
  
-   ODBC 설명자 핸들입니다.  
  
-   SQLUINTEGER 값입니다.  
  
-   SQLULEN 값입니다.  
  
-   다음 중 하나에 대 한 포인터입니다.  
  
    -   Null로 끝나는 문자열입니다.  
  
    -   이진 버퍼입니다.  
  
    -   SQLLEN, SQLULEN 또는 SQLUSMALLINT 형식의 값 또는 배열입니다.  
  
    -   드라이버 정의 값입니다.  
  
 *특성* 인수가 드라이버별 값인 경우에는 Signed *eptr* 이 부호 있는 정수일 수 있습니다.  
  
 *StringLength*  
 입력 *특성이* ODBC에 정의 된 *특성이 고,* 이상 문자열이 문자열 또는 이진 버퍼를 가리키는 경우이 인수는이 인수의 길이 여야 합니다 \* *ValuePtr*. *Attribute* 가 ODBC에 정의 된 특성이 고 *valueptr* 이 정수 이면 *stringlength* 는 무시 됩니다.  
  
 *특성이* 드라이버 정의 특성인 경우 응용 프로그램은 *stringlength* 인수를 설정 하 여 특성의 특성을 드라이버 관리자에 게 표시 합니다. *Stringlength* 에는 다음 값을 사용할 수 있습니다.  
  
-   *Valueptr* 이 문자열에 대 한 포인터인 경우 *stringlength* 는 문자열 또는 SQL_NTS의 길이입니다.  
  
-   *Valueptr* 이 이진 버퍼에 대 한 포인터인 경우 응용 프로그램은 SQL_LEN_BINARY_ATTR (*length*) 매크로의 결과를 *stringlength*로 배치 합니다. 그러면 음수 값이 *Stringlength*에 배치 됩니다.  
  
-   *Valueptr* 이 문자열 또는 이진 문자열이 아닌 값에 대 한 포인터인 경우 *stringlength* 의 값은 SQL_IS_POINTER 이어야 합니다.  
  
-   *Valueptr* 이 고정 길이 값을 포함 하는 경우에는 *stringlength* 가 SQL_IS_INTEGER 또는 SQL_IS_UINTEGER입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLSetStmtAttr** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLSetStmtAttr** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01 S 02|옵션 값 변경 됨|드라이버가 지정 된 값을 지원 하지 *않거나, 구현*작업 조건 때문에 지정 된 값이 잘못 되었습니다 .이로 인해 드라이버가 유사한 값으로 *대체 되었습니다.* (**SQLGetStmtAttr** 를 호출 하 여 임시로 대체 된 값을 확인할 수 있습니다.) 대체 값은 커서가 닫힐 때까지 *StatementHandle* 에 유효 합니다 .이 시점에서 statement 특성은 이전 값으로 되돌아갑니다. 변경할 수 있는 문 특성은 다음과 같습니다.<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT SQL_ATTR_ROW_ARRAY_SIZE SQL_ ATTR_SIMULATE_CURSOR<br /><br /> 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|24000|잘못된 커서 상태|*특성이* SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR 또는 SQL_ATTR_USE_BOOKMARKS 되었으며 커서가 열려 있습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. * \* MessageText* 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY009|Null 포인터 사용이 잘못 되었습니다.|*특성* 인수는 문자열 특성을 필요로 하는 문 특성을 식별 하 고 *, 인수는* null 포인터입니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLSetStmtAttr** 함수가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수가 호출 되었으며이 함수가 호출 될 때 여전히 실행 되 고 있습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY011|특성을 지금 설정할 수 없습니다.|*특성이* SQL_ATTR_CONCURRENCY, SQL_ ATTR_CURSOR_TYPE, SQL_ ATTR_SIMULATE_CURSOR 또는 SQL_ ATTR_USE_BOOKMARKS 되었고 문이 준비 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY017|자동으로 할당 된 설명자 핸들 사용이 잘못 되었습니다.|(DM) *특성* 인수가 SQL_ATTR_IMP_ROW_DESC 되었거나 SQL_ATTR_IMP_PARAM_DESC 되었습니다.<br /><br /> (DM) *특성* 인수가 SQL_ATTR_APP_ROW_DESC 또는 SQL_ATTR_APP_PARAM_DESC 되었으며,이 값은 원래 또는 apd에 대해 원래 할당 된 핸들을 제외 하 고 암시적으로 *할당 된 설명자 핸들 이었습니다.*|  
|HY024|잘못 된 특성 값|지정 된 *특성* 값이 지정 된 경우에는 잘못 된 값이 *valueptr*에 지정 되었습니다. (드라이버 관리자는 SQL_ATTR_ACCESS_MODE 또는 SQL_ ATTR_ASYNC_ENABLE와 같은 불연속 값 집합을 허용 하는 문 특성 및 연결에 대해서만이 SQLSTATE를 반환 합니다. 다른 모든 연결 및 문 특성의 경우 드라이버에서 지정 된 값을 확인 해야 *합니다.*<br /><br /> *특성* 인수가 SQL_ATTR_APP_ROW_DESC 또는 SQL_ATTR_APP_PARAM_DESC 되었으며, *StatementHandle* 인수와 동일한 연결에 없는 명시적으로 *할당 된 설명자* 핸들입니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|( *DM)가 \* 문자열* 이 고 *stringlength* 인수가 0 보다 작지만 SQL_NTS 되지 않았습니다.|  
|HY092|특성/옵션 식별자가 잘못 되었습니다.|(DM) 인수 *특성* 에 지정 된 값이 드라이버에서 지 원하는 ODBC 버전에 적합 하지 않습니다.<br /><br /> (DM) 인수 *특성* 에 지정 된 값이 읽기 전용 특성입니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|인수 *특성* 에 지정 된 값이 드라이버에서 지원 되는 odbc 버전에 대 한 올바른 odbc 문 특성 이지만 드라이버에서 지원 하지 않습니다.<br /><br /> *특성* 인수가 SQL_ATTR_ASYNC_ENABLE 되었으며 SQL_ASYNC_MODE *InfoType* 의 **SQLGetInfo** 호출은 SQL_AM_CONNECTION를 반환 합니다.<br /><br /> *특성* 인수가 SQL_ATTR_ENABLE_AUTO_IPD 되었으며 연결 특성 SQL_ATTR_AUTO_IPD의 값이 SQL_FALSE 되었습니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|S1118|드라이버가 비동기 알림을 지원 하지 않습니다.|**SQLSetStmtAttr** 을 호출 하 여 SQL_ATTR_ASYNC_STMT_EVENT를 설정 하는 경우 드라이버에서 비동기 알림을 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 문에 대 한 문 특성은 **SQLSetStmtAttr** 에 대 한 다른 호출로 변경 되거나 **sqlfreehandle**을 호출 하 여 문을 삭제할 때까지 계속 적용 됩니다. SQL_CLOSE, SQL_UNBIND 또는 SQL_RESET_PARAMS 옵션을 사용 하 여 **SQLFreeStmt** 를 호출 하면 문 특성이 다시 설정 되지 않습니다.  
  
 일부 문 특성은 데이터 소스가 지정 된 값을 지원 하지 않는 경우 유사한 값의 *대체를 지원 합니다.* 이 경우 드라이버는 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01 S 02 (옵션 값이 변경 됨)를 반환 합니다. 예를 들어 SQL_ATTR_CONCURRENCY *특성이* 이 고 이상 *값이 SQL_CONCUR_ROWVER 되 고* 데이터 소스에서이 기능을 지원 하지 않는 경우 드라이버는 SQL_CONCUR_VALUES 대체 하 고 SQL_SUCCESS_WITH_INFO를 반환 합니다. 대체 값을 결정 하기 위해 응용 프로그램은 **SQLGetStmtAttr**를 호출 합니다.  
  
 지정 된 *특성*에 따라 결정 되는 정보 형식을 사용 *하 여 설정* 합니다. **SQLSetStmtAttr** 는 두 가지 형식 (문자열 또는 정수 값) 중 하나로 특성 정보를 허용 합니다. 각의 형식은 특성의 설명에 설명 되어 있습니다. 이 형식은 **SQLGetStmtAttr**의 각 특성에 대해 반환 되는 정보에 적용 됩니다. **SQLSetStmtAttr** 의 *valueptr* 인수에서 가리키는 문자열의 길이가 *stringlength*입니다.  
  
> [!NOTE]
>  **SQLSetConnectAttr** 를 호출 하 여 연결 수준에서 문 특성을 설정 하는 *기능은 ODBC 3.x*에서 더 이상 사용 되지 않습니다. ODBC *3.x 응용 프로그램은 연결* 수준에서 문 특성을 설정 하면 안 됩니다. ODBC 3.x 문 특성은 연결 수준에서 설정할 수 없습니다 *.* SQL_ATTR_METADATA_ID 및 SQL_ATTR_ASYNC_ENABLE 특성은 연결 특성과 문 특성 모두 이며 연결 수준 또는 문 수준에서 설정할 수 있습니다.  
> 
> [!NOTE]
>  Odbc *3.x 드라이버는* 연결 수준에서 odbc 2.x 문 옵션을 설정 하는 odbc *2.x 응용 프로그램* 을 사용 해야 하는 경우에만이 기능을 지원 해야 *합니다.* 자세한 내용은 이전 버전과의 호환성을 위한 부록 G: 드라이버 지침의 [SQLSetConnectOption 매핑](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) 에서 "연결 수준에서 문 옵션 설정"을 참조 하세요.  
  
## <a name="statement-attributes-that-set-descriptor-fields"></a>설명자 필드를 설정 하는 문 특성  
 많은 문 특성은 설명자의 헤더 필드에 해당 합니다. 이러한 특성을 설정 하면 실제로 설명자 필드의 설정이 생성 됩니다. **SQLSetDescField** 대신 **SQLSetStmtAttr** 를 호출 하 여 필드를 설정 하면 함수 호출에 대해 설명자 핸들을 가져올 필요가 없다는 장점이 있습니다.  
  
> [!CAUTION]  
>  한 문에 대해 **SQLSetStmtAttr** 를 호출 하면 다른 문에 영향을 줄 수 있습니다. 이는 문과 연결 된 APD 또는가 명시적으로 할당 되 고 다른 문과도 연결 될 때 발생 합니다. **SQLSetStmtAttr** 는 apd를 수정 하기 때문에이 설명자가 연결 된 모든 문에 수정 내용이 적용 됩니다. 이 동작이 필요 하지 않은 경우 응용 프로그램은 **SQLSetStmtAttr** 를 다시 호출 하기 전에 **SQLSetStmtAttr** 를 호출 하 여 SQL_ATTR_APP_ROW_DESC 또는 SQL_ATTR_APP_PARAM_DESC 필드를 다른 설명자 핸들로 설정) 다른 문에서이 설명자를 분리 해야 합니다.  
  
 설정 되는 해당 문 특성의 결과로 설명자 필드가 설정 된 경우이 필드는 현재 *StatementHandle* 인수로 식별 되는 문과 연결 된 해당 설명자에 대해서만 설정 되며, 특성 설정은 나중에 해당 문과 연결 될 수 있는 설명자에 영향을 주지 않습니다. **SQLSetDescField**를 호출 하 여 문 특성 이기도 한 설명자 필드도 설정 하면 해당 문 특성이 설정 됩니다. 명시적으로 할당 된 설명자가 문에서 분리 될 경우 헤더 필드에 해당 하는 문 특성은 암시적으로 할당 된 설명자의 필드 값으로 되돌아갑니다.  
  
 문이 할당 될 때 ( [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)참조) 4 개의 설명자 핸들이 자동으로 할당 되 고 문과 연결 됩니다. 명시적으로 할당 된 설명자 핸들은 *fHandleType* SQL_HANDLE_DESC의 **SQLAllocHandle** 를 호출 하 여 설명자 핸들을 할당 한 다음 **SQLSetStmtAttr** 를 호출 하 여 설명자 핸들을 문과 연결 하 여 문에 연결할 수 있습니다.  
  
 다음 표의 문 특성은 설명자 헤더 필드에 해당 합니다.  
  
|Statement 특성|헤더 필드|설명.|  
|-------------------------|------------------|-----------|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_DESC_BIND_OFFSET_PTR|APD|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_DESC_BIND_TYPE|APD|  
|SQL_ATTR_PARAM_OPERATION_PTR|SQL_DESC_ARRAY_STATUS_PTR|APD|  
|SQL_ATTR_PARAM_STATUS_PTR|SQL_DESC_ARRAY_STATUS_PTR|IPD|  
|SQL_ATTR_PARAMS_PROCESSED_PTR|SQL_DESC_ROWS_PROCESSED_PTR|IPD|  
|SQL_ATTR_PARAMSET_SIZE|SQL_DESC_ARRAY_SIZE|APD|  
|SQL_ATTR_ROW_ARRAY_SIZE|SQL_DESC_ARRAY_SIZE|카드|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|SQL_DESC_BIND_OFFSET_PTR|카드|  
|SQL_ATTR_ROW_BIND_TYPE|SQL_DESC_BIND_TYPE|카드|  
|SQL_ATTR_ROW_OPERATION_PTR|SQL_DESC_ARRAY_STATUS_PTR|카드|  
|SQL_ATTR_ROW_STATUS_PTR|SQL_DESC_ARRAY_STATUS_PTR|IRD|  
|SQL_ATTR_ROWS_FETCHED_PTR|SQL_DESC_ROWS_PROCESSED_PTR|IRD|  
  
## <a name="statement-attributes"></a>문 특성  
 현재 정의 된 특성과 해당 특성이 소개 된 ODBC 버전이 다음 표에 나와 있습니다. 다른 데이터 원본을 활용 하기 위해 드라이버에서 더 많은 특성을 정의 해야 합니다. 특성 범위는 ODBC에서 예약 됩니다. 드라이버 개발자는 Open Group에서 고유한 드라이버별 사용에 대 한 값을 예약 해야 합니다. 자세한 내용은 [드라이버별 데이터 형식, 설명자 형식, 정보 형식, 진단 유형 및 특성](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)을 참조 하세요.  
  
|attribute|*ValuePtr* 이상 내용|  
|---------------|-------------------------|  
|SQL_ATTR_APP_PARAM_DESC (ODBC 3.0)|**Sqlexecute** 에 대 한 후속 호출 및 문 핸들에 대 한 **sqlexecdirect** 에 대 한 apd 핸들입니다. 이 특성의 초기 값은 문이 처음 할당 될 때 설명자가 암시적으로 할당 된 것입니다. 이 특성의 값이 SQL_NULL_DESC 또는 설명자에 대해 원래 할당 된 핸들로 설정 된 경우 이전에 문 핸들과 연결 된 명시적으로 할당 된 APD 핸들을 분리 하 고 문 핸들을 암시적으로 할당 된 APD 핸들로 되돌립니다.<br /><br /> 이 특성은 다른 문이나 동일한 문에 암시적으로 설정 된 다른 설명자 핸들에 대해 암시적으로 할당 된 설명자 핸들로 설정할 수 없습니다. 암시적으로 할당 된 설명자 핸들은 둘 이상의 문이나 설명자 핸들에 연결할 수 없습니다.|  
|SQL_ATTR_APP_ROW_DESC (ODBC 3.0)|문 핸들에 대 한 후속 인출에 대 한 핸들입니다. 이 특성의 초기 값은 문이 처음 할당 될 때 설명자가 암시적으로 할당 된 것입니다. 이 특성의 값이 SQL_NULL_DESC 또는 설명자에 대해 원래 할당 된 핸들로 설정 된 경우 이전에 문 핸들과 연결 된 명시적으로 할당 된 핸들을 분리 하 고 문 핸들이 암시적으로 할당 된 핸들로 되돌아갑니다.<br /><br /> 이 특성은 다른 문이나 동일한 문에 암시적으로 설정 된 다른 설명자 핸들에 대해 암시적으로 할당 된 설명자 핸들로 설정할 수 없습니다. 암시적으로 할당 된 설명자 핸들은 둘 이상의 문이나 설명자 핸들에 연결할 수 없습니다.|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 1.0)|지정 된 문을 사용 하 여 호출 된 함수가 비동기적으로 실행 되는지 여부를 지정 하는 SQLULEN 값입니다.<br /><br /> SQL_ASYNC_ENABLE_OFF = 문 수준 비동기 실행 지원 (기본값)을 사용 하지 않습니다.<br /><br /> SQL_ASYNC_ENABLE_ON = 문 수준 비동기 실행 지원을 사용 합니다.<br /><br /> 자세한 내용은 [비동기 실행 (폴링 방법)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)을 참조 하세요.<br /><br /> 문 수준 비동기 실행 지원이 포함 된 드라이버의 경우 문 특성 SQL_ATTR_ASYNC_ENABLE 읽기 전용입니다. 해당 값은 문 핸들이 할당 된 시간에 동일한 이름을 가진 연결 수준 특성의 값과 동일 합니다.<br /><br /> **SQLSetStmtAttr** 를 호출 하 여 SQL_ASYNC_MODE *InfoType* SQL_AM_CONNECTION 반환 되는 경우 SQL_ATTR_ASYNC_ENABLE를 설정 합니다. 자세한 내용은 [SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) 를 참조 하세요.|  
|SQL_ATTR_ASYNC_STMT_EVENT (ODBC 3.8)|이벤트 핸들 인 SQLPOINTER 값입니다.<br /><br /> 비동기 함수의 완료 알림은 **SQLSetStmtAttr** 를 호출 하 여 **SQL_ATTR_ASYNC_STMT_EVENT** 특성을 설정 하 고 이벤트 핸들을 지정 하 여 사용 하도록 설정 됩니다.|  
|SQL_ATTR_ASYNC_STMT_PCALLBACK (ODBC 3.8)|비동기 콜백 함수에 대 한 SQLPOINTER입니다.<br /><br /> 드라이버 관리자만이 특성을 사용 하 여 드라이버의 **SQLSetStmtAttr** 함수를 호출할 수 있습니다.|  
|SQL_ATTR_ASYNC_STMT_PCONTEXT (ODBC 3.8)|컨텍스트 구조에 대 한 SQLPOINTER<br /><br /> 드라이버 관리자만이 특성을 사용 하 여 드라이버의 **SQLSetStmtAttr** 함수를 호출할 수 있습니다.|  
|SQL_ATTR_CONCURRENCY (ODBC 2.0)|커서 동시성을 지정 하는 SQLULEN 값입니다.<br /><br /> SQL_CONCUR_READ_ONLY = 커서가 읽기 전용입니다. 업데이트는 허용 되지 않습니다.<br /><br /> SQL_CONCUR_LOCK = 커서는 행이 업데이트 될 수 있도록 가장 낮은 수준의 잠금을 사용 합니다.<br /><br /> SQL_CONCUR_ROWVER = 커서는 SQLBase ROWID 또는 Sybase TIMESTAMP와 같은 행 버전을 비교 하 여 낙관적 동시성 제어를 사용 합니다.<br /><br /> SQL_CONCUR_VALUES = 커서는 낙관적 동시성 제어를 사용 하 여 값을 비교 합니다.<br /><br /> SQL_ATTR_CONCURRENCY의 기본값은 SQL_CONCUR_READ_ONLY입니다.<br /><br /> 이 특성은 열린 커서에 대해 지정할 수 없습니다. 자세한 내용은 [동시성 형식](../../../odbc/reference/develop-app/concurrency-types.md)을 참조 하세요.<br /><br /> SQL_ATTR_CURSOR_TYPE *특성이* SQL_ATTR_CONCURRENCY의 현재 값을 지원 하지 않는 형식으로 변경 된 경우 실행 시 SQL_ATTR_CONCURRENCY 값이 변경 되 고 **sqlexecdirect** 또는 **sqlprepare** 가 호출 될 때 발생 하는 경고가 생성 됩니다.<br /><br /> 드라이버가 **SELECT FOR UPDATE** 문을 지원 하 고 SQL_ATTR_CONCURRENCY 값이 SQL_CONCUR_READ_ONLY으로 설정 된 상태에서 해당 문이 실행 되 면 오류가 반환 됩니다. SQL_ATTR_CONCURRENCY 값이 SQL_ATTR_CURSOR_TYPE의 일부 값에 대해 지원 되는 값으로 변경 되었지만 현재 SQL_ATTR_CURSOR_TYPE 값이 아닌 경우에는 SQL_ATTR_CURSOR_TYPE의 값이 실행 시 변경 되 고 SQLSTATE 01 S 02 (옵션 값이 변경 됨)는 **Sqlexecdirect** 또는 **sqlprepare** 가 호출 될 때 실행 됩니다.<br /><br /> 지정 된 동시성이 데이터 원본에서 지원 되지 않는 경우 드라이버는 다른 동시성을 대체 하 고 SQLSTATE 01 S 02 (옵션 값이 변경 됨)를 반환 합니다. SQL_CONCUR_VALUES의 경우 드라이버는 SQL_CONCUR_ROWVER를 대체 하며 그 반대의 경우도 마찬가지입니다. SQL_CONCUR_LOCK의 경우 드라이버는 순서 대로 (SQL_CONCUR_ROWVER 또는 SQL_CONCUR_VALUES를 대체 합니다. 대체 된 값의 유효성은 실행 시간까지 확인 되지 않습니다.<br /><br /> SQL_ATTR_CONCURRENCY와 다른 커서 특성 간의 관계에 대 한 자세한 내용은 [커서 특징 및 커서 유형](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)을 참조 하세요.|  
|SQL_ATTR_CURSOR_SCROLLABLE (ODBC 3.0)|응용 프로그램에 필요한 지원 수준을 지정 하는 SQLULEN 값입니다. 이 특성을 설정 하면 **Sqlexecdirect** 및 **sqlexecute**에 대 한 후속 호출에 영향을 줍니다.<br /><br /> SQL_NONSCROLLABLE = 스크롤 가능 커서는 문 핸들에 필요 하지 않습니다. 응용 프로그램에서이 핸들에 대해 **Sqlfetchscroll** 을 호출 하는 경우 *fetchorientation* 의 올바른 값만 SQL_FETCH_NEXT 됩니다. 이것이 기본값입니다.<br /><br /> SQL_SCROLLABLE = 문 핸들에 스크롤 가능한 커서가 필요 합니다. **Sqlfetchscroll**을 호출 하는 경우 응용 프로그램은 *fetchorientation*의 유효한 값을 지정 하 여 순차적 모드 이외의 모드에서 커서 위치를 달성할 수 있습니다.<br /><br /> 스크롤할 때 커서에 대 한 자세한 내용은 [스크롤 가능 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)를 참조 하세요. SQL_ATTR_CURSOR_SCROLLABLE와 다른 커서 특성 간의 관계에 대 한 자세한 내용은 [커서 특징 및 커서 유형](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md) 을 참조 하세요.|  
|SQL_ATTR_CURSOR_SENSITIVITY (ODBC 3.0)|문 핸들의 커서가 다른 커서에의 한 결과 집합의 변경 내용을 볼 수 있는지 여부를 지정 하는 SQLULEN 값입니다. 이 특성을 설정 하면 **Sqlexecdirect** 및 **sqlexecute**에 대 한 후속 호출에 영향을 줍니다. 응용 프로그램은이 특성 값을 다시 읽어 가장 최근에 응용 프로그램에서 설정한 대로 초기 상태나 상태를 가져올 수 있습니다.<br /><br /> SQL_UNSPECIFIED = 커서 유형의 정의와 문 핸들의 커서가 다른 커서에의 한 결과 집합의 변경 내용을 볼 수 있는지 여부를 지정 하지 않습니다. 문 핸들의 커서는 표시 되지 않거나, 일부 또는 모든 변경 내용을 볼 수 있습니다. 이것이 기본값입니다.<br /><br /> SQL_INSENSITIVE = 문 핸들의 모든 커서는 다른 커서에의 한 변경 내용을 반영 하지 않고 결과 집합을 표시 합니다. 구분 되지 않는 커서는 읽기 전용입니다. 이는 읽기 전용인 동시성이 있는 정적 커서에 해당 합니다.<br /><br /> SQL_SENSITIVE = 문 핸들의 모든 커서는 다른 커서에의 한 결과 집합의 모든 변경 내용을 표시 합니다.<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY와 다른 커서 특성 간의 관계에 대 한 자세한 내용은 [커서 특징 및 커서 유형](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)을 참조 하세요.|  
|SQL_ATTR_CURSOR_TYPE (ODBC 2.0)|커서 유형을 지정 하는 SQLULEN 값입니다.<br /><br /> SQL_CURSOR_FORWARD_ONLY = 커서는 앞 으로만 스크롤됩니다.<br /><br /> SQL_CURSOR_STATIC = 결과 집합의 데이터가 정적입니다.<br /><br /> SQL_CURSOR_KEYSET_DRIVEN = 드라이버는 SQL_ATTR_KEYSET_SIZE statement 특성에 지정 된 행 수에 대 한 키를 저장 하 고 사용 합니다.<br /><br /> SQL_CURSOR_DYNAMIC = 드라이버는 행 집합의 행에 대 한 키만 저장 하 고 사용 합니다.<br /><br /> 기본값은 SQL_CURSOR_FORWARD_ONLY입니다. SQL 문이 준비 된 후에는이 특성을 지정할 수 없습니다.<br /><br /> 데이터 원본에서 지정 된 커서 유형을 지원 하지 않는 경우 드라이버는 다른 커서 유형을 대체 하 고 SQLSTATE 01 S 02 (옵션 값이 변경 됨)을 반환 합니다. 혼합 또는 동적 커서의 경우 드라이버는 키 집합 커서 또는 정적 커서를 순서 대로 대체 합니다. 키 집합 커서의 경우 드라이버는 정적 커서를 대체 합니다.<br /><br /> 스크롤할 때 커서 유형에 대 한 자세한 내용은 [스크롤 가능 커서 유형](../../../odbc/reference/develop-app/scrollable-cursor-types.md)을 참조 하세요. SQL_ATTR_CURSOR_TYPE와 다른 커서 특성 간의 관계에 대 한 자세한 내용은 [커서 특징 및 커서 유형](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)을 참조 하세요.|  
|SQL_ATTR_ENABLE_AUTO_IPD (ODBC 3.0)|IPD 자동 채우기를 수행할지 여부를 지정 하는 SQLULEN 값입니다.<br /><br /> SQL_TRUE = **Sqlprepare**를 호출한 후 IPD 자동 채우기를 설정 합니다. SQL_FALSE = **Sqlprepare**를 호출한 후 IPD 자동 채우기를 해제 합니다. 응용 프로그램은 지원 되는 경우 **SQLDescribeParam**를 호출 하 여 IPD 필드 정보를 가져올 수 있습니다. Statement 특성 SQL_ATTR_ENABLE_AUTO_IPD의 기본값은 SQL_FALSE입니다. 자세한 내용은 [IPD의 자동 채우기](../../../odbc/reference/develop-app/automatic-population-of-the-ipd.md)를 참조 하세요.|  
|SQL_ATTR_FETCH_BOOKMARK_PTR (ODBC 3.0)|\*이진 책갈피 값을 가리키는 SQLLEN입니다. SQL_FETCH_BOOKMARK와 동일한 *Ffetchorientation* 를 사용 하 여 **sqlfetchscroll** 을 호출 하면 드라이버는이 필드에서 책갈피 값을 선택 합니다. 이 필드의 기본값은 null 포인터입니다. 자세한 내용은 [책갈피로 스크롤](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)(영문)을 참조 하세요.<br /><br /> 이 필드에 의해 가리키는 값은 행 집합 버퍼에 캐시 된 책갈피를 사용 하는 **SQLBulkOperations**에서 책갈피, 책갈피에의 한 업데이트 또는 책갈피 작업에의 한 삭제에 사용 되지 않습니다.|  
|SQL_ATTR_IMP_PARAM_DESC (ODBC 3.0)|IPD에 대 한 핸들입니다. 이 특성의 값은 문이 처음 할당 될 때 할당 되는 설명자입니다. 응용 프로그램에서이 특성을 설정할 수 없습니다.<br /><br /> 이 특성은 **SQLGetStmtAttr** 를 호출 하 여 검색할 수 있지만 **SQLSetStmtAttr**에 대 한 호출로는 설정할 수 없습니다.|  
|SQL_ATTR_IMP_ROW_DESC (ODBC 3.0)|IRD에 대 한 핸들입니다. 이 특성의 값은 문이 처음 할당 될 때 할당 되는 설명자입니다. 응용 프로그램에서이 특성을 설정할 수 없습니다.<br /><br /> 이 특성은 **SQLGetStmtAttr** 를 호출 하 여 검색할 수 있지만 **SQLSetStmtAttr**에 대 한 호출로는 설정할 수 없습니다.|  
|SQL_ATTR_KEYSET_SIZE (ODBC 2.0)|키 집합 커서에 대 한 키 집합의 행 수를 지정 하는 SQLULEN입니다. 키 집합 크기가 0 (기본값) 이면 커서는 완전히 키 집합을 기반으로 합니다. 키 집합 크기가 0 보다 크면 커서는 혼합 됩니다 (키 집합 내에서 키 집합을 기반으로 하 고 키 집합 외부의 동적). 기본 키 집합 크기는 0입니다. 키 집합 커서에 대 한 자세한 내용은 [키 집합 커서](../../../odbc/reference/develop-app/keyset-driven-cursors.md)를 참조 하세요.<br /><br /> 지정 된 크기가 최대 키 집합 크기를 초과 하는 경우 드라이버는 해당 크기를 대체 하 고 SQLSTATE 01 S 02 (옵션 값이 변경 됨)를 반환 합니다.<br /><br /> 키 집합 크기가 0 보다 크고 행 집합 크기 보다 작은 경우 **Sqlfetch** 또는 **sqlfetchscroll** 에서 오류를 반환 합니다.|  
|SQL_ATTR_MAX_LENGTH (ODBC 1.0)|드라이버가 문자 또는 이진 열에서 반환 하는 데이터의 최대 크기를 지정 하는 SQLULEN 값입니다. *Valueptr* 이 사용 가능한 데이터의 길이 보다 작은 경우 **Sqlfetch** 또는 **SQLGetData** 는 데이터를 자르고 SQL_SUCCESS을 반환 합니다. *Valueptr* 이 0 (기본값) 이면 드라이버는 사용 가능한 모든 데이터를 반환 하려고 시도 합니다.<br /><br /> 지정 된 길이가 데이터 원본에서 반환할 수 있는 데이터의 최소 크기 보다 작거나 데이터 원본에서 반환할 수 있는 최대 데이터 크기 보다 작은 경우 드라이버는 해당 값을 대체 하 고 SQLSTATE 01 S 02 (옵션 값이 변경 됨)를 반환 합니다.<br /><br /> 이 특성의 값은 열린 커서에 대해 설정할 수 있습니다. 그러나 설정이 즉시 적용 되는 것은 아닙니다 .이 경우 드라이버는 SQLSTATE 01 S 02 (옵션 값이 변경 됨)를 반환 하 고 특성을 원래 값으로 다시 설정 합니다.<br /><br /> 이 특성은 네트워크 트래픽을 줄이기 위한 것 이며, 다중 계층 드라이버의 데이터 원본 (드라이버와 반대)이이를 구현할 수 있는 경우에만 지원 되어야 합니다. 응용 프로그램에서 데이터를 잘라내는 데이 메커니즘을 사용 하면 안 됩니다. 수신 된 데이터를 잘라내려면 응용 프로그램은 **SQLBindCol** 또는 **SQLGetData**의 *bufferlength* 인수에 최대 버퍼 길이를 지정 해야 합니다.|  
|SQL_ATTR_MAX_ROWS (ODBC 1.0)|**SELECT** 문에 대해 응용 프로그램에 반환할 최대 행 수에 해당 하는 SQLULEN 값입니다. \* *Valueptr* 이 0 (기본값) 이면 드라이버는 모든 행을 반환 합니다.<br /><br /> 이 특성은 네트워크 트래픽을 줄이기 위한 것입니다. 개념적으로 결과 집합을 만들 때 적용 되며 결과 집합 *을 첫 번째* 값에서 첫 번째 행으로 제한 합니다. 결과 집합의 행 수가 *Valueptr*보다 크면 결과 집합이 잘립니다.<br /><br /> SQL_ATTR_MAX_ROWS는 카탈로그 함수에서 반환 된 결과 집합을 포함 하 여 *문의*모든 결과 집합에 적용 됩니다. SQL_ATTR_MAX_ROWS는 커서 행 수의 값에 대 한 최대값을 설정 합니다.<br /><br /> 드라이버는 **Sqlfetch** 또는 **sqlfetchscroll** 에 대 한 SQL_ATTR_MAX_ROWS 동작을 에뮬레이트 해서는 안 됩니다 (결과 집합 크기 제한이 데이터 원본에서 구현 될 수 없는 경우) SQL_ATTR_MAX_ROWS 제대로 구현 되도록 보장할 수 없습니다.<br /><br /> SELECT 문 (예: 카탈로그 함수) 이외의 문에 SQL_ATTR_MAX_ROWS 적용 되는지 여부를 드라이버에서 정의 합니다.<br /><br /> 이 특성의 값은 열린 커서에 대해 설정할 수 있습니다. 그러나 설정이 즉시 적용 되는 것은 아닙니다 .이 경우 드라이버는 SQLSTATE 01 S 02 (옵션 값이 변경 됨)를 반환 하 고 특성을 원래 값으로 다시 설정 합니다.|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|카탈로그 함수의 문자열 인수를 처리 하는 방법을 결정 하는 SQLULEN 값입니다.<br /><br /> SQL_TRUE 경우 카탈로그 함수의 문자열 인수는 식별자로 처리 됩니다. 이 경우에는 중요 하지 않습니다. 구분 되지 않은 문자열의 경우 드라이버는 후행 공백을 제거 하 고 문자열을 대문자로 접 합니다. 구분 기호로 분리 된 문자열의 경우 드라이버는 선행 또는 후행 공백을 모두 제거 하 고 구분 기호 사이에 어떤 것을 그대로 사용 합니다. 이러한 인수 중 하나가 null 포인터로 설정 된 경우 함수는 SQL_ERROR 및 SQLSTATE HY009 (null 포인터 사용이 잘못 되었습니다)를 반환 합니다.<br /><br /> SQL_FALSE 경우 카탈로그 함수의 문자열 인수는 식별자로 처리 되지 않습니다. 이 경우는 중요 합니다. 인수에 따라 문자열 검색 패턴을 포함할 수도 있고 그렇지 않을 수도 있습니다.<br /><br /> 기본값은 SQL_FALSE입니다.<br /><br /> 값 목록을 사용 하는 **Sqltables**의 *TableType* 인수는이 특성의 영향을 받지 않습니다.<br /><br /> 연결 수준에서 SQL_ATTR_METADATA_ID 설정할 수도 있습니다. (이 및 SQL_ATTR_ASYNC_ENABLE는 연결 특성 이기도 한 유일한 문 특성입니다.)<br /><br /> 자세한 내용은 [Catalog 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)를 참조 하세요.|  
|SQL_ATTR_NOSCAN (ODBC 1.0)|드라이버가 이스케이프 시퀀스에 대 한 SQL 문자열을 검색 해야 하는지 여부를 나타내는 SQLULEN 값입니다.<br /><br /> SQL_NOSCAN_OFF = 드라이버는 SQL 문자열의 이스케이프 시퀀스 (기본값)를 검색 합니다.<br /><br /> SQL_NOSCAN_ON = 드라이버는 SQL 문자열에서 이스케이프 시퀀스를 검색 하지 않습니다. 대신 드라이버가 데이터 원본에 직접 문을 보냅니다.<br /><br /> 자세한 내용은 [ODBC의 이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)를 참조 하세요.|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR (ODBC 3.0)|동적 매개 변수의 바인딩을 변경 하기 위해 포인터에 추가 되는 오프셋을 가리키는 SQLULEN * 값입니다. 이 필드가 null이 아닌 경우 드라이버는 포인터를 역참조 하 고 설명자 레코드 (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR)의 각 지연 된 필드에 역참조 된 값을 추가 하 고 바인딩할 때 새 포인터 값을 사용 합니다. 기본적으로 null로 설정 됩니다.<br /><br /> 바인딩 오프셋은 항상 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 필드에 직접 추가 됩니다. 오프셋이 다른 값으로 변경 되 면 새 값은 여전히 설명자 필드의 값에 직접 추가 됩니다. 새 오프셋은 필드 값에 이전 오프셋에 추가 되지 않습니다.<br /><br /> 자세한 내용은 [매개 변수 바인딩 오프셋](../../../odbc/reference/develop-app/parameter-binding-offsets.md)(영문)을 참조 하세요.<br /><br /> 이 문 특성을 설정 하면 APD 헤더의 SQL_DESC_BIND_OFFSET_PTR 필드가 설정 됩니다.|  
|SQL_ATTR_PARAM_BIND_TYPE (ODBC 3.0)|동적 매개 변수에 사용할 바인딩 방향을 나타내는 SQLULEN 값입니다.<br /><br /> 이 필드는 열 단위 바인딩을 선택 하는 SQL_PARAM_BIND_BY_COLUMN (기본값)로 설정 됩니다.<br /><br /> 행 단위 바인딩을 선택 하기 위해이 필드는 동적 매개 변수 집합에 바인딩되는 구조의 길이 또는 버퍼의 인스턴스로 설정 됩니다. 이 길이에는 바인딩된 매개 변수의 주소가 지정 된 길이 만큼 증가 하는 경우 결과는 다음 매개 변수 집합에서 동일한 매개 변수의 시작을 가리키도록 하기 위해 모든 바인딩된 매개 변수의 공간 및 구조체 또는 버퍼의 안쪽 여백을 포함 해야 합니다. ANSI C에서 *sizeof* 연산자를 사용 하는 경우이 동작이 보장 됩니다.<br /><br /> 자세한 내용은 [매개 변수 배열 바인딩](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)을 참조 하세요.<br /><br /> 이 문 특성을 설정 하면 APD 헤더의 SQL_DESC_ BIND_TYPE 필드가 설정 됩니다.|  
|SQL_ATTR_PARAM_OPERATION_PTR (ODBC 3.0)|\*SQL 문을 실행 하는 동안 매개 변수를 무시 하는 데 사용 되는 SQLUSMALLINT 값의 배열을 가리키는 SQLUSMALLINT 값입니다. 각 값은 SQL_PARAM_PROCEED (실행할 매개 변수의 경우) 또는 SQL_PARAM_IGNORE (매개 변수가 무시 되도록)로 설정 됩니다.<br /><br /> APD에서 SQL_DESC_ARRAY_STATUS_PTR가 가리키는 배열의 상태 값을 SQL_PARAM_IGNORE로 설정 하 여 처리 하는 동안 매개 변수 집합을 무시할 수 있습니다. 상태 값이 SQL_PARAM_PROCEED로 설정 된 경우 또는 배열에 요소가 설정 되지 않은 경우 매개 변수 집합이 처리 됩니다.<br /><br /> 이 문 특성은 null 포인터로 설정할 수 있으며,이 경우 드라이버는 매개 변수 상태 값을 반환 하지 않습니다. 이 특성은 언제 든 지 설정할 수 있지만 다음 번에 **Sqlexecdirect** 또는 **sqlexecute** 를 호출할 때까지 새 값이 사용 되지 않습니다.<br /><br /> 바인딩된 매개 변수가 없는 경우이 특성은 무시 됩니다.<br /><br /> 자세한 내용은 [매개 변수 배열 사용](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)을 참조 하세요.<br /><br /> 이 문 특성을 설정 하면 APD 헤더의 SQL_DESC_ARRAY_STATUS_PTR 필드가 설정 됩니다.|  
|SQL_ATTR_PARAM_STATUS_PTR (ODBC 3.0)|\* **Sqlexecute** 또는 **sqlexecdirect**를 호출한 후 매개 변수 값의 각 행에 대 한 상태 정보를 포함 하는 SQLUSMALLINT 값의 배열을 가리키는 SQLUSMALLINT 값입니다. 이 필드는 PARAMSET_SIZE 1 보다 큰 경우에만 필요 합니다.<br /><br /> 상태 값은 다음 값을 포함할 수 있습니다.<br /><br /> SQL_PARAM_SUCCESS:이 매개 변수 집합에 대해 SQL 문이 성공적으로 실행 되었습니다.<br /><br /> SQL_PARAM_SUCCESS_WITH_INFO:이 매개 변수 집합에 대해 SQL 문이 성공적으로 실행 되었습니다. 그러나 경고 정보는 진단 데이터 구조에서 사용할 수 있습니다.<br /><br /> SQL_PARAM_ERROR:이 매개 변수 집합을 처리 하는 동안 오류가 발생 했습니다. 추가 오류 정보는 진단 데이터 구조에서 사용할 수 있습니다.<br /><br /> SQL_PARAM_UNUSED:이 매개 변수 집합은 일부 이전 매개 변수 설정으로 인해 추가 처리가 중단 된 오류가 발생 했거나, SQL_ATTR_PARAM_OPERATION_PTR에서 지정한 배열의 해당 매개 변수 집합에 대해 SQL_PARAM_IGNORE 설정 되었기 때문에 사용 되지 않았습니다.<br /><br /> SQL_PARAM_DIAG_UNAVAILABLE: 드라이버는 매개 변수 배열을 모놀리식 단위로 처리 하므로이 수준의 오류 정보를 생성 하지 않습니다.<br /><br /> 이 문 특성은 null 포인터로 설정할 수 있으며,이 경우 드라이버는 매개 변수 상태 값을 반환 하지 않습니다. 이 특성은 언제 든 지 설정할 수 있지만 다음에 **Sqlexecute** 또는 **sqlexecdirect** 를 호출할 때까지 새 값이 사용 되지 않습니다. 이 특성을 설정 하면 드라이버에서 구현 하는 출력 매개 변수 동작에 영향을 줄 수 있습니다.<br /><br /> 자세한 내용은 [매개 변수 배열 사용](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)을 참조 하세요.<br /><br /> 이 문 특성을 설정 하면 IPD 헤더의 SQL_DESC_ARRAY_STATUS_PTR 필드가 설정 됩니다.|  
|SQL_ATTR_PARAMS_PROCESSED_PTR (ODBC 3.0)|\*오류 집합을 포함 하 여 처리 된 매개 변수 집합의 수를 반환할 버퍼를 가리키는 SQLULEN 레코드 필드입니다. Null 포인터인 경우에는 숫자가 반환 되지 않습니다.<br /><br /> 이 문 특성을 설정 하면 IPD 헤더의 SQL_DESC_ROWS_PROCESSED_PTR 필드가 설정 됩니다.<br /><br /> 이 특성이 가리키는 버퍼를 채우는 **Sqlexecdirect** 또는 **sqlexecute** 를 호출 하는 경우 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 반환 되지 않습니다. 버퍼의 내용은 정의 되지 않습니다.<br /><br /> 자세한 내용은 [매개 변수 배열 사용](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)을 참조 하세요.|  
|SQL_ATTR_PARAMSET_SIZE (ODBC 3.0)|각 매개 변수의 값 수를 지정 하는 SQLULEN 값입니다. SQL_ATTR_PARAMSET_SIZE가 1 보다 크면 APD에서 배열에 대 한 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR입니다. 각 배열의 카디널리티는이 필드의 값과 같습니다.<br /><br /> 바인딩된 매개 변수가 없는 경우이 특성은 무시 됩니다.<br /><br /> 자세한 내용은 [매개 변수 배열 사용](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)을 참조 하세요.<br /><br /> 이 문 특성을 설정 하면 APD 헤더의 SQL_DESC_ARRAY_SIZE 필드가 설정 됩니다.|  
|SQL_ATTR_QUERY_TIMEOUT (ODBC 1.0)|응용 프로그램으로 반환 되기 전에 SQL 문이 실행 될 때까지 대기 하는 시간 (초)에 해당 하는 SQLULEN 값입니다. 값 *Eptr* 이 0 (기본값) 이면 시간 제한이 없습니다.<br /><br /> 지정 된 제한 시간이 데이터 원본의 최대 시간 제한을 초과 하거나 최소 시간 제한 보다 작은 경우 **SQLSetStmtAttr** 는 해당 값을 대체 하 고 SQLSTATE 01 S 02 (옵션 값이 변경 됨)를 반환 합니다.<br /><br /> **Select** 문이 시간 초과 되 면 응용 프로그램에서 **SQLCloseCursor** 를 호출 하 여 문을 다시 사용할 필요가 없습니다.<br /><br /> 이 문 특성에 설정 된 쿼리 제한 시간은 동기 모드와 비동기 모드 모두에서 유효 합니다.|  
|SQL_ATTR_RETRIEVE_DATA (ODBC 2.0)|SQLULEN 값:<br /><br /> SQL_RD_ON = **Sqlfetchscroll** 및 ODBC 3.X에서 **sqlfetch** 는 지정 된 위치에 커서를 배치 하 고 나 서 *데이터를 검색*합니다. 이것이 기본값입니다.<br /><br /> SQL_RD_OFF = **Sqlfetchscroll** 및 ODBC 3.X에서 **sqlfetch** 는 커서가 배치 된 후 *데이터를 검색*하지 않습니다.<br /><br /> 응용 프로그램은 SQL_RETRIEVE_DATA를 SQL_RD_OFF 설정 하 여 행이 존재 하는지 확인 하거나 행을 검색 하는 오버 헤드를 발생 시 키 지 않고 행의 책갈피를 검색할 수 있습니다. 자세한 내용은 [행 스크롤 및 페치](../../../odbc/reference/develop-app/scrolling-and-fetching-rows-odbc.md)를 참조 하세요.<br /><br /> 이 특성의 값은 열린 커서에 대해 설정할 수 있습니다. 그러나 설정이 즉시 적용 되는 것은 아닙니다 .이 경우 드라이버는 SQLSTATE 01 S 02 (옵션 값이 변경 됨)를 반환 하 고 특성을 원래 값으로 다시 설정 합니다.|  
|SQL_ATTR_ROW_ARRAY_SIZE (ODBC 3.0)|Sqlfetch 또는 **Sqlulen**에 대 한 각 호출에서 반환 되는 행 **SQLFetch** 수를 지정 하는 sqlulen 값입니다. **SQLBulkOperations**의 대량 책갈피 작업에 사용 되는 책갈피 배열의 행 수 이기도 합니다. 기본값은 1입니다.<br /><br /> 지정 된 행 집합이 데이터 원본에서 지원 되는 최대 행 집합 크기를 초과 하는 경우 드라이버는 해당 값을 대체 하 고 SQLSTATE 01 S 02 (옵션 값이 변경 됨)를 반환 합니다.<br /><br /> 자세한 내용은 [행 집합 크기](../../../odbc/reference/develop-app/rowset-size.md)를 참조 하십시오.<br /><br /> 이 문 특성을 설정 하면 고가 헤더의 SQL_DESC_ARRAY_SIZE 필드가 설정 됩니다.|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR (ODBC 3.0)|열 데이터의 바인딩을 변경 하기 위해 포인터에 추가 되는 오프셋을 가리키는 SQLULEN * 값입니다. 이 필드가 null이 아닌 경우 드라이버는 포인터를 역참조 하 고 설명자 레코드 (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR)의 각 지연 된 필드에 역참조 된 값을 추가 하 고 바인딩할 때 새 포인터 값을 사용 합니다. 기본적으로 null로 설정 됩니다.<br /><br /> 이 문 특성을 설정 하면 고가 헤더의 SQL_DESC_BIND_OFFSET_PTR 필드가 설정 됩니다.|  
|SQL_ATTR_ROW_BIND_TYPE (ODBC 1.0)|연결 된 문에서 **Sqlfetch** 또는 **sqlulen** 을 호출할 때 사용할 바인딩 방향을 설정 하는 sqlulen 값입니다. 값을 SQL_BIND_BY_COLUMN 설정 하 여 열 단위 바인딩을 선택 합니다. 행 단위 바인딩은 값을 구조체의 길이 또는 결과 열이 바인딩될 버퍼의 인스턴스로 설정 하 여 선택 합니다.<br /><br /> 길이가 지정 된 경우 바인딩된 열의 주소가 지정 된 길이 만큼 증가 하는 경우 결과는 다음 행에서 동일한 열의 시작을 가리키도록 하기 위해 모든 바인딩된 열과 구조 또는 버퍼의 패딩에 대 한 공간을 포함 해야 합니다. ANSI C의 구조체 또는 공용 구조체와 함께 **sizeof** 연산자를 사용 하는 경우이 동작이 보장 됩니다.<br /><br /> 열 단위 바인딩은 **Sqlfetch** 및 **sqlfetchscroll**에 대 한 기본 바인딩 방향입니다.<br /><br /> 자세한 내용은 [블록 커서에 사용할 열 바인딩](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)을 참조 하세요.<br /><br /> 이 문 특성을 설정 하면 고가 헤더의 SQL_DESC_BIND_TYPE 필드가 설정 됩니다.|  
|SQL_ATTR_ROW_NUMBER (ODBC 2.0)|전체 결과 집합의 현재 행 번호를 나타내는 SQLULEN 값입니다. 현재 행의 번호를 확인할 수 없거나 현재 행이 없는 경우 드라이버는 0을 반환 합니다.<br /><br /> 이 특성은 **SQLGetStmtAttr** 를 호출 하 여 검색할 수 있지만 **SQLSetStmtAttr**에 대 한 호출로는 설정할 수 없습니다.|  
|SQL_ATTR_ROW_OPERATION_PTR (ODBC 3.0)|SQLSetPos를 \* 사용 하 여 대량 작업을 수행 하는 동안 행을 무시 하는 데 사용 되는 **SQLSetPos**SQLUSMALLINT 값의 배열을 가리키는 SQLUSMALLINT 값입니다. 각 값은 SQL_ROW_PROCEED (대량 작업에 포함 될 행의 경우) 또는 SQL_ROW_IGNORE (대량 작업에서 제외 될 행의 경우)로 설정 됩니다. **SQLBulkOperations**를 호출 하는 동안이 배열을 사용 하 여 행을 무시할 수 없습니다.<br /><br /> 이 문 특성은 null 포인터로 설정할 수 있으며,이 경우 드라이버는 행 상태 값을 반환 하지 않습니다. 이 특성은 언제 든 지 설정할 수 있지만 다음에 **SQLSetPos** 를 호출할 때까지 새 값이 사용 되지 않습니다.<br /><br /> 자세한 내용은 SQLSetPos를 사용 하 여 행 [집합의 행 업데이트](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md) 및 [sqlsetpos를 사용 하 여 행 집합에서 행 삭제](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)를 참조 하세요.<br /><br /> 이 문 특성을 설정 하면 SQL_DESC_ARRAY_STATUS_PTR 필드가 설정 됩니다.|  
|SQL_ATTR_ROW_STATUS_PTR (ODBC 3.0)|\* **Sqlfetch** 또는 **sqlfetchscroll**을 호출한 후 행 상태 값을 포함 하는 SQLUSMALLINT 값의 배열을 가리키는 SQLUSMALLINT 값입니다. 배열에 행 집합의 행 수 만큼의 요소가 있습니다.<br /><br /> 이 문 특성은 null 포인터로 설정할 수 있으며,이 경우 드라이버는 행 상태 값을 반환 하지 않습니다. 이 특성은 언제 든 지 설정할 수 있지만 다음 번에 **SQLBulkOperations**, **sqlfetch**, **sqlfetchscroll**또는 **SQLSetPos** 를 호출할 때까지 새 값이 사용 되지 않습니다.<br /><br /> 자세한 내용은 [인출 된 행 수 및 상태](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)를 참조 하세요.<br /><br /> 이 문 특성을 설정 하면 IRD 헤더의 SQL_DESC_ARRAY_STATUS_PTR 필드가 설정 됩니다.<br /><br /> 이 특성은 **Sqlextendedfetch**호출에서 ODBC *2.X 드라이버를* *rgbRowStatus* 배열에 매핑합니다.|  
|SQL_ATTR_ROWS_FETCHED_PTR (ODBC 3.0)|\*Sqlfetch 또는 **Sqlulen**에 대 한 호출 후 인출 된 행 수, SQL_REFRESH의 *작업* 인수를 사용 하 **SQLFetch** 여 **SQLSetPos** 호출에 의해 수행 된 대량 작업의 영향을 받는 행 수 또는 **SQLBulkOperations**에서 수행 하는 대량 작업의 영향을 받는 행 수를 반환 하는 sqlulen 값입니다. 이 수에는 오류 행이 포함 됩니다.<br /><br /> 자세한 내용은 [인출 된 행 수 및 상태](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)를 참조 하세요.<br /><br /> 이 문 특성을 설정 하면 IRD 헤더의 SQL_DESC_ROWS_PROCESSED_PTR 필드가 설정 됩니다.<br /><br /> 이 특성이 가리키는 버퍼를 채우는 **Sqlfetch** 또는 **sqlfetchscroll** 에 대 한 호출이 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하지 않는 경우 버퍼의 내용이 정의 되지 않습니다.|  
|SQL_ATTR_SIMULATE_CURSOR (ODBC 2.0)|위치 지정 update 및 delete 문을 시뮬레이트하는 드라이버가 하나의 단일 행에만 영향을 주는지 여부를 지정 하는 SQLULEN 값입니다.<br /><br /> 현재 행의 각 열 값을 지정 하는 **where** 절을 포함 하는 검색 된 **update** 또는 **delete** 문을 구성 하는 경우에는 위치 지정 update 및 delete 문을 시뮬레이트할 수 있습니다. 이러한 열이 고유 키를 구성 하지 않는 한 이러한 문은 둘 이상의 행에 영향을 줄 수 있습니다.<br /><br /> 이러한 문이 하나의 행에만 영향을 주기 위해 드라이버는 고유 키의 열을 결정 하 고 이러한 열을 결과 집합에 추가 합니다. 응용 프로그램에서 결과 집합의 열이 고유 키를 구성 하는 것을 보장 하는 경우 드라이버는이 작업을 수행할 필요가 없습니다. 이로 인해 실행 시간이 줄어들 수 있습니다.<br /><br /> SQL_SC_NON_UNIQUE = 드라이버는 시뮬레이트된 위치 지정 update 또는 delete 문이 하나의 행에만 영향을 주는지 보장 하지 않습니다. 이 작업은 응용 프로그램의 책임입니다. 문이 둘 이상의 행에 영향을 주는 경우 **Sqlexecute**, **sqlexecdirect**또는 **SQLSetPos** 는 SQLSTATE 01001 (커서 작업 충돌)를 반환 합니다.<br /><br /> SQL_SC_TRY_UNIQUE = 드라이버가 시뮬레이션 된 위치 지정 update 또는 delete 문이 하나의 행에만 영향을 주는지 보장 하려고 합니다. 드라이버는 고유 키가 없는 경우와 같이 둘 이상의 행에 영향을 줄 수 있는 경우에도 이러한 문을 항상 실행 합니다. 문이 둘 이상의 행에 영향을 주는 경우 **Sqlexecute**, **sqlexecdirect**또는 **SQLSetPos** 는 SQLSTATE 01001 (커서 작업 충돌)를 반환 합니다.<br /><br /> SQL_SC_UNIQUE = 드라이버는 시뮬레이트된 위치 지정 update 또는 delete 문이 하나의 행에만 영향을 줍니다. 드라이버가 지정 된 문에 대해이를 보장할 수 없는 경우 **Sqlexecdirect** 또는 **sqlprepare** 에서 오류를 반환 합니다.<br /><br /> 데이터 원본에서 위치 지정 update 및 delete 문에 대 한 기본 SQL 지원을 제공 하 고 드라이버가 커서를 시뮬레이션 하지 않는 경우 SQL_SIMULATE_CURSOR에 대해 SQL_SC_UNIQUE 요청 될 때 SQL_SUCCESS 반환 됩니다. SQL_SC_TRY_UNIQUE 또는 SQL_SC_NON_UNIQUE를 요청 하면 SQL_SUCCESS_WITH_INFO 반환 됩니다. 데이터 원본에서 지원 되는 SQL_SC_TRY_UNIQUE 수준을 제공 하는데 드라이버가 그렇지 않으면 SQL_SC_TRY_UNIQUE에 대해 SQL_SUCCESS 반환 되 고 SQL_SC_NON_UNIQUE에 대해 SQL_SUCCESS_WITH_INFO 반환 됩니다.<br /><br /> 데이터 원본에서 지정 된 커서 시뮬레이션 유형을 지원 하지 않는 경우 드라이버는 다른 시뮬레이션 유형을 대체 하 고 SQLSTATE 01 S 02 (옵션 값이 변경 됨)을 반환 합니다. SQL_SC_UNIQUE의 경우 드라이버는 순서 대로 (SQL_SC_TRY_UNIQUE 또는 SQL_SC_NON_UNIQUE를 대체 합니다. SQL_SC_TRY_UNIQUE의 경우 드라이버는 SQL_SC_NON_UNIQUE 대체 합니다.<br /><br /> 기본값은 SQL_SC_UNIQUE입니다.<br /><br /> 자세한 내용은 [위치 지정 업데이트 및 Delete 문 시뮬레이션](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)을 참조 하세요.|  
|SQL_ATTR_USE_BOOKMARKS (ODBC 2.0)|응용 프로그램에서 커서와 함께 책갈피를 사용할지 여부를 지정 하는 SQLULEN 값입니다.<br /><br /> SQL_UB_OFF = Off (기본값)<br /><br /> SQL_UB_VARIABLE = 응용 프로그램은 커서와 함께 책갈피를 사용 하 고, 지원 되는 경우 드라이버는 가변 길이 책갈피를 제공 합니다. SQL_UB_FIXED *은 ODBC 3.x*에서 더 이상 사용 되지 않습니다. ODBC *2.x 응용 프로그램은 항상* 가변 길이 책갈피를 사용 해야 *합니다. odbc 2.x 드라이버 (* 4 바이트, 고정 길이 책갈피만 지원 됨)로 작업 하는 경우에도 마찬가지입니다. 고정 길이 책갈피는 가변 길이 책갈피의 특별 한 경우에만 발생 하기 때문입니다. ODBC 2.x 드라이버를 사용 하는 경우 드라이버 관리자는 SQL_UB_VARIABLE를 SQL_UB_FIXED에 *매핑합니다.*<br /><br /> 커서와 함께 책갈피를 사용 하려면 커서를 열기 전에 응용 프로그램에서 SQL_UB_VARIABLE 값을 사용 하 여이 특성을 지정 해야 합니다.<br /><br /> 자세한 내용은 [책갈피 검색](../../../odbc/reference/develop-app/retrieving-bookmarks.md)을 참조 하세요.|  
  
 [1] 설명자가 응용 프로그램 설명자가 아니라 구현 설명자 인 경우에만 이러한 함수를 비동기적으로 호출할 수 있습니다.  
  
 [열 단위](../../../odbc/reference/develop-app/column-wise-binding.md) 바인딩 및 [행 단위 바인딩](../../../odbc/reference/develop-app/row-wise-binding.md)을 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|연결 특성의 설정 반환|[SQLGetConnectAttr 함수(SQLGetConnectAttr Function)](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|문 특성의 설정 반환|[SQLGetStmtAttr 함수](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|연결 특성 설정|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|설명자의 단일 필드 설정|[SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
