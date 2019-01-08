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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aad8baf55dc8960c533e1694309083952dece3d3
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591247"
---
# <a name="sqlsetconnectattr-function"></a>SQLSetConnectAttr 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLSetConnectAttr** 연결의 측면을 제어 하는 특성을 설정 합니다.  
  
> [!NOTE]
>  새로운 드라이버 관리자는이 함수를 경우 맵을 ODBC 3 대 한 자세한 내용은 *.x* 는 ODBC 2를 사용 하 여 응용 프로그램이 작동 *.x* 드라이버를 참조 하세요. [뒤로 대 한 대체 함수 매핑 응용 프로그램의 호환성](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)합니다.  
  
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
  
 *특성*  
 [입력] 특성을 설정 하려면 "주석입니다."에 나열 된  
  
 *ValuePtr*  
 [입력] 와 연결할 값에 대 한 포인터 *특성*합니다. 값에 따라 *특성*하십시오 *ValuePtr* 부호 없는 정수 값 또는 null로 끝나는 문자열을 가리킵니다. 정수 유형의 합니다 *특성* 인수 길이 고정 될 수 있습니다 세부 정보에 대 한 설명 섹션을 참조 합니다.  
  
 *StringLength*  
 [입력] 하는 경우 *특성* 은 ODBC 정의 특성 및 *ValuePtr* 문자열 또는 이진 버퍼를 가리키는,이 인수 길이 여야 합니다 **ValuePtr*합니다. 문자 문자열 데이터의 경우이 인수는 문자열의 바이트 수를 포함 해야 합니다.  
  
 하는 경우 *특성* 은 ODBC 정의 특성 및 *ValuePtr* 정수 이면 *StringLength* 무시 됩니다.  
  
 하는 경우 *특성* 은 드라이버에서 정의 된 특성을 응용 프로그램을 설정 하 여 드라이버 관리자에 특성의 특성을 나타내는 합니다 *StringLength* 인수. *StringLength* 다음 값을 가질 수 있습니다.  
  
-   하는 경우 *ValuePtr* 문자열에 대 한 포인터 이면 *StringLength* SQL_NTS 또는 문자열의 길이입니다.  
  
-   하는 경우 *ValuePtr* 이진 버퍼에 대 한 포인터 이면 응용 프로그램을 SQL_LEN_BINARY_ATTR의 결과 배치 (*길이*)에서 매크로 *StringLength*합니다. 에 음수 값이 배치 *StringLength*합니다.  
  
-   하는 경우 *ValuePtr* 이 아닌 문자열 또는 이진 문자열 값에 대 한 포인터 이면 *StringLength* SQL_IS_POINTER 값이 있어야 합니다.  
  
-   하는 경우 *ValuePtr* 다음을 고정 길이 값이 포함 되어 *StringLength* SQL_IS_INTEGER 또는 SQL_IS_UINTEGER를 적절 하 게 됩니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE, 또는 SQL_STILL_EXECUTING 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLSetConnectAttr** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* 의 SQL_HANDLE_DBC와 *처리할* 의 *ConnectionHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLSetConnectAttr** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
 드라이버 옵션을 설정 하는 결과 대 한 정보를 제공 하는 SQL_SUCCESS_WITH_INFO를 반환할 수 있습니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S02|옵션 값이 변경 됨|드라이버에서 지정 된 값을 지원 하지 않았습니다 *ValuePtr* 유사한 값을 대체 합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08002|연결 이름 사용|합니다 *특성* 인수가 SQL_ATTR_ODBC_CURSORS, 및 드라이버 데이터 원본에 이미 연결 되었습니다.|  
|08003|연결이 열려 있지 않습니다.|(DM)는 *특성* 에 대해 열린 연결을 필요로 하는 값이 지정 되지만 *ConnectionHandle* 가 연결 된 상태가 아닙니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|24000|잘못된 커서 상태|합니다 *특성* 인수가 SQL_ATTR_CURRENT_CATALOG, 및 결과 집합을 보류 중 이었습니다.|  
|25000|로컬 트랜잭션이 있는 동안 잘못 된 작업|로컬 트랜잭션에서 분산된 트랜잭션 (DTC) 연결을 SQL_ATTR_ENLIST_IN_DTC 연결 특성을 설정 하 여 인 리스트 먼 트 하는 동안 연결이 했습니다.<br /><br /> DTC 연결을 이미 등록 되어 있습니다.<br /><br /> 분산된 트랜잭션 연결을 등록 된 연결 및 SQL_ATTR_AUTOCOMMIT을 SQL_AUTOCOMMIT_OFF를 설정 하 여 로컬 트랜잭션을 시작 했습니다.|  
|3D000|잘못 된 카탈로그 이름|합니다 *특성* 인수가 SQL_CURRENT_CATALOG, 및 지정 된 카탈로그 이름이 잘못 되었습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *ConnectionHandle*합니다. **SQLSetConnectAttr** 함수가 호출 되 고 실행을 완료 하기 전에 [SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md) 가 호출 될 합니다 *ConnectionHandle*, 차례로 **SQLSetConnectAttr** 에서 다시 호출 된 함수는 *ConnectionHandle*합니다.<br /><br /> 또는 **SQLSetConnectAttr** 함수가 호출 되 고 실행을 완료 하기 전에 **SQLCancelHandle** 가 호출 된 *ConnectionHandle* 의 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|합니다 *특성* 인수는 문자열 값이 필요한 연결 특성을 식별 하며 *ValuePtr* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수에 대해 호출 되었습니다를 *StatementHandle* 연관 된 *ConnectionHandle* 때 계속 실행 하 고 **SQLSetConnectAttr**였습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *ConnectionHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**, 또는 **SQLMoreResults** 관련 된 문 핸들 중 하나에 대해 호출한는 *ConnectionHandle* SQL_PARAM_DATA_AVAILABLE를 반환 합니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된를 *StatementHandle*  연관 된 *ConnectionHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.<br /><br /> (DM) **SQLBrowseConnect** 에 대해 호출 된 합니다 *ConnectionHandle* SQL_NEED_DATA를 반환 합니다. 하기 전에이 함수를 호출한 **SQLBrowseConnect** SQL_SUCCESS_WITH_INFO 또는 관계 없이 SQL_SUCCESS를 반환 합니다.|  
|HY011|특성을 지금 설정할 수 없습니다.|합니다 *특성* 인수가 SQL_ATTR_TXN_ISOLATION을 및 트랜잭션이 열려 있습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY024|잘못 된 특성 값|지정 된 주어진 *특성* 값을 잘못 된 값에 지정 된 *ValuePtr*합니다. (드라이버 관리자 연결 및 문 특성 SQL_ATTR_ACCESS_MODE 등 SQL_ATTR_ASYNC_ENABLE 값의 불연속 집합을 허용 하는 경우에이 SQLSTATE를 반환 하는 데 사용 합니다. 다른 모든 연결 및 문 특성에 대 한 드라이버에 지정 된 값을 확인 해야 합니다 *ValuePtr*.)<br /><br /> 합니다 *특성* 인수가 SQL_ATTR_TRACEFILE 또는 SQL_ATTR_TRANSLATE_LIB, 및 *ValuePtr* 가 빈 문자열입니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|*(DM) \*ValuePtr* 문자열, 및 *StringLength* 인수가 0 보다 작은 하지만 SQL_NTS 없습니다.|  
|HY092|잘못 된 특성/옵션 식별자입니다.|인수에 지정 된 값 (DM) *특성* ODBC 드라이버에서 지 원하는 버전에 올바르지 않습니다.<br /><br /> 인수에 지정 된 값 (DM) *특성* 읽기 전용 특성을 했습니다.|  
|HY114|드라이버는 연결 수준 비동기 함수 실행을 지원 하지 않습니다.|(DM) 응용 프로그램 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 사용 하 여 비동기 연결 작업을 지원 하지 않는 드라이버에 대 한 비동기 함수 실행을 사용 하도록 설정 하려고 합니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HY121|커서 라이브러리 및 드라이버 인식 풀링 동시에 사용할 수 없습니다.|자세한 내용은 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|인수에 지정 된 값 *특성* 유효한 ODBC 연결 된 또는 버전의 ODBC 문 특성 드라이버에서 지원 되지만 드라이버에서 지원 되지 않습니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *ConnectionHandle* 함수를 지원 하지 않습니다.|  
|IM009|변환 DLL을 로드할 수 없습니다.|드라이버 변환 연결에 대해 지정 된 DLL을 로드할 수 없습니다. 이 오류는 경우에만 반환 될 수 있습니다 *특성* SQL_ATTR_TRANSLATE_LIB 됩니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
|S1118|드라이버 비동기 알림을 지원 하지 않습니다.|(연결) 후 SQL_ATTR_ASYNC_DBC_EVENT 설정한 있지만 비동기 알림이 드라이버에서 지원 되지 않습니다.|  
  
 때 *특성* 문 특성 이라는 **SQLSetConnectAttr** 반환한 모든 Sqlstate를 반환할 수 있습니다 **SQLSetStmtAttr**합니다.  
  
## <a name="comments"></a>주석  
 연결 특성에 대 한 일반적인 정보를 참조 하세요 [연결 특성](../../../odbc/reference/develop-app/connection-attributes.md)합니다.  
  
 현재 정의 된 특성 및 도입 된 ODBC의 버전은이 섹션의 뒷부분에 나오는 표에 표시 됩니다. 다른 데이터 원본 활용 하기 위해 더 많은 특성을 정의할는 예상 됩니다. 특성의 범위는 ODBC;에 예약 되어 있습니다. 드라이버 개발자는 Open Group에서 자신의 드라이버별 사용에 대 한 값을 예약 해야 합니다.  
  
> [!NOTE]
>  연결 수준에서 호출 하 여 문 특성을 설정 하는 기능 **SQLSetConnectAttr** ODBC 3에서 사용 되지 *.x*합니다. ODBC 3 *.x* 응용 프로그램 연결 수준에서 문 특성을 설정 해서는 안됩니다. ODBC 3 *.x* 문 특성은 연결 특성 및 문 특성을 둘 다 수 있으며 SQL_ATTR_METADATA_ID 및 SQL_ATTR_ASYNC_ENABLE 특성을 제외 하 고 연결 수준에서 설정할 수 없습니다 연결 수준 또는 문 수준에서 설정 합니다.  
> 
>  ODBC 3 *.x* ODBC 2를 사용 하 여 작동 해야 하는 경우 드라이버에서이 기능은 지원 해야 *.x* ODBC 2를 설정 하는 응용 프로그램 *.x* 연결 수준에서 문 옵션입니다. 자세한 내용은 [SQLSetConnectOption 매핑](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) 부록 g:에서 이전 버전과 호환성에 대 한 드라이버 지침입니다.  
  
 응용 프로그램에서 호출할 수 있습니다 **SQLSetConnectAttr** 언제 든 지는 시간 사이의 연결이 할당 되 고 해제 합니다. 연결에 대 한 응용 프로그램에서 성공적으로 설정 하는 모든 연결 및 문 특성 될 때까지 지속 **SQLFreeHandle** 연결에서 호출 됩니다. 예를 들어 응용 프로그램 호출 **SQLSetConnectAttr** 특성을 데이터 원본에 연결 하기 전에 지속 되 면 경우에 **SQLSetConnectAttr** 응용 프로그램에 연결 하는 경우 드라이버에서 실패를 데이터 원본 드라이버별 특성을 설정 하는 응용 프로그램, 응용 프로그램을 연결에서 다른 드라이버에 연결 하는 경우에 특성이 유지 됩니다.  
  
 연결 된; 전에만 일부 연결 특성을 설정할 수 있습니다. 다른 연결 된 후에 설정할 수 있습니다. 다음 표에서 이전 또는 이후에 연결에 설정 해야 하는 연결 특성을 보여 줍니다. *두* 전이나 연결한 후 특성을 설정할 수 없음을 나타냅니다.  
  
|attribute|전이나 연결한 후 설정?|  
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
  
 [1] SQL_ATTR_ACCESS_MODE 및 SQL_ATTR_CURRENT_CATALOG 앞 이나 뒤에 연결 하는 드라이버에 따라 설정할 수 있습니다. 그러나 상호 운용 가능한 응용 프로그램 설정에 연결 하기 전에 일부 드라이버는 연결 되 면 이러한 변경를 지원 하지 않기 때문입니다.  
  
 [2] SQL_ATTR_ASYNC_ENABLE 활성 문 전에 설정 되어야 합니다.  
  
 [3] SQL_ATTR_TXN_ISOLATION 연결에서 열려 있는 트랜잭션이 필요한 경우에 설정할 수 있습니다. 데이터 원본에 지정 된 값을 지원 하지 않는 경우 일부 연결 특성 지원 유사한 값의 대체 \* *ValuePtr*합니다. 이러한 경우 드라이버는 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01S02를 반환 합니다. (옵션 값이 변경 됨). 예를 들어 경우 *특성* SQL_ATTR_PACKET_SIZE 됩니다 하 고 \* *ValuePtr* 최대 패킷 크기를 초과, 최대 크기를 대체 하는 드라이버입니다. 대체 값을 확인 하려면 응용 프로그램 호출 **SQLGetConnectAttr**합니다.  
  
 [드라이버 관리자 4] SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 연결이 열려 전에 설정 하는 경우 호출 하는 동안 드라이버를 로드할 때 드라이버의 특성을 설정 됩니다 **SQLBrowseConnect**, **SQLConnect**, 또는 **SQLDriverConnect**합니다. 호출 하기 전에 **SQLBrowseConnect**, **SQLConnect**, 또는 **SQLDriverConnect**, 드라이버 관리자에 연결 하는 드라이버를 인식 하지 못합니다 및 알 수 없습니다 여부는 드라이버는 비동기 연결 작업을 지원합니다. 따라서 드라이버 관리자는 항상 관계 없이 SQL_SUCCESS를 반환합니다. 하지만 경우 드라이버 비동기 연결 작업에 대 한 호출을 지원 하지 않습니다 **SQLBrowseConnect**를 **SQLConnect**, 또는 **SQLDriverConnect** 실패 합니다.  
  
 [5] SQL_ATTR_AUTOCOMMIT을 FALSE로 설정 하면 모든 API 트랜잭션 일관성을 유지 하는 SQL_ERROR를 반환 하는 경우 응용 프로그램 SQLEndTran(SQL_ROLLBACK)를 호출 해야 합니다.  
  
 설정 하는 정보의 형식을 합니다 \* *ValuePtr* 지정 된 버퍼에 따라 달라 집니다 *특성*합니다. **SQLSetConnectAttr** 두 가지 형식 중 하나에 대 한 특성 정보를 수락할: null로 끝나는 문자열 또는 정수 값입니다. 형식에 대해 특성의 설명에 표시 됩니다. 가리키는 문자열을 *ValuePtr* 인수의 **SQLSetConnectAttr** 길이 *StringLength* 바이트입니다.  
  
 합니다 *StringLength* 인수 길이 특성으로 정의 되어 있으면 ODBC 2에 도입 된 모든 특성의 경우와 마찬가지로 *.x* 또는 이전 버전입니다.  
  
|*특성*|*ValuePtr* 내용|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE (ODBC 1.0)|SQLUINTEGER 값입니다. SQL_MODE_READ_ONLY는 드라이버나 데이터 원본에서 연결이 필요 하지 않은 업데이트는 SQL 문을 지원 하기 위해 표시기로 사용 됩니다. 이 모드에서 드라이버 또는 데이터 원본에 따라 다른 영역 잠금 전략, 트랜잭션 관리를 최적화 하기 위해 사용할 수 있습니다. 드라이버는 이러한 문의 데이터 원본에 전송 되지 않도록 방지 필요가 없습니다. 드라이버 및 데이터 원본 없는 읽기 전용으로 읽기 전용으로 연결 하는 동안 SQL 문을 처리 하 라는 메시지가 표시 되는 경우의 동작은 구현 시 정의 합니다. SQL_MODE_READ_WRITE 기본값입니다.|  
|SQL_ATTR_ASYNC_DBC_EVENT (ODBC 3.8)|이벤트 핸들에 해당 하는 대 SQLPOINTER 값입니다.<br /><br /> 호출 하 여 비동기 함수 완료 알림을 설정할지 **SQLSetConnectAttr** SQL_ATTR_ASYNC_STMT_EVENT 특성 및 이벤트 핸들을 지정 합니다. **참고:**  알림 방법은 커서 라이브러리를 사용 하 여 지원 되지 않습니다. 응용 프로그램 알림 방법을 사용 하는 경우 SQLSetConnectAttr 통해 커서 라이브러리를 사용 하도록 설정 하려고 하면 오류 메시지가 표시 됩니다.|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE (ODBC 3.8)|연결 핸들에 대해 선택한 함수의 비동기 실행을 사용 하지 않도록 설정 하는 SQLUINTEGER 값입니다. 자세한 내용은 [비동기 실행 (폴링 메서드)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)합니다.<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = 지정 된 연결 관련 함수에 대 한 비동기 작업을 사용 하도록 설정 합니다.<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = 지정 된 연결 관련 함수에 대 한 비동기 작업 (기본값) 사용 하지 않도록 설정 합니다.<br /><br /> 설정 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE은 항상 동기 (즉, 돌아가지 SQL_STILL_EXECUTING).<br /><br /> 문 작업의 비동기 실행 SQL_ATTR_ASYNC_ENABLE을 사용 하 여 사용할 수 있습니다.|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK (ODBC 3.8)|상황에 맞는 구조를 가리키는 대 SQLPOINTER 값입니다.<br /><br /> 드라이버 관리자는 드라이버를 호출할 수 있습니다만 **SQLSetStmtAttr** 이 특성을 사용 하 여 함수입니다.|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT (ODBC 3.8)|상황에 맞는 구조를 가리키는 대 SQLPOINTER 값입니다.<br /><br /> 드라이버 관리자는 드라이버를 호출할 수 있습니다만 **SQLSetStmtAttr** 이 특성을 사용 하 여 함수입니다.|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 3.0)|지정된 된 연결에서 문을 사용 하 여 호출 된 함수를 비동기적으로 실행 되는지 여부를 지정 하는 SQLULEN 값:<br /><br /> SQL_ASYNC_ENABLE_OFF = 문 작업 (기본값)에 대 한 연결 수준 비동기 실행 지원 사용 하지 않도록 설정 합니다.<br /><br /> Sql_async_enable_on으로 = 문 작업에 대 한 연결 수준 비동기 실행 지원 사용 합니다.<br /><br /> 이 특성 수 있는지 여부를 설정 **SQLGetInfo** SQL_ASYNC_MODE 정보를 사용 하 여 형식 SQL_AM_CONNECTION 또는 SQL_AM_STATEMENT을 반환 합니다.|  
|SQL_ATTR_AUTO_IPD (ODBC 3.0)|지정 하는 읽기 전용 SQLUINTEGER 값 여부를를 호출한 후 IPD의 자동 채우기 **SQLPrepare** 지원 됩니다.<br /><br /> SQL_TRUE =를 호출한 후 IPD의 자동 채우기 **SQLPrepare** 드라이버에서 지원 됩니다.<br /><br /> SQL_FALSE =를 호출한 후 IPD의 자동 채우기 **SQLPrepare** 드라이버에서 지원 되지 않습니다. 문 준비를 지원 하지 않는 서버 IPD를 자동으로 채울 수 없습니다.<br /><br /> SQL_TRUE SQL_ATTR_AUTO_IPD 연결 특성에 대해 반환 되 면 문 특성 SQL_ATTR_ENABLE_AUTO_IPD IPD의 자동 채우기 기능을 켜거나 끄려면를 설정할 수 있습니다. SQL_ATTR_AUTO_IPD SQL_FALSE 이면 SQL_ATTR_ENABLE_AUTO_IPD SQL_TRUE로 설정할 수 없습니다. 기본값인 SQL_ATTR_ENABLE_AUTO_IPD SQL_ATTR_AUTO_IPD 값과 같습니다.<br /><br /> 이 연결 특성에서 반환 될 수 있습니다 **SQLGetConnectAttr** 으로 설정할 수 있지만 **SQLSetConnectAttr**합니다.|  
|SQL_ATTR_AUTOCOMMIT (ODBC 1.0)|자동 커밋 또는 수동 커밋 모드를 사용할지 여부를 지정 하는 SQLUINTEGER 값:<br /><br /> SQL_AUTOCOMMIT_OFF = 수동 커밋 모드를 사용 하는 드라이버 및 응용 프로그램이 명시적으로 커밋하거나 사용 하 여 트랜잭션을 롤백합니다 **SQLEndTran**합니다.<br /><br /> Sql_autocommit_on으로 드라이버는 자동 커밋 모드 =. 각 문이 실행 된 후에 즉시 커밋됩니다. 기본값입니다. 수동 커밋 모드에서 다시 자동 커밋 모드로 변경 하려면 SQL_ATTR_AUTOCOMMIT을 sql_autocommit_on으로 설정 된 경우 연결에서 열려 있는 모든 트랜잭션이 커밋됩니다.<br /><br /> 자세한 내용은 [커밋 모드](../../../odbc/reference/develop-app/commit-mode.md)합니다. **중요:**  일부 데이터 원본 액세스 계획을 삭제 하 고 문이 커밋됩니다 때마다 연결의 모든 문에 대해 커서 닫기 자동 커밋 모드는 각 nonquery 문이 실행 된 후 또는 쿼리에 대 한 커서를 닫을 때 발생 합니다.이 발생할 수 있습니다. 자세한 내용은 참조에서 SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 형식과 SQL_CURSOR_COMMIT_BEHAVIOR [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 하 고 [커서 및 준비 된 문에서 영향의 트랜잭션을](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)합니다. <br /><br /> 일괄 처리는 자동 커밋 모드에서 실행 되 면 두 가지 있을 수 있습니다. 전체 일괄 처리는 autocommitable 단위로 처리 되거나 일괄 처리의 각 문에 autocommitable 단위로 취급 됩니다. 특정 데이터 소스 모두 이러한 동작을 지원할 수 있으며 둘 중 하나를 선택 하는 방법을 제공할 수 있습니다. Autocommitable 단위로 일괄 처리는 처리 하는 여부 또는 일괄 처리 내의 각 개별 문을 autocommitable 인지 드라이버 정의입니다.|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> (ODBC 3.5)|읽기 전용 SQLUINTEGER 하는 값 연결의 상태를 나타냅니다. 경우 SQL_CD_TRUE를 연결이 끊어졌습니다. SQL_CD_FALSE를 연결 아직 활성 상태인 경우 합니다.|  
|SQL_ATTR_CONNECTION_TIMEOUT (ODBC 3.0)|응용 프로그램에 반환 하기 전에 완료에 대 한 연결에서 모든 요청에 대 한 대기 시간 (초) 수에 해당 하는 SQLUINTEGER 값입니다. 드라이버는 SQLSTATE HYT00 반환할지 (제한 시간 만료 됨)는 쿼리 실행 또는 로그인을 사용 하 여 연결 되지 않은 상황에서 시간 초과 수는 언제 든 지 합니다.<br /><br /> 하는 경우 *ValuePtr* 은 0 (기본값) 일 제한 시간은 없습니다.|  
|SQL_ATTR_CURRENT_CATALOG (ODBC 2.0)|데이터 원본에서 사용할 카탈로그의 이름을 포함 하는 문자열입니다. 예를 들어, SQL Server에서 카탈로그는 데이터베이스 드라이버 보냅니다를 **사용 하 여** _데이터베이스_ 문은 데이터 원본에 있는 *데이터베이스* 에 지정 된 데이터베이스 \* *ValuePtr*합니다. 단일 계층 드라이버의 경우 드라이버에서 지정한 디렉터리를 현재 디렉터리를 변경 하므로 카탈로그 디렉터리를 수 있습니다 **ValuePtr*합니다.|  
|(ODBC 3.8 SQL_ATTR_DBC_INFO_TOKEN|설정 하는 데 대 SQLPOINTER 값 다시는 dbc 입니다에 연결 정보 토큰 처리 시기 [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)의 (\**pRating*) 매개 변수를 100와 같지 않습니다.<br /><br /> SQL_ATTR_DBC_INFO_TOKEN 집합 전용입니다. 사용 하는 것이 불가능 **SQLGetConnectAttr** 하거나 **SQLGetConnectOption** 이 값을 검색 합니다. 드라이버 관리자의 **SQLSetConnectAttr** 응용 프로그램은이 특성을 설정 하지 않아야 하므로 SQL_ATTR_DBC_INFO_TOKEN를 허용 하지 것입니다.<br /><br /> SQL_ATTR_DBC_INFO_TOKEN를 설정한 후 SQL_ERROR를 반환 하는 드라이버를 하는 경우 풀에서 방금 가져온 연결 해제 됩니다. 그런 다음 드라이버 관리자는 다른 연결 풀에서 가져올 하려고 합니다. 참조 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md) 자세한 내용은 합니다.|  
|SQL_ATTR_ENLIST_IN_DTC (ODBC 3.0)|Microsoft 구성 요소 서비스에 의해 조정 된 분산 트랜잭션에서 ODBC 드라이버를 사용할지 여부를 지정 하는 대 SQLPOINTER 값입니다.<br /><br /> DTC OLE 트랜잭션 개체를 SQL Server, 또는 SQL_DTC_DONE DTC와 연결 종료에 내보낼 트랜잭션을 지정 하는 전달 합니다.<br /><br /> 클라이언트는 MS DTC 트랜잭션을 시작 하 여 트랜잭션을 나타내는 MS DTC 트랜잭션 개체를 만들 Microsoft Distributed Transaction Coordinator (MS DTC) OLE itransactiondispenser:: Begintransaction 메서드를 호출 합니다. 그러면 응용 프로그램이 ODBC 연결을 사용 하 여 트랜잭션 개체를 연결 하는 SQL_ATTR_ENLIST_IN_DTC 옵션을 사용 하 여 SQLSetConnectAttr를 호출 합니다. 관련된 모든 데이터베이스 작업은 MS DTC 트랜잭션의 보호 아래 수행됩니다. 응용 프로그램에 대 한 호출에서는 sql_dtc_done과 함께 SQLSetConnectAttr DTC와 연결을 종료 합니다. 자세한 내용은 MS DTC 설명서를 참조하십시오.|  
|SQL_ATTR_LOGIN_TIMEOUT (ODBC 1.0)|로그인 요청을 응용 프로그램에 반환 하기 전에 완료 될 때까지 기다리는 시간 (초) 수에 해당 하는 SQLUINTEGER 값입니다. 기본값은 드라이버에 따라 다릅니다. 하는 경우 *ValuePtr* 이 0 이면의 제한 시간이 비활성화 되었는지 이며 연결 시도 무기한으로 대기 합니다.<br /><br /> 지정된 된 시간 제한 데이터 원본에서 최대 로그인 제한 시간을 초과 하면 드라이버 해당 값을 대체 하 고 SQLSTATE 01S02를 반환 합니다 (옵션 값이 변경 됨).|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|카탈로그 함수의 문자열 인수를 처리 하는 방법을 결정 하는 SQLUINTEGER 값입니다.<br /><br /> 면 SQL_TRUE를 카탈로그 함수의 문자열 인수는 식별자로 처리 됩니다. 대/소문자는 중요 하지 않습니다. Nondelimited 문자열에 대 한 드라이버 후행 공백을 제거한 문자열을 대문자로 정리 됩니다. 구분 기호로 분리 된 문자열에 대 한 드라이버 선행 또는 후행 공백을 제거 하 고 무엇이 든 간에 구분 기호 문자 그대로 사용 합니다. 함수 반환 SQL_ERROR 및 SQLSTATE HY009 null 포인터로 설정 되어 이러한 인수 중 하나 (null 포인터를 잘못 사용).<br /><br /> 경우 SQL_FALSE를 카탈로그 함수의 문자열 인수를 사용 하는 식별자로 처리 되지 됩니다. 대/소문자는 중요 합니다. 포함할 수 있습니다 하거나 문자열 검색 패턴으로 인수에 따라.<br /><br /> 기본값은 SQL_FALSE입니다.<br /><br /> *TableType* 인수의 **SQLTables**,이 특성에 의해 영향을 받지 않습니다 값 목록을 사용 합니다.<br /><br /> SQL_ATTR_METADATA_ID 문 수준에서 설정할 수도 있습니다. (은 연결 특성 문 특성 이기도 합니다.)<br /><br /> 자세한 내용은 [카탈로그 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)합니다.|  
|SQL_ATTR_ODBC_CURSORS (ODBC 2.0)|드라이버 관리자는 ODBC 커서 라이브러리를 사용 하는 방법을 지정 하는 SQLULEN 값:<br /><br /> SQL_CUR_USE_IF_NEEDED 필요할 경우에 The Driver Manager에서 사용 하는 ODBC 커서 라이브러리를 =. 드라이버에서 SQL_FETCH_PRIOR 옵션을 지 원하는 경우 **SQLFetchScroll**, 드라이버 관리자 드라이버의 스크롤 기능을 사용 합니다. 그렇지 않은 경우 ODBC 커서 라이브러리를 사용합니다.<br /><br /> SQL_CUR_USE_ODBC = The Driver Manager에서 사용 하는 ODBC 커서 라이브러리입니다.<br /><br /> SQL_CUR_USE_DRIVER = The Driver Manager에서 사용 하는 드라이버의 스크롤 기능입니다. 이 값은 기본 설정입니다.<br /><br /> ODBC 커서 라이브러리에 대 한 자세한 내용은 참조 하세요. [부록 f: ODBC 커서 라이브러리](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)합니다. **경고:**  커서 라이브러리는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.|  
|SQL_ATTR_PACKET_SIZE (ODBC 2.0)|네트워크 패킷 크기를 바이트 단위로 지정 하는 SQLUINTEGER 값입니다. **참고:**  여러 데이터 원본은이 옵션을 하거나 지원 하지 않습니다 또는 반환 하지만 네트워크 패킷 크기를 설정 하지 수만 있습니다. <br /><br /> 지정된 된 크기 최대 패킷 크기를 초과 하거나 최소 패킷 크기 보다 작으면, 드라이버 해당 값을 대체 하 고 SQLSTATE 01S02를 반환 합니다 (옵션 값이 변경 됨).<br /><br /> 연결을 이미 수행 된 후 패킷 크기를 설정 하는 응용 프로그램, 드라이버 SQLSTATE HY011 반환 됩니다 (특성 지금 설정할 수 없습니다).|  
|SQL_ATTR_QUIET_MODE (ODBC 2.0)|창 핸들 (HWND)입니다.<br /><br /> 창 핸들을 null 포인터 이면 드라이버는 모든 대화 상자를 표시 되지 않습니다.<br /><br /> 창 핸들을 null 포인터를 없는 경우 응용 프로그램의 부모 창 핸들을 해야 합니다. 기본값입니다. 드라이버는이 핸들을 사용 하 여 대화 상자를 표시 하도록 합니다. **참고:**  SQL_ATTR_QUIET_MODE 연결 특성으로 표시 하는 대화 상자에 적용 되지 않습니다 **SQLDriverConnect**합니다.|  
|SQL_ATTR_TRACE (ODBC 1.0)|드라이버 관리자 추적을 수행할지 여부를 지시 하는 SQLUINTEGER 값:<br /><br /> SQL_OPT_TRACE_OFF 추적 off (기본값) =<br /><br /> SQL_OPT_TRACE_ON 추적 = on<br /><br /> 추적 되 면 드라이버 관리자 추적 파일에 각 ODBC 함수 호출을 씁니다. **참고:**  추적이 설정 되어 드라이버 관리자 SQLSTATE IM013를 반환할 수 있습니다 (파일 오류 추적) 함수에서. <br /><br /> 응용 프로그램 SQL_ATTR_TRACEFILE 옵션을 사용 하 여 추적 파일을 지정합니다. 파일이 이미 있는 경우 드라이버 관리자는 파일에 추가 합니다. 그렇지 않은 경우 파일을 만듭니다. 추적에 있고 지정 된 추적 파일이 없습니다 드라이버 관리자는 SQL 파일에 씁니다. 루트 디렉터리에 로그인 합니다.<br /><br /> 응용 프로그램 변수를 설정할 수 있습니다 **ODBCSharedTraceFlag** 동적으로 추적을 사용 하도록 설정 합니다. 추적은 현재 실행 중인 모든 ODBC 응용 프로그램에 대 한 설정 됩니다. 응용 프로그램 추적을 해제, 해당 응용 프로그램에 대해서만 꺼져 있습니다.<br /><br /> 경우는 **추적** 시스템 정보에는 키워드는 응용 프로그램이 호출 하면 1로 설정 됩니다 **SQLAllocHandle** 사용 하 여는 *HandleType* SQL_HANDLE_ENV의 모든 추적을 사용 처리합니다. 호출 하는 응용 프로그램에 대해서만 사용 하도록 설정 **SQLAllocHandle**합니다.<br /><br /> 호출 **SQLSetConnectAttr** 사용 하 여는 *특성* SQL_ATTR_TRACE의 필요가 없는 합니다 *ConnectionHandle* 인수 유효 경우 SQL_ERROR를 반환 하지 것입니다 하 고 *ConnectionHandle* NULL입니다. 이 특성은 모든 연결에 적용 됩니다.|  
|SQL_ATTR_TRACEFILE (ODBC 1.0)|추적 파일의 이름을 포함 하는 null로 끝나는 문자열입니다.<br /><br /> SQL_ATTR_TRACEFILE 특성의 기본 값이 지정 된 된 **TraceFile** 시스템 정보에는 키워드입니다. 자세한 내용은 [ODBC 하위 키](../../../odbc/reference/install/odbc-subkey.md)합니다.<br /><br /> 호출 **SQLSetConnectAttr** 사용 하 여는 *특성* SQL_ATTR_ TRACEFILE의 필요 하지 않습니다는 *ConnectionHandle* 인수가 유효한 경우 SQL_ERROR를 반환 하지 것입니다 하 고 *ConnectionHandle* 올바르지 않습니다. 이 특성은 모든 연결에 적용 됩니다.|  
|SQL_ATTR_TRANSLATE_LIB (ODBC 1.0)|함수를 포함 하는 라이브러리의 이름이 포함 된 null로 끝나는 문자열로 **SQLDriverToDataSource** 하 고 **SQLDataSourceToDriver** 드라이버 액세스와 같은 작업을 수행 하는 문자 집합 변환 합니다. 이 옵션은 드라이버에 데이터 원본에 연결 하는 경우에 지정 합니다. 이 특성의 설정은 연결 간에 유지 됩니다. 데이터를 변환 하는 방법에 대 한 자세한 내용은 참조 하세요. [변환 Dll](../../../odbc/reference/develop-app/translation-dlls.md) 하 고 [변환 DLL 함수 참조](../../../odbc/reference/syntax/translation-dll-api-reference.md)합니다.|  
|SQL_ATTR_TRANSLATE_OPTION (ODBC 1.0)|변환 DLL에 전달 되는 32 비트 플래그 값입니다. 이 특성 수 드라이버에 데이터 원본에 연결 하는 경우에 지정 합니다. 데이터를 변환 하는 방법에 대 한 내용은 [변환 Dll](../../../odbc/reference/develop-app/translation-dlls.md)합니다.|  
|SQL_ATTR_TXN_ISOLATION (ODBC 1.0)|현재 연결에 대 한 트랜잭션 격리 수준을 설정 하는 32 비트 비트 마스크입니다. 응용 프로그램에서 호출 해야 합니다 **SQLEndTran** 커밋하거나 호출 하기 전에 연결에서 열려 있는 모든 트랜잭션을 롤백합니다 **SQLSetConnectAttr** 이 옵션을 사용 하 여 합니다.<br /><br /> 유효한 값은 *ValuePtr* 를 호출 하 여 확인할 수 있습니다 **SQLGetInfo** 사용 하 여 *정보 항목* SQL_TXN_ISOLATION_OPTIONS 같음.<br /><br /> 트랜잭션 격리 수준에 대 한 참조 SQL_DEFAULT_TXN_ISOLATION 정보 형식에 대 한 설명은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 하 고 [트랜잭션 격리 수준](../../../odbc/reference/develop-app/transaction-isolation-levels.md)합니다.|  
  
 [설명자가 응용 프로그램 설명자를 하지 설명자를 구현 하는 경우에 1] 이러한 함수를 비동기적으로 호출할 수 있습니다.  
  
## <a name="code-example"></a>코드 예  
 참조 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|연결 특성의 설정을 반환합니다.|[SQLGetConnectAttr 함수](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
