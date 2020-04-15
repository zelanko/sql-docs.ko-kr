---
title: SQLConnect 기능 | 마이크로 소프트 문서
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
ms.openlocfilehash: ab0a31845efeb484c554a9c9cf1afeaeab1a8bea
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301219"
---
# <a name="sqlconnect-function"></a>SQLConnect 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLConnect는** 드라이버 및 데이터 원본에 대한 연결을 설정합니다. 연결 핸들은 상태, 트랜잭션 상태 및 오류 정보를 포함하여 데이터 원본에 대한 연결에 대한 모든 정보의 저장소를 참조합니다.  
  
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
 *연결 핸들*  
 [Input] 연결 핸들입니다.  
  
 *ServerName*  
 [입력] 데이터 원본 이름입니다. 데이터는 프로그램과 동일한 컴퓨터에 있거나 네트워크의 다른 컴퓨터에 있을 수 있습니다. 응용 프로그램이 데이터 원본을 선택하는 방법에 대한 자세한 내용은 [데이터 원본 또는 드라이버 선택을](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)참조하십시오.  
  
 *NameLength1*  
 [입력] 문자의 ** 서버 이름의* 길이입니다.  
  
 *사용자*  
 [입력] 사용자 식별자입니다.  
  
 *이름 길이2*  
 [입력] * 문자의*사용자 이름* 길이입니다.  
  
 *인증*  
 [입력] 인증 문자열(일반적으로 암호)입니다.  
  
 *이름 길이3*  
 [입력] * 문자*인증의* 길이입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE 또는 SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>진단  
 **SQLConnect가** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *SQL_HANDLE_DBC 핸들 유형* 및 *연결 핸들*핸들을 사용하는 *Handle* **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 일반적으로 **SQLConnect에서** 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01S02|옵션 값이 변경되었습니다.|드라이버는 **SQLSetConnectAttr에서** *ValuePtr* 인수의 지정된 값을 지원 하지 않고 비슷한 값을 대체 했습니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08001|연결을 설정할 수 없는 클라이언트|드라이버가 데이터 원본과 연결을 설정할 수 없습니다.|  
|08002|사용 중 연결 이름|(DM) 지정된 *ConnectionHandle이* 이미 데이터 원본과의 연결을 설정하는 데 사용되었으며 연결이 여전히 열려 있거나 사용자가 연결을 검색중이었습니다.|  
|08004|서버가 연결을 거부했습니다.|데이터 원본은 구현 정의 이유로 연결 의 설치를 거부했습니다.|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결하려고 했던 데이터 원본 간의 통신 링크가 실패했습니다.|  
|28000|잘못된 권한 부여 사양|인수 *UserName에* 대해 지정된 값 또는 인수 *인증에* 대해 지정된 값은 데이터 원본에 정의된 제한을 위반했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|(DM) 드라이버 관리자가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*연결 핸들*에 대해 비동기 처리가 활성화되었습니다. **SQLConnect** 함수가 호출되었고 실행을 완료하기 전에 [SQLCancelHandle 함수가](../../../odbc/reference/syntax/sqlcancelhandle-function.md) *연결 핸들에서*호출된 다음 **SQLConnect** 함수가 *연결 핸들*에서 다시 호출되었습니다.<br /><br /> 또는 **SQLConnect** 함수가 호출되었으며 실행을 완료하기 전에 **SQLCancelHandle은** 다중 스레드 응용 프로그램의 다른 스레드에서 *ConnectionHandle에서* 호출되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) 비동기적으로 실행 되는 함수 (이 하나) *연결 핸들에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) 인수 *NameLength1,* *NameLength2*또는 *NameLength3에* 대해 지정된 값은 0보다 작지만 SQL_NTS 같지 는 않습니다.<br /><br /> (DM) 인수 *NameLength1에* 대해 지정된 값이 데이터 원본 이름의 최대 길이를 초과했습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에 대한 연결이 완료되기 전에 쿼리 시간 시간 만료 기간이 만료되었습니다. 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT 통해 설정됩니다.|  
|HY14|드라이버 연결 수준 비동기 함수 실행을 지원 하지 않습니다.|(DM) 응용 프로그램은 연결을 하기 전에 연결 핸들에서 비동기 작업을 사용하도록 설정했습니다. 그러나 드라이버는 연결 핸들에서 비동기 작업을 지원하지 않습니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) 데이터 원본 이름으로 지정된 드라이버가 함수를 지원하지 않습니다.|  
|IM002|데이터 원본을 찾을 수 없으며 기본 드라이버가 지정되지 않았습니다.|(DM) *인수 ServerName에* 지정된 데이터 원본 이름이 시스템 정보에서 찾을 수 없으며 기본 드라이버 사양이 없습니다.|  
|IM003|지정된 드라이버를 연결할 수 없습니다.|(DM) 시스템 정보의 데이터 원본 사양에 나열된 드라이버를 찾을 수 없거나 다른 이유로 연결할 수 없습니다.|  
|IM004|SQL_HANDLE_ENV 대한 드라이버의 SQLAllocHandle이 실패했습니다.|(DM) **SQLConnect**동안 드라이버 관리자는 *핸들 SQL_HANDLE_ENV 핸들 유형이* 있는 드라이버의 **SQLAllocHandle** 함수를 호출하고 드라이버가 오류를 반환했습니다.|  
|IM005|SQL_HANDLE_DBC 드라이버의 SQLAllocHandle실패|(DM) **SQLConnect**동안 드라이버 관리자는 *핸들 유형* SQL_HANDLE_DBC 드라이버의 **SQLAllocHandle** 함수를 호출하 고 드라이버 오류를 반환 했습니다.|  
|IM006|드라이버의 SQLSetConnectAttr 실패|**SQLConnect**중에 드라이버 관리자는 드라이버의 **SQLSetConnectAttr** 함수를 호출하고 드라이버가 오류를 반환했습니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|IM009|번역 DLL에 연결할 수 없음|드라이버가 데이터 원본에 대해 지정된 번역 DLL에 연결할 수 없습니다.|  
|IM010|데이터 원본 이름이 너무 깁니다.|(DM) * \*서버 이름이* SQL_MAX_DSN_LENGTH 문자보다 길다.|  
|IM014|지정된 DSN에는 드라이버와 응용 프로그램 간의 아키텍처 불일치가 포함되어 있습니다.|(DM) 32비트 애플리케이션은 64비트 드라이버에 연결하는 DSN을 사용합니다. 또는 그 반대의 경우도 마찬가지입니다.|  
|IM015|SQL_HANDLE_DBC_INFO_HANDLE 드라이버의 SQLConnect가 실패했습니다.|드라이버가 SQL_ERROR 반환하면 드라이버 관리자가 SQL_ERROR 응용 프로그램에 반환하고 연결이 실패합니다.<br /><br /> SQL_HANDLE_DBC_INFO_TOKEN 대한 자세한 내용은 [ODBC 드라이버에서 연결-풀 인식 개발을](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)참조하십시오.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
|S1118|드라이버가 비동기 알림을 지원하지 않습니다.|드라이버가 비동기 알림을 지원하지 않는 경우 SQL_ATTR_ASYNC_DBC_EVENT 설정할 수 없습니다 SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="comments"></a>주석  
 응용 프로그램에서 **SQLConnect를**사용하는 이유에 대한 자세한 내용은 [SQLConnect연결 연결을 참조하십시오.](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
 드라이버 관리자는 응용 프로그램이 드라이버에 연결하는**함수(SQLConnect,** **SQLDriverConnect**또는 **SQLBrowseConnect)를**호출할 때까지 드라이버에 연결되지 않습니다. 이 시점까지 드라이버 관리자는 자체 핸들을 사용하며 연결 정보를 관리합니다. 응용 프로그램이 연결 함수를 호출할 때 드라이버 관리자는 드라이버가 지정된 *ConnectionHandle:*  
  
-   드라이버가 연결되지 않은 경우 드라이버 관리자는 드라이버에 연결하고 *핸들 유형* SQL_HANDLE_ENV **SQLAllocHandle,** 핸들 *유형SQL_HANDLE_DBC* **SQLAllocHandle,** **SQLSetConnectAttr(응용** 프로그램이 연결 특성을 지정한 경우) 및 드라이버의 연결 함수를 호출합니다. 드라이버 관리자는 SQLSTATE IM006(드라이버의 **SQLSetConnectOption** 실패)을 반환하고 드라이버가 **SQLSetConnectAttr**에 대한 오류를 반환한 경우 연결 함수에 대한 SQL_SUCCESS_WITH_INFO. 자세한 내용은 [데이터 원본 또는 드라이버에 연결 을](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)참조하십시오.  
  
-   지정된 드라이버가 *ConnectionHandle에*이미 연결되어 있는 경우 드라이버 관리자는 드라이버의 연결 기능만 호출합니다. 이 경우 드라이버는 *ConnectionHandle에* 대한 모든 연결 특성이 현재 설정을 유지관리해야 합니다.  
  
-   다른 드라이버가 연결되어 있는 경우 드라이버 관리자는 SQL_HANDLE_DBC *HandleType을* 사용하여 **SQLFreeHandle을** 호출한 다음 해당 환경에서 다른 드라이버가 연결되지 않은 경우 연결된 드라이버의 *핸들 유형* SQL_HANDLE_ENV **사용하여 SQLFreeHandle을** 호출한 다음 해당 드라이버의 연결을 끊습니다. 그런 다음 드라이버가 연결되지 않은 경우와 동일한 작업을 수행합니다.  
  
 그런 다음 드라이버는 핸들을 할당하고 자체를 초기화합니다.  
  
 응용 프로그램에서 **SQLDisconnect를**호출하면 드라이버 관리자는 드라이버에서 **SQLDisconnect를** 호출합니다. 그러나 드라이버의 연결을 끊지 않습니다. 이렇게 하면 데이터 원본에 반복적으로 연결하고 연결을 끊는 응용 프로그램의 경우 드라이버가 메모리에 유지됩니다. 응용 프로그램이 *핸들 유형* SQL_HANDLE_DBC **SQLFreeHandle을** 호출할 때 드라이버 관리자는 *핸들 유형* SQL_HANDLE_DBC **SQLFreeHandle을** 호출한 다음 드라이버의 핸들 SQL_HANDLE_ENV 핸들 *유형이* 있는 **SQLFreeHandle을** 호출한 다음 드라이버를 연결 해제합니다.  
  
 ODBC 응용 프로그램은 두 개 이상의 연결을 설정할 수 있습니다.  
  
## <a name="driver-manager-guidelines"></a>드라이버 관리자 가이드라인  
 **ServerName의* 내용은 드라이버 관리자와 드라이버가 함께 작동하여 데이터 원본에 대한 연결을 설정하는 방법에 영향을 미칩니다.  
  
-   \* *ServerName에* 유효한 데이터 원본 이름이 포함된 경우 드라이버 관리자는 시스템 정보에서 해당 데이터 원본 사양을 찾아 관련 드라이버에 연결합니다. 드라이버 관리자는 각 **SQLConnect** 인수를 드라이버에 전달합니다.  
  
-   데이터 원본 이름을 찾을 수 없거나 *ServerName이* null 포인터인 경우 드라이버 관리자는 기본 데이터 원본 사양을 찾아 관련 드라이버에 연결합니다. 드라이버 관리자는 *수정되지* 않은 사용자 이름 및 *인증* 인수를 드라이버에 전달하고 *ServerName* 인수에 대해 "DEFAULT"를 전달합니다.  
  
-   *ServerName* 인수가 "DEFAULT"인 경우 드라이버 관리자는 기본 데이터 원본 사양을 찾고 연결된 드라이버에 연결합니다. 드라이버 관리자는 각 **SQLConnect** 인수를 드라이버에 전달합니다.  
  
-   데이터 원본 이름을 찾을 수 없거나 *ServerName이* null 포인터이고 기본 데이터 원본 사양이 없는 경우 드라이버 관리자는 SQLSTATE IM002(데이터 원본 이름을 찾을 수 없고 기본 드라이버가 지정되지 않음)를 사용하여 SQL_ERROR 반환합니다.  
  
 드라이버 관리자에 의해 연결된 후 드라이버는 시스템 정보에서 해당 데이터 원본 사양을 찾고 사양에서 드라이버 별 정보를 사용하여 필요한 연결 정보 집합을 완료할 수 있습니다.  
  
 데이터 원본의 시스템 정보에 기본 변환 라이브러리가 지정되면 드라이버가 연결됩니다. 다른 번역 라이브러리는 **sqlSetConnectAttr을** SQL_ATTR_TRANSLATE_LIB 특성으로 호출하여 연결할 수 있습니다. **sqlSetConnectAttr을** SQL_ATTR_TRANSLATE_OPTION 특성으로 호출하여 변환 옵션을 지정할 수 있습니다.  
  
 드라이버가 **SQLConnect를**지원하는 경우 드라이버에 대한 시스템 정보의 드라이버 키워드 섹션에는 첫 번째 문자가 "Y"로 설정된 **ConnectFunctions** 키워드가 포함되어야 합니다.  
  
### <a name="connection-pooling"></a>연결 풀링  
 연결 풀링을 사용하면 응용 프로그램이 이미 생성된 연결을 다시 사용할 수 있습니다. 연결 풀링을 사용하도록 설정하고 **SQLConnect를** 호출하는 경우 드라이버 관리자는 연결 풀링을 위해 지정된 환경에서 연결 풀의 일부인 연결을 사용하여 연결을 시도합니다. 이 환경은 풀에서 연결을 사용하는 모든 응용 프로그램에서 사용되는 공유 환경입니다.  
  
 **SQLSetEnvAttr을** 호출하여 SQL_ATTR_CONNECTION_POOLING SQL_CP_ONE_PER_DRIVER(드라이버당 최대 하나의 풀을 지정함) 또는 SQL_CP_ONE_PER_HENV(환경당 최대 풀을 지정함)으로 설정하여 환경을 할당하기 전에 연결 풀링을 사용할 수 있습니다. 이 경우 **SQLSetEnvAttr은** *환경 핸들을* null로 설정하여 호출되어 특성을 프로세스 수준 특성으로 만듭니다. SQL_ATTR_CONNECTION_POOLING SQL_CP_OFF 설정하면 연결 풀링이 비활성화됩니다.  
  
 연결 풀링을 사용하도록 설정한 후 *핸들 유형* SQL_HANDLE_ENV 있는 **SQLAllocHandle을** 호출하여 환경을 할당합니다. 연결 풀링이 활성화되었기 때문에 이 호출에서 할당된 환경은 공유 환경입니다. 그러나 사용할 환경은 *핸들 유형* SQL_HANDLE_DBC 호출될 때까지 **SQLAllocHandle이** 결정되지 않습니다.  
  
 *핸들 유형* SQL_HANDLE_DBC **있는 SQLAllocHandle** 연결을 할당 하기 위해 호출 됩니다. 드라이버 관리자는 응용 프로그램에서 설정한 환경 특성과 일치하는 기존 공유 환경을 찾으려고 합니다. 이러한 환경이 없으면 하나는 암시적 *공유 환경으로*만들어집니다. 일치하는 공유 환경이 발견되면 환경 핸들이 응용 프로그램에 반환되고 참조 수가 증가합니다.  
  
 그러나 사용할 연결은 **SQLConnect가** 호출될 때까지 결정되지 않습니다. 이 때 드라이버 관리자는 응용 프로그램에서 요청한 조건과 일치하는 연결 풀에서 기존 연결을 찾으려고 합니다. 이러한 기준에는 **SQLConnect** 호출에서 요청한 연결 *옵션(서버이름,* *UserName*및 *인증* 키워드의 값) 및 *핸들 유형SQL_HANDLE_DBC* **SQLAllocHandle이** 호출된 이후 설정된 모든 연결 특성이 포함됩니다. 드라이버 관리자는 풀의 연결에 있는 해당 연결 키워드 및 특성에 대해 이러한 조건을 확인합니다. 일치하는 연결이 발견되면 풀의 연결이 사용됩니다. 일치하는 연결이 없는 경우 새 연결이 만들어집니다.  
  
 SQL_ATTR_CP_MATCH 환경 특성이 SQL_CP_STRICT_MATCH 설정된 경우 풀의 연결을 사용할 때 일치하는 일치가 정확해야 합니다. SQL_ATTR_CP_MATCH 환경 특성이 SQL_CP_RELAXED_MATCH 설정된 경우 **SQLConnect** 호출의 연결 옵션이 일치해야 하지만 모든 연결 특성이 일치해야 하는 것은 아닙니다.  
  
 다음 규칙은 **SQLConnect가** 호출되기 전에 응용 프로그램에서 설정한 연결 특성이 풀에서 연결의 연결 특성과 일치하지 않을 때 적용됩니다.  
  
-   연결하기 전에 연결 특성을 설정해야 하는 경우:  
  
     SQL_ATTR_CP_MATCH SQL_CP_STRICT_MATCH 경우 풀린 연결의 SQL_ATTR_PACKET_SIZE 응용 프로그램에서 설정한 특성과 동일해야 합니다. SQL_CP_RELAXED_MATCH 경우 SQL_ATTR_PACKET_SIZE 값이 다를 수 있습니다.  
  
     SQL_ATTR_LOGIN_VALUE 값은 일치에 영향을 주지 않습니다.  
  
-   연결 특성을 연결하기 전이나 후에 설정할 수 있는 경우:  
  
     연결 특성이 응용 프로그램에서 설정되지 않았지만 풀의 연결에 설정되어 있고 기본값이 있는 경우 풀린 연결의 연결 특성이 기본값으로 다시 설정되고 일치가 선언됩니다. 기본값이 없는 경우 풀겨진 연결은 일치하는 것으로 간주되지 않습니다.  
  
     응용 프로그램에서 연결 특성을 설정했지만 풀의 연결에 대해 설정되지 않은 경우 풀의 연결 특성이 응용 프로그램에 의해 설정된 것으로 변경되고 일치가 선언됩니다.  
  
     응용 프로그램에서 연결 특성을 설정하고 풀의 연결에 대해서도 설정했지만 값이 다른 경우 응용 프로그램의 연결 특성 값이 사용되고 일치가 선언됩니다.  
  
-   드라이버 별 연결 특성의 값이 동일하지 않고 SQL_ATTR_CP_MATCH SQL_CP_STRICT_MATCH 설정하면 풀의 연결이 사용되지 않습니다.  
  
 응용 프로그램에서 연결을 끊기 위해 **SQLDisconnect를** 호출하면 연결이 연결 풀로 반환되고 다시 사용할 수 있습니다.  
  
### <a name="optimizing-connection-pooling-performance"></a>연결 풀링 성능 최적화  
 분산 트랜잭션이 관련된 경우 SQLUINTEGER 비트마스크인 **SQL_DTC_TRANSITION_COST**사용하여 연결 풀링 성능을 최적화할 수 있습니다. 참조되는 전환은 값 0에서 0이 아닌 SQL_ATTR_ENLIST_IN_DTC 연결 특성의 전환이며 그 반대의 경우도 마찬가지입니다. 이 연결은 분산 트랜잭션에 등록되지 않은 연결에서 분산 트랜잭션에 등록된 연결이며 그 반대의 경우도 마찬가지입니다. 드라이버가 인리스트먼트를 구현한 방식에 따라(연결 특성 설정 SQL_ATTR_ENLIST_IN_DTC) 이러한 전환은 비용이 많이 들 수 있으므로 최상의 성능을 위해 피해야 합니다.  
  
 드라이버에서 반환되는 값에는 다음 비트의 조합이 포함됩니다.  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**설정하면 0에서 비영지 전환이 0에서 다른 비영값으로의 전환보다 훨씬 더 비싸다는 것을 의미합니다(다음 트랜잭션에서 이전에 등록된 연결을 등록함).  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**설정하면 비영~0전환이 이미 SQL_ATTR_ENLIST_IN_DTC 특성이 0으로 설정된 연결을 사용하는 것보다 훨씬 더 비싸다는 것을 의미합니다.  
  
 성능과 연결 사용 절충안이 있습니다. 드라이버가 이러한 전환 중 하나 이상이 비용이 많이 드는 경우 드라이버 관리자의 연결 풀러는 풀에 더 많은 연결을 유지하여 이에 응답합니다. 풀의 일부 연결은 비트랜잭션 용으로 선호되며 일부는 트랜잭션 용으로 선호됩니다. 그러나 드라이버가 이러한 전환이 비용이 많이 나지 않는다고 표시하면 비트랜잭션 및 트랜잭션 사용 간에 번갈아 가며 사용할 수 있는 연결 수가 줄어듭니다.  
  
 SQL_ATTR_ENLIST_IN_DTC 지원하지 않는 드라이버는 SQL_DTC_TRANSITION_COST 지원할 필요가 없습니다. SQL_ATTR_ENLIST_IN_DTC 지원하지만 SQL_DTC_TRANSITION_COST 않는 드라이버의 경우 드라이버가 이 값에 대해 0(비트 집합 없음)을 반환한 것처럼 전환비용이 많이 드는 것으로 가정합니다.  
  
 SQL_DTC_TRANSITION_COST ODBC 3.5, ODBC 2에 도입되었다. *드라이버* 관리자는 드라이버 버전에 관계없이 이 정보를 쿼리하기 때문에 x 드라이버도 지원할 수 있습니다.  
  
### <a name="code-example"></a>코드 예  
 다음 예제에서 응용 프로그램은 환경 및 연결 핸들을 할당합니다. 그런 다음 사용자 ID JohnS 및 암호 참깨와 함께 SalesOrders 데이터 원본에 연결하고 데이터를 처리합니다. 데이터 처리가 완료되면 데이터 원본에서 연결이 끊어지고 핸들이 해제됩니다.  
  
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
  
|원하는 정보|참조|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|데이터 원본에 연결하는 데 필요한 값 검색 및 확대|[SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|데이터 원본연결 해제|[SQLDisconnect 함수](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|연결 문자열 또는 대화 상자를 사용하여 데이터 원본에 연결|[SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|연결 특성의 설정 반환|[SQLGetConnectAttr 함수(SQLGetConnectAttr Function)](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|연결 특성 설정|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
