---
title: "SQLConnect 함수 | Microsoft Docs"
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
- SQLConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConnect
helpviewer_keywords:
- SQLConnect function [ODBC]
ms.assetid: 59075e46-a0ca-47bf-972a-367b08bb518d
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f3954538b63739fe19435aeb5cd30449edbc9d24
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlconnect-function"></a>SQLConnect 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLConnect** 드라이버 및 데이터 원본에 대 한 연결을 설정 합니다. 연결 핸들의 상태, 트랜잭션 상태 및 오류 정보를 포함 하 여 데이터 원본에 연결 하는 방법에 대 한 모든 정보 저장소를 참조 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
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
 [입력] 연결 핸들입니다.  
  
 *데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면*  
 [입력] 데이터 원본 이름입니다. 데이터에는 프로그램과 동일한 컴퓨터에서 또는 네트워크의 임의 위치에서 다른 컴퓨터에 있을 수 있습니다. 응용 프로그램에서 데이터 소스를 선택 하는 방법에 대 한 정보를 참조 하십시오. [데이터 원본이 나 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)합니다.  
  
 *NameLength1*  
 [입력] 길이 **ServerName* 문자 수입니다.  
  
 *UserName*  
 [입력] 사용자 식별자입니다.  
  
 *NameLength2*  
 [입력] 길이 **UserName* 문자 수입니다.  
  
 *인증*  
 [입력] 인증 문자열 (일반적으로 암호)입니다.  
  
 *NameLength3*  
 [입력] 길이 **인증* 문자 수입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE, 또는 SQL_STILL_EXECUTING 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLConnect** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* SQL_의 HANDLE_DBC 및 *처리* 의 *ConnectionHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLConnect** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01 S 02|옵션 값이 변경 됨|드라이버의 지정된 된 값을 지원 하지 않았습니다 고 *ValuePtr* 인수에 **SQLSetConnectAttr** 유사한 값을 대체 합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08001|클라이언트 연결을 설정할 수 없습니다.|드라이버는 데이터 원본과 연결을 설정할 수 없습니다.|  
|08002|사용 중인 연결 이름|(DM) 지정 된 *ConnectionHandle* 아직 열려 데이터 원본과 연결 및 연결 된 연결에 대 한 사용자가 검색 또는 설정 하는 데 이미 사용 되어 있었습니다.|  
|08004|서버 연결을 거부 했습니다.|데이터 원본 구현에서 정의 된 이유로 연결 만들기를 거부 했습니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버를 드라이버 연결 하려고 데이터 소스 간의 통신 링크 하지 못했습니다.|  
|28000|잘못 된 권한 지정|인수에 대해 지정 된 값 *UserName* 인수에 대해 지정 된 값 또는 *인증* 데이터 원본에 정의 된 제한을 위반 합니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에 * \*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버 관리자에서 (DM) 함수는 완료 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *ConnectionHandle*합니다. **SQLConnect** 함수를 호출 하 고, 실행을 완료 하기 전에 [SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md) 에서 호출 된는 *ConnectionHandle*, 및 다음 **SQLConnect** 에서 다시 호출 된 함수는 *ConnectionHandle*합니다.<br /><br /> 또는 **SQLConnect** 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancelHandle** 에서 호출 된는 *ConnectionHandle* 의 서로 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *ConnectionHandle* 호출 되었을 때 계속 실행 하 고 있습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|인수에 대해 지정 된 값 (DM) *NameLength1*, *NameLength2*, 또는 *NameLength3* 같지 않음 SQL_NTS 하지만 0 보다 작습니다.<br /><br /> 인수에 대해 지정 된 값 (DM) *NameLength1* 데이터 원본 이름에 대 한 최대 길이 초과 합니다.|  
|HYT00|제한 시간이 만료되었습니다.|완료 된 데이터 원본에 연결 하기 전에 쿼리 제한 시간 만료 되었습니다. 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT 합니다.|  
|HY114|드라이버는 연결 수준 비동기 함수 실행을 지원 하지 않습니다.|(DM) 응용 프로그램 연결 핸들에 연결 하기 전에 비동기 작업을 사용할 수 있습니다. 그러나, 드라이버는 연결 핸들에 대 한 비동기 작업을 지원 하지 않습니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 데이터 원본 이름으로 지정 된 드라이버의 기능을 지원 하지 않습니다.|  
|IM002|기본 드라이버를 지정 하 고 데이터 원본을 찾을 수 없습니다|DM ()는 데이터 소스는 인수에 지정 된 이름 *ServerName* 시스템 정보에서 찾을 수 없습니다도 기본 드라이버 사양 없었습니다.|  
|IM003|지정 된 드라이버에 연결 되어 있지|(DM) 드라이버는 데이터에 나열 된 시스템 정보에 소스 사양을 찾을 수 없거나 다른 이유로 연결 되지 못했습니다.|  
|IM004|드라이버의 SQLAllocHandle SQL_HANDLE_ENV에 실패 했습니다.|(DM) 하는 동안 **SQLConnect**, 드라이버 관리자를 호출 했지만 드라이버의 **SQLAllocHandle** 작동 한 *HandleType* SQL_HANDLE_ENV와 드라이버의 오류를 반환 합니다.|  
|IM005|드라이버의 SQLAllocHandle sql_handle_dbc 라는에 실패 했습니다.|(DM) 중 **SQLConnect**, 드라이버 관리자를 호출 했지만 드라이버의 **SQLAllocHandle** 작동 한 *HandleType* sql_handle_dbc 라는 드라이버의 오류를 반환 합니다.|  
|IM006|드라이버의 SQLSetConnectAttr 못했습니다.|동안 **SQLConnect**, 드라이버 관리자를 호출 했지만 드라이버의 **SQLSetConnectAttr** 함수 및 드라이버에서 오류를 반환 합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|IM009|변환 DLL에 연결할 수 없습니다.|드라이버 변환 데이터 원본에 대해 지정 된 DLL에 연결할 수 없습니다.|  
|IM010|데이터 원본 이름이 너무 깁니다.|(DM) * \*ServerName* SQL_MAX_DSN_LENGTH 자를 초과 합니다.|  
|IM014|지정된 된 DSN 드라이버 및 응용 프로그램 사이 아키텍처 불일치가 포함|64 비트 드라이버;에 연결 하는 DSN을 사용 하 여 (DM) 32 비트 응용 프로그램 또는 그 반대의 경우도 마찬가지입니다.|  
|IM015|드라이버의 SQLConnect SQL_HANDLE_DBC_INFO_HANDLE에 실패 했습니다.|드라이버가 SQL_ERROR를 반환 하면 드라이버 관리자 응용 프로그램에 sql_error가 반환 하 고 연결이 실패 합니다.<br /><br /> SQL_HANDLE_DBC_INFO_TOKEN에 대 한 자세한 내용은 참조 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)합니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
|S1118|드라이버는 비동기 알림을 지원 하지 않습니다.|드라이버는 비동기 알림을 지원 하지 않습니다, SQL_ATTR_ASYNC_DBC_EVENT 또는 SQL_ATTR_ASYNC_DBC_RETCODE_PTR 설정할 수 없습니다.|  
  
## <a name="comments"></a>설명  
 응용 프로그램에서 이유에 대 한 내용은 다음을 사용 합니다. **SQLConnect**, 참조 [SQLConnect를 사용 하 여 연결](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)합니다.  
  
 드라이버 관리자는 응용 프로그램에는 함수 호출 될 때까지 드라이버에 연결 되지 않습니다 (**SQLConnect**, **SQLDriverConnect**, 또는 **SQLBrowseConnect**)에 연결 하는 드라이버입니다. 따라서 그 시점 까지는 드라이버 관리자는 자체 핸들을 사용 하 고 연결 정보를 관리 합니다. 연결 함수를 호출 하는 응용 프로그램, 드라이버 관리자 확인 여부를 드라이버에 현재 연결 되어 지정 된 *ConnectionHandle*:  
  
-   드라이버 관리자는 드라이버 및 호출에 연결 하는 드라이버에 연결 되어 있지 않으면, **SQLAllocHandle** 와 *HandleType* SQL_HANDLE_ENV의 **SQLAllocHandle** 으로 *HandleType* sql_handle_dbc 라는의 **SQLSetConnectAttr** (하는 경우 응용 프로그램이 지정 된 모든 연결 특성), 및 드라이버에서 연결 함수입니다. 드라이버 관리자 SQLSTATE IM006 반환 (드라이버의 **SQLSetConnectOption** 실패) 및 드라이버에 대 한 오류를 반환 하는 경우 연결 함수에 대 한 SQL_SUCCESS_WITH_INFO **SQLSetConnectAttr**합니다. 자세한 내용은 참조 [데이터 원본이 나 드라이버에 연결](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)합니다.  
  
-   지정된 된 드라이버에서 이미 연결 되어 있으면는 *ConnectionHandle*, 드라이버 관리자는 드라이버에만 연결 함수를 호출 합니다. 이 경우 드라이버는의 모든 연결에 대 한 특성 있는지 확인 해야는 *ConnectionHandle* 의 현재 설정은 유지 관리 합니다.  
  
-   드라이버 관리자를 호출 하는 다른 드라이버를 연결할 경우 **SQLFreeHandle** 와 *HandleType* sql_handle_dbc 라는의 다른 드라이버가 없는 해당 환경에서에 연결 된 경우 호출 됩니다 **SQLFreeHandle** 와 *HandleType* SQL_HANDLE_ENV 연결된 드라이버에의 한 다음 해당 드라이버 연결이 끊어집니다. 다음 드라이버에 연결 되지 않은 경우와 동일한 작업을 수행 합니다.  
  
 그런 다음 드라이버 핸들을 할당 하 고 자체를 초기화 합니다.  
  
 응용 프로그램 호출 하는 경우 **SQLDisconnect**, 드라이버 관리자를 호출 하 여 **SQLDisconnect** 드라이버에서입니다. 그러나, 드라이버를 끊어지지 않습니다. 그러면 드라이버 반복 해 서 연결 하 고 데이터 원본에서 분리 하는 응용 프로그램에 대 한 메모리에 유지 됩니다. 응용 프로그램 호출 하는 경우 **SQLFreeHandle** 와 *HandleType* 드라이버 관리자를 호출 sql_handle_dbc 라는의 **SQLFreeHandle** 와 *HandleType * sql_handle_dbc 라는의 차례로 **SQLFreeHandle** 와 *HandleType* SQL_HANDLE_ENV 드라이버에서의 다음 드라이버 연결을 끊습니다.  
  
 ODBC 응용 프로그램이 둘 이상의 연결을 설정할 수 있습니다.  
  
## <a name="driver-manager-guidelines"></a>드라이버 관리자 지침  
 내용을 **ServerName* 드라이버 관리자와 드라이버 연동 방법을 데이터 원본에 연결을 설정할 수에 영향을 줍니다.  
  
-   경우 \* *ServerName* 유효한 데이터 원본 이름이 포함 된 드라이버 관리자가 시스템 정보에 해당 하는 데이터 원본 설정을 찾아 관련된 드라이버에 연결 합니다. 드라이버 관리자는 각각 전달 **SQLConnect** 드라이버에 대 한 인수입니다.  
  
-   데이터 원본 이름을 찾을 수 없는 경우 또는 *ServerName* 가 null 포인터 이면 드라이버 관리자가 지정 된 기본 데이터 소스를 찾아 관련된 드라이버에 연결 합니다. 드라이버 관리자 드라이버에 전달는 *UserName* 및 *인증* 수정 되지 않은 인수 및에 대 한 "DEFAULT"는 *ServerName* 인수입니다.  
  
-   경우는 *ServerName* 인수는 "DEFAULT", 드라이버 관리자가 지정 된 기본 데이터 소스를 찾아 관련된 드라이버에 연결 합니다. 드라이버 관리자는 각각 전달 **SQLConnect** 드라이버에 대 한 인수입니다.  
  
-   데이터 원본 이름을 찾을 수 없는 경우 또는 *ServerName* null 포인터 이며 데이터 원본 지정 존재 하지 않는 기본, 드라이버 관리자 SQLSTATE IM002 인 sql_error가 반환 (데이터 원본 이름을 찾을 수 없습니다 및 기본값 없음 지정 된 드라이버)입니다.  
  
 드라이버 관리자에서에 연결 되 면 후 드라이버 시스템 정보에는 해당 하는 데이터 원본 설정을 찾을 수 있습니다 및 사양과에서 드라이버 관련 정보를 사용 하 여 필요한 연결 정보 집합이 완료할 합니다.  
  
 데이터 원본에 대 한 시스템 정보에는 기본 변환 라이브러리를 지정 하는 경우 드라이버에 연결 합니다. 다른 변환 라이브러리를 호출 하 여 연결할 수 **SQLSetConnectAttr** SQL_ATTR_TRANSLATE_LIB 특성을 사용 합니다. 번역 옵션을 호출 하 여 지정할 수 있습니다 **SQLSetConnectAttr** SQL_ATTR_TRANSLATE_OPTION 특성을 사용 합니다.  
  
 드라이버에서 지 원하는 경우 **SQLConnect**, 드라이버 키워드 섹션 드라이버에 대 한 시스템 정보를 포함 해야 합니다는 **ConnectFunctions** 키워드의 첫 번째 문자로 "Y"로 설정  
  
### <a name="connection-pooling"></a>연결 풀링  
 연결 풀링은 응용을 프로그램을 이미 만들어져 있는 연결을 다시 사용할 수 있습니다. 연결 풀링을 사용할 때와 **SQLConnect** 호출 드라이버 관리자 연결 풀링에 대해 지정 된 환경에서 연결 풀의 일부인 연결을 사용 하 여 연결 하려고 합니다. 이 환경은 연결 풀에서 사용 하는 모든 응용 프로그램에서 사용 되는 공유 환경이입니다.  
  
 연결 풀링을 사용 하는 환경을 호출 하 여 할당 된 전에 **SQLSetEnvAttr** SQL_ATTR_CONNECTION_POOLING SQL_CP_ONE_PER_DRIVER (지정 하는 드라이버 당 하나의 풀의 최대) 또는 SQL_CP_ONE_PER_HENV로 설정 (단일 풀 환경당 최대 지정 함). **SQLSetEnvAttr** 이 예에서 사용 하 여 호출 *EnvironmentHandle* 프로세스 수준 특성 특성에는 null로 설정 합니다. SQL_ATTR_CONNECTION_POOLING SQL_CP_OFF로 설정 되 면 연결 풀링이 사용 되지 않습니다.  
  
 연결 풀링을 활성화 되어 있는 후 **SQLAllocHandle** 와 *HandleType* SQL_HANDLE_ENV의 환경에 할당 하기 위해 호출 합니다. 연결 풀링을 설정 되어 있으므로이 호출으로 할당 된 환경은 공유 환경. 그러나 사용 되는 환경까지 확인 되지 않으면 **SQLAllocHandle** 와 *HandleType* sql_handle_dbc 라는의 호출 됩니다.  
  
 **SQLAllocHandle** 와 *HandleType* sql_handle_dbc 라는의 연결을 할당 하기 위해 호출 합니다. 드라이버 관리자는 기존 응용 프로그램에서 설정한 환경 특성을 일치 하는 공유 환경 찾으려고 합니다. 이러한 환경이 있는 경우 암시적으로 만들어집니다 하나 *공유 환경*합니다. 일치 하는 공유 환경 발견 되 면 환경 핸들이 응용 프로그램에 반환 되 고 참조 개수가 증가 합니다.  
  
 그러나 사용 되는 연결 될 때까지 확인 되지 않으면 **SQLConnect** 호출 됩니다. 이 시점에서 드라이버 관리자는 응용 프로그램에서 요청한 조건과 일치 하는 연결 풀에서 기존 연결을 찾을 하려고 시도 합니다. 이러한 조건에 대 한 호출에서 요청 된 연결 옵션에 포함 **SQLConnect** (의 값은 *ServerName*, *UserName*, 및 * 인증* 키워드) 이후 연결 특성을 설정 하 고 **SQLAllocHandle** 와 *HandleType* sql_handle_dbc 라는의 호출 되었습니다. 드라이버 관리자는 해당 연결 키워드 및 풀에서 연결의 특성에 대해 이러한 조건을 확인합니다. 일치 하는 항목이 없는 경우 풀에서 연결 사용 됩니다. 일치 하는 항목이 새 연결이 생성 됩니다.  
  
 SQL_CP_STRICT_MATCH를 SQL_ATTR_CP_MATCH 환경 특성을 설정 하는 경우 일치 하는 사용할 풀에서 연결에 대 한 정확 하 게 해야 합니다. SQL_ATTR_CP_MATCH 환경 특성이 SQL_CP_RELAXED_MATCH로 설정 된, 연결 옵션에 대 한 호출을 **SQLConnect** 해야 일치 하지만 일부 연결 특성 일치 해야 합니다.  
  
 다음 규칙 전에 응용 프로그램에서 설정한 대로 때 연결 특성을 적용 됩니다 **SQLConnect** 호출 되 면 풀에서 연결의 연결 특성을 일치 하지 않습니다.  
  
-   연결 특성을 먼저 설정 해야 하는 경우 연결이 구성 됩니다.  
  
     SQL_ATTR_CP_MATCH SQL_CP_STRICT_MATCH 이면 SQL_ATTR_PACKET_SIZE 풀링된 연결에는 응용 프로그램에 의해 설정 된 특성에 동일 해야 합니다. 경우 SQL_CP_RELAXED_MATCH, SQL_ATTR_PACKET_SIZE 값은 다 수 있습니다.  
  
     SQL_ATTR_LOGIN_VALUE의 값에 일치 하는 영향을 주지 않습니다.  
  
-   경우 이전 또는 연결 된 후에 연결 특성을 설정할 수 있습니다.  
  
     연결 특성 응용 프로그램에 의해 설정 되지 않은 이지만 경우 풀에서 연결에 설정 된 기본값은, 풀링된 연결의 연결 특성을 기본값으로 다시 설정 됩니다와 일치 하는 선언 됩니다. 기본값은 없습니다 이면 풀링된 연결에는 일치 하는 간주 되지 않습니다.  
  
     응용 프로그램으로 설정 된 연결 특성 풀에서 연결에 설정 되지 않은 경우에 풀에 연결 특성 응용 프로그램에서 해당 집합에 변경 되 고 일치 하는 선언 됩니다.  
  
     연결 특성 응용 프로그램에 의해 설정 되 고 또한에 설정한 연결 풀에 있지만 값이 다른 경우 응용 프로그램의 연결 특성의 값 사용 되 고 일치 하는 선언 됩니다.  
  
-   드라이버별 연결 특성의 값이 동일 하지 않은 경우 SQL_ATTR_CP_MATCH SQL_CP_STRICT_MATCH로 설정 된 풀에서 연결이 사용 되지 않습니다.  
  
 응용 프로그램 호출 하는 경우 **SQLDisconnect** 연결을 끊고 연결이 연결 풀으로 반환 되 고 다시 사용할 수 있습니다.  
  
### <a name="optimizing-connection-pooling-performance"></a>연결 풀링 성능 최적화  
 사용 하 여 성능 풀링 연결을 최적화할 수는 분산된 트랜잭션에 관련 된 경우 **SQL_DTC_TRANSITION_COST**, SQLUINTEGER 비트 마스크입니다. 참조의 변화는 연결 특성에 0이 아닌 값이 0에서 이동 SQL_ATTR_ENLIST_IN_DTC 전환 하거나 그 반대로 합니다. 이것은 이동에서 연결을 분산 트랜잭션에 참여 하지 그 반대의 분산 트랜잭션에 인 리스트 먼 트 합니다. 드라이버는 인 리스트 먼 트 (연결 특성을 설정 SQL_ATTR_ENLIST_IN_DTC), 구현 방식에 따라 이러한 전환 성능이 떨어질 수 있습니다 및 따라서 최상의 성능을 위해 피해 야 합니다.  
  
 다음 비트의 조합을 포함 하는 드라이버에서 반환 되는 값:  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**, 설정, 0이 아닌 전환 0에서 0이 아닌 다른 0이 아닌 값 (다음 해당 트랜잭션에서 이전에 등록 된 연결 인 리스트 먼 트)의 전환을 보다 훨씬 더 비쌉니다 것을 의미 합니다.  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**, 설정, 것을 의미는 0이 아니고 0 전환 인이 SQL_ATTR_ENLIST_IN_DTC 특성은 이미 0으로 설정 하는 연결을 사용 하 여 보다 훨씬 더 비쌉니다.  
  
 성능 연결 사용량 적절 한 균형을 대 있습니다. 드라이버 하나 이상의 이러한 전환과 많이 소모 되며 데이터를 나타내는 경우 드라이버 관리자 연결 풀러는 풀에서 더 많은 연결을 유지 하 여이에 응답 합니다. 풀에서 연결 중 일부는 비트랜잭션 사용에 대 한 기본 설정 및 일부 트랜잭션 사용에 대 한 기본 설정 됩니다. 그러나 이러한 전환과 저렴 드라이버 나타내면 연결 수를 줄이기 사용할 수 있습니다, 비트랜잭션 및 트랜잭션 사용 교대로 아마도.  
  
 SQL_ATTR_ENLIST_IN_DTC를 지원 하지 않는 드라이버 SQL_DTC_TRANSITION_COST 지원 하기 위해 필요가 없습니다. SQL_ATTR_ENLIST_IN_DTC 하지만 하지 SQL_DTC_TRANSITION_COST를 지 원하는 드라이버의 변화는 드라이버 (비트 집합 제외)이이 값에 0을 반환 하는 경우에 저렴 가정 합니다.  
  
 하지만 SQL_DTC_TRANSITION_COST ODBC 3.5, ODBC 2에서에서 도입 되었습니다. *x* 드라이버도에서 지 원하는 드라이버 관리자 드라이버 버전에 관계 없이이 정보를 쿼리 하 때문에 있습니다.  
  
### <a name="code-example"></a>코드 예  
 다음 예제에서는 응용 프로그램이 할당 환경 및 연결 핸들입니다. 그런 다음 사용자 ID JohnS 사용 하 여 SalesOrders 데이터 소스 및 Sesame 암호에 연결 하 고 데이터를 처리 합니다. 데이터 처리 완료 될 때 데이터 원본에서 연결 해제 하 고 실행 하 여 핸들을 해제 합니다.  
  
```  
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
|검색 하 고 데이터 원본에 연결 하는 데 필요한 값을 열거|[SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|데이터 원본에서 연결 끊기|[SQLDisconnect 함수](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|연결 문자열 또는 대화 상자를 사용 하 여 데이터 원본에 연결|[SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|연결 특성의 설정은 반환|[SQLGetConnectAttr 함수](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|연결 특성을 설정합니다.|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
