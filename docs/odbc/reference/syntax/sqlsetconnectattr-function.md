---
title: "SQLSetConnectAttr 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLSetConnectAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConnectAttr
helpviewer_keywords:
- SQLSetConnectAttr function [ODBC]
ms.assetid: 97fc7445-5a66-4eb9-8e77-10990b5fd685
caps.latest.revision: 83
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4006d05403781ada24cf43903cd14a971366e12a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconnectattr-function"></a>SQLSetConnectAttr 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLSetConnectAttr** 연결의 측면을 제어 하는 특성을 설정 합니다.  
  
> [!NOTE]  
>  어떤 드라이버 관리자는이 함수를 경우 맵을 ODBC 3에 대 한 자세한 내용은*.x* 응용 프로그램이 ODBC 2와 작동*.x* 드라이버 참조 [뒤로 대 한 대체 함수 매핑 응용 프로그램 호환성](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLSetConnectAttr(  
     SQLHDBC       ConnectionHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>인수  
 *ConnectionHandle*  
 [입력] 연결 핸들입니다.  
  
 *Attribute*  
 [입력] 특성을 설정 하려면 "설명"에 나열 된  
  
 *ValuePtr*  
 [입력] 연결 된 값에 대 한 포인터 *특성*합니다. 값에 따라 *특성*, *ValuePtr* 부호 없는 정수 값 또는 null로 끝나는 문자열을 가리킵니다. 정수 계열 형식이 고 *특성* 인수 길이가 고정 될 수 있습니다 세부 정보에 대 한 설명 섹션을 참조 합니다.  
  
 *StringLength*  
 [입력] 경우 *특성* 은 ODBC 정의 된 특성 및 *ValuePtr* 문자열 또는 이진 버퍼를 가리키거나,이 인수 길이 여야 합니다 **ValuePtr*합니다. 문자 문자열 데이터에 대 한이 인수는 문자열의 바이트 수를 포함 해야 합니다.  
  
 경우 *특성* 은 ODBC 정의 된 특성 및 *ValuePtr* 정수 이면 *StringLength* 는 무시 됩니다.  
  
 경우 *특성* 드라이버에서 정의 된 특성은 응용 프로그램을 설정 하 여 드라이버 관리자 특성의 특성을 나타내는 *StringLength* 인수입니다. *StringLength* 다음 값을 가질 수 있습니다.  
  
-   경우 *ValuePtr* 다음 문자열을에 대 한 포인터는 *StringLength* SQL_NTS 또는 문자열의 길이입니다.  
  
-   경우 *ValuePtr* 이진 버퍼에 대 한 포인터에 있으면 응용 프로그램은 SQL_LEN_BINARY_ATTR의 결과 배치 (*길이*) 매크로에서 *StringLength*합니다. 이렇게 하면 배치에 음수 값 *StringLength*합니다.  
  
-   경우 *ValuePtr* 문자열 또는 이진 문자열 이외의 값에 대 한 포인터는 *StringLength* SQL_IS_POINTER 값이 있어야 합니다.  
  
-   경우 *ValuePtr* 고정 길이 값이 다음 포함 *StringLength* 되었거나 SQL_IS_INTEGER SQL_IS_UINTEGER를 적절 하 게 합니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE, 또는 SQL_STILL_EXECUTING 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLSetConnectAttr** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* 의 Sql_handle_dbc 라는 및 *처리* 의 *ConnectionHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLSetConnectAttr** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
 드라이버는 옵션을 설정할 때의 결과 대 한 정보를 제공 하는 SQL_SUCCESS_WITH_INFO를 반환할 수 있습니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01 S 02|옵션 값이 변경 됨|드라이버에 지정 된 값을 지원 하지 않았습니다 *ValuePtr* 유사한 값을 대체 합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08002|사용 중인 연결 이름|*특성* 인수 SQL_ATTR_ODBC_CURSORS, 였으며 드라이버는 데이터 원본에 이미 연결 되었습니다.|  
|08003|연결이 열려 있지 않습니다|DM ()는 *특성* 열려 있는 연결을 필요로 하는 값이 지정 되지만 *ConnectionHandle* 가 연결 된 상태가 아닙니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|24000|잘못된 커서 상태|*특성* 인수 SQL_ATTR_CURRENT_CATALOG, 였으며 결과 집합을 보류 중 상태 였습니다.|  
|25000|로컬 트랜잭션이 있는 동안 잘못 된 작업|SQL_ATTR_ENLIST_IN_DTC 연결 특성을 설정 하 여 분산된 트랜잭션 연결 (DTC)에 참여 하는 동안 로컬 트랜잭션에 대 한 연결이 했습니다.<br /><br /> 연결이 DTC를 이미 등록 되어 있습니다.<br /><br /> 분산된 트랜잭션 연결을 등록 된 연결 및 SQL_ATTR_AUTOCOMMIT을 SQL_AUTOCOMMIT_OFF로 설정 하 여 로컬 트랜잭션을 시작 합니다.|  
|3D000|잘못 된 카탈로그 이름|*특성* 인수 SQL_CURRENT_CATALOG, 되었으며 지정 된 카탈로그 이름이 올바르지 않습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에 * \*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *ConnectionHandle*합니다. **SQLSetConnectAttr** 함수를 호출 하 고, 실행을 완료 하기 전에 [SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md) 에서 호출 된는 *ConnectionHandle*, 다음의 **SQLSetConnectAttr** 에서 다시 호출 된 함수는 *ConnectionHandle*합니다.<br /><br /> 또는 **SQLSetConnectAttr** 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancelHandle** 에서 호출 된는 *ConnectionHandle* 의 서로 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|*특성* 인수 문자열 값이 필요한 한 연결 특성을 식별 및 *ValuePtr* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()를 비동기적으로 실행 중인 함수에 대해 호출 되었습니다는 *StatementHandle* 연관 된 *ConnectionHandle* 때 계속 실행 하 고 **SQLSetConnectAttr**호출 되었습니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *ConnectionHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 와 관련 된 문 핸들 중 하나에 대해 호출한는 *ConnectionHandle* SQL_PARAM_DATA_AVAILABLE를 반환 합니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 되었으며 한 *StatementHandle * 연관는 *ConnectionHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.<br /><br /> (DM) **SQLBrowseConnect** 에 대 한 호출 된는 *ConnectionHandle* SQL_NEED_DATA를 반환 합니다. 이 함수를 호출 **SQLBrowseConnect** SQL_SUCCESS_WITH_INFO 또는 관계 없이 SQL_SUCCESS를 반환 합니다.|  
|HY011|특성을 지금 설정할 수 없습니다.|*특성* 인수 SQL_ATTR_TXN_ISOLATION, 한 트랜잭션이 열려 였습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY024|잘못 된 특성 값|지정 된 주어진 *특성* 값에 잘못 된 값을 지정 된 *ValuePtr*합니다. (드라이버 관리자 연결 및 문 특성 SQL_ATTR_ACCESS_MODE 또는 SQL_ATTR_ASYNC_ENABLE 같은 값의 불연속 집합을 허용 하는 경우에이 SQLSTATE를 반환 합니다. 모든 다른 연결 및 문 특성에 대 한 드라이버에 지정 된 값을 확인 해야 *ValuePtr*.)<br /><br /> *특성* 인수 SQL_ATTR_TRACEFILE 되었거나 SQL_ATTR_TRANSLATE_LIB, 및 *ValuePtr* 가 빈 문자열입니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|*(DM) \*ValuePtr* , 문자열 및 *StringLength* 에 인수가 0 보다 작지 않음 SQL_NTS 없습니다.|  
|HY092|잘못 된 특성/옵션 식별자|인수에 대해 지정 된 값 (DM) *특성* ODBC 드라이버에서 지 원하는 버전에 대해 올바르지 않습니다.<br /><br /> 인수에 대해 지정 된 값 (DM) *특성* 읽기 전용 특성이 있습니다.|  
|HY114|드라이버가 연결 수준의 비동기 함수 실행을 지원 하지 않습니다.|(DM) 응용 프로그램 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 사용 하 여 비동기 연결 작업을 지원 하지 않는 드라이버에 대 한 비동기 함수 실행을 사용 하도록 설정 하려고 합니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HY121|커서 라이브러리 및 드라이버 인식 풀링 동시에 사용할 수 없습니다.|자세한 내용은 참조 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|인수에 대해 지정 된 값 *특성* 유효한 ODBC 연결 했습니다. 오류 또는 ODBC의 버전에 대 한 문 특성 드라이버에서 지원 되지만 드라이버에서 지원 하지 않았습니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *ConnectionHandle* 함수를 지원 하지 않습니다.|  
|IM009|변환 DLL을 로드할 수 없습니다.|드라이버 변환 연결에 대해 지정 된 DLL을 로드할 수 없습니다. 이 오류는 경우에만 반환 될 수 *특성* SQL_ATTR_TRANSLATE_LIB 됩니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
|S1118|드라이버는 비동기 알림을 지원 하지 않습니다.|SQL_ATTR_ASYNC_DBC_EVENT (연결) 한 후 설정한 있지만 비동기 알림이 드라이버에서 지원 되지 않습니다.|  
  
 때 *특성* 문 특성은 **SQLSetConnectAttr** 에서 반환 된 Sqlstate를 반환할 수 **SQLSetStmtAttr**합니다.  
  
## <a name="comments"></a>설명  
 연결 특성에 대 한 일반 정보를 참조 하십시오. [연결 특성](../../../odbc/reference/develop-app/connection-attributes.md)합니다.  
  
 현재 정의 된 특성 및 이러한 기능이 도입 된 ODBC 버전입니다;이 섹션의 뒷부분에 나오는 표에 표시 됩니다. 다른 데이터 원본 활용 하기 위해 더 많은 특성을 정의할는 사용할 수 있습니다. 특성의 범위는 ODBC;에 예약 되어 있습니다. 드라이버 개발자는 Open Group에서 드라이버 관련 사용을 위해 값을 예약 해야 합니다.  
  
> [!NOTE]  
>  연결 수준에서 호출 하 여 문 특성을 설정 하는 기능 **SQLSetConnectAttr** ODBC 3에서 사용 되지*.x*합니다. ODBC 3*.x* 응용 프로그램 연결 수준에서 문 특성을 설정 해서는 안됩니다. ODBC 3*.x* 연결 특성 및 문 특성 모두에 있으며 수 있는 SQL_ATTR_METADATA_ID 및 SQL_ATTR_ASYNC_ENABLE 특성을 제외 하 고 연결 수준에서 문 특성을 설정할 수 없습니다 연결 수준 또는 문 수준에서 설정 합니다.  
>   
>  ODBC 3*.x* 드라이버 ODBC 2와 작동 해야 하는 경우이 기능을 지원만 필요한*.x* ODBC 2를 설정 하는 응용 프로그램*.x* 연결 수준에서 문 옵션입니다. 자세한 내용은 참조 [SQLSetConnectOption 매핑](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) 이전 버전과 호환성에 대 한 부록 g: 드라이버 지침에 있습니다.  
  
 응용 프로그램에서 호출할 수 **SQLSetConnectAttr** 언제 든 지는 시간 사이의 연결이 할당 되 고 해제 합니다. 성공적으로 연결에 대 한 응용 프로그램을 설정 하는 모든 연결 및 문 특성 될 때까지 지속 **SQLFreeHandle** 연결에서 호출 됩니다. 예를 들어, 응용 프로그램을 호출 하는 경우 **SQLSetConnectAttr** 특성으로 데이터 원본에 연결 하기 전에 계속 되 면 경우에 **SQLSetConnectAttr** 응용 프로그램에 연결 하는 경우 드라이버에서 작동 하지 않습니다는 데이터 소스 응용 프로그램에 드라이버별 특성 설정, 응용 프로그램 연결에서 다른 드라이버에 연결 하는 경우에 특성 유지 합니다.  
  
 연결 된; 전에만 일부 연결 특성을 설정할 수 있습니다. 다른 사용자를 연결한 후에 설정할 수 있습니다. 다음 표에서 이전 또는 이후에 연결에 설정 해야 하는 해당 연결 특성을 나타냅니다. *어느* 앞 이나 뒤 연결 특성을 설정할 수 있도록 나타냅니다.  
  
|Attribute|하기 전이나 후 연결 설정|  
|---------------|-------------------------------------|  
|SQL_ATTR_ACCESS_MODE|[1]|  
|SQL_ATTR_ASYNC_DBC_EVENT|모두|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE|[4]|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK|모두|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT|모두|  
|SQL_ATTR_ASYNC_ENABLE|[2]|  
|SQL_ATTR_AUTO_IPD|모두|  
|SQL_ATTR_AUTOCOMMIT|[5]|  
|SQL_ATTR_CONNECTION_DEAD|After|  
|SQL_ATTR_CONNECTION_TIMEOUT|모두|  
|SQL_ATTR_CURRENT_CATALOG|[1]|  
|SQL_ATTR_DBC_INFO_TOKEN|After|  
|SQL_ATTR_ENLIST_IN_DTC|After|  
|SQL_ATTR_LOGIN_TIMEOUT|이전|  
|SQL_ATTR_METADATA_ID|모두|  
|SQL_ATTR_ODBC_CURSORS|이전|  
|SQL_ATTR_PACKET_SIZE|이전|  
|SQL_ATTR_QUIET_MODE|모두|  
|SQL_ATTR_TRACE|모두|  
|SQL_ATTR_TRACEFILE|모두|  
|SQL_ATTR_TRANSLATE_LIB|After|  
|SQL_ATTR_TRANSLATE_OPTION|After|  
|SQL_ATTR_TXN_ISOLATION|[3]|  
  
 [1] SQL_ATTR_ACCESS_MODE 및 SQL_ATTR_CURRENT_CATALOG 앞 이나 뒤에 연결 하는 드라이버에 따라 설정할 수 있습니다. 반면 상호 운용 가능한 응용 프로그램 설정에 연결 하기 전에 일부 드라이버에 연결한 후 이러한 변경 지원 하지 않기 때문입니다.  
  
 [2] SQL_ATTR_ASYNC_ENABLE 활성 문 사용이 설정 되어야 합니다.  
  
 [3] SQL_ATTR_TXN_ISOLATION 연결에서 열려 있는 트랜잭션이 있는 경우에 설정할 수 있습니다. 데이터 원본에 지정 된 값을 지원 하지 않는 경우 일부 연결 특성 값이 비슷한 대체를 지원 \* *ValuePtr*합니다. 이러한 경우 드라이버는 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01 s 02 반환 (옵션 값이 변경 됨). 예를 들어 경우 *특성* SQL_ATTR_PACKET_SIZE은 및 \* *ValuePtr* 최대 패킷 크기를 초과, 드라이버의 최대 크기를 대체 합니다. 대체 값을 확인 하려면 응용 프로그램이 호출 **SQLGetConnectAttr**합니다.  
  
 [호출 하는 동안 드라이버를 로드할 때 드라이버 관리자 드라이버의 특성을 설정 합니다 4] SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 설정 된 경우 연결이 열려 전에, **SQLBrowseConnect**, **SQLConnect**, 또는 **SQLDriverConnect**합니다. 에 대 한 호출 하기 전에 **SQLBrowseConnect**, **SQLConnect**, 또는 **SQLDriverConnect**, 드라이버 관리자에 연결 하는 드라이버를 알지 못하고 및 알 수 없습니다 여부는 드라이버는 비동기 연결 작업을 지원합니다. 따라서 드라이버 관리자는 항상 관계 없이 SQL_SUCCESS를 반환합니다. 하지만 드라이버 비동기 연결 작업에 대 한 호출의 경우를 지원 하지 않는 경우 **SQLBrowseConnect**, **SQLConnect**, 또는 **SQLDriverConnect** 실패 합니다.  
  
 [5] SQL_ATTR_AUTOCOMMIT을 FALSE로 설정 하면 응용 프로그램 API 트랜잭션 일관성을 유지 하는 SQL_ERROR를 반환 하는 경우 SQLEndTran(SQL_ROLLBACK) 호출 해야 합니다.  
  
 설정 하는 정보의 형식을 \* *ValuePtr* 지정 된 버퍼에 따라 달라 집니다 *특성*합니다. **SQLSetConnectAttr** 두 가지 형식 중 하나에 대 한 특성 정보를 수락할: null로 끝나는 문자열 또는 정수 값입니다. 각각의 형식 특성의 설명에 표시 됩니다. 가 가리키는 문자열은 *ValuePtr* 의 인수 **SQLSetConnectAttr** 길이 *StringLength* 바이트입니다.  
  
 *StringLength* 인수 길이 특성으로 정의 되어 있으면 ODBC 2에 도입 된 모든 특성의 경우 처럼*.x* 또는 이전 버전입니다.  
  
|*Attribute*|*ValuePtr* 내용|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE (ODBC 1.0)|SQLUINTEGER 값입니다. SQL_MODE_READ_ONLY는 드라이버 또는 데이터 소스에서 연결이 필요 하지 않은 업데이트를 수행할 발생 하는 SQL 문을 지원 하기 위해 표시기로 사용 됩니다. 이 모드를 사용 하 여 잠금 전략, 트랜잭션 관리 또는 드라이버 또는 데이터 원본에 따라 다른 영역 최적화할 수 있습니다. 드라이버는 데이터 원본에 전송 되지 않도록 이러한 문을 실행할 필요가 없습니다. 드라이버 및 데이터 원본 읽기 전용은 읽기 전용 연결 하는 동안 SQL 문을 처리 하도록 요청 될 때의 동작은 구현 시 정의 합니다. SQL_MODE_READ_WRITE 기본값입니다.|  
|SQL_ATTR_ASYNC_DBC_EVENT (ODBC 3.8)|이벤트 핸들에 해당 하는 대 SQLPOINTER 값입니다.<br /><br /> 비동기 함수의 완료 알림을 호출 하 여 **SQLSetConnectAttr** SQL_ATTR_ASYNC_STMT_EVENT 특성과 이벤트 핸들을 지정 하를 사용 합니다. **참고:** 알림 방법을 커서 라이브러리와 함께 사용할 수 없습니다. 응용 프로그램 알림 방법을 사용 하도록 설정한 경우 SQLSetConnectAttr 통해 커서 라이브러리를 사용 하도록 설정 하려고 하면 오류 메시지가 표시 됩니다.|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE (ODBC 3.8)|비동기 실행을 사용할지 여부를 지정 하는 SQLUINTEGER 값 연결 핸들에는 함수를 선택 합니다. 자세한 내용은 참조 [비동기 실행 (폴링 방법)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)합니다.<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = 지정 된 연결 관련 함수에 대 한 비동기 작업을 활성화 합니다.<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = 지정 된 연결 관련 함수에 대 한 비동기 작업 (기본값) 사용 하지 않도록 설정 합니다.<br /><br /> 설정 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE은 항상 동기 (즉, 돌아가지 SQL_STILL_EXECUTING).<br /><br /> 문 작업의 비동기 실행 SQL_ATTR_ASYNC_ENABLE을 사용 하도록 설정 됩니다.|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK (ODBC 3.8)|Context 구조체를 가리키는 대 SQLPOINTER 값입니다.<br /><br /> 드라이버 관리자는 드라이버를 호출할 수만 **SQLSetStmtAttr** 이 특성이 있는 함수입니다.|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT (ODBC 3.8)|상황에 맞는 구조체를 가리키는 대 SQLPOINTER 값입니다.<br /><br /> 드라이버 관리자는 드라이버를 호출할 수만 **SQLSetStmtAttr** 이 특성이 있는 함수입니다.|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 3.0)|지정된 된 연결에서 문을 사용 하 여 호출 하는 함수를 비동기적으로 실행 되는지 여부를 지정 하는 SQLULEN 값:<br /><br /> SQL_ASYNC_ENABLE_OFF = 문 작업 (기본값)에 대 한 연결 수준 비동기 실행 지원을 사용 하지 않도록 설정 합니다.<br /><br /> SQL_ASYNC_ENABLE_ON = 문 작업에 대 한 연결 수준 비동기 실행 지원을 사용 하도록 설정 합니다.<br /><br /> 이 특성은 수 있는지 여부를 설정 **SQLGetInfo** SQL_ASYNC_MODE 정보로 유형 SQL_AM_CONNECTION 또는 SQL_AM_STATEMENT을 반환 합니다.|  
|SQL_ATTR_AUTO_IPD (ODBC 3.0)|지정 하는 읽기 전용 SQLUINTEGER 값 여부을 호출한 후에 IPD의 자동 채우기를 **SQLPrepare** 지원 됩니다.<br /><br /> SQL_TRUE을 호출한 후에 IPD의 자동 채우기를 = **SQLPrepare** 드라이버에서 지원 됩니다.<br /><br /> SQL_FALSE을 호출한 후에 IPD의 자동 채우기를 = **SQLPrepare** 드라이버에서 지원 되지 않습니다. 준비 된 문을 지원 하지 않는 서버는 IPD를 자동으로 채울 수 없습니다.<br /><br /> SQL_TRUE SQL_ATTR_AUTO_IPD 연결 특성에 대해 반환 되 면 SQL_ATTR_ENABLE_AUTO_IPD 문 특성은 IPD의 자동 채우기를 켜기 / 끄기를 설정할 수 있습니다. SQL_ATTR_AUTO_IPD SQL_FALSE 이면 SQL_ATTR_ENABLE_AUTO_IPD SQL_TRUE로 설정할 수 없습니다. 기본값인 SQL_ATTR_ENABLE_AUTO_IPD SQL_ATTR_AUTO_IPD의 값과 같습니다.<br /><br /> 이 연결 특성에서 반환 될 수 **SQLGetConnectAttr** 으로 설정할 수 있지만 **SQLSetConnectAttr**합니다.|  
|SQL_ATTR_AUTOCOMMIT (ODBC 1.0)|자동 커밋 또는 수동 커밋 모드를 사용할지 여부를 지정 하는 SQLUINTEGER 값:<br /><br /> SQL_AUTOCOMMIT_OFF = 수동 커밋 모드를 사용 하는 드라이버 및 응용 프로그램이 명시적으로 커밋하거나 사용 하 여 트랜잭션을 롤백할 **SQLEndTran**합니다.<br /><br /> SQL_AUTOCOMMIT_ON = 드라이버 사용 하 여 자동 커밋 모드입니다. 각 문이 실행 된 직후에 커밋됩니다. 기본값입니다. 수동 커밋 모드에서 자동 커밋 모드로 변경 하려면 SQL_ATTR_AUTOCOMMIT을 SQL_AUTOCOMMIT_ON로 설정 된 연결에서 열려 있는 모든 트랜잭션이 커밋됩니다.<br /><br /> 자세한 내용은 참조 [커밋 모드](../../../odbc/reference/develop-app/commit-mode.md)합니다. **중요:** 액세스 계획을 삭제 하는 일부 데이터 원본 및 닫기 때마다 연결의 모든 문에 대해 커서 문이 커밋될 지; 자동 커밋 모드로 실행할지 아니면 커서가 있는 경우 각 nonquery 문이 실행 된 후에 발생할 수 있습니다 쿼리에 대 한 닫힙니다. 자세한 내용은 참조에서 SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 유형이 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 및 [커서 및 준비 된 문에서 영향의 트랜잭션을](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)합니다. <br /><br /> 일괄 처리는 자동 커밋 모드에서 실행 되 면 다음 두 가지 될 수 있습니다. 전체 일괄 처리는 autocommitable 단위로 처리 되거나 일괄 처리의 각 문에 autocommitable 단위로 처리 됩니다. 특정 데이터 원본 모두 이러한 동작을 지원할 수 있습니다 및 둘 중 하나를 선택 하는 방법을 제공할 수 있습니다. 각 개별 일괄 처리 문의 autocommitable 인지 또는 autocommitable 단위로 일괄 처리는 처리할지 여부를 드라이버에서 정의한지 않습니다.|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> (ODBC 3.5)|읽기 전용 SQLUINTEGER 값 연결의 상태를 나타내는입니다. SQL_CD_TRUE, 연결이 손실 된 경우에 합니다. SQL_CD_FALSE, 연결이 아직 활성 상태인 경우 사용 됩니다.|  
|SQL_ATTR_CONNECTION_TIMEOUT (ODBC 3.0)|모든 요청에 대 한 연결을 응용 프로그램에 반환 하기 전에 완료를 대기할 시간 (초)의 수에 해당 하는 SQLUINTEGER 값입니다. 드라이버는 SQLSTATE HYT00 반환 해야 (제한 시간이 만료 되었습니다) 언제 든 지 해당 하는 것 가능 쿼리 실행 또는 로그인에 연결 되지 않은 경우에서 시간 초과 합니다.<br /><br /> 경우 *ValuePtr* 은 0 (기본값) 같음, 시간 제한은 없습니다.|  
|SQL_ATTR_CURRENT_CATALOG (ODBC 2.0)|데이터 원본에서 사용할 수 있는 카탈로그의 이름을 포함 하는 문자열입니다. 예를 들어 SQL Server에서 카탈로그 이므로 데이터베이스 드라이버 보냅니다는 **사용** *데이터베이스* 문의 데이터 원본에 있는 *데이터베이스* 은에 지정 된 데이터베이스 \* *ValuePtr*합니다. 단일 계층 드라이버를 드라이버에서 현재 디렉터리에 지정 된 디렉터리 변경 카탈로그 디렉터리를 수 있습니다 **ValuePtr*합니다.|  
|SQL_ATTR_DBC_INFO_TOKEN (ODBC 3.8|설정 하는 데 대 SQLPOINTER 값 다시 연결 정보 토큰의 dbc 입니다에 처리할 때 [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)의 (\**pRating*) 매개 변수는 100과 같습니다.<br /><br /> SQL_ATTR_DBC_INFO_TOKEN 집합 전용입니다. 사용할 수 없으면 **SQLGetConnectAttr** 또는 **SQLGetConnectOption** 이 값을 검색 합니다. 드라이버 관리자 **SQLSetConnectAttr** 응용 프로그램은이 특성을 설정 하지 않아야 하므로 SQL_ATTR_DBC_INFO_TOKEN을 허용 하지 것입니다.<br /><br /> SQL_ATTR_DBC_INFO_TOKEN를 설정한 후 SQL_ERROR를 반환 하는 드라이버, 풀에서 얻은 연결을 삭제할 수 있습니다. 그런 다음 드라이버 관리자는 다른 연결 풀에서 가져오기 하려고 합니다. 참조 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md) 자세한 정보에 대 한 합니다.|  
|SQL_ATTR_ENLIST_IN_DTC (ODBC 3.0)|ODBC 드라이버를 사용할지 여부를 지정 하는 대 SQLPOINTER 값 분산 트랜잭션을 Microsoft 구성 요소 서비스에 의해 조정 합니다.<br /><br /> DTC OLE 트랜잭션 개체 연결 사이의 DTC 관계를 종료 하려면 SQL Server 또는 SQL_DTC_DONE에 내보낼 트랜잭션을 지정 하는 전달 합니다.<br /><br /> 클라이언트는 하 여 MS DTC 트랜잭션을 시작 하 고 해당 트랜잭션을 나타내는 MS DTC 트랜잭션 개체를 만들 Microsoft Distributed Transaction Coordinator (MS DTC) OLE itransactiondispenser:: Begintransaction 메서드를 호출 합니다. 그런 다음 응용 프로그램 ODBC 연결과 트랜잭션 개체를 연결 하는 SQL_ATTR_ENLIST_IN_DTC 옵션 사용 SQLSetConnectAttr을 호출 합니다. 관련된 모든 데이터베이스 작업은 MS DTC 트랜잭션의 보호 아래 수행됩니다. 응용 프로그램에 대 한 호출에서는 sql_dtc_done과 함께와 SQLSetConnectAttr 연결 사이의 DTC 관계를 종료 합니다. 자세한 내용은 MS DTC 설명서를 참조하십시오.|  
|SQL_ATTR_LOGIN_TIMEOUT (ODBC 1.0)|로그인 요청을 응용 프로그램에 반환 하기 전에 완료 될 때까지 기다리는 시간 (초) 번호에 해당 하는 SQLUINTEGER 값입니다. 기본값은 드라이버에 따라 다릅니다. 경우 *ValuePtr* 0 이며 제한 시간을 사용할 수 없습니다. 연결 시도 무기한 대기 합니다.<br /><br /> 지정된 된 제한 시간 데이터 원본에서 최대 로그인 제한 시간을 초과 하면 드라이버 해당 값을 대체 하 고 SQLSTATE 01 s 02 반환 (옵션 값이 변경 됨).|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|카탈로그 함수의 문자열 인수를 처리 하는 방법을 결정 하는 SQLUINTEGER 값입니다.<br /><br /> 경우 카탈로그 함수에서 문자열 인수의 sql_true는 해당 식별자로 처리 됩니다. 대/소문자는 중요 하지 않습니다. Nondelimited 문자열에 대 한 드라이버 후행 공백을 제거 하 고 문자열은 대문자로 접히지 키를 누릅니다. 구분 기호로 분리 된 문자열에 대 한 드라이버 선행 또는 후행 공백을 모두 제거 하 고이 구분 기호 사이 관계 없이 말 그대로 사용 합니다. 이러한 인수 중 하나가 null 포인터로 설정 되어, 함수 반환 SQL_ERROR 및 SQLSTATE HY009 (null 포인터를 잘못 사용).<br /><br /> 경우 SQL_FALSE, 문자열 인수는 카탈로그 함수 식별자로 처리 되지 않습니다. 대/소문자는 중요 합니다. 수 포함 하거나 string 검색 패턴 여부는 인수에 따라 합니다.<br /><br /> 기본값은 SQL_FALSE입니다.<br /><br /> *TableType* 의 인수 **SQLTables**,이 특성에 의해 영향을 받지 않습니다 값 목록을 사용 하는 합니다.<br /><br /> SQL_ATTR_METADATA_ID 문 수준에서 설정할 수도 있습니다. (이 문 특성 이기도 유일한 연결 특성.)<br /><br /> 자세한 내용은 참조 [카탈로그 함수의 인수와](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)합니다.|  
|SQL_ATTR_ODBC_CURSORS (ODBC 2.0)|드라이버 관리자에서 ODBC 커서 라이브러리를 사용 하는 방법을 지정 하는 SQLULEN 값:<br /><br /> SQL_CUR_USE_IF_NEEDED 필요할 경우에 사용 하 여 드라이버 관리자에서 ODBC 커서 라이브러리 = 합니다. 드라이버에서 SQL_FETCH_PRIOR 옵션을 지 원하는 경우 **SQLFetchScroll**, 드라이버 관리자는 드라이버의 스크롤 기능을 사용 합니다. 이렇게 하지 않으면 ODBC 커서 라이브러리를 사용합니다.<br /><br /> SQL_CUR_USE_ODBC = 드라이버 관리자에서 사용 하 여 ODBC 커서 라이브러리입니다.<br /><br /> SQL_CUR_USE_DRIVER = 드라이버 관리자에서 사용 하 여 드라이버의 스크롤 기능입니다. 이 값은 기본 설정입니다.<br /><br /> ODBC 커서 라이브러리에 대 한 자세한 내용은 참조 [부록 f: ODBC 커서 라이브러리](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)합니다. **경고:** 커서 라이브러리는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.|  
|SQL_ATTR_PACKET_SIZE (ODBC 2.0)|네트워크 패킷 크기 (바이트)를 지정 하는 SQLUINTEGER 값입니다. **참고:** 만 반환 하지만 설정할 수 없습니다는 네트워크 패킷 크기 또는 많은 데이터 원본은이 옵션을 하거나 지원 하지 않습니다. <br /><br /> 지정된 된 크기는 최대 패킷 크기를 초과 하거나 최소 패킷 크기 보다 작으면를 드라이버 해당 값을 대체 하 고 SQLSTATE 01 s 02를 반환 합니다 (옵션 값이 변경 됨).<br /><br /> 연결을 이미 수행 된 후 패킷 크기를 설정 하는 응용 프로그램, 드라이버는 SQLSTATE HY011를 반환 합니다 (특성 지금 설정할 수 없습니다).|  
|SQL_ATTR_QUIET_MODE (ODBC 2.0)|창 핸들 (HWND)입니다.<br /><br /> Null 포인터 창 핸들을 사용 하는 경우 드라이버는 모든 대화 상자를 표시 하지 않습니다.<br /><br /> 창 핸들 null 포인터 이면 응용 프로그램의 부모 창 핸들 이어야 합니다. 기본값입니다. 드라이버 대화 상자를 표시할이 핸들을 사용 합니다. **참고:** SQL_ATTR_QUIET_MODE 연결 특성으로 표시 되는 대화 상자에 적용 되지 않습니다 **SQLDriverConnect**합니다.|  
|SQL_ATTR_TRACE (ODBC 1.0)|드라이버 관리자 추적을 수행할 것인지 나타내는 제공 하는 SQLUINTEGER 값:<br /><br /> SQL_OPT_TRACE_OFF 추적 off (기본값) =<br /><br /> SQL_OPT_TRACE_ON =에 대 한 추적<br /><br /> 추적이 설정 되어 때 드라이버 관리자 추적 파일에는 각 ODBC 함수 호출을 씁니다. **참고:** 추적이 설정 되어 드라이버 관리자 SQLSTATE IM013를 반환할 수 있습니다 (파일 오류 추적)는 함수에서. <br /><br /> 응용 프로그램 SQL_ATTR_TRACEFILE 옵션으로 추적 파일을 지정합니다. 파일이 이미 있는 경우 드라이버 관리자는 파일에 추가 합니다. 그렇지 않으면 파일을 만듭니다. 추적에 있고 지정 된 추적 파일이 없는 경우에 드라이버 관리자는 SQL 파일에 씁니다. 루트 디렉터리에 로그인 합니다.<br /><br /> 응용 프로그램 변수를 설정할 수 **ODBCSharedTraceFlag** 추적을 동적으로 사용할 수 있도록 합니다. 현재 실행 중인 모든 ODBC 응용 프로그램에 대 한 추적을 사용할 수 합니다. 응용 프로그램 추적을 해제, 해당 응용 프로그램에 대해서만 기능이 비활성화 됩니다.<br /><br /> 경우는 **추적** 시스템 정보에 대 한 키워드는 응용 프로그램이 호출 하는 경우 1로 설정 되어 **SQLAllocHandle** 와 *HandleType* SQL_HANDLE_ENV의 모든 추적을 사용 처리합니다. 호출한 응용 프로그램에 대해서만 사용 하도록 설정 **SQLAllocHandle**합니다.<br /><br /> 호출 **SQLSetConnectAttr** 와 *특성* SQL_ATTR_TRACE의 필요가 없는 *ConnectionHandle* 인수에 유효한 일 경우 SQL_ERROR가 반환 되지 것입니다 *ConnectionHandle* 은 NULL입니다. 모든 연결에이 특성이 적용 됩니다.|  
|SQL_ATTR_TRACEFILE (ODBC 1.0)|추적 파일의 이름을 포함 하는 null로 끝나는 문자 문자열입니다.<br /><br /> 지정 된 SQL_ATTR_TRACEFILE 특성의 기본 값의 **TraceFile** 시스템 정보에는 키워드입니다. 자세한 내용은 참조 [ODBC 하위 키](../../../odbc/reference/install/odbc-subkey.md)합니다.<br /><br /> 호출 **SQLSetConnectAttr** 와 *특성* SQL_ATTR_ TRACEFILE의 필요 하지 않습니다는 *ConnectionHandle* 유효 하려면 인수 경우 SQL_ERROR가 반환 되지 것입니다 *ConnectionHandle* 올바르지 않습니다. 모든 연결에이 특성이 적용 됩니다.|  
|SQL_ATTR_TRANSLATE_LIB (ODBC 1.0)|Null로 끝나는 문자열 함수를 포함 하는 라이브러리의 이름이 들어 있는 **SQLDriverToDataSource** 및 **SQLDataSourceToDriver** 와 같은 작업을 수행 하는 드라이버에서 액세스 하 문자 집합 변환 합니다. 이 옵션 수 드라이버 데이터 원본에 연결 된 경우에 지정 합니다. 이 특성의 설정은 연결 간에 유지 됩니다. 에 데이터를 변환 하는 방법에 대 한 자세한 내용은 참조 [번역 Dll](../../../odbc/reference/develop-app/translation-dlls.md) 및 [번역 DLL 함수 참조](../../../odbc/reference/syntax/translation-dll-api-reference.md)합니다.|  
|SQL_ATTR_TRANSLATE_OPTION (ODBC 1.0)|변환 DLL에 전달 되는 32 비트 플래그 값입니다. 이 특성은 수 드라이버 데이터 원본에 연결 된 경우에 지정 합니다. 에 데이터를 변환 하는 방법에 대 한 정보를 참조 하십시오. [번역 Dll](../../../odbc/reference/develop-app/translation-dlls.md)합니다.|  
|SQL_ATTR_TXN_ISOLATION (ODBC 1.0)|현재 연결에 대 한 트랜잭션 격리 수준을 설정 하는 32 비트 비트 마스크입니다. 호출 하는 응용 프로그램 **SQLEndTran** 커밋하거나 호출 하기 전에 연결에서 열려 있는 모든 트랜잭션을 롤백하려고 **SQLSetConnectAttr** 이 옵션을 사용 합니다.<br /><br /> 에 대 한 유효한 값 *ValuePtr* 호출 하 여 확인할 수 **SQLGetInfo** 와 *정보 항목* SQL_TXN_ISOLATION_OPTIONS 같음.<br /><br /> 트랜잭션 격리 수준에 대 한 참조에서 SQL_DEFAULT_TXN_ISOLATION 정보 유형의 설명을 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 및 [트랜잭션 격리 수준](../../../odbc/reference/develop-app/transaction-isolation-levels.md)합니다.|  
  
 [설명자가 구현 설명자, 응용 프로그램 설명자 하지 하는 경우에 1]이이 함수를 비동기적으로 호출할 수 있습니다.  
  
## <a name="code-example"></a>코드 예  
 참조 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|연결 특성의 설정은 반환|[SQLGetConnectAttr 함수](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
