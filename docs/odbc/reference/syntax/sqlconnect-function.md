---
description: SQLConnect 함수
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 714bc6f69a72609ee266effff71f1898d62ec7d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461205"
---
# <a name="sqlconnect-function"></a>SQLConnect 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLConnect** 는 드라이버와 데이터 원본에 대 한 연결을 설정 합니다. 연결 핸들은 상태, 트랜잭션 상태 및 오류 정보를 포함 하 여 데이터 원본에 대 한 연결에 대 한 모든 정보의 저장소를 참조 합니다.  
  
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
 입력 데이터 원본 이름입니다. 데이터는 프로그램과 동일한 컴퓨터 또는 네트워크의 다른 컴퓨터에 있을 수 있습니다. 응용 프로그램에서 데이터 원본을 선택 하는 방법에 대 한 자세한 내용은 [데이터 원본 또는 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)을 참조 하십시오.  
  
 *NameLength1*  
 입력 **ServerName* 의 길이 (문자)입니다.  
  
 *UserName*  
 입력 사용자 식별자입니다.  
  
 *NameLength2*  
 입력 **UserName* 의 길이 (문자)입니다.  
  
 *인증*  
 입력 인증 문자열 (일반적으로 암호)입니다.  
  
 *NameLength3*  
 입력 문자에서 **인증* 의 길이입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE 또는 SQL_STILL_EXECUTING입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLConnect** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_DBC의 *HandleType* 및 *ConnectionHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLConnect** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01 S 02|옵션 값 변경 됨|드라이버가 **SQLSetConnectAttr** 에서 *지정 된 값* 을 지원 하지 않아 유사한 값으로 대체 되었습니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08001|클라이언트에서 연결을 설정할 수 없음|드라이버가 데이터 원본과의 연결을 설정할 수 없습니다.|  
|08002|사용 중인 연결 이름|(DM) 지정한 *ConnectionHandle* 가 이미 데이터 원본과의 연결을 설정 하는 데 사용 되었으며 연결이 열려 있거나 사용자가 연결을 검색 하 고 있습니다.|  
|08004|서버에서 연결을 거부 했습니다.|데이터 소스에서 구현 정의 이유에 대 한 연결 설정을 거부 했습니다.|  
|08S01|통신 연결 오류|드라이버가 연결을 시도 하는 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|28000|잘못 된 권한 부여 사양|인수 *사용자 이름* 또는 인수 *인증* 에 지정 된 값에 지정 된 값이 데이터 원본에 정의 된 제한을 위반 했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. * \* MessageText* 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|(DM) 드라이버 관리자가 함수의 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*ConnectionHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. **SQLConnect** 함수를 호출 하 고 실행을 완료 하기 전에 *ConnectionHandle*에서 [Sqlcancelhandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md) 를 호출한 다음 *ConnectionHandle*에서 **SQLConnect** 함수를 다시 호출 했습니다.<br /><br /> 또는 **SQLConnect** 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *ConnectionHandle* 에 대해 호출 되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *ConnectionHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 인수 *NameLength1*, *NameLength2*또는 *NameLength3* 에 지정 된 값이 0 보다 작지만 SQL_NTS와 같지 않습니다.<br /><br /> (DM) 인수 *NameLength1* 에 지정 된 값이 데이터 원본 이름의 최대 길이를 초과 했습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에 대 한 연결이 완료 되기 전에 쿼리 제한 시간이 만료 되었습니다. 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT을 통해 설정 됩니다.|  
|HY114|드라이버가 연결 수준 비동기 함수 실행을 지원 하지 않습니다.|(DM) 연결을 만들기 전에 응용 프로그램에서 연결 핸들에 대해 비동기 작업을 사용 하도록 설정 했습니다. 그러나 드라이버는 연결 핸들에 대해 비동기 작업을 지원 하지 않습니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) 데이터 원본 이름으로 지정 된 드라이버에서 함수를 지원 하지 않습니다.|  
|IM002|데이터 원본을 찾을 수 없으며 기본 드라이버가 지정 되지 않았습니다.|(DM) 인수 *ServerName* 에 지정 된 데이터 원본 이름이 시스템 정보에 없거나 기본 드라이버 사양이 없습니다.|  
|IM003|지정 된 드라이버를 다음에 연결할 수 없습니다.|(DM) 시스템 정보의 데이터 원본 사양에 나열 된 드라이버를 찾을 수 없거나 다른 이유로 인해 연결할 수 없습니다.|  
|IM004|SQL_HANDLE_ENV에서 드라이버의 SQLAllocHandle 실패|(DM) **SQLConnect**를 사용 하는 동안 드라이버 관리자는 *HandleType* SQL_HANDLE_ENV의 **SQLAllocHandle** 함수를 호출 하 고 드라이버에서 오류를 반환 했습니다.|  
|IM005|SQL_HANDLE_DBC에서 드라이버의 SQLAllocHandle 실패|(DM) **SQLConnect**를 사용 하는 동안 드라이버 관리자는 *HandleType* SQL_HANDLE_DBC의 **SQLAllocHandle** 함수를 호출 하 고 드라이버에서 오류를 반환 했습니다.|  
|IM006|드라이버의 SQLSetConnectAttr 실패|**SQLConnect**중에 드라이버 관리자가 드라이버의 **SQLSetConnectAttr** 함수를 호출 하 고 드라이버에서 오류를 반환 했습니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|IM009|변환 DLL에 연결할 수 없습니다.|드라이버에서 데이터 원본에 대해 지정 된 변환 DLL에 연결할 수 없습니다.|  
|IM010|데이터 원본 이름이 너무 깁니다.|(DM) * \* ServerName* 이 SQL_MAX_DSN_LENGTH 자 보다 깁니다.|  
|IM014|지정 된 DSN에 드라이버와 응용 프로그램 간의 아키텍처가 일치 하지 않습니다.|(DM) 32 비트 응용 프로그램은 64 비트 드라이버에 연결 하는 DSN을 사용 합니다. 또는 그 반대의 경우도 마찬가지입니다.|  
|IM015|SQL_HANDLE_DBC_INFO_HANDLE에서 드라이버의 SQLConnect 실패|드라이버가 SQL_ERROR을 반환 하는 경우 드라이버 관리자는 응용 프로그램에 SQL_ERROR을 반환 하 고 연결에 실패 합니다.<br /><br /> SQL_HANDLE_DBC_INFO_TOKEN에 대 한 자세한 내용은 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)을 참조 하세요.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
|S1118|드라이버가 비동기 알림을 지원 하지 않습니다.|드라이버가 비동기 알림을 지원 하지 않는 경우 SQL_ATTR_ASYNC_DBC_EVENT 또는 SQL_ATTR_ASYNC_DBC_RETCODE_PTR를 설정할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램에서 **SQLConnect**를 사용 하는 이유에 대 한 자세한 내용은 [SQLConnect를 사용 하 여 연결](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)을 참조 하세요.  
  
 드라이버 관리자는 응용 프로그램이 함수 (**SQLConnect**, **SQLDriverConnect**또는 **SQLBrowseConnect**)를 호출 하 여 드라이버에 연결할 때까지 드라이버에 연결 하지 않습니다. 이 시점까지 드라이버 관리자는 자체 핸들을 사용 하 여 작동 하며 연결 정보를 관리 합니다. 응용 프로그램에서 연결 함수를 호출 하면 드라이버 관리자는 지정 된 *ConnectionHandle*에 대해 드라이버가 현재 연결 되어 있는지 여부를 확인 합니다.  
  
-   드라이버가에 연결 되지 않은 경우 드라이버 관리자는 드라이버에 연결 하 고 *HandleType* SQL_HANDLE_ENV SQL_HANDLE_DBC **SQLAllocHandle** , **SQLSetConnectAttr** (응용 프로그램에서 *연결 특성을* 지정한 경우) 및 드라이버의 연결 기능을 사용 하 여 **SQLAllocHandle** 를 호출 합니다. 드라이버 관리자는 SQLSTATE IM006 (드라이버의 **SQLSetConnectOption** 실패)를 반환 하 고 **SQLSetConnectAttr**에 대 한 오류를 반환 하는 경우 연결 함수에 대 한 SQL_SUCCESS_WITH_INFO 합니다. 자세한 내용은 [데이터 원본 또는 드라이버에 연결](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)을 참조 하세요.  
  
-   지정 된 드라이버가 *ConnectionHandle*에 이미 연결 되어 있는 경우 드라이버 관리자는 드라이버의 연결 함수만 호출 합니다. 이 경우 드라이버는 *ConnectionHandle* 에 대 한 모든 연결 특성이 현재 설정을 유지 하는지 확인 해야 합니다.  
  
-   다른 드라이버가에 연결 된 경우 드라이버 관리자는 SQL_HANDLE_DBC의 *HandleType* 를 사용 하 여 **sqlfreehandle** 을 호출 하 고, 해당 환경에 연결 된 다른 드라이버가 없으면 연결 된 드라이버에서 *HandleType* 의 SQL_HANDLE_ENV를 사용 하 여 **sqlfreehandle** 을 호출 하 고 해당 드라이버의 연결을 끊습니다. 그런 다음 드라이버가에 연결 되지 않은 경우와 동일한 작업을 수행 합니다.  
  
 그러면 드라이버가 핸들을 할당 하 고 자체적으로 초기화 됩니다.  
  
 응용 프로그램이 **Sqldisconnect**를 호출 하면 드라이버 관리자는 드라이버에서 **sqldisconnect** 를 호출 합니다. 그러나 드라이버의 연결을 끊지 않습니다. 이렇게 하면 데이터 원본에 반복 해 서 연결 하 고 연결을 해제 하는 응용 프로그램에 대 한 드라이버가 메모리에 유지 됩니다. 응용 프로그램이 SQL_HANDLE_DBC *HandleType* 를 사용 하 여 **sqlfreehandle** 을 호출 하는 경우 드라이버 관리자는 SQL_HANDLE_DBC *HandleType* 의 HandleType를 사용 하 여 sqlfreehandle **을 호출 하** 고, 드라이버에서 SQL_HANDLE_ENV *HandleType* 가 있는 **sqlfreehandle** 을 호출 하 고, 드라이버의 연결을 끊습니다.  
  
 ODBC 응용 프로그램은 둘 이상의 연결을 설정할 수 있습니다.  
  
## <a name="driver-manager-guidelines"></a>드라이버 관리자 지침  
 **ServerName* 의 내용은 드라이버 관리자와 드라이버가 함께 작동 하 여 데이터 원본에 대 한 연결을 설정 하는 방법에 영향을 줍니다.  
  
-   \* *ServerName* 이 유효한 데이터 원본 이름을 포함 하는 경우 드라이버 관리자는 시스템 정보에서 해당 하는 데이터 원본 사양을 찾고 연결 된 드라이버에 연결 합니다. 드라이버 관리자는 각 **SQLConnect** 인수를 드라이버에 전달 합니다.  
  
-   데이터 원본 이름을 찾을 수 없거나 *ServerName* 이 null 포인터인 경우 드라이버 관리자는 기본 데이터 원본 사양을 찾고 연결 된 드라이버에 연결 합니다. 드라이버 관리자는 수정 되지 않은 *사용자 이름* 및 *인증* 인수를 드라이버에 전달 하 고 *SERVERNAME* 인수에 대해 "DEFAULT"를 전달 합니다.  
  
-   *ServerName* 인수가 "default" 이면 드라이버 관리자는 기본 데이터 원본 사양을 찾고 연결 된 드라이버에 연결 합니다. 드라이버 관리자는 각 **SQLConnect** 인수를 드라이버에 전달 합니다.  
  
-   데이터 원본 이름을 찾을 수 없거나 *ServerName* 이 null 포인터이 고 기본 데이터 원본 사양이 없으면 드라이버 관리자는 SQLSTATE IM002 (데이터 원본 이름을 찾을 수 없으며 기본 드라이버가 지정 되지 않음)를 사용 하 여 SQL_ERROR을 반환 합니다.  
  
 드라이버 관리자가에 연결한 후 드라이버는 시스템 정보에서 해당 하는 데이터 원본 사양을 찾고 사양의 드라이버 관련 정보를 사용 하 여 필요한 연결 정보 집합을 완성할 수 있습니다.  
  
 데이터 원본에 대 한 시스템 정보에 기본 번역 라이브러리가 지정 된 경우 드라이버는 연결에 연결 합니다. SQL_ATTR_TRANSLATE_LIB 특성을 사용 하 여 **SQLSetConnectAttr** 를 호출 하면 다른 변환 라이브러리를에 연결할 수 있습니다. SQL_ATTR_TRANSLATE_OPTION 특성을 사용 하 여 **SQLSetConnectAttr** 를 호출 하 여 변환 옵션을 지정할 수 있습니다.  
  
 드라이버에서 **SQLConnect**를 지 원하는 경우 드라이버에 대 한 시스템 정보의 드라이버 키워드 섹션에는 첫 번째 문자가 "Y"로 설정 된 **connectfunctions** 키워드가 포함 되어야 합니다.  
  
### <a name="connection-pooling"></a>연결 풀링  
 연결 풀링을 사용 하면 응용 프로그램에서 이미 생성 된 연결을 다시 사용할 수 있습니다. 연결 풀링을 사용 하도록 설정 하 고 **SQLConnect** 를 호출 하면 드라이버 관리자는 연결 풀링을 위해 지정 된 환경의 연결 풀에 속하는 연결을 사용 하 여 연결을 시도 합니다. 이 환경은 풀의 연결을 사용 하는 모든 응용 프로그램에서 사용 하는 공유 환경입니다.  
  
 **SQLSetEnvAttr** 를 호출 하 여 SQL_CP_ONE_PER_DRIVER (드라이버만 하나의 풀을 지정 함) 또는 SQL_CP_ONE_PER_HENV (환경 당 최대 하나의 풀을 지정 함)로 SQL_ATTR_CONNECTION_POOLING을 호출 하 여 환경을 할당 하기 전에 연결 풀링을 사용 하도록 설정 합니다. 이 경우 **SQLSetEnvAttr** 는 *EnvironmentHandle* 를 null로 설정 하 여 호출 됩니다. 그러면이 특성이 프로세스 수준 특성으로 설정 됩니다. SQL_ATTR_CONNECTION_POOLING을 SQL_CP_OFF로 설정 하면 연결 풀링이 사용 되지 않습니다.  
  
 연결 풀링을 사용 하도록 설정 하 고 나면 SQL_HANDLE_ENV *HandleType* 의 **SQLAllocHandle** 를 호출 하 여 환경을 할당 합니다. 연결 풀링이 사용 하도록 설정 되어 있기 때문에이 호출에서 할당 한 환경이 공유 환경입니다. 그러나 사용 되는 환경은 SQL_HANDLE_DBC *HandleType* 의 **SQLAllocHandle** 가 호출 될 때까지 결정 되지 않습니다.  
  
 **SQLAllocHandle** 가 SQL_HANDLE_DBC *HandleType* 인를 호출 하 여 연결을 할당 합니다. 드라이버 관리자는 응용 프로그램에서 설정한 환경 특성과 일치 하는 기존 공유 환경을 찾으려고 시도 합니다. 이러한 환경이 없으면 암시적 *공유 환경*으로 만들어집니다. 일치 하는 공유 환경이 발견 되 면 환경 핸들이 응용 프로그램에 반환 되 고 참조 횟수가 증가 합니다.  
  
 그러나 사용 되는 연결은 **SQLConnect** 가 호출 될 때까지 결정 되지 않습니다. 이 시점에서 드라이버 관리자는 연결 풀에서 응용 프로그램에 의해 요청 된 조건과 일치 하는 기존 연결을 찾으려고 시도 합니다. 이러한 조건에는 **SQLConnect** 에 대 한 호출에서 요청 된 연결 옵션 ( *ServerName*, *UserName*및 *Authentication* 키워드의 값)과 *HandleType* of SQL_HANDLE_DBC **SQLAllocHandle** 이 호출 된 이후 설정 된 연결 특성이 포함 됩니다. 드라이버 관리자는 풀에 있는 연결의 해당 연결 키워드 및 특성에 대해 이러한 조건을 확인 합니다. 일치 하는 항목이 있으면 풀의 연결이 사용 됩니다. 일치 하는 항목이 없으면 새 연결이 생성 됩니다.  
  
 SQL_ATTR_CP_MATCH 환경 특성이 SQL_CP_STRICT_MATCH으로 설정 된 경우 사용할 풀의 연결에 대해 일치 하는 항목이 정확히 일치 해야 합니다. SQL_ATTR_CP_MATCH environment 특성이 SQL_CP_RELAXED_MATCH로 설정 된 경우 **SQLConnect** 에 대 한 호출의 연결 옵션은 일치 해야 하지만 일부 연결 특성이 일치 해야 합니다.  
  
 **SQLConnect** 가 호출 되기 전에 응용 프로그램에 의해 설정 된 연결 특성이 풀에 있는 연결의 연결 특성과 일치 하지 않는 경우 다음 규칙이 적용 됩니다.  
  
-   연결을 설정 하기 전에 연결 특성을 설정 해야 하는 경우 다음을 수행 합니다.  
  
     SQL_ATTR_CP_MATCH SQL_CP_STRICT_MATCH 되는 경우 풀링된 연결의 SQL_ATTR_PACKET_SIZE는 응용 프로그램에서 설정한 특성과 동일 해야 합니다. SQL_CP_RELAXED_MATCH 경우 SQL_ATTR_PACKET_SIZE의 값이 다를 수 있습니다.  
  
     SQL_ATTR_LOGIN_VALUE 값은 일치에 영향을 주지 않습니다.  
  
-   연결 특성을 설정할 수 있는 경우 연결 하려면 다음을 수행 합니다.  
  
     연결 특성이 응용 프로그램에 의해 설정 되지 않았지만 풀의 연결에 설정 되어 있고 기본값이 있는 경우 풀링된 연결의 연결 특성이 기본값으로 다시 설정 되 고 일치 항목이 선언 됩니다. 기본값이 없으면 풀링된 연결이 일치 하는 것으로 간주 되지 않습니다.  
  
     연결 특성이 응용 프로그램에 의해 설정 되었지만 풀의 연결에 설정 되어 있지 않은 경우에는 풀의 연결 특성이 응용 프로그램에 의해 설정 된로 변경 되 고 일치 항목이 선언 됩니다.  
  
     응용 프로그램에서 연결 특성을 설정 하 고 풀의 연결에도 설정 했지만 값이 다른 경우 응용 프로그램의 연결 특성 값이 사용 되 고 일치가 선언 됩니다.  
  
-   드라이버별 연결 특성의 값이 동일 하지 않고 SQL_ATTR_CP_MATCH SQL_CP_STRICT_MATCH으로 설정 된 경우에는 풀의 연결이 사용 되지 않습니다.  
  
 응용 프로그램에서 **Sqldisconnect** 를 호출 하 여 연결을 끊으면 연결이 연결 풀로 반환 되 고 다시 사용할 수 있습니다.  
  
### <a name="optimizing-connection-pooling-performance"></a>연결 풀링 성능 최적화  
 분산 트랜잭션이 관련 된 경우 SQLUINTEGER 비트 마스크 인 **SQL_DTC_TRANSITION_COST**를 사용 하 여 연결 풀링 성능을 최적화할 수 있습니다. 여기서 참조 하는 전환은 0에서 0이 아닌 값으로 이동 하 SQL_ATTR_ENLIST_IN_DTC 연결 특성의 전환 이며 그 반대의 경우도 마찬가지입니다. 분산 트랜잭션에 참여 하지 않고 분산 트랜잭션에 참여 하는 것이 아니라 그 반대의 연결입니다. 드라이버가 등록을 구현 하는 방법 (연결 특성 SQL_ATTR_ENLIST_IN_DTC 설정)에 따라 이러한 전환은 부담이 될 수 있으므로 최상의 성능을 위해 피해 야 합니다.  
  
 드라이버에서 반환 되는 값에는 다음 비트의 조합이 포함 됩니다.  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**설정 된 경우 0에서 0이 아닌 전환은 0에서 0이 아닌 다른 값으로 전환 하는 것 보다 훨씬 더 비쌉니다 (이전에 다음 트랜잭션에 등록 된 연결 참여).  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**설정 하면 SQL_ATTR_ENLIST_IN_DTC 특성이 이미 0으로 설정 된 연결을 사용 하는 것 보다 0에서 0으로 전환 하는 것을 의미 합니다.  
  
 성능과 연결 사용이 균형을 비교 합니다. 드라이버가 이러한 전환 중 하나 이상에 비용이 많이 드는 것으로 표시 되 면 드라이버 관리자의 연결 풀러는 풀에 더 많은 연결을 유지 하 여이에 응답 합니다. 풀의 일부 연결은 비트랜잭션 사용을 위한 것 이며, 일부는 트랜잭션 사용에 대 한 기본 설정입니다. 그러나 드라이버가 이러한 전환에 비용이 많이 들 수 없는 것으로 표시 되는 경우 비트랜잭션 사용과 트랜잭션 사용을 번갈아 사용 하는 연결 수를 줄일 수 있습니다.  
  
 SQL_ATTR_ENLIST_IN_DTC를 지원 하지 않는 드라이버는 SQL_DTC_TRANSITION_COST를 지원할 필요가 없습니다. SQL_ATTR_ENLIST_IN_DTC를 지원 하지만 SQL_DTC_TRANSITION_COST 하지 않는 드라이버의 경우 드라이버에서이 값에 대해 0 (비트 집합 없음)을 반환 하는 것 처럼 전환이 비용이 많이 드는 것으로 간주 됩니다.  
  
 SQL_DTC_TRANSITION_COST는 odbc 3.5에 도입 되었지만 ODBC 2에는 있습니다. *x* 드라이버는 드라이버 버전에 관계 없이이 정보를 쿼리 하므로이를 지원할 수도 있습니다.  
  
### <a name="code-example"></a>코드 예  
 다음 예제에서 응용 프로그램은 환경 및 연결 핸들을 할당 합니다. 그런 다음 사용자 ID 존스 및 암호 Sesame를 사용 하 여 SalesOrders 데이터 원본에 연결 하 고 데이터를 처리 합니다. 데이터 처리가 완료 되 면 데이터 원본에서 연결을 끊고 핸들을 해제 합니다.  
  
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
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|데이터 원본에 연결 하는 데 필요한 값 검색 및 열거|[SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|데이터 원본에서 연결 끊기|[SQLDisconnect 함수](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|연결 문자열 또는 대화 상자를 사용 하 여 데이터 원본에 연결|[SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|연결 특성의 설정 반환|[SQLGetConnectAttr 함수(SQLGetConnectAttr Function)](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|연결 특성 설정|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
