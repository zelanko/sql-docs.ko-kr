---
title: SQLSetConnectAttr 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8424462ddde4f99196e26d633fddfa5bb2ed6ee9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301939"
---
# <a name="sqlsetconnectattr-function"></a>SQLSetConnectAttr 함수
**규칙**  
 소개 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLSetConnectAttr** 는 연결의 여러 측면을 제어 하는 특성을 설정 합니다.  
  
> [!NOTE]
>  ODBC*2.x 응용 프로그램이* odbc*2.x 드라이버를 사용할 때 드라이버 관리자* 가이 기능을에 매핑하는 방법에 대 한 자세한 내용은 [응용 프로그램의 이전 버전과의 호환성을 위한 대체 함수 매핑](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)을 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLSetConnectAttr(  
     SQLHDBC       ConnectionHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>인수  
 *ConnectionHandle*  
 [Input] 연결 핸들입니다.  
  
 *특성도*  
 입력 설정할 특성입니다. "Comments"에 나열 되어 있습니다.  
  
 *ValuePtr*  
 입력 *특성과*연결 될 값에 대 한 포인터입니다. *특성*의 값에 *따라, 이상 값은 부호* 없는 정수 값이 되거나 null로 끝나는 문자열을 가리킵니다. *특성* 인수의 정수 계열 형식은 고정 길이가 아닐 수 있습니다. 자세한 내용은 설명 섹션을 참조 하세요.  
  
 *StringLength*  
 입력 *Attribute* 가 ODBC에 정의 된 *특성이 고 이상* 문자열이 문자열 또는 이진 버퍼를 가리키는 경우이 인수*는 *의 길이 여야 합니다.* 문자열 데이터의 경우이 인수는 문자열의 바이트 수를 포함 해야 합니다.  
  
 *Attribute* 가 ODBC에 정의 된 특성이 고 *valueptr* 이 정수 이면 *stringlength* 는 무시 됩니다.  
  
 *특성이* 드라이버 정의 특성인 경우 응용 프로그램은 *stringlength* 인수를 설정 하 여 특성의 특성을 드라이버 관리자에 게 표시 합니다. *Stringlength* 에는 다음 값을 사용할 수 있습니다.  
  
-   *Valueptr* 이 문자열에 대 한 포인터인 경우 *stringlength* 는 문자열 또는 SQL_NTS의 길이입니다.  
  
-   *Valueptr* 이 이진 버퍼에 대 한 포인터인 경우 응용 프로그램은 SQL_LEN_BINARY_ATTR (*length*) 매크로의 결과를 *stringlength*로 배치 합니다. 그러면 음수 값이 *Stringlength*에 배치 됩니다.  
  
-   *Valueptr* 이 문자열 또는 이진 문자열이 아닌 값에 대 한 포인터인 경우 *stringlength* 의 값은 SQL_IS_POINTER 이어야 합니다.  
  
-   *Valueptr* 이 고정 길이 값을 포함 하는 경우에는 *stringlength* 가 SQL_IS_INTEGER 또는 SQL_IS_UINTEGER입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE 또는 SQL_STILL_EXECUTING입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLSetConnectAttr** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_DBC의 *HandleType* 및 *ConnectionHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLSetConnectAttr** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
 드라이버는 SQL_SUCCESS_WITH_INFO을 반환 하 여 옵션 설정 결과에 대 한 정보를 제공할 수 있습니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01 S 02|옵션 값 변경 됨|드라이버가 *Valueptr* 에 지정 된 값을 지원 하지 않고 유사한 값으로 대체 되었습니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08002|사용 중인 연결 이름|*특성* 인수가 SQL_ATTR_ODBC_CURSORS 되었으며 드라이버가 데이터 원본에 이미 연결 되어 있습니다.|  
|08003|연결이 열려 있지 않음|(DM) 열린 연결이 필요한 *특성* 값이 지정 되었지만 *ConnectionHandle* 가 연결 된 상태가 아닙니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|24000|잘못된 커서 상태|*특성* 인수가 SQL_ATTR_CURRENT_CATALOG 되었으며 결과 집합이 보류 중입니다.|  
|25000|로컬 트랜잭션에서 잘못 된 작업|연결 특성 SQL_ATTR_ENLIST_IN_DTC 설정 하 여 DTC (분산 트랜잭션 연결)에 참여 하려고 하는 동안 로컬 트랜잭션에 연결이 있었습니다.<br /><br /> 연결이 DTC에 이미 참여 하 고 있습니다.<br /><br /> 연결이 분산 트랜잭션 연결에 참여 하 고 SQL_ATTR_AUTOCOMMIT를 SQL_AUTOCOMMIT_OFF으로 설정 하 여 로컬 트랜잭션을 시작 했습니다.|  
|가는 000|카탈로그 이름이 잘못 되었습니다.|*특성* 인수가 SQL_CURRENT_CATALOG 되었으며 지정 된 카탈로그 이름이 잘못 되었습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*ConnectionHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. **SQLSetConnectAttr** 함수를 호출 하 고 실행을 완료 하기 전에 *ConnectionHandle*에서 [Sqlcancelhandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md) 를 호출한 다음 *ConnectionHandle*에서 **SQLSetConnectAttr** 함수를 다시 호출 했습니다.<br /><br /> 또는 **SQLSetConnectAttr** 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *ConnectionHandle* 에 대해 호출 되었습니다.|  
|HY009|Null 포인터 사용이 잘못 되었습니다.|*특성* 인수는 문자열 값이 필요한 연결 특성을 식별 하 고, 값 *eptr* 인수는 null 포인터입니다.|  
|HY010|함수 시퀀스 오류|(DM) *ConnectionHandle* 와 연결 된 *StatementHandle* 에 대해 비동기적으로 실행 되는 함수가 호출 되었으며 **SQLSetConnectAttr** 가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) *ConnectionHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **Sqlexecdirect**또는 **SQLMoreResults** 가 *ConnectionHandle* 와 연결 된 문 핸들 중 하나에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 는 *ConnectionHandle* 와 연결 된 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 됩니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.<br /><br /> (DM) **SQLBrowseConnect** 가 *ConnectionHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 **SQLBrowseConnect** 가 SQL_SUCCESS_WITH_INFO 또는 SQL_SUCCESS을 반환 하기 전에 호출 되었습니다.|  
|HY011|특성을 지금 설정할 수 없습니다.|*특성* 인수가 SQL_ATTR_TXN_ISOLATION 되었으며 트랜잭션이 열려 있습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY024|잘못 된 특성 값|지정 된 *특성* 값이 지정 된 경우에는 잘못 된 값이 *valueptr*에 지정 되었습니다. (드라이버 관리자는 SQL_ATTR_ACCESS_MODE 또는 SQL_ATTR_ASYNC_ENABLE와 같이 불연속 값 집합을 허용 하는 문 특성 및 연결에 대해서만이 SQLSTATE를 반환 합니다. 다른 모든 연결 및 문 특성의 경우 드라이버에서 지정 된 값을 확인 해야 *합니다.*<br /><br /> *특성* 인수가 SQL_ATTR_TRACEFILE 또는 SQL_ATTR_TRANSLATE_LIB 되었으며, *valueptr* 이 빈 문자열 이었습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|*(DM) \** 가 문자열이 고 *stringlength* 인수가 0 보다 작지만 SQL_NTS 되지 않았습니다.|  
|HY092|특성/옵션 식별자가 잘못 되었습니다.|(DM) 인수 *특성* 에 지정 된 값이 드라이버에서 지 원하는 ODBC 버전에 적합 하지 않습니다.<br /><br /> (DM) 인수 *특성* 에 지정 된 값이 읽기 전용 특성입니다.|  
|HY114|드라이버가 연결 수준의 비동기 함수 실행을 지원 하지 않습니다.|(DM) 비동기 연결 작업을 지원 하지 않는 드라이버에 대 한 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE를 사용 하 여 비동기 함수 실행을 사용 하도록 응용 프로그램을 시도 했습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HY121|커서 라이브러리와 드라이버 인식 풀링이 동시에 사용 하도록 설정할 수 없습니다.|자세한 내용은 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)을 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|인수 *특성* 에 지정 된 값이 드라이버에서 지원 되는 odbc 버전에 대 한 올바른 odbc 연결 또는 statement 특성 이지만 드라이버에서 지원 하지 않습니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *ConnectionHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM009|변환 DLL을 로드할 수 없습니다.|드라이버가 연결에 대해 지정 된 변환 DLL을 로드할 수 없습니다. 이 오류는 *특성이* SQL_ATTR_TRANSLATE_LIB 경우에만 반환 될 수 있습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
|S1118|드라이버가 비동기 알림을 지원 하지 않습니다.|연결 된 후에 SQL_ATTR_ASYNC_DBC_EVENT가 설정 되었지만 드라이버에서 비동기 알림을 지원 하지 않습니다.|  
  
 *Attribute* 가 statement 특성인 경우 **SQLSetConnectAttr** 는 **SQLSetStmtAttr**에서 반환 된 sqlstates를 반환할 수 있습니다.  
  
## <a name="comments"></a>주석  
 연결 특성에 대 한 일반적인 내용은 [연결 특성](../../../odbc/reference/develop-app/connection-attributes.md)을 참조 하세요.  
  
 현재 정의 된 특성과이 특성이 도입 된 ODBC 버전은이 섹션의 뒷부분에 나와 있습니다. 다른 데이터 원본을 활용 하기 위해 더 많은 특성을 정의 해야 합니다. 특성 범위는 ODBC에서 예약 됩니다. 드라이버 개발자는 Open Group에서 고유한 드라이버별 사용에 대 한 값을 예약 해야 합니다.  
  
> [!NOTE]
>  **SQLSetConnectAttr** 를 호출 하 여 연결 수준에서 문 특성을 설정 하는 기능은 ODBC 3.x에서 더 이상 사용 되지*않습니다.* ODBC 3.x*응용 프로그램은 연결* 수준에서 문 특성을 설정 하면 안 됩니다. ODBC 3.x 문 특성은 연결 수준에서 설정할 수 없습니다 *.* 이 특성은 연결 특성과 문 특성 모두 이며 연결 수준 또는 문 수준에서 설정 될 수 있는 SQL_ATTR_METADATA_ID 및 SQL_ATTR_ASYNC_ENABLE 특성을 제외 하 고는 예외입니다.  
> 
>  Odbc 3.x*드라이버는* 연결 수준에서 odbc*2.x 문 옵션* 을 설정 하는 odbc 2.x*응용 프로그램* 을 사용 해야 하는 경우에만이 기능을 지원 해야 합니다. 자세한 내용은 부록 G: 이전 버전과의 호환성을 위한 드라이버 지침의 [SQLSetConnectOption 매핑](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) 을 참조 하세요.  
  
 응용 프로그램은 연결이 할당 되 고 해제 된 시간 사이에 언제 든 지 **SQLSetConnectAttr** 를 호출할 수 있습니다. 연결에 대해 **Sqlfreehandle** 이 호출 될 때까지 응용 프로그램에서 연결에 대해 성공적으로 설정한 모든 연결 및 문 특성을 유지 합니다. 예를 들어 응용 프로그램이 데이터 원본에 연결 하기 전에 **SQLSetConnectAttr** 를 호출 하는 경우 응용 프로그램이 데이터 원본에 연결할 때 드라이버가 드라이버 **에서 실패 하** 는 경우에도 특성이 유지 됩니다. 응용 프로그램에서 드라이버별 특성을 설정 하는 경우 응용 프로그램이 연결의 다른 드라이버에 연결 되는 경우에도 특성이 유지 됩니다.  
  
 일부 연결 특성은 연결 된 후에만 설정할 수 있습니다. 다른 항목은 연결 된 후에만 설정할 수 있습니다. 다음 표에서는 연결이 설정 되기 전이나 후에 설정 해야 하는 연결 특성을 나타냅니다. 는 연결 전후에 특성을 설정할 수 *있음을 나타냅니다.*  
  
|특성|연결 전후에 설정 하나요?|  
|---------------|-------------------------------------|  
|SQL_ATTR_ACCESS_MODE|[1]|  
|SQL_ATTR_ASYNC_DBC_EVENT|여기서는|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE|[4]|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK|여기서는|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT|여기서는|  
|SQL_ATTR_ASYNC_ENABLE|[2]|  
|SQL_ATTR_AUTO_IPD|여기서는|  
|SQL_ATTR_AUTOCOMMIT|[5]|  
|SQL_ATTR_CONNECTION_DEAD|After|  
|SQL_ATTR_CONNECTION_TIMEOUT|여기서는|  
|SQL_ATTR_CURRENT_CATALOG|[1]|  
|SQL_ATTR_DBC_INFO_TOKEN|After|  
|SQL_ATTR_ENLIST_IN_DTC|After|  
|SQL_ATTR_LOGIN_TIMEOUT|이전|  
|SQL_ATTR_METADATA_ID|여기서는|  
|SQL_ATTR_ODBC_CURSORS|이전|  
|SQL_ATTR_PACKET_SIZE|이전|  
|SQL_ATTR_QUIET_MODE|여기서는|  
|SQL_ATTR_TRACE|여기서는|  
|SQL_ATTR_TRACEFILE|여기서는|  
|SQL_ATTR_TRANSLATE_LIB|After|  
|SQL_ATTR_TRANSLATE_OPTION|After|  
|SQL_ATTR_TXN_ISOLATION|[3]|  
  
 [1] SQL_ATTR_ACCESS_MODE 및 SQL_ATTR_CURRENT_CATALOG는 드라이버에 따라 연결 전이나 후에 설정할 수 있습니다. 그러나 일부 드라이버에서는 연결 후에 이러한 변경이 지원 되지 않으므로 상호 운용 가능한 응용 프로그램은 연결 전에 설정 합니다.  
  
 [2] SQL_ATTR_ASYNC_ENABLE은 활성 문이 되기 전에 설정 해야 합니다.  
  
 [3] SQL_ATTR_TXN_ISOLATION 연결에 열려 있는 트랜잭션이 없는 경우에만 설정할 수 있습니다. 일부 연결 특성은 데이터 원본이 지정 \*된 값을 지원 하지 않는 경우 유사한 값의 대체를 지원 합니다. *ValuePtr* 이 경우 드라이버는 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01 S 02 (옵션 값이 변경 됨)를 반환 합니다. 예를 들어, *특성이* SQL_ATTR_PACKET_SIZE이 고 \*, *valueptr* 이 최대 패킷 크기를 초과 하는 경우 드라이버는 최대 크기를 대체 합니다. 대체 값을 결정 하기 위해 응용 프로그램은 **SQLGetConnectAttr**를 호출 합니다.  
  
 [4] 연결을 열기 전에 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 설정 하면 드라이버 관리자는 **SQLBrowseConnect**, **SQLConnect**또는 **SQLDriverConnect**를 호출 하는 동안 드라이버가 로드 될 때 드라이버의 특성을 설정 합니다. **SQLBrowseConnect**, **SQLConnect**또는 **SQLDriverConnect**를 호출 하기 전에 드라이버 관리자는 연결할 드라이버를 알 수 없으며 드라이버가 비동기 연결 작업을 지원 하는지 여부를 알 수 없습니다. 따라서 드라이버 관리자는 항상 SQL_SUCCESS을 반환 합니다. 그러나 드라이버가 비동기 연결 작업을 지원 하지 않는 경우 **SQLBrowseConnect**, **SQLConnect**또는 **SQLDriverConnect** 에 대 한 호출이 실패 합니다.  
  
 [5] SQL_ATTR_AUTOCOMMIT FALSE로 설정 된 경우 API가 트랜잭션 일관성을 보장 하기 위해 SQL_ERROR 반환 하는 경우 응용 프로그램에서 SQLEndTran (SQL_ROLLBACK)을 호출 해야 합니다.  
  
 \* *Valueptr* 버퍼에 설정 된 정보 형식은 지정 된 *특성*에 따라 다릅니다. **SQLSetConnectAttr** 는 null로 끝나는 문자열 또는 정수 값의 두 가지 형식 중 하나로 특성 정보를 허용 합니다. 각의 형식은 특성의 설명에 설명 되어 있습니다. **SQLSetConnectAttr** 의 *valueptr* 인수에서 가리키는 문자열의 길이는 *stringlength* 바이트입니다.  
  
 ODBC*2.x 또는 이전* 버전에서 도입 된 모든 특성의 경우와 마찬가지로 길이가 특성에 의해 정의 되는 경우에는 *stringlength* 인수가 무시 됩니다.  
  
|*특성도*|*ValuePtr* 이상 내용|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE (ODBC 1.0)|SQLUINTEGER 값입니다. SQL_MODE_READ_ONLY은 드라이버가 업데이트를 발생 시키는 SQL 문을 지원 하지 않아도 되는 표시기로 드라이버 또는 데이터 원본에 사용 됩니다. 이 모드는 드라이버 또는 데이터 원본에 적절 한 잠금 전략, 트랜잭션 관리 또는 기타 영역을 최적화 하는 데 사용할 수 있습니다. 드라이버는 이러한 문이 데이터 원본에 전송 되지 않도록 방지 하는 데 필요 하지 않습니다. 읽기 전용 연결 중에 읽기 전용이 아닌 SQL 문을 처리 하도록 요청 된 경우 드라이버 및 데이터 원본의 동작은 구현에 정의 되어 있습니다. 기본값은 SQL_MODE_READ_WRITE입니다.|  
|SQL_ATTR_ASYNC_DBC_EVENT (ODBC 3.8)|이벤트 핸들 인 SQLPOINTER 값입니다.<br /><br /> 비동기 함수의 완료 알림은 SQL_ATTR_ASYNC_STMT_EVENT 특성을 사용 하 여 **SQLSetConnectAttr** 를 호출 하 고 이벤트 핸들을 지정 하 여 사용 하도록 설정 됩니다. **참고:**  알림 방법은 커서 라이브러리에서 지원 되지 않습니다. 알림 방법이 사용 하도록 설정 된 경우 응용 프로그램에서 SQLSetConnectAttr을 통해 커서 라이브러리를 사용 하도록 설정 하려고 하면 오류 메시지가 표시 됩니다.|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE (ODBC 3.8)|연결 핸들에서 선택한 함수의 비동기 실행을 사용 하거나 사용 하지 않도록 설정 하는 SQLUINTEGER 값입니다. 자세한 내용은 [비동기 실행 (폴링 방법)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)을 참조 하세요.<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = 지정 된 연결 관련 함수에 대해 비동기 작업을 사용 하도록 설정 합니다.<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = (기본값) 지정 된 연결 관련 함수에 대해 비동기 작업을 사용 하지 않도록 설정 합니다.<br /><br /> SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 설정은 항상 동기식입니다. 즉, SQL_STILL_EXECUTING를 반환 하지 않습니다.<br /><br /> SQL_ATTR_ASYNC_ENABLE를 사용 하 여 문 작업의 비동기 실행을 사용 하도록 설정 합니다.|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK (ODBC 3.8)|컨텍스트 구조를 가리키는 SQLPOINTER 값입니다.<br /><br /> 드라이버 관리자만이 특성을 사용 하 여 드라이버의 **SQLSetStmtAttr** 함수를 호출할 수 있습니다.|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT (ODBC 3.8)|컨텍스트 구조를 가리키는 SQLPOINTER 값입니다.<br /><br /> 드라이버 관리자만이 특성을 사용 하 여 드라이버의 **SQLSetStmtAttr** 함수를 호출할 수 있습니다.|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 3.0)|지정 된 연결에서 문을 사용 하 여 호출 된 함수가 비동기적으로 실행 되는지 여부를 지정 하는 SQLULEN 값입니다.<br /><br /> SQL_ASYNC_ENABLE_OFF = 문 작업에 대 한 연결 수준 비동기 실행 지원을 사용 하지 않도록 설정 합니다 (기본값).<br /><br /> SQL_ASYNC_ENABLE_ON = 문 작업에 대해 연결 수준 비동기 실행 지원을 사용 하도록 설정 합니다.<br /><br /> 이 특성은 SQL_ASYNC_MODE 된 정보 형식의 **SQLGetInfo** 가 SQL_AM_CONNECTION 또는 SQL_AM_STATEMENT를 반환할지 여부를 설정할 수 있습니다.|  
|SQL_ATTR_AUTO_IPD (ODBC 3.0)|**Sqlprepare** 호출 후 IPD 자동 채우기가 지원 되는지 여부를 지정 하는 읽기 전용 SQLUINTEGER 값입니다.<br /><br /> SQL_TRUE = **Sqlprepare** 호출 후 드라이버에서 IPD 자동 채우기를 지원 합니다.<br /><br /> SQL_FALSE = **Sqlprepare** 호출 후 드라이버에서 IPD 자동 채우기를 지원 하지 않습니다. 준비 된 문을 지원 하지 않는 서버는 자동으로 IPD를 채울 수 없습니다.<br /><br /> SQL_ATTR_AUTO_IPD 연결 특성에 대해 SQL_TRUE 반환 되는 경우 IPD의 자동 채우기를 설정 하거나 해제 하도록 statement 특성 SQL_ATTR_ENABLE_AUTO_IPD를 설정할 수 있습니다. SQL_ATTR_AUTO_IPD SQL_FALSE 경우 SQL_ATTR_ENABLE_AUTO_IPD를 SQL_TRUE로 설정할 수 없습니다. SQL_ATTR_ENABLE_AUTO_IPD의 기본값은 SQL_ATTR_AUTO_IPD의 값과 같습니다.<br /><br /> 이 연결 특성은 **SQLGetConnectAttr** 에서 반환 될 수 있지만 **SQLSetConnectAttr**로 설정할 수 없습니다.|  
|SQL_ATTR_AUTOCOMMIT (ODBC 1.0)|자동 커밋 모드를 사용할지 수동 커밋 모드를 사용할지를 지정 하는 SQLUINTEGER 값입니다.<br /><br /> SQL_AUTOCOMMIT_OFF = 드라이버가 수동 커밋 모드를 사용 하 고 응용 프로그램에서 **Sqlendtran**을 사용 하 여 트랜잭션을 명시적으로 커밋하거나 롤백해야 합니다.<br /><br /> SQL_AUTOCOMMIT_ON = 드라이버가 자동 커밋 모드를 사용 합니다. 각 문은 실행 된 직후에 커밋됩니다. 기본값입니다. 수동 커밋 모드에서 자동 커밋 모드로 변경 하기 위해 SQL_ATTR_AUTOCOMMIT를 SQL_AUTOCOMMIT_ON로 설정 하면 연결에서 열려 있는 트랜잭션이 커밋됩니다.<br /><br /> 자세한 내용은 [커밋 모드](../../../odbc/reference/develop-app/commit-mode.md)를 참조 하세요. **중요:**  일부 데이터 원본은 문이 커밋될 때마다 액세스 계획을 삭제 하 고 연결의 모든 문에 대해 커서를 닫습니다. 자동 커밋 모드에서는 쿼리가 아닌 각 문이 실행 되거나 쿼리에 대해 커서가 닫힐 때 이러한 현상이 발생할 수 있습니다. 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 의 SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 형식 및 [커서와 준비 된 문의 트랜잭션 효과](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)를 참조 하세요. <br /><br /> 일괄 처리가 자동 커밋 모드에서 실행 되는 경우 두 가지 작업을 수행할 수 있습니다. 전체 일괄 처리는 autocommitable 단위로 처리할 수 있으며 일괄 처리의 각 문은 autocommitable 단위로 처리 됩니다. 특정 데이터 원본은 이러한 동작을 모두 지원할 수 있으며 하나를 선택 하는 방법을 제공할 수 있습니다. 일괄 처리가 autocommitable 단위로 처리 되는지 또는 일괄 처리 내의 각 개별 문이 autocommitable 인지 여부를 드라이버에서 정의 합니다.|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> (ODBC 3.5)|연결 상태를 나타내는 읽기 전용 SQLUINTEGER 값입니다. SQL_CD_TRUE 경우 연결이 손실 된 것입니다. SQL_CD_FALSE 경우 연결이 여전히 활성 상태입니다.|  
|SQL_ATTR_CONNECTION_TIMEOUT (ODBC 3.0)|응용 프로그램으로 반환 하기 전에 연결에 대 한 모든 요청이 완료 될 때까지 대기 하는 시간 (초)에 해당 하는 SQLUINTEGER 값입니다. 이 드라이버는 쿼리 실행 또는 로그인과 연결 되지 않은 상황에서 시간 초과가 발생할 수 있는 경우에는 항상 SQLSTATE HYT00 (Timeout 만료 됨)을 반환 해야 합니다.<br /><br /> 값 *Eptr* 이 0 (기본값) 이면 시간 제한이 없습니다.|  
|SQL_ATTR_CURRENT_CATALOG (ODBC 2.0)|데이터 원본에서 사용할 카탈로그의 이름을 포함 하는 문자열입니다. 예를 들어 SQL Server에서 카탈로그는 데이터베이스 이므로 드라이버는 **USE** _database_ 문을 데이터 \* *원본에 보냅니다. 여기서* *database* 는 지정 된 데이터베이스입니다. 단일 계층 드라이버의 경우 카탈로그는 디렉터리가 될 수 있으므로 드라이버는 현재 디렉터리를 **Valueptr*에 지정 된 디렉터리로 변경 합니다.|  
|SQL_ATTR_DBC_INFO_TOKEN (ODBC 3.8|[SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)의 (\**pra)* 매개 변수가 100과 같지 않을 때 연결 정보 토큰을 DBC 핸들로 다시 설정 하는 데 사용 되는 sqlpointer 값입니다.<br /><br /> SQL_ATTR_DBC_INFO_TOKEN은 설정 전용입니다. **SQLGetConnectAttr** 또는 **SQLGetConnectOption** 를 사용 하 여이 값을 검색할 수 없습니다. 응용 프로그램에서이 특성을 설정 하지 않으므로 드라이버 관리자의 **SQLSetConnectAttr** SQL_ATTR_DBC_INFO_TOKEN 허용 되지 않습니다.<br /><br /> SQL_ATTR_DBC_INFO_TOKEN 설정한 후 드라이버가 SQL_ERROR을 반환 하는 경우 풀에서 가져온 연결은 해제 됩니다. 그러면 드라이버 관리자가 풀에서 다른 연결을 가져오려고 시도 합니다. 자세한 내용은 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md) 을 참조 하세요.|  
|SQL_ATTR_ENLIST_IN_DTC (ODBC 3.0)|Microsoft 구성 요소 서비스에서 조정 하는 분산 트랜잭션에서 ODBC 드라이버를 사용할지 여부를 지정 하는 SQLPOINTER 값입니다.<br /><br /> SQL Server로 내보낼 트랜잭션을 지정 하는 DTC OLE 트랜잭션 개체를 전달 하거나 SQL_DTC_DONE 하 여 연결의 DTC 연결을 종료 합니다.<br /><br /> 클라이언트는 ms dtc (Microsoft DTC(Distributed Transaction Coordinator)) OLE ITransactionDispenser:: BeginTransaction 메서드를 호출 하 여 MS DTC 트랜잭션을 시작 하 고 해당 트랜잭션을 나타내는 MS DTC 트랜잭션 개체를 만듭니다. 그런 다음 응용 프로그램은 SQL_ATTR_ENLIST_IN_DTC 옵션을 사용 하 여 SQLSetConnectAttr을 호출 하 여 트랜잭션 개체를 ODBC 연결과 연결 합니다. 관련된 모든 데이터베이스 작업은 MS DTC 트랜잭션의 보호 아래 수행됩니다. 응용 프로그램에서는 SQL_DTC_DONE과 함께 SQLSetConnectAttr을 호출하여 DTC와의 연결을 종료합니다. 자세한 내용은 MS DTC 설명서를 참조하십시오.|  
|SQL_ATTR_LOGIN_TIMEOUT (ODBC 1.0)|응용 프로그램으로 반환 하기 전에 로그인 요청이 완료 될 때까지 대기 하는 시간 (초)에 해당 하는 SQLUINTEGER 값입니다. 기본값은 드라이버에 따라 달라 집니다. *Valueptr* 이 0 이면 시간 제한이 비활성화 되 고 연결 시도는 무기한 대기 합니다.<br /><br /> 지정 된 제한 시간이 데이터 원본의 최대 로그인 제한 시간을 초과 하는 경우 드라이버는 해당 값을 대체 하 고 SQLSTATE 01 S 02 (옵션 값이 변경 됨)를 반환 합니다.|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|카탈로그 함수의 문자열 인수를 처리 하는 방법을 결정 하는 SQLUINTEGER 값입니다.<br /><br /> SQL_TRUE 경우 카탈로그 함수의 문자열 인수는 식별자로 처리 됩니다. 이 경우에는 중요 하지 않습니다. 구분 되지 않은 문자열의 경우 드라이버는 후행 공백을 제거 하 고 문자열을 대문자로 접 합니다. 구분 기호로 분리 된 문자열의 경우 드라이버는 선행 또는 후행 공백을 제거 하 고 구분 기호 사이에 아무 것도 그대로 사용 합니다. 이러한 인수 중 하나가 null 포인터로 설정 된 경우 함수는 SQL_ERROR 및 SQLSTATE HY009 (null 포인터 사용이 잘못 되었습니다)를 반환 합니다.<br /><br /> SQL_FALSE 경우 카탈로그 함수의 문자열 인수는 식별자로 처리 되지 않습니다. 이 경우는 중요 합니다. 인수에 따라 문자열 검색 패턴을 포함할 수도 있고 그렇지 않을 수도 있습니다.<br /><br /> 기본값은 SQL_FALSE입니다.<br /><br /> 값 목록을 사용 하는 **Sqltables**의 *TableType* 인수는이 특성의 영향을 받지 않습니다.<br /><br /> SQL_ATTR_METADATA_ID는 문 수준에서 설정할 수도 있습니다. (문 특성 이기도 한 유일한 연결 특성입니다.)<br /><br /> 자세한 내용은 [Catalog 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)를 참조 하세요.|  
|SQL_ATTR_ODBC_CURSORS (ODBC 2.0)|드라이버 관리자에서 ODBC 커서 라이브러리를 사용 하는 방법을 지정 하는 SQLULEN 값입니다.<br /><br /> SQL_CUR_USE_IF_NEEDED = 드라이버 관리자는 필요한 경우에만 ODBC 커서 라이브러리를 사용 합니다. 드라이버가 **Sqlfetchscroll**에서 SQL_FETCH_PRIOR 옵션을 지 원하는 경우 드라이버 관리자는 드라이버의 스크롤 기능을 사용 합니다. 그렇지 않으면 ODBC 커서 라이브러리를 사용 합니다.<br /><br /> SQL_CUR_USE_ODBC = 드라이버 관리자는 ODBC 커서 라이브러리를 사용 합니다.<br /><br /> SQL_CUR_USE_DRIVER = 드라이버 관리자는 드라이버의 스크롤 기능을 사용 합니다. 이 값은 기본 설정입니다.<br /><br /> ODBC 커서 라이브러리에 대 한 자세한 내용은 [부록 F: Odbc 커서 라이브러리](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)를 참조 하십시오. **경고:**  커서 라이브러리는 이후 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.|  
|SQL_ATTR_PACKET_SIZE (ODBC 2.0)|네트워크 패킷 크기 (바이트)를 지정 하는 SQLUINTEGER 값입니다. **참고:**  많은 데이터 원본에서이 옵션을 지원 하지 않거나 반환만 가능 하지만 네트워크 패킷 크기는 설정 하지 않습니다. <br /><br /> 지정 된 크기가 최대 패킷 크기를 초과 하거나 최소 패킷 크기 보다 작은 경우 드라이버는 해당 값을 대체 하 고 SQLSTATE 01 S 02 (옵션 값이 변경 됨)를 반환 합니다.<br /><br /> 연결이 이미 설정 된 후에 응용 프로그램에서 패킷 크기를 설정 하는 경우 드라이버는 SQLSTATE HY011 (특성을 지금 설정할 수 없음)를 반환 합니다.|  
|SQL_ATTR_QUIET_MODE (ODBC 2.0)|창 핸들 (HWND)입니다.<br /><br /> 창 핸들이 null 포인터인 경우 드라이버는 대화 상자를 표시 하지 않습니다.<br /><br /> 창 핸들이 null 포인터가 아닌 경우 응용 프로그램의 부모 창 핸들 이어야 합니다. 기본값입니다. 드라이버는이 핸들을 사용 하 여 대화 상자를 표시 합니다. **참고:**  SQL_ATTR_QUIET_MODE 연결 특성은 **SQLDriverConnect**에서 표시 하는 대화 상자에는 적용 되지 않습니다.|  
|SQL_ATTR_TRACE (ODBC 1.0)|추적을 수행할지 여부를 드라이버 관리자에 게 알려 주는 SQLUINTEGER 값입니다.<br /><br /> SQL_OPT_TRACE_OFF = 추적 해제 (기본값)<br /><br /> SQL_OPT_TRACE_ON = 추적<br /><br /> 추적이 설정 되 면 드라이버 관리자는 각 ODBC 함수 호출을 추적 파일에 기록 합니다. **참고:**  추적이 설정 되 면 드라이버 관리자는 모든 함수에서 SQLSTATE IM013 (추적 파일 오류)를 반환할 수 있습니다. <br /><br /> 응용 프로그램은 SQL_ATTR_TRACEFILE 옵션을 사용 하 여 추적 파일을 지정 합니다. 파일이 이미 있는 경우 드라이버 관리자가 파일에 추가 합니다. 그렇지 않으면 파일을 만듭니다. 추적을 설정 하 고 추적 파일을 지정 하지 않은 경우 드라이버 관리자는 SQL 파일에 기록 합니다. 루트 디렉터리에 로그인 합니다.<br /><br /> 응용 프로그램은 **ODBCSharedTraceFlag** 변수를 설정 하 여 동적으로 추적을 사용 하도록 설정할 수 있습니다. 그런 다음 현재 실행 중인 모든 ODBC 응용 프로그램에 대해 추적을 사용 하도록 설정 합니다. 응용 프로그램에서 추적 기능을 해제 하면 해당 응용 프로그램에 대해서만 해제 됩니다.<br /><br /> 응용 프로그램에서 *HandleType* 가 SQL_HANDLE_ENV 인 **SQLAllocHandle** 를 호출할 때 시스템 정보의 **Trace** 키워드가 1로 설정 된 경우 모든 핸들에 대해 추적을 사용할 수 있습니다. **SQLAllocHandle**를 호출한 응용 프로그램에 대해서만 사용할 수 있습니다.<br /><br /> SQL_ATTR_TRACE *특성* 을 사용 하 여 **SQLSetConnectAttr** 를 호출 하는 경우 *ConnectionHandle* 인수가 유효 하지 않아도 되 고 *ConnectionHandle* 가 NULL 인 경우에는 SQL_ERROR를 반환 하지 않습니다. 이 특성은 모든 연결에 적용 됩니다.|  
|SQL_ATTR_TRACEFILE (ODBC 1.0)|추적 파일의 이름을 포함 하는 null로 끝나는 문자열입니다.<br /><br /> SQL_ATTR_TRACEFILE 특성의 기본값은 시스템 정보에서 **Tracefile** 키워드를 사용 하 여 지정 됩니다. 자세한 내용은 [ODBC 하위 키](../../../odbc/reference/install/odbc-subkey.md)를 참조 하세요.<br /><br /> SQL_ATTR_ TRACEFILE *특성* 을 사용 하 여 **SQLSetConnectAttr** 를 호출 하는 경우 *ConnectionHandle* 인수가 유효 하지 않아도 되 고 *ConnectionHandle* 가 잘못 된 경우에는 SQL_ERROR을 반환 하지 않습니다. 이 특성은 모든 연결에 적용 됩니다.|  
|SQL_ATTR_TRANSLATE_LIB (ODBC 1.0)|드라이버가 문자 집합 변환과 같은 작업을 수행 하기 위해 액세스 하는 **SQLDriverToDataSource** 및 **SQLDataSourceToDriver** 함수를 포함 하는 라이브러리의 이름을 포함 하는 null로 끝나는 문자열입니다. 이 옵션은 드라이버가 데이터 원본에 연결 된 경우에만 지정할 수 있습니다. 이 특성의 설정은 연결에서 유지 됩니다. 데이터 변환에 대 한 자세한 내용은 [변환 dll](../../../odbc/reference/develop-app/translation-dlls.md) 및 [변환 dll 함수 참조](../../../odbc/reference/syntax/translation-dll-api-reference.md)를 참조 하세요.|  
|SQL_ATTR_TRANSLATE_OPTION (ODBC 1.0)|변환 DLL로 전달 되는 32 비트 플래그 값입니다. 드라이버가 데이터 원본에 연결 된 경우에만이 특성을 지정할 수 있습니다. 데이터 변환에 대 한 자세한 내용은 [변환 dll](../../../odbc/reference/develop-app/translation-dlls.md)을 참조 하세요.|  
|SQL_ATTR_TXN_ISOLATION (ODBC 1.0)|현재 연결에 대 한 트랜잭션 격리 수준을 설정 하는 32 비트 비트 마스크입니다. 이 옵션을 사용 하 여 **SQLSetConnectAttr** 를 호출 하기 전에 응용 프로그램은 **sqlendtran** 을 호출 하 여 연결에서 열려 있는 모든 트랜잭션을 커밋하거나 롤백해야 합니다.<br /><br /> *InfoType* 와 동일한 **SQLGetInfo** 를 호출 하 여와 같은 값 SQL_TXN_ISOLATION_OPTIONS을 사용 하 여 값을 확인할 *수 있습니다.*<br /><br /> 트랜잭션 격리 수준에 대 한 설명은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 및 [트랜잭션 격리 수준](../../../odbc/reference/develop-app/transaction-isolation-levels.md)에서 SQL_DEFAULT_TXN_ISOLATION 정보 형식에 대 한 설명을 참조 하세요.|  
  
 [1] 설명자가 응용 프로그램 설명자가 아니라 구현 설명자 인 경우에만 이러한 함수를 비동기적으로 호출할 수 있습니다.  
  
## <a name="code-example"></a>코드 예  
 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)를 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|연결 특성의 설정 반환|[SQLGetConnectAttr 함수(SQLGetConnectAttr Function)](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
