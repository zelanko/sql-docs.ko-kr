---
title: SQLSetConnectAttr 기능 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301939"
---
# <a name="sqlsetconnectattr-function"></a>SQLSetConnectAttr 함수
**규칙**  
 버전 출시: ODBC 3.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLSetConnectAttr** 연결의 측면을 제어 하는 특성을 설정 합니다.  
  
> [!NOTE]
>  ODBC 3 *.x* 응용 프로그램이 ODBC 2 *.x* 드라이버로 작업할 때 드라이버 관리자가 이 함수를 매핑하는 작업에 대한 자세한 내용은 [응용 프로그램의 이전 버전과의 호환성에 대한 매핑 교체 함수를](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLSetConnectAttr(  
     SQLHDBC       ConnectionHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>인수  
 *연결 핸들*  
 [Input] 연결 핸들입니다.  
  
 *특성*  
 [입력] "주석"에 나열된 설정 특성입니다.  
  
 *ValuePtr*  
 [입력] *속성에*연결할 값에 대한 포인터 . *특성값에*따라 *ValuePtr은* 부호없는 정수 값이 되거나 null 종료된 문자 문자열을 가리킵니다. *특성* 인수의 정수 유형은 길이가 고정되지 않을 수 있으며 자세한 내용은 주석 섹션을 참조하십시오.  
  
 *문자열 길이*  
 [입력] *특성이* ODBC 정의 특성이고 *ValuePtr이* 문자 문자열 또는 이진 버퍼를 가리키는 경우 이 인수는 **ValuePtr*의 길이여야 합니다. 문자열 데이터의 경우 이 인수에는 문자열의 바이트 수가 포함되어야 합니다.  
  
 *특성이* ODBC 정의 특성이고 *ValuePtr이* 정수인 경우 *StringLength는* 무시됩니다.  
  
 *특성이* 드라이버 정의 특성인 경우 응용 프로그램은 *StringLength* 인수를 설정하여 드라이버 관리자에 대한 특성의 특성을 나타냅니다. *StringLength에는* 다음 값이 있을 수 있습니다.  
  
-   *ValuePtr이* 문자열 문자열에 대한 포인터인 경우 *StringLength는* 문자열 또는 SQL_NTS 길이입니다.  
  
-   *ValuePtr이* 이진 버퍼에 대한 포인터인 경우 응용 프로그램은 *stringLength에**SQL_LEN_BINARY_ATTR(길이)* 매크로의 결과를 배치합니다. 그러면 *문자열Length에*음수 값이 배치됩니다.  
  
-   *ValuePtr이* 문자열 또는 이진 문자열 이외 값에 대한 포인터인 경우 *StringLength는* SQL_IS_POINTER 값을 가져야 합니다.  
  
-   *ValuePtr* 고정 길이 값을 포함 하는 경우 *StringLength는* SQL_IS_INTEGER 또는 SQL_IS_UINTEGER 적절 하 게.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE 또는 SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>진단  
 **SQLSetConnectAttr** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 관련 된 SQLSTATE 값 SQL_HANDLE_DBC *핸들 SQL_HANDLE_DBC* 및 연결 *핸들의* **핸들을** 호출 하 여 가져올 수 있습니다. *Handle* 다음 표에서는 **SQLSetConnectAttr에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
 드라이버는 SQL_SUCCESS_WITH_INFO 반환하여 옵션 설정 결과에 대한 정보를 제공할 수 있습니다.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01S02|옵션 값이 변경되었습니다.|드라이버는 *ValuePtr에* 지정된 값을 지원하지 않고 유사한 값을 대체했습니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08002|사용 중 연결 이름|*특성* 인수가 SQL_ATTR_ODBC_CURSORS 드라이버가 이미 데이터 원본에 연결되었습니다.|  
|08003|연결이 열려 있지 않음|(DM) 열린 연결이 필요한 *특성* 값이 지정되었지만 *ConnectionHandle이* 연결된 상태가 아닙니다.|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|24000|잘못된 커서 상태|*특성* 인수가 SQL_ATTR_CURRENT_CATALOG 결과 집합이 보류 중이었습니다.|  
|25000|로컬 트랜잭션 중 불법 작업|연결 특성을 SQL_ATTR_ENLIST_IN_DTC 설정하여 DTC(분산 트랜잭션 연결)에 참여하려고 시도하는 동안 로컬 트랜잭션에 연결되었습니다.<br /><br /> 연결이 이미 DTC에 등록되어 있습니다.<br /><br /> 분산 트랜잭션 연결에 연결이 등록되었으며 SQL_ATTR_AUTOCOMMIT SQL_AUTOCOMMIT_OFF 설정하여 로컬 트랜잭션이 시작되었습니다.|  
|3D000|카탈로그 이름이 잘못되었습니다.|*특성* 인수가 SQL_CURRENT_CATALOG 지정한 카탈로그 이름이 잘못되었습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*연결 핸들*에 대해 비동기 처리가 활성화되었습니다. **SQLSetConnectAttr** 함수가 호출되었고 실행을 완료하기 전에 [SQLCancelHandle 함수가](../../../odbc/reference/syntax/sqlcancelhandle-function.md) *연결 핸들에서*호출된 다음 **SQLSetConnectAttr** 함수가 *연결 핸들*에서 다시 호출되었습니다.<br /><br /> 또는 **SQLSetConnectAttr** 함수가 호출되었으며 실행을 완료하기 전에 **SQLCancelHandle은** 다중 스레드 응용 프로그램의 다른 스레드에서 *ConnectionHandle에서* 호출되었습니다.|  
|HY09|null 포인터의 잘못된 사용|*특성* 인수는 문자열 값이 필요한 연결 특성을 식별했으며 *ValuePtr* 인수는 null 포인터였습니다.|  
|HY010|함수 시퀀스 오류|(DM) *연결 핸들과* 연결된 *문핸들에* 대해 비동기적으로 실행 되는 함수가 호출 되었으며 **SQLSetConnectAttr** 호출 될 때 여전히 실행 되 고 있었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *연결 핸들에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *연결 핸들과* 연결된 문 핸들 중 하나를 호출하고 반환 된 SQL_PARAM_DATA_AVAILABLE. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *연결 핸들과* 연결된 *문핸들을* 호출하고 SQL_NEED_DATA 반환했습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.<br /><br /> (DM) **SQLBrowseConnect는** *연결 핸들에* 대 한 호출 하 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 **SQLBrowseConnect가** SQL_SUCCESS_WITH_INFO 또는 SQL_SUCCESS 반환하기 전에 호출되었습니다.|  
|HY011|특성을 지금 설정할 수 없습니다.|*특성* 인수가 SQL_ATTR_TXN_ISOLATION 트랜잭션이 열려 있었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY024|잘못된 특성 값|지정된 *특성* 값이 주어지면 *값Ptr*에 잘못된 값이 지정되었습니다. 드라이버 관리자는 SQL_ATTR_ACCESS_MODE 또는 SQL_ATTR_ASYNC_ENABLE 같은 개별 값 집합을 허용하는 연결 및 명령문 특성에 대해서만 이 SQLSTATE를 반환합니다. 다른 모든 연결 및 문 특성의 경우 드라이버는 *ValuePtr에*지정된 값을 확인해야 합니다.)<br /><br /> *특성* 인수는 SQL_ATTR_TRACEFILE 또는 SQL_ATTR_TRANSLATE_LIB 값 *Ptr빈* 문자열입니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|*(DM) \*ValuePtr은* 문자 문자열이며 *StringLength* 인수는 0보다 작지만 SQL_NTS 않았습니다.|  
|HY092|잘못된 특성/옵션 식별자|(DM) 인수 *특성에* 대해 지정된 값이 드라이버에서 지원하는 ODBC 버전에 대해 유효하지 않습니다.<br /><br /> (DM) 인수 *특성에* 대해 지정된 값은 읽기 전용 특성입니다.|  
|HY14|드라이버는 연결 수준 비동기 함수 실행을 지원하지 않습니다.|(DM) 응용 프로그램이 비동기 연결 작업을 지원하지 않는 드라이버에 대해 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 사용하여 비동기 함수 실행을 사용하도록 설정하려고 했습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HY121|커서 라이브러리 및 드라이버 인식 풀링을 동시에 사용할 수 없습니다.|자세한 내용은 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)을 참조하십시오.|  
|하이크00|구현되지 않은 선택적 기능|인수 *특성에* 대해 지정된 값은 드라이버에서 지원하는 ODBC 버전에 대한 유효한 ODBC 연결 또는 문 특성이지만 드라이버에서 지원되지 않았습니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *연결 핸들과* 연결된 드라이버가 기능을 지원하지 않습니다.|  
|IM009|번역 DLL을 로드할 수 없음|드라이버가 연결에 지정된 번역 DLL을 로드할 수 없습니다. 이 오류는 *특성이* SQL_ATTR_TRANSLATE_LIB 경우에만 반환할 수 있습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
|S1118|드라이버가 비동기 알림을 지원하지 않습니다.|SQL_ATTR_ASYNC_DBC_EVENT 설정되었지만(연결이 이루어진 후) 비동기 알림은 드라이버에서 지원되지 않습니다.|  
  
 *특성이* 명령문 특성인 경우 **SQLSetConnectAttr은** **SQLSetStmtAttr**에서 반환된 모든 SQLSTATEs를 반환할 수 있습니다.  
  
## <a name="comments"></a>주석  
 연결 특성에 대한 일반 정보는 [연결 특성 을](../../../odbc/reference/develop-app/connection-attributes.md)참조하십시오.  
  
 현재 정의된 특성과 해당 특성이 도입된 ODBC 버전은 이 섹션의 다음 표에 나와 있습니다. 다른 데이터 원본을 활용하기 위해 더 많은 특성이 정의될 것으로 예상됩니다. 특성의 범위는 ODBC에 의해 예약됩니다. 드라이버 개발자는 Open Group에서 드라이버별 사용을 위해 값을 예약해야 합니다.  
  
> [!NOTE]
>  **SQLSetConnectAttr을** 호출하여 연결 수준에서 문 특성을 설정하는 기능은 ODBC 3 *.x*. ODBC 3 *.x* 응용 프로그램은 연결 수준에서 문 특성을 설정해서는 안 됩니다. ODBC 3 *.x* 문 특성은 SQL_ATTR_METADATA_ID 연결 특성및 SQL_ATTR_ASYNC_ENABLE 특성을 제외하고 연결 수준에서 설정할 수 없으며 연결 특성 및 문 특성모두이며 연결 수준 또는 문 수준에서 설정할 수 있습니다.  
> 
>  ODBC 3 *.x* 드라이버는 연결 수준에서 ODBC 2 *.x* 문 옵션을 설정한 ODBC 2 *.x* 응용 프로그램과 함께 작동해야 하는 경우에만 이 기능을 지원하면 됩니다. 자세한 내용은 부록 G: 이전 버전과의 호환성을 위한 드라이버 지침의 [SQLSetConnectOption 매핑을](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) 참조하십시오.  
  
 응용 프로그램은 연결이 할당되고 해제될 때까지 언제든지 **SQLSetConnectAttr을** 호출할 수 있습니다. 연결에 대한 응용 프로그램에서 성공적으로 설정한 모든 연결 및 문 특성은 **연결에서 SQLFreeHandle이** 호출될 때까지 유지됩니다. 예를 들어 응용 프로그램이 데이터 원본에 연결하기 전에 **SQLSetConnectAttr을** 호출하는 경우 응용 프로그램이 데이터 원본에 연결할 때 **SQLSetConnectAttr이** 드라이버에서 실패하더라도 특성이 유지됩니다. 응용 프로그램이 드라이버 관련 특성을 설정하면 응용 프로그램이 연결의 다른 드라이버에 연결되더라도 특성이 유지됩니다.  
  
 일부 연결 특성은 연결이 이루어지기 전에만 설정할 수 있습니다. 다른 사용자는 연결이 이루어진 후에만 설정할 수 있습니다. 다음 표는 연결이 이루어지기 전이나 후에 설정해야 하는 연결 특성을 나타냅니다. *어느 쪽이든* 속성이 연결 전이나 후에 설정할 수 있음을 나타냅니다.  
  
|특성|연결 전이나 후에 설정?|  
|---------------|-------------------------------------|  
|SQL_ATTR_ACCESS_MODE|어느 쪽이든[1]|  
|SQL_ATTR_ASYNC_DBC_EVENT|여기서는|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE|어느 쪽도 [4]|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK|여기서는|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT|여기서는|  
|SQL_ATTR_ASYNC_ENABLE|어느 쪽도 [2]|  
|SQL_ATTR_AUTO_IPD|여기서는|  
|SQL_ATTR_AUTOCOMMIT|어느 쪽도 [5]|  
|SQL_ATTR_CONNECTION_DEAD|After|  
|SQL_ATTR_CONNECTION_TIMEOUT|여기서는|  
|SQL_ATTR_CURRENT_CATALOG|어느 쪽이든[1]|  
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
|SQL_ATTR_TXN_ISOLATION|어느 쪽도 [3]|  
  
 [1] SQL_ATTR_ACCESS_MODE 및 SQL_ATTR_CURRENT_CATALOG 드라이버에 따라 연결 전후에 설정할 수 있습니다. 그러나 일부 드라이버는 연결 후 이러한 변경을 지원하지 않기 때문에 상호 운용 가능한 응용 프로그램은 연결하기 전에 설정합니다.  
  
 [2] SQL_ATTR_ASYNC_ENABLE 활성 문이 있기 전에 설정해야 합니다.  
  
 [3] SQL_ATTR_TXN_ISOLATION 연결에 열려 있는 트랜잭션이 없는 경우에만 설정할 수 있습니다. 일부 연결 특성은 데이터 원본이 \* *ValuePtr에*지정된 값을 지원하지 않는 경우 유사한 값의 대체를 지원합니다. 이러한 경우 드라이버는 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01S02(옵션 값이 변경)를 반환합니다. 예를 들어 *특성이* SQL_ATTR_PACKET_SIZE \* *ValuePtr이* 최대 패킷 크기를 초과하는 경우 드라이버는 최대 크기를 대체합니다. 대체 값을 결정하기 위해 응용 프로그램은 **SQLGetConnectAttr**을 호출합니다.  
  
 [4] 연결을 열기 전에 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 설정하면 드라이버 관리자는 **SQLBrowseConnect,** **SQLConnect**또는 **SQLDriverConnect**를 호출하는 동안 드라이버가 로드될 때 드라이버 특성을 설정합니다. **SQLBrowseConnect,** **SQLConnect**또는 **SQLDriverConnect를**호출하기 전에 드라이버 관리자는 연결할 드라이버를 알지 못하며 드라이버가 비동기 연결 작업을 지원하는지 여부를 알지 못합니다. 따라서 드라이버 관리자는 항상 SQL_SUCCESS 반환합니다. 그러나 드라이버가 비동기 연결 작업을 지원하지 않는 경우 **SQLBrowseConnect,** **SQLConnect**또는 **SQLDriverConnect에** 대한 호출이 실패합니다.  
  
 [5] SQL_ATTR_AUTOCOMMIT FALSE로 설정된 경우 API가 트랜잭션 일관성을 보장하기 위해 SQL_ERROR 반환하는 경우 응용 프로그램은 SQLEndTran(SQL_ROLLBACK)을 호출해야 합니다.  
  
 \* *ValuePtr* 버퍼에 설정된 정보 형식은 지정된 *특성*에 따라 다릅니다. **SQLSetConnectAttr** 는 null 종료 된 문자 문자열 또는 정수 값의 두 가지 형식 중 하나에서 특성 정보를 수락합니다. 각 형식은 특성 설명에 기록됩니다. **SQLSetConnectAttr의** *ValuePtr* 인수에 의해 가리키는 문자열 문자열 문자열 *문자열의* 길이 문자열 길이 바이트.  
  
 *STRINGLength* 인수는 ODBC 2 *.x* 또는 이전에 도입된 모든 특성의 경우와 마찬가지로 길이가 특성에 의해 정의된 경우 무시됩니다.  
  
|*특성*|*밸류Ptr* 내용|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE (ODBC 1.0)|SQLUINTEGER 값입니다. SQL_MODE_READ_ONLY 드라이버 또는 데이터 원본에서 업데이트가 발생하는 SQL 문을 지원하기 위해 연결이 필요하지 않다는 표시기로 사용됩니다. 이 모드는 드라이버 또는 데이터 원본에 적합한 잠금 전략, 트랜잭션 관리 또는 기타 영역을 최적화하는 데 사용할 수 있습니다. 드라이버는 이러한 진술이 데이터 원본에 제출되는 것을 방지할 필요가 없습니다. 읽기 전용 연결 중에 읽기 전용이 아닌 SQL 문을 처리하라는 메시지가 표시됩니다. SQL_MODE_READ_WRITE 기본값입니다.|  
|SQL_ATTR_ASYNC_DBC_EVENT (ODBC 3.8)|이벤트 핸들인 SQLPOINTER 값입니다.<br /><br /> 비동기 함수의 완료에 대한 알림은 **SQLSetConnectAttr을** SQL_ATTR_ASYNC_STMT_EVENT 특성으로 호출하고 이벤트 핸들을 지정하여 사용할 수 있습니다. **참고:**  알림 메서드는 커서 라이브러리에서 지원되지 않습니다. 응용 프로그램은 알림 메서드를 사용하도록 설정하면 SQLSetConnectAttr을 통해 커서 라이브러리를 사용하도록 설정하려고 하면 오류 메시지가 표시됩니다.|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE (ODBC 3.8)|연결 핸들에서 선택한 함수의 비동기 실행을 활성화하거나 사용하지 않도록 설정하는 SQLUINTEGER 값입니다. 자세한 내용은 [비동기 실행(폴링 메서드)을](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)참조하십시오.<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = 지정된 연결 관련 함수에 대해 비동기 작업을 사용하도록 설정합니다.<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = (기본값) 지정된 연결 관련 함수에 대해 비동기 작업을 사용하지 않도록 설정합니다.<br /><br /> SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 설정은 항상 동기식입니다(즉, SQL_STILL_EXECUTING 반환되지 않습니다).<br /><br /> 명령문 작업의 비동기 실행은 SQL_ATTR_ASYNC_ENABLE 함께 활성화됩니다.|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK (ODBC 3.8)|컨텍스트 구조를 가리키는 SQLPOINTER 값입니다.<br /><br /> 드라이버 관리자만 이 특성을 가진 드라이버의 **SQLSetStmtAttr** 함수를 호출할 수 있습니다.|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT (ODBC 3.8)|컨텍스트 구조를 가리키는 SQLPOINTER 값입니다.<br /><br /> 드라이버 관리자만 이 특성을 가진 드라이버의 **SQLSetStmtAttr** 함수를 호출할 수 있습니다.|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 3.0)|지정된 연결에 문으로 호출된 함수가 비동기적으로 실행되는지 여부를 지정하는 SQLULEN 값은 다음과 같은 것입니다.<br /><br /> SQL_ASYNC_ENABLE_OFF = 명령문 작업에 대한 연결 수준 비동기 실행 지원(기본값)을 사용하지 않도록 설정합니다.<br /><br /> SQL_ASYNC_ENABLE_ON = 문 작업에 대한 연결 수준 비동기 실행 지원을 활성화합니다.<br /><br /> 이 특성은 SQL_ASYNC_MODE 정보 형식이 SQL_AM_CONNECTION 반환하는지 또는 SQL_AM_STATEMENT **대해 SQLGetInfo를** 사용할지 여부를 설정할 수 있습니다.|  
|SQL_ATTR_AUTO_IPD (ODBC 3.0)|**SQLPrepare를** 호출한 후 IPD의 자동 모집단이 지원되는지 여부를 지정하는 읽기 전용 SQLUINTEGER 값은 다음과 같은 방식으로 지원됩니다.<br /><br /> SQL_TRUE = **SQLPrepare** 를 호출한 후 IPD의 자동 채우기는 드라이버에서 지원됩니다.<br /><br /> SQL_FALSE = **SQLPrepare** 를 호출한 후 IPD의 자동 채우기는 드라이버에서 지원되지 않습니다. 준비된 문을 지원하지 않는 서버는 IPD를 자동으로 채울 수 없습니다.<br /><br /> SQL_ATTR_AUTO_IPD 연결 특성에 대해 SQL_TRUE 반환되는 경우 SQL_ATTR_ENABLE_AUTO_IPD 문 특성을 설정하여 IPD의 자동 모집단을 켜거나 끌 수 있습니다. SQL_ATTR_AUTO_IPD SQL_FALSE 경우 SQL_ATTR_ENABLE_AUTO_IPD SQL_TRUE 설정할 수 없습니다. SQL_ATTR_ENABLE_AUTO_IPD 기본값은 SQL_ATTR_AUTO_IPD 값과 같습니다.<br /><br /> 이 연결 특성은 **SQLGetConnectAttr에서** 반환할 수 있지만 **SQLSetConnectAttr에서**설정할 수 없습니다.|  
|SQL_ATTR_AUTOCOMMIT (ODBC 1.0)|자동 커밋 또는 수동 커밋 모드를 사용할지 여부를 지정하는 SQLUINTEGER 값입니다.<br /><br /> SQL_AUTOCOMMIT_OFF = 드라이버는 수동 커밋 모드를 사용하며 응용 프로그램은 **SQLEndTran**.<br /><br /> SQL_AUTOCOMMIT_ON = 드라이버가 자동 커밋 모드를 사용합니다. 각 문은 실행 된 직후에 커밋됩니다. 이것이 기본값입니다. SQL_ATTR_AUTOCOMMIT 수동 커밋 모드에서 자동 커밋 모드로 변경하도록 SQL_AUTOCOMMIT_ON 설정되면 연결의 모든 열려 있는 트랜잭션이 커밋됩니다.<br /><br /> 자세한 내용은 [커밋 모드를](../../../odbc/reference/develop-app/commit-mode.md)참조하십시오. **중요 사항:**  일부 데이터 원본은 액세스 계획을 삭제하고 문이 커밋될 때마다 연결의 모든 명령문에 대한 커서를 닫습니다. 자동 커밋 모드는 각 비쿼리 문이 실행되거나 쿼리에 대해 커서가 닫힐 때 이러한 일이 발생할 수 있습니다. 자세한 내용은 [SQLGetInfo의](../../../odbc/reference/syntax/sqlgetinfo-function.md) SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 유형 및 [커서 및 준비된 명령문에 대한 트랜잭션의 효과를](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)참조하십시오. <br /><br /> 일괄 처리가 자동 커밋 모드에서 실행되면 두 가지 가능한 작업을 수행할 수 있습니다. 전체 일괄 처리는 자동 커밋 할 수있는 단위로 처리하거나 일괄 처리의 각 문은 자동 커밋 가능한 단위로 처리됩니다. 특정 데이터 원본은 이러한 동작을 모두 지원할 수 있으며 둘 중 하나를 선택할 수 있는 방법을 제공할 수 있습니다. 일괄 처리가 자동 커밋 가능한 단위로 처리되는지 또는 일괄 처리 내의 각 개별 문이 자동 커밋가능한지 여부를 드라이버 정의합니다.|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> (ODBC 3.5)|연결 상태를 나타내는 읽기 전용 SQLUINTEGER 값입니다. SQL_CD_TRUE 연결이 끊어졌습니다. SQL_CD_FALSE 경우 연결이 계속 활성 상태입니다.|  
|SQL_ATTR_CONNECTION_TIMEOUT (ODBC 3.0)|SQLUINTEGER 값은 응용 프로그램으로 돌아가기 전에 연결에 대한 요청이 완료될 때까지 기다리는 시간(초)에 해당하는 값입니다. 드라이버는 쿼리 실행 또는 로그인과 연결되지 않은 상황에서 시간 중지가 가능할 수 있는 SQLSTATE HYT00(시간 시간 만료)을 언제든지 반환해야 합니다.<br /><br /> *ValuePtr이* 0(기본값)과 같으면 시간 설정이 없습니다.|  
|SQL_ATTR_CURRENT_CATALOG (ODBC 2.0)|데이터 원본에서 사용할 카탈로그 이름을 포함하는 문자열입니다. 예를 들어 SQL Server에서 카탈로그는 데이터베이스이므로 드라이버는 \* *ValuePtr*에 지정된 *데이터베이스인* 데이터 원본에 **USE** _데이터베이스_ 문을 보냅니다. 단일 계층 드라이버의 경우 카탈로그가 디렉터리일 수 있으므로 드라이버는 현재 디렉터리를 **ValuePtr에*지정된 디렉토리로 변경합니다.|  
|SQL_ATTR_DBC_INFO_TOKEN (ODBC 3.8|[SQLRateConnection의](../../../odbc/reference/syntax/sqlrateconnection-function.md)\**(pRating)* 매개 변수가 100과 같지 않을 때 연결 정보 토큰을 DBC 핸들로 다시 설정하는 데 사용되는 SQLPOINTER 값입니다.<br /><br /> SQL_ATTR_DBC_INFO_TOKEN 설정 전용입니다. 이 값을 검색하려면 **SQLGetConnectAttr** 또는 **SQLGetConnectOption을** 사용할 수 없습니다. 응용 프로그램이 이 특성을 설정하지 않아야 하므로 드라이버 관리자의 **SQLSetConnectAttr은** SQL_ATTR_DBC_INFO_TOKEN 허용하지 않습니다.<br /><br /> 드라이버가 SQL_ATTR_DBC_INFO_TOKEN 설정한 후 SQL_ERROR 반환하면 풀에서 방금 얻은 연결이 해제됩니다. 그런 다음 드라이버 관리자는 풀에서 다른 연결을 얻으려고 시도합니다. 자세한 내용은 [ODBC 드라이버에서 연결 풀 인식 개발을](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md) 참조하십시오.|  
|SQL_ATTR_ENLIST_IN_DTC (ODBC 3.0)|Microsoft 구성 요소 서비스에서 조정하는 분산 트랜잭션에서 ODBC 드라이버를 사용할지 여부를 지정하는 SQLPOINTER 값입니다.<br /><br /> 트랜잭션을 SQL Server로 내보낼 지정하거나 연결의 DTC 연결을 종료하도록 SQL_DTC_DONE 지정하는 DTC OLE 트랜잭션 개체를 전달합니다.<br /><br /> 클라이언트는 MS DTC(분산 트랜잭션 코디네이터) OLE ITransaction디스펜서::BeginTransaction 메서드를 호출하여 MS DTC 트랜잭션을 시작하고 트랜잭션을 나타내는 MS DTC 트랜잭션 개체를 만듭니다. 그런 다음 응용 프로그램은 트랜잭션 개체를 ODBC 연결과 연결하는 SQL_ATTR_ENLIST_IN_DTC 옵션으로 SQLSetConnectAttr을 호출합니다. 관련된 모든 데이터베이스 작업은 MS DTC 트랜잭션의 보호 아래 수행됩니다. 응용 프로그램에서는 SQL_DTC_DONE과 함께 SQLSetConnectAttr을 호출하여 DTC와의 연결을 종료합니다. 자세한 내용은 MS DTC 설명서를 참조하십시오.|  
|SQL_ATTR_LOGIN_TIMEOUT (ODBC 1.0)|응용 프로그램으로 돌아가기 전에 로그인 요청이 완료될 때까지 기다리는 시간(초)에 해당하는 SQLUINTEGER 값입니다. 기본값은 드라이버에 따라 다릅니다. *ValuePtr이* 0이면 시간 지정이 비활성화되고 연결 시도가 무기한 대기됩니다.<br /><br /> 지정된 시간 초과가 데이터 원본의 최대 로그인 시간 초과를 초과하면 드라이버는 해당 값을 대체하고 SQLSTATE 01S02(옵션 값이 변경)를 반환합니다.|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|카탈로그 함수의 문자열 인수를 처리하는 방법을 결정하는 SQLUINTEGER 값입니다.<br /><br /> SQL_TRUE 경우 카탈로그 함수의 문자열 인수는 식별자로 처리됩니다. 이 경우는 중요하지 않습니다. 제한되지 않은 문자열의 경우 드라이버는 후행 공간을 제거하고 문자열을 대문자로 접습니다. 구분된 문자열의 경우 드라이버는 선행 또는 후행 공백을 제거하고 구분 기호 사이에 문자 그대로 모든 것을 취합니다. 이러한 인수 중 하나가 null 포인터로 설정된 경우 함수는 SQL_ERROR 및 SQLSTATE HY009(null 포인터의 잘못된 사용)를 반환합니다.<br /><br /> SQL_FALSE 경우 카탈로그 함수의 문자열 인수는 식별자로 처리되지 않습니다. 이 경우는 중요합니다. 인수에 따라 문자열 검색 패턴을 포함하거나 포함하지 않을 수 있습니다.<br /><br /> 기본값은 SQL_FALSE.<br /><br /> 값 목록을 사용하는 **SQLTable의** *TableType* 인수는 이 특성의 영향을 받지 않습니다.<br /><br /> SQL_ATTR_METADATA_ID 문 수준에서 설정할 수도 있습니다. (명령문 특성이기도 한 유일한 연결 특성입니다.)<br /><br /> 자세한 내용은 [카탈로그 함수의 인수를](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)참조하십시오.|  
|SQL_ATTR_ODBC_CURSORS (ODBC 2.0)|드라이버 관리자가 ODBC 커서 라이브러리를 사용하는 방법을 지정하는 SQLULEN 값입니다.<br /><br /> SQL_CUR_USE_IF_NEEDED = 드라이버 관리자는 필요한 경우에만 ODBC 커서 라이브러리를 사용합니다. 드라이버가 **SQLFetchScroll에서**SQL_FETCH_PRIOR 옵션을 지원하는 경우 드라이버 관리자는 드라이버의 스크롤 기능을 사용합니다. 그렇지 않으면 ODBC 커서 라이브러리를 사용합니다.<br /><br /> SQL_CUR_USE_ODBC = 드라이버 관리자는 ODBC 커서 라이브러리를 사용합니다.<br /><br /> SQL_CUR_USE_DRIVER = 드라이버 관리자는 드라이버의 스크롤 기능을 사용합니다. 이 값은 기본 설정입니다.<br /><br /> ODBC 커서 라이브러리에 대한 자세한 내용은 [부록 F: ODBC 커서 라이브러리를](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)참조하십시오. **경고:**  커서 라이브러리는 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.|  
|SQL_ATTR_PACKET_SIZE (ODBC 2.0)|네트워크 패킷 크기를 바이트로 지정하는 SQLUINTEGER 값입니다. **참고:**  많은 데이터 원본이 이 옵션을 지원하지 않거나 반환할 수 있지만 네트워크 패킷 크기를 설정할 수는 없습니다. <br /><br /> 지정된 크기가 최대 패킷 크기를 초과하거나 최소 패킷 크기보다 작으면 드라이버는 해당 값을 대체하고 SQLSTATE 01S02(옵션 값이 변경)를 반환합니다.<br /><br /> 응용 프로그램이 이미 연결한 후 패킷 크기를 설정하면 드라이버는 SQLSTATE HY011을 반환합니다(특성은 지금 설정할 수 없음).|  
|SQL_ATTR_QUIET_MODE (ODBC 2.0)|창 핸들(HWND)입니다.<br /><br /> 창 핸들이 null 포인터인 경우 드라이버는 대화 상자를 표시하지 않습니다.<br /><br /> 창 핸들이 null 포인터가 아닌 경우 응용 프로그램의 상위 창 핸들이어야 합니다. 이것이 기본값입니다. 드라이버는 이 핸들을 사용하여 대화 상자를 표시합니다. **참고:**  SQL_ATTR_QUIET_MODE 연결 특성은 **SQLDriverConnect**에서 표시되는 대화 상자에 적용되지 않습니다.|  
|SQL_ATTR_TRACE (ODBC 1.0)|SQLUINTEGER 값은 드라이버 관리자에게 추적을 수행할지 여부를 알려줍니다.<br /><br /> SQL_OPT_TRACE_OFF = 추적 해제(기본값)<br /><br /> SQL_OPT_TRACE_ON = 추적 켜기<br /><br /> 추적이 켜지면 드라이버 관리자는 각 ODBC 함수 호출을 추적 파일에 씁니다. **참고:**  추적이 켜지면 드라이버 관리자는 모든 함수에서 SQLSTATE IM013(추적 파일 오류)을 반환할 수 있습니다. <br /><br /> 응용 프로그램은 SQL_ATTR_TRACEFILE 옵션을 가진 추적 파일을 지정합니다. 파일이 이미 있는 경우 드라이버 관리자가 파일에 부가됩니다. 그렇지 않으면 파일을 만듭니다. 추적이 켜지고 추적 파일이 지정되지 않은 경우 드라이버 관리자는 파일 SQL에 기록합니다. 루트 디렉토리에 로그인합니다.<br /><br /> 응용 프로그램은 변수 **ODBCSharedTraceFlag를** 설정하여 동적으로 추적할 수 있습니다. 그런 다음 현재 실행 중인 모든 ODBC 응용 프로그램에 대해 추적이 활성화됩니다. 응용 프로그램이 추적을 해제하면 해당 응용 프로그램에 대해서만 꺼집니다.<br /><br /> 응용 프로그램에서 *핸들 유형* SQL_HANDLE_ENV **SQLAllocHandle을** 호출할 때 시스템 정보의 **추적** 키워드가 1로 설정된 경우 모든 핸들에 대해 추적이 활성화됩니다. **SQLAllocHandle**이라고 하는 응용 프로그램에 대해서만 사용 됩니다.<br /><br /> SQL_ATTR_TRACE *특성을* 가진 **SQLSetConnectAttr을** 호출하는 것은 ConnectionHandle 인수가 유효하지 않으며 *ConnectionHandle이* NULL인 경우 SQL_ERROR 반환되지 않습니다. *ConnectionHandle* 이 특성은 모든 연결에 적용됩니다.|  
|SQL_ATTR_TRACEFILE (ODBC 1.0)|추적 파일의 이름을 포함하는 null-종단 문자 문자열입니다.<br /><br /> SQL_ATTR_TRACEFILE 특성의 기본값은 시스템 정보의 **TraceFile** 키워드와 함께 지정됩니다. 자세한 내용은 [ODBC 하위 키](../../../odbc/reference/install/odbc-subkey.md)를 참조하십시오.<br /><br /> SQL_ATTR_ TRACEFILE의 *특성을* 사용하여 **SQLSetConnectAttr을** 호출하는 것은 *ConnectionHandle* 인수가 유효할 필요가 없으며 *연결 핸들이* 유효하지 않은 경우 SQL_ERROR 반환되지 않습니다. 이 특성은 모든 연결에 적용됩니다.|  
|SQL_ATTR_TRANSLATE_LIB (ODBC 1.0)|드라이버가 문자 집합 변환과 같은 작업을 수행하기 위해 액세스하는 **SQLDriverToDataSource** 및 **SQLDataSourceToDriver** 함수를 포함하는 라이브러리의 이름을 포함하는 null-terminated 문자 문자열입니다. 이 옵션은 드라이버가 데이터 원본에 연결된 경우에만 지정할 수 있습니다. 이 특성의 설정은 연결 간에 유지됩니다. 데이터 변환에 대한 자세한 내용은 [번역 DLL](../../../odbc/reference/develop-app/translation-dlls.md) 및 [번역 DLL 함수 참조를](../../../odbc/reference/syntax/translation-dll-api-reference.md)참조하십시오.|  
|SQL_ATTR_TRANSLATE_OPTION (ODBC 1.0)|번역 DLL에 전달되는 32비트 플래그 값입니다. 이 특성은 드라이버가 데이터 원본에 연결된 경우에만 지정할 수 있습니다. 데이터 변환에 대한 자세한 내용은 [번역 DLL을](../../../odbc/reference/develop-app/translation-dlls.md)참조하십시오.|  
|SQL_ATTR_TXN_ISOLATION (ODBC 1.0)|현재 연결에 대한 트랜잭션 격리 수준을 설정하는 32비트 비트 마스크입니다. 응용 프로그램은 **SQLEndTran을** 호출하여 연결에서 열려 있는 모든 트랜잭션을 커밋하거나 롤백한 다음 이 옵션을 사용하여 **SQLSetConnectAttr을** 호출해야 합니다.<br /><br /> *ValuePtr에* 대 한 유효한 값은 SQL_TXN_ISOLATION_OPTIONS 같은 *InfoType와* **SQLGetInfo를** 호출 하 여 확인할 수 있습니다.<br /><br /> 트랜잭션 격리 수준에 대한 설명은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 및 트랜잭션 격리 [수준에서](../../../odbc/reference/develop-app/transaction-isolation-levels.md)SQL_DEFAULT_TXN_ISOLATION 정보 형식에 대한 설명을 참조하십시오.|  
  
 [1] 이러한 함수는 설명자가 응용 프로그램 설명자가 아닌 구현 설명자인 경우에만 비동기적으로 호출할 수 있습니다.  
  
## <a name="code-example"></a>코드 예  
 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)를 참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|연결 특성의 설정 반환|[SQLGetConnectAttr 함수(SQLGetConnectAttr Function)](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
