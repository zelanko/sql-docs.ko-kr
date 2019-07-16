---
title: SQLConnect 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConnect
helpviewer_keywords:
- SQLConnect function [ODBC]
ms.assetid: 59075e46-a0ca-47bf-972a-367b08bb518d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b1c0b20fed0e6c15fef76b1bcbebc98edd37cfbc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121458"
---
# <a name="sqlconnect-function"></a>SQLConnect 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLConnect** 드라이버 및 데이터 원본에 대 한 연결을 설정 합니다. 연결 핸들의 상태, 트랜잭션 상태 및 오류 정보를 포함 하 여 데이터 원본에 연결 하는 방법에 대 한 모든 정보는 저장소를 참조 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLConnect(  
     SQLHDBC        ConnectionHandle,  
     SQLCHAR *      ServerName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      UserName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      Authentication,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>인수  
 *ConnectionHandle*  
 [Input] 연결 핸들입니다.  
  
 *데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면*  
 [입력] 데이터 원본 이름입니다. 데이터는 프로그램과 동일한 컴퓨터 또는 네트워크에서 다른 컴퓨터에 있을 수 있습니다. 응용 프로그램에서 데이터 소스를 선택 하는 방법에 대 한 자세한 내용은 [데이터 원본 또는 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)합니다.  
  
 *NameLength1*  
 [입력] 길이 **ServerName* 문자에서입니다.  
  
 *UserName*  
 [입력] 사용자 식별자입니다.  
  
 *NameLength2*  
 [입력] 길이 **UserName* 문자에서입니다.  
  
 *인증*  
 [입력] 인증 문자열 (일반적으로 암호)입니다.  
  
 *NameLength3*  
 [입력] 길이 **인증* 문자에서입니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE, 또는 SQL_STILL_EXECUTING 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLConnect** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* SQL_의 HANDLE_DBC와 *처리할* 의 *ConnectionHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLConnect** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S02|옵션 값이 변경 됨|드라이버의 지정된 된 값을 지원 하지 않았습니다 합니다 *ValuePtr* 에서 인수 **SQLSetConnectAttr** 유사한 값을 대체 합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08001|클라이언트를 연결할 수 없습니다.|드라이버는 데이터 원본과 연결을 설정할 수 없습니다.|  
|08002|연결 이름 사용|(DM) 지정 된 *ConnectionHandle* 데이터 원본에 연결 및 연결 된 열려 또는 사용자가 검색 하 고 연결에 대 한 설정에 이미 사용 된 했습니다.|  
|08004|서버 연결을 거부 했습니다.|데이터 원본 연결의 설정 구현 시 정의 된 이유로 인해 거부 합니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 연결을 시도 된 드라이버는 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|28000|잘못 된 권한 부여 사양|인수에 지정 된 값 *사용자 이름* 또는 인수에 지정 된 값 *인증* 데이터 원본에 의해 정의 된 제한을 위반 합니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|(DM)의 드라이버 관리자 지원 함수 완료 또는 실행 하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *ConnectionHandle*합니다. **SQLConnect** 함수가 호출 되 고 실행을 완료 하기 전에 [SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md) 에서 호출 된 합니다 *ConnectionHandle*, 및 다음**SQLConnect** 함수에서 다시 호출 된는 *ConnectionHandle*합니다.<br /><br /> 또는 **SQLConnect** 함수가 호출 되 고 실행을 완료 하기 전에 **SQLCancelHandle** 에서 호출한 합니다 *ConnectionHandle* 의 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *ConnectionHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|인수에 대 한 지정 된 값 (DM) *NameLength1*를 *NameLength2*, 또는 *NameLength3* 0 보다 작지만 같지 않음 SQL_NTS 되었습니다.<br /><br /> 인수에 대 한 지정 된 값 (DM) *NameLength1* 데이터 원본 이름에 대 한 최대 길이 초과 합니다.|  
|HYT00|제한 시간이 만료되었습니다.|쿼리 제한 시간을 완료 하는 데이터 원본에 연결 되기 전에 만료 되었습니다. 시간 제한 기간을 통해 설정 됩니다 **SQLSetConnectAttr**을 SQL_ATTR_LOGIN_TIMEOUT입니다.|  
|HY114|드라이버는 연결 수준 비동기 함수 실행을 지원 하지 않습니다.|(DM) 응용 프로그램 연결 핸들에 연결 하기 전에 비동기 작업을 사용할 수 있습니다. 그러나 드라이버는 연결 핸들에 비동기 작업을 지원 하지 않습니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 데이터 원본 이름으로 지정 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM002|데이터 원본을 찾을 수 없습니다 및 없습니다 지정 하지 않았습니다.|(DM) 데이터 원본 이름 인수에서 지정한 *ServerName* 시스템 정보를 찾을 수 없습니다도 기본 드라이버 사양 없었습니다.|  
|IM003|지정 된 드라이버에 연결 되어 있지|데이터에서 (DM) 드라이버가 나열 시스템 정보에서 소스 사양 찾을 수 없거나 다른 이유로 연결 되지 못했습니다.|  
|IM004|SQL_HANDLE_ENV에서 드라이버의 SQLAllocHandle이 실패 했습니다.|(DM) 하는 동안 **SQLConnect**, 드라이버 관리자가 드라이버의 호출 **SQLAllocHandle** 함수를 *HandleType* SQL_HANDLE_ENV 및 드라이버에서 오류를 반환 합니다.|  
|IM005|SQL_HANDLE_DBC에서 드라이버의 SQLAllocHandle이 실패 했습니다.|(DM) 하는 동안 **SQLConnect**, 드라이버 관리자가 드라이버의 호출 **SQLAllocHandle** 함수를 *HandleType* SQL_HANDLE_DBC 및 드라이버에서 오류를 반환 합니다.|  
|IM006|드라이버의 SQLSetConnectAttr 실패|하는 동안 **SQLConnect**, 드라이버 관리자가 드라이버의 호출 **SQLSetConnectAttr** 함수 및 드라이버에서 오류를 반환 합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|IM009|변환 DLL에 연결할 수 없습니다.|드라이버 변환 데이터 원본에 대해 지정 된 DLL에 연결할 수 없습니다.|  
|IM010|데이터 원본 이름이 너무 깁니다.|(DM)  *\*ServerName* SQL_MAX_DSN_LENGTH 자를 초과 합니다.|  
|IM014|지정 된 DSN은 드라이버와 응용 프로그램 간 아키텍처 불일치를 포함합니다.|64 비트 드라이버를;에 연결 하는 DSN을 사용 하 여 (DM) 32 비트 응용 프로그램 또는 그 반대의 경우도 마찬가지입니다.|  
|IM015|드라이버의 SQLConnect SQL_HANDLE_DBC_INFO_HANDLE에 실패 했습니다.|SQL_ERROR를 반환 하는 드라이버를 드라이버 관리자에서 응용 프로그램에 SQL_ERROR를 반환 하 고 연결이 실패 합니다.<br /><br /> SQL_HANDLE_DBC_INFO_TOKEN에 대 한 자세한 내용은 참조 하세요. [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)합니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
|S1118|드라이버 비동기 알림을 지원 하지 않습니다.|드라이버는 비동기 알림을 지원 하지 않습니다, SQL_ATTR_ASYNC_DBC_EVENT 또는 SQL_ATTR_ASYNC_DBC_RETCODE_PTR 설정할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램에서 한 이유에 대 한 자세한 내용은 다음을 사용 합니다. **SQLConnect**를 참조 하십시오 [SQLConnect로 연결](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)합니다.  
  
 응용 프로그램 함수를 호출할 때까지 드라이버에 드라이버 관리자 연결 되지 않습니다 (**SQLConnect**를 **SQLDriverConnect**, 또는 **SQLBrowseConnect**)에 연결 하는 드라이버입니다. 그 전 까지는 드라이버 관리자는 자체 핸들을 사용 하 여 작동 하 고 연결 정보를 관리 합니다. 연결 함수를 호출 하는 응용 프로그램, 드라이버 관리자 드라이버를 지정 된 현재 연결할 여부를 확인 *ConnectionHandle*:  
  
-   드라이버 관리자 연결 호출 드라이버를 드라이버에 연결 되어 있지 않으면, **SQLAllocHandle** 사용 하 여를 *HandleType* SQL_HANDLE_ENV의 **SQLAllocHandle** 으로 *HandleType* SQL_HANDLE_DBC의 **SQLSetConnectAttr** (응용 프로그램 지정 된 경우 연결 특성) 및 드라이버에서 연결 함수입니다. 드라이버 관리자 SQLSTATE IM006를 반환 합니다. (운전 **SQLSetConnectOption** 실패) 및 드라이버에 대 한 오류를 반환 하는 경우 연결 함수에 대 한 SQL_SUCCESS_WITH_INFO **SQLSetConnectAttr**. 자세한 내용은 [데이터 원본 또는 드라이버에 연결할](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)합니다.  
  
-   지정된 된 드라이버를 이미 연결 되어 있으면 합니다 *ConnectionHandle*, 드라이버 관리자는 드라이버에만 연결 함수를 호출 합니다. 이 경우 드라이버는의 모든 연결에 대 한 특성 있는지 확인 해야 합니다 *ConnectionHandle* 현재 해당 설정을 유지 합니다.  
  
-   드라이버 관리자를 호출 하는 다른 드라이버에 연결할 경우 **SQLFreeHandle** 사용 하 여를 *HandleType* SQL_HANDLE_DBC의 한 없는 다른 드라이버를 해당 환경에 연결할 경우 호출 **SQLFreeHandle** 사용 하 여는 *HandleType* SQL_HANDLE_ENV 연결 된 드라이버에서의 다음 해당 드라이버 연결을 끊습니다. 그런 다음 드라이버에 연결 되지 않은 경우와 동일한 작업을 수행 합니다.  
  
 그런 다음 드라이버는 핸들을 할당 하 고 자체를 초기화 합니다.  
  
 응용 프로그램을 호출할 때 **SQLDisconnect**, 드라이버 관리자 호출 **SQLDisconnect** 드라이버에서입니다. 그러나 드라이버를 끊지 않습니다. 그러면 드라이버 반복적으로 연결 하 고 데이터 원본에서 분리 하는 응용 프로그램에 대 한 메모리에 유지 됩니다. 응용 프로그램을 호출할 때 **SQLFreeHandle** 사용 하 여를 *HandleType* SQL_HANDLE_DBC의 드라이버 관리자는 다음과 같이 호출 됩니다. **SQLFreeHandle** 사용 하 여를 *HandleType*  SQL_HANDLE_DBC의 차례로 **SQLFreeHandle** 사용 하 여를 *HandleType* 드라이버에서 SQL_HANDLE_ENV의 다음 드라이버 연결을 끊습니다.  
  
 ODBC 응용 프로그램이 둘 이상의 연결을 설정할 수 있습니다.  
  
## <a name="driver-manager-guidelines"></a>드라이버 관리자 지침  
 내용을 **ServerName* 드라이버 관리자와 드라이버를 함께 하는 방법을 데이터 원본에 대 한 연결 설정에 영향을 줍니다.  
  
-   하는 경우 \* *ServerName* 에 유효한 데이터 원본 이름이 포함 된 드라이버 관리자가 시스템 정보에 해당 하는 데이터 원본 설정을 찾고 관련된 드라이버에 연결 합니다. 드라이버 관리자는 각 전달 **SQLConnect** 드라이버에 대 한 인수입니다.  
  
-   데이터 원본 이름을 찾을 수 없는 경우 또는 *ServerName* 가 null 포인터인 경우 드라이버 관리자가 기본 데이터 원본 사양을 찾아 관련된 드라이버에 연결 합니다. 드라이버를 드라이버 관리자를 전달 합니다 *사용자 이름* 및 *인증* 수정 되지 않은 인수 및에 대 한 "기본"는 *ServerName* 인수입니다.  
  
-   경우는 *ServerName* 인수는 "DEFAULT", 드라이버 관리자가 기본 데이터 원본 사양을 찾아 관련된 드라이버에 연결 합니다. 드라이버 관리자는 각 전달 **SQLConnect** 드라이버에 대 한 인수입니다.  
  
-   데이터 원본 이름을 찾을 수 없는 경우 또는 *ServerName* null 포인터 및 데이터 원본 사양 존재 하지 않는 기본 이면 드라이버 관리자 SQLSTATE IM002 인 sql_error가 반환 (데이터 원본 이름을 찾을 수 없습니다 및 기본값 없음 드라이버 지정)입니다.  
  
 드라이버 관리자에 의해에 연결 되 면 드라이버 시스템 정보에는 해당 데이터 원본 사양 찾을 업데이트 하 고 사양에서 드라이버 관련 정보를 사용 하 여 해당 집합이 필요한 연결 정보를 완료할 수 있습니다.  
  
 데이터 원본에 대 한 시스템 정보에는 기본 변환 라이브러리를 지정 하는 경우 드라이버를 연결 합니다. 다른 변환 라이브러리를 호출 하 여 연결할 수 있습니다 **SQLSetConnectAttr** SQL_ATTR_TRANSLATE_LIB 특성을 사용 합니다. 변환 옵션을 호출 하 여 지정할 수 있습니다 **SQLSetConnectAttr** SQL_ATTR_TRANSLATE_OPTION 특성을 사용 합니다.  
  
 드라이버에서 지 원하는 경우 **SQLConnect**, 드라이버 키워드 부분 드라이버에 대 한 시스템 정보를 포함 해야 합니다 **ConnectFunctions** 첫 번째 문자를 사용 하 여 키워드 "Y."로 설정  
  
### <a name="connection-pooling"></a>연결 풀링  
 연결 풀링을 통해 응용 프로그램을을 이미 만든 연결을 다시 사용할 수 있습니다. 연결 풀링을 사용할 때와 **SQLConnect** 라고, 드라이버 관리자 연결 풀링에 대해 지정 된 환경에서 연결 풀의 일부인 연결을 사용 하 여 연결 하려고 합니다. 이 환경에는 풀에서 연결을 사용 하는 모든 응용 프로그램에서 사용 되는 공유 환경이입니다.  
  
 연결 풀링을 사용 하는 환경 호출에 의해 할당 되었습니다 전에 **SQLSetEnvAttr** SQL_CP_ONE_PER_DRIVER (지정 하는 드라이버 당 하나의 풀 최대) 또는 SQL_CP_ONE_PER_HENV SQL_ATTR_CONNECTION_POOLING 설정 하려면 (환경 당 하나의 풀 최대 지정 함). **SQLSetEnvAttr** 사용 하 여이 경우 라고 *EnvironmentHandle* 특성 프로세스 수준 특성을 사용 하면 null로 설정 합니다. SQL_ATTR_CONNECTION_POOLING SQL_CP_OFF로 설정 된 경우 연결 풀링 비활성화 됩니다.  
  
 연결 풀링을 활성화 되 면 **SQLAllocHandle** 사용 하 여를 *HandleType* SQL_HANDLE_ENV의 environment 할당할 호출 됩니다. 이 호출에 의해 할당 되는 환경에서는 공유 환경 이므로 연결 풀링이 사용 되었습니다. 그러나 사용 되는 환경을 일까 지 결정 되지 않습니다 **SQLAllocHandle** 사용 하 여를 *HandleType* SQL_HANDLE_DBC의 호출 됩니다.  
  
 **SQLAllocHandle** 사용 하 여는 *HandleType* SQL_HANDLE_DBC의 라고는 연결을 할당 합니다. 드라이버 관리자는 응용 프로그램이 설정한 환경 특성과 일치 하는 기존 공유 환경 찾으려고 합니다. 이러한 환경이 없고 있으면 암시적으로 만들어집니다 하나 *공유 환경*합니다. 일치 하는 공유 환경 있으면 환경 핸들을 응용 프로그램에 반환 됩니다 하 고 해당 참조 개수가 증가 합니다.  
  
 그러나 사용 되는 연결 될 때까지 결정 되지 않습니다 **SQLConnect** 라고 합니다. 이 시점에서 드라이버 관리자는 응용 프로그램에서 요청 된 조건과 일치 하는 연결 풀에서 기존 연결을 찾으려고 합니다. 이러한 조건에 대 한 호출에서 요청 된 연결 옵션에 포함 **SQLConnect** (값을 *ServerName*를 *UserName*, 및  *인증* 키워드) 이후 연결 특성을 설정 하 고 **SQLAllocHandle** 사용 하 여를 *HandleType* SQL_HANDLE_DBC의 호출 되었습니다. 드라이버 관리자는 해당 연결 키워드 및 풀에서 연결의 특성에 대해 이러한 조건을 확인합니다. 일치 하는 항목이 있으면 풀에서 연결이 됩니다. 일치 하는 항목이 없으면 새 연결이 만들어집니다.  
  
 SQL_ATTR_CP_MATCH 환경 특성 SQL_CP_STRICT_MATCH로 일치 하는 데 사용할 풀에서 연결에 대 한 정확한 이어야 합니다. SQL_ATTR_CP_MATCH 환경 특성 SQL_CP_RELAXED_MATCH로 연결에 대 한 호출의 옵션 **SQLConnect** 해야 일치 하지만 일부 연결 특성을 일치 해야 합니다.  
  
 다음 규칙이 적용 됩니다 연결 특성을 하기 전에 응용 프로그램에서 설정한 대로 **SQLConnect** 호출 되 면 연결 풀의 연결 특성을 일치 하지 않습니다.  
  
-   경우 연결을 시작 하기 전에 연결 특성을 설정 해야 합니다.  
  
     SQL_ATTR_CP_MATCH SQL_CP_STRICT_MATCH 이면 SQL_ATTR_PACKET_SIZE 풀링된 연결의 응용 프로그램에 의해 설정 된 특성에 동일 해야 합니다. 경우 SQL_CP_RELAXED_MATCH, SQL_ATTR_PACKET_SIZE 값 다를 수 있습니다.  
  
     SQL_ATTR_LOGIN_VALUE 값 일치 하는 영향을 주지 않습니다.  
  
-   경우 이전 또는 이후에 연결 되는 연결 특성을 설정할 수 있습니다.  
  
     연결 특성을 응용 프로그램에 의해 설정 되지 않은 되었지만 풀에 연결에서 설정 되며 경우 기본값, 풀링된 연결의 연결 특성을 기본값으로 다시 설정 됩니다 및 일치 하는 선언 됩니다. 기본값이 있으면 풀링된 연결에는 일치 하는 고려 하지 않습니다.  
  
     연결 특성을 응용 프로그램에서 설정 된 풀의 연결에서 설정 되지 않은 하지만 풀에 대 한 연결 특성 응용 프로그램에서 해당 집합에 변경 되 고 일치 하는 선언 됩니다.  
  
     연결 특성을 응용 프로그램에서 설정 되 고도 설정 되었으므로 연결에서 풀에 있지만 값이 다른 응용 프로그램의 연결 특성의 값이 사용 되 고 일치 하는 선언 됩니다.  
  
-   드라이버별 연결 특성의 값이 동일 하지 않은 SQL_ATTR_CP_MATCH SQL_CP_STRICT_MATCH로 설정 된 경우 연결 풀에서 사용 되지 않습니다.  
  
 응용 프로그램을 호출할 때 **SQLDisconnect** 연결을 끊으려면 연결이 연결 풀으로 반환 되 고 다시 사용할 수 있습니다.  
  
### <a name="optimizing-connection-pooling-performance"></a>연결 풀링 성능 최적화  
 분산된 트랜잭션에 관련 된 경우에 사용 하 여 성능 풀링 연결을 최적화할 수 있습니다 **SQL_DTC_TRANSITION_COST**, SQLUINTEGER 비트 마스크입니다. 참조 하는 전이 연결 특성에 0이 아닌 값이 0에서 이동 SQL_ATTR_ENLIST_IN_DTC의 전환 및 그 반대의 경우도 마찬가지입니다. 이동 연결을 분산 트랜잭션에 참여 하지 그 반대로 분산 트랜잭션에 인 리스트 먼 트 합니다. 드라이버에 인 리스트 먼 트 (설정 연결 특성 SQL_ATTR_ENLIST_IN_DTC), 구현 방식에 따라 이러한 전환을 비용이 많이 드는 수 있으며 최상의 성능을 위해 피해 야 합니다.  
  
 다음 비트의 조합을 포함 하는 드라이버에서 반환 되는 값:  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**, 설정, 0이 아닌 전환 0에서 0이 아닌 다른 0이 아닌 값 (다음 해당 트랜잭션에서 이전에 등록 된 연결 인 리스트 먼 트)으로 전환은 보다 훨씬 더 비쌉니다 의미 합니다.  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**, 설정, 의미는 0이 아닌 0 전환 인이 SQL_ATTR_ENLIST_IN_DTC 특성은 이미 0으로 설정 하는 연결을 사용 하 여 보다 훨씬 더 비쌉니다.  
  
 성능과 연결 사용 단점이 있습니다. 드라이버는 하나 이상의 이러한 전환을 비용이 많이 드는 경우, 풀에 더 많은 연결을 유지 하 여 드라이버 관리자의 연결 풀러에서이에 응답 합니다. 풀에서 연결의 일부는 비트랜잭션 사용에 대 한 기본 하 고 일부는 트랜잭션 사용에 대 한 기본 키를 누릅니다. 그러나 이러한 전환을 비용이 별로 들지 않습니다 드라이버 나타내면 연결 수를 줄입니다 사용할 수 있습니다, 비트랜잭션 사이의 트랜잭션 사용 하 여 교대로 반복 되는 아마도.  
  
 SQL_ATTR_ENLIST_IN_DTC를 지원 하지 않는 드라이버 SQL_DTC_TRANSITION_COST 지원 필요가 없습니다. SQL_ATTR_ENLIST_IN_DTC 하지만 하지 SQL_DTC_TRANSITION_COST를 지 원하는 드라이버를 드라이버 (비트 집합 제외)이이 값에 0을 반환 하는 경우에 따라 비용이 전환 되지 가정 합니다.  
  
 하지만 SQL_DTC_TRANSITION_COST ODBC 3.5에는 ODBC 2에서 도입 되었습니다. *x* 드라이버도 지 원하는 드라이버 관리자가 드라이버 버전에 관계 없이이 정보를 쿼리 하기 때문에 있습니다.  
  
### <a name="code-example"></a>코드 예  
 다음 예제에서는 응용 프로그램 할당 환경 및 연결 핸들입니다. 사용자 ID JohnS를 사용 하 여 SalesOrders 데이터 원본과 Sesame 암호에 연결 하 고 데이터를 처리 합니다. 데이터를 처리 완료 될 때 데이터 원본에서 연결 해제 하 고 핸들을 해제 합니다.  
  
```cpp  
// SQLConnect_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
  
   SQLCHAR * OutConnStr = (SQLCHAR * )malloc(255);  
   SQLSMALLINT * OutConnStrLen = (SQLSMALLINT *)malloc(255);  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLCHAR*) "NorthWind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
### <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|검색 및 데이터 원본에 연결 하는 데 필요한 값을 열거|[SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|데이터 원본에서 연결 끊기|[SQLDisconnect 함수](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|연결 문자열 또는 대화 상자를 사용 하 여 데이터 원본에 연결|[SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|연결 특성의 설정을 반환합니다.|[SQLGetConnectAttr 함수](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|연결 특성을 설정합니다.|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
