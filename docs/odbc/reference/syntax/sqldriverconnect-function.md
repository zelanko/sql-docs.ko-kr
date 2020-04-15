---
title: SQL드라이버연결 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDriverConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDriverConnect
helpviewer_keywords:
- SQLDriverConnect function [ODBC]
ms.assetid: e299be1d-5c74-4ede-b6a3-430eb189134f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 88ec70d68b46beca97fd6b0d758e21aab5d4f4b2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302774"
---
# <a name="sqldriverconnect-function"></a>SQLDriverConnect 함수(SQLDriverConnect Function)
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ODBC  
  
 **요약**  
 **SQLDriverConnect는** **SQLConnect의**대안입니다. **SQLConnect의**세 인수보다 더 많은 연결 정보가 필요한 데이터 원본, 모든 연결 정보를 사용자에게 묻는 대화 상자 및 시스템 정보에 정의되지 않은 데이터 원본을 지원합니다.  
  
 **SQLDriverConnect는** 다음과 같은 연결 특성을 제공합니다.  
  
-   데이터 원본 이름, 하나 이상의 사용자 ID, 하나 이상의 암호 및 데이터 원본에 필요한 기타 정보가 포함된 연결 문자열을 사용하여 연결을 설정합니다.  
  
-   부분 연결 문자열을 사용하거나 추가 정보를 사용하지 않고 연결을 설정합니다. 이 경우 드라이버 관리자와 드라이버는 각각 사용자에게 연결 정보를 묻는 메시지를 표시할 수 있습니다.  
  
-   시스템 정보에 정의되지 않은 데이터 원본에 대한 연결을 설정합니다. 응용 프로그램이 부분 연결 문자열을 제공하는 경우 드라이버는 사용자에게 연결 정보를 묻는 메시지를 표시할 수 있습니다.  
  
-   .dsn 파일의 정보에서 생성된 연결 문자열을 사용하여 데이터 원본에 대한 연결을 설정합니다.  
  
 연결이 설정되면 **SQLDriverConnect는** 완료된 연결 문자열을 반환합니다. 응용 프로그램은 후속 연결 요청에 이 문자열을 사용할 수 있습니다. 자세한 내용은 [SQLDriverConnect 연결](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)을 참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLDriverConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLHWND         WindowHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr,  
     SQLUSMALLINT    DriverCompletion);  
```  
  
## <a name="arguments"></a>인수  
 *연결 핸들*  
 [Input] 연결 핸들입니다.  
  
 *창 핸들*  
 [입력] 창 핸들입니다. 응용 프로그램은 해당되는 경우 부모 창의 핸들을 전달하거나 창 핸들이 적용되지 않거나 **SQLDriverConnect가** 대화 상자를 표시하지 않는 경우 null 포인터를 전달할 수 있습니다.  
  
 *인커넥션 스트링*  
 [입력] 전체 연결 문자열("주석"의 구문 참조), 부분 연결 문자열 또는 빈 문자열입니다.  
  
 *문자열 길이1*  
 [입력] **InConnectionString의*길이는 문자열이 유니코드인 경우 문자로, 문자열이 ANSI 또는 DBCS인 경우 바이트입니다.  
  
 *아웃커넥션 스트링*  
 [출력] 완료된 연결 문자열에 대한 버퍼에 대한 포인터입니다. 대상 데이터 원본에 성공적으로 연결하면 이 버퍼에는 완료된 연결 문자열이 포함됩니다. 응용 프로그램은 이 버퍼에 대해 최소 1,024자를 할당해야 합니다.  
  
 *OutConnectionString이* NULL인 경우 *StringLength2Ptr은* *OutConnectionString에서*가리키는 버퍼에서 반환할 수 있는 총 문자 수(문자 데이터에 대한 null 종료 문자 제외)를 반환합니다.  
  
 *버퍼 길이*  
 [입력] **OutConnectionString* 버퍼의 길이입니다.  
  
 *문자열길이2Ptr*  
 [출력] \* *OutConnectionString에서*반환할 수 있는 총 문자 수(null-termination 문자 제외)를 반환하는 버퍼에 대한 포인터입니다. 반환할 수 있는 문자 수가 *BufferLength보다*크거나 같으면 \* *OutConnectionString의* 완료된 연결 문자열이 *BufferLength에* 잘려null 종료 문자의 길이를 뺀 값입니다.  
  
 *드라이버 완료*  
 [입력] 드라이버 관리자 또는 드라이버가 추가 연결 정보를 요청해야 하는지 여부를 나타내는 플래그는 다음과 같은 것입니다.  
  
 SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED 또는 SQL_DRIVER_NOPROMPT.  
  
 (자세한 내용은 "댓글"을 참조하십시오.)  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE 또는 SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>진단  
 **SQLDriverConnect가** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *SQL_HANDLE_DBC fHandleType* 및 연결 *핸들의* *hHandle을* 사용 하 여 **SQLGetDiagRec를** 호출 하 여 관련 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 **SQLDriverConnect에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|버퍼 \* *OutConnectionString* 전체 연결 문자열을 반환 하기에 충분 하지 않은 연결 문자열 잘 린 되었습니다. 잘린 연결 문자열의 길이는 **StringLength2Ptr에서*반환됩니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01S00|잘못된 연결 문자열 특성|잘못된 특성 키워드가 연결*문자열(InConnectionString)에*지정되었지만 드라이버는 데이터 원본에 연결할 수 있었습니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01S02|옵션 값이 변경되었습니다.|드라이버는 **SQLSetConnectAttr의** *ValuePtr* 인수에서 가리키는 지정된 값을 지원하지 않고 유사한 값을 대체했습니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01S08|오류 저장 파일 DSN|* \*InConnectionString의* 문자열에는 **FILEDSN** 키워드가 포함되어 있지만 .dsn 파일은 저장되지 않았습니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01S09|잘못된 키워드|(DM) * \*InConnectionString의* 문자열에는 **SAVEFILE** 키워드가 포함되어 있지만 **드라이버** 또는 **FILEDSN** 키워드는 포함되지 않습니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08001|연결을 설정할 수 없는 클라이언트|드라이버가 데이터 원본과 연결을 설정할 수 없습니다.|  
|08002|사용 중 연결 이름|(DM) 지정된 *ConnectionHandle이* 이미 데이터 원본과의 연결을 설정하는 데 사용되었으며 연결이 여전히 열려 있습니다.|  
|08004|서버가 연결을 거부했습니다.|데이터 원본은 구현 정의 이유로 연결 의 설치를 거부했습니다.|  
|08S01|통신 링크 오류|**SQLDriverConnect** 함수가 처리를 완료하기 전에 드라이버와 드라이버가 연결을 시도하려는 데이터 원본 간의 통신 링크가 실패했습니다.|  
|28000|잘못된 권한 부여 사양|사용자 식별자 또는 권한 부여 문자열 또는 둘 다 연결*문자열(InConnectionString)에*지정된 대로 데이터 원본에서 정의한 제한을 위반했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. szMessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류및 그 원인을 설명합니다. * \**|  
|HY000|일반 오류: 잘못된 파일 dsn|(DM) **InConnectionString의* 문자열에 FILEDSN 키워드가 포함되어 있지만 .dsn 파일의 이름을 찾을 수 없습니다.|  
|HY000|일반 오류: 파일 버퍼를 만들 수 없습니다.|(DM) **InConnectionString의* 문자열에 FILEDSN 키워드가 포함되어 있지만 .dsn 파일을 읽을 수 없습니다.|  
|HY01|메모리 할당 오류|드라이버 관리자가 **SQLDriverConnect** 기능의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.<br /><br /> 드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*연결 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 [SQLCancelHandle 함수가](../../../odbc/reference/syntax/sqlcancelhandle-function.md) *ConnectionHandle에서*호출된 다음 **SQLDriverConnect** 함수가 *ConnectionHandle*에서 다시 호출되었습니다.<br /><br /> 또는 **SQLDriverConnect** 함수가 호출되었으며 실행을 완료하기 전에 **SQLCancelHandle은** 다중 스레드 응용 프로그램의 다른 스레드에서 *ConnectionHandle에서* 호출되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) **SQLDriverConnect가**아닌 비동기적으로 실행되는 또 다른 함수는 *연결 핸들에* 대해 호출되었으며 **SQLDriverConnect** 함수가 호출될 때 계속 실행 중이었습니다.|  
|HY013|메모리 관리 오류|**SQLDriverConnect** 함수 호출은 메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) *인수 StringLength1에* 대해 지정된 값은 0보다 크고 SQL_NTS 같지 않았습니다.<br /><br /> (DM) 인수 *BufferLength에* 대해 지정된 값이 0보다 적습니다.|  
|HY092|잘못된 특성/옵션 식별자|(DM) *드라이버완성* 인수가 SQL_DRIVER_PROMPT 및 *WindowHandle* 인수는 null 포인터였습니다.|  
|HY110|드라이버가 잘못 완료되었습니다.|(DM) *인수 드라이버완성에* 대해 지정된 값이 SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED 또는 SQL_DRIVER_NOPROMPT 같지 않았습니다.<br /><br /> (DM) 연결 풀링이 활성화되었고 *인수 DriverCompletion에* 대해 지정된 값이 SQL_DRIVER_NOPROMPT 같지 않았습니다.|  
|하이크00|구현되지 않은 선택적 기능|드라이버는 응용 프로그램이 요청한 ODBC 동작의 버전을 지원하지 않습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에 대한 연결이 완료되기 전에 로그인 시간 시간 만료 기간이 만료되었습니다. 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT 통해 설정됩니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) 지정된 데이터 원본 이름에 해당하는 드라이버가 함수를 지원하지 않습니다.|  
|IM002|데이터 원본을 찾을 수 없으며 기본 드라이버가 지정되지 않았습니다.|(DM) 연결*문자열(InConnectionString)에*지정된 데이터 원본 이름이 시스템 정보에서 찾을 수 없으며 기본 드라이버 사양이 없습니다.<br /><br /> (DM) ODBC 데이터 원본 및 기본 드라이버 정보를 시스템 정보에서 찾을 수 없습니다.|  
|IM003|지정된 드라이버를 로드할 수 없습니다.|(DM) 시스템 정보의 데이터 원본 사양에 나열되거나 **DRIVER** 키워드에 의해 지정된 드라이버를 찾을 수 없거나 다른 이유로 로드할 수 없습니다.|  
|IM004|SQL_HANDLE_ENV 대한 드라이버의 **SQLAllocHandle실패**|(DM) **SQLDriverConnect**동안 드라이버 관리자는 *SQL_HANDLE_ENV fHandleType을* 사용 하 고 드라이버의 **SQLAllocHandle** 함수를 호출 하 고 드라이버 오류를 반환 했습니다.|  
|IM005|SQL_HANDLE_DBC 대한 드라이버의 **SQLAllocHandle이** 실패했습니다.|(DM) **SQLDriverConnect**동안 드라이버 관리자는 *SQL_HANDLE_DBC fHandleType을* 사용 하 고 드라이버의 **SQLAllocHandle** 함수를 호출 하 고 드라이버 오류를 반환 했습니다.|  
|IM006|드라이버의 **SQLSetConnectAttr** 실패|(DM) **SQLDriverConnect**동안 드라이버 관리자는 드라이버의 **SQLSetConnectAttr** 함수를 호출하고 드라이버가 오류를 반환했습니다.|  
|IM007|데이터 원본또는 드라이버를 지정하지 않습니다. 대화 상자 금지|연결 문자열에 데이터 원본 이름이나 드라이버가 지정되지 않았으며 *DriverCompletion이* SQL_DRIVER_NOPROMPT.|  
|IM008|대화 상자에 실패했습니다.|드라이버가 로그인 대화 상자를 표시하려고 했지만 실패했습니다.<br /><br /> *WindowHandle은* null 포인터이고 *드라이버완료는* SQL_DRIVER_NO_PROMPT 않았습니다.|  
|IM009|번역 DLL을 로드할 수 없음|드라이버가 데이터 원본 또는 연결에 대해 지정된 변환 DLL을 로드할 수 없습니다.|  
|IM010|데이터 원본 이름이 너무 깁니다.|(DM) DSN 키워드의 특성 값이 SQL_MAX_DSN_LENGTH 문자보다 길다.|  
|IM011|드라이버 이름이 너무 깁니다.|(DM) **DRIVER** 키워드의 속성 값이 255자보다 길다.|  
|IM012|DRIVER 키워드 구문 오류|(DM) **DRIVER** 키워드의 키워드 값 쌍에는 구문 오류가 포함되어 있습니다.<br /><br /> (DM) * \*InConnectionString의* 문자열에는 **FILEDSN** 키워드가 포함되어 있지만 .dsn **파일에DRIVER** 키워드 또는 **DSN** 키워드가 포함되어 있지 않았습니다.|  
|IM014|지정된 DSN에는 드라이버와 응용 프로그램 간의 아키텍처 불일치가 포함되어 있습니다.|(DM) 32비트 애플리케이션은 64비트 드라이버에 연결하는 DSN을 사용합니다. 또는 그 반대의 경우도 마찬가지입니다.|  
|IM015|SQL_HANDLE_DBC_INFO_HANDLE 드라이버의 SQLDriverConnect가 실패했습니다.|드라이버가 SQL_ERROR 반환하면 드라이버 관리자가 SQL_ERROR 응용 프로그램에 반환하고 연결이 실패합니다.<br /><br /> SQL_HANDLE_DBC_INFO_TOKEN 대한 자세한 내용은 [ODBC 드라이버에서 연결-풀 인식 개발을](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)참조하십시오.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
|S1118|드라이버가 비동기 알림을 지원하지 않습니다.|드라이버가 비동기 알림을 지원하지 않는 경우 SQL_ATTR_ASYNC_DBC_EVENT 설정할 수 없습니다 SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="comments"></a>주석  
 연결 문자열에는 다음과 같은 구문이 있습니다.  
  
 *연결 문자열* ::= *빈 문자열*[;] &#124; *특성*[;] &#124; *특성;* *연결 문자열*  
  
 *빈 문자열* ::= 특성 ::=*특성* ::= *속성 -키워드*=*속성-값* &#124; DRIVER=[{]*특성 값*[}]  
  
 *속성 키워드* ::= DSN &#124; UID &#124; PWD &#124; *드라이버 정의-속성-키워드*  
  
 *특성 값* ::= *문자 문자열*  
  
 *드라이버 정의-특성-키워드* ::= *식별자*  
  
 *여기서 문자 문자열에* 문자가 0개 이상인 경우; *식별자에* 하나 이상의 문자가 있습니다. *특성 키워드는* 대/소문자를 구분하지 않습니다. *특성 값은* 대/소문자를 구분할 수 있습니다. **DSN** 키워드의 값은 공백으로만 구성되지 않습니다.  
  
 연결 문자열 및 초기화 파일 문법, 문자 **[]{}(;)를 포함하는 키워드 및 특성 값으로 인해? \*=!!@중괄호로** 묶이지 않는 것은 피해야 합니다. **DSN** 키워드의 값은 공백으로만 구성될 수 없으며 선행 공백을 포함해서는 안 됩니다. 시스템 정보의 문법때문에 키워드와 데이터 원본 이름은 백슬래시()\\문자를 포함할 수 없습니다.  
  
 응용 프로그램은 특성에 세미콜론(;)이 포함되어 있지 않으면 **DRIVER** 키워드 다음의 특성 값 주위에 중괄호를 추가할 필요가 없습니다. 드라이버가 받는 특성 값에 중괄호가 포함된 경우 드라이버는 중괄호를 제거하지 말고 반환된 연결 문자열의 일부여야 합니다.  
  
 중괄호 () 문자{} **[]{}(,;)를 포함하는 중괄호로 둘러싸인 DSN 또는 연결 문자열 값? \*=!@은** 드라이버에 그대로 전달됩니다. 그러나 키워드에서 이러한 문자를 사용할 때 드라이버 관리자는 파일 DSN으로 작업할 때 오류를 반환하지만 일반 연결 문자열에 대한 연결 문자열을 드라이버에 전달합니다. 키워드 값에 포함된 중괄호를 사용하지 마십시오.  
  
 연결 문자열에는 드라이버 정의 키워드의 수에 관계없이 포함될 수 있습니다. **DRIVER** 키워드는 시스템 정보의 정보를 사용하지 않으므로 드라이버는 연결 문자열의 정보만 사용하여 데이터 원본에 연결할 수 있도록 충분한 키워드를 정의해야 합니다. 자세한 내용은 이 섹션의 "운전자 지침"을 참조하십시오. 드라이버는 데이터 원본에 연결하는 데 필요한 키워드를 정의합니다.  
  
 다음 표에서는 **DSN,** **FILEDSN,** **드라이버,** **UID,** **PWD**및 **SAVEFILE** 키워드의 특성 값을 설명합니다.  
  
|키워드|특성 값 설명|  
|-------------|---------------------------------|  
|**Dsn**|**SQLDataSource** 또는 **SQLDriverConnect의**데이터 원본 대화 상자에서 반환되는 데이터 원본의 이름 입니다.|  
|**출원된 SN**|데이터 원본에 대해 연결 문자열을 빌드할 .dsn 파일의 이름입니다. 이러한 데이터 원본을 파일 데이터 원본이라고 합니다.|  
|**드라이버**|**SQLDriver** 함수에서 반환되는 드라이버에 대한 설명입니다. 예를 들어 Rdb 또는 SQL Server입니다.|  
|**UID**|사용자 ID입니다.|  
|**Pwd**|사용자 ID(PWD=;)에 대한 암호가 없는 경우 사용자 ID에 해당하는 암호 또는 빈 문자열입니다.|  
|**Savefile**|현재, 성공적인 연결을 만드는 데 사용되는 키워드의 특성 값을 저장하는 .dsn 파일의 파일 이름입니다.|  
  
 응용 프로그램이 데이터 원본 또는 드라이버를 선택하는 방법에 대한 자세한 내용은 [데이터 원본 또는 드라이버 선택을](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)참조하십시오.  
  
 연결 문자열에서 키워드가 반복되는 경우 드라이버는 키워드의 첫 번째 발생과 관련된 값을 사용합니다. **DSN** 및 **DRIVER** 키워드가 동일한 연결 문자열에 포함된 경우 드라이버 관리자와 드라이버가 먼저 표시되는 키워드를 사용합니다.  
  
 **FILEDSN** 및 **DSN** 키워드는 상호 배타적입니다. 반면, **FILEDSN** 및 **DRIVER** 키워드는 상호 배타적이지 않습니다. **FILESN이**있는 연결 문자열에 키워드가 있으면 .dsn 파일에서 동일한 키워드의 특성 값이 아니라 연결 문자열에 있는 키워드의 특성 값이 사용됩니다.  
  
 **FILEDSN** 키워드를 사용하는 경우 .dsn 파일에 지정된 키워드를 사용하여 연결 문자열을 만듭니다. 자세한 내용은 이 섹션의 다음 부분인 "파일 데이터 원본"을 참조하십시오. **UID** 키워드는 선택 사항입니다. .dsn 파일은 **DRIVER** 키워드로만 만들 수 있습니다. **PWD** 키워드는 .dsn 파일에 저장되지 않습니다. .dsn 파일을 저장하고 로드하기 위한 기본 디렉토리는 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion 및 "ODBC\DataSource"에서 **CommonFileDir이** 지정한 경로의 조합입니다. (CommonFileDir이 "C:\\프로그램 파일\일반 파일"인 경우 기본 디렉토리는 "C:\프로그램 파일\일반 파일\ODBC\데이터 원본"입니다.)  
  
> [!NOTE]  
>  .dsn 파일은 설치 프로그램 DLL에서 [SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md) 및 [SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md) 함수를 호출하여 직접 조작할 수 있습니다.  
  
 **SAVEFILE** 키워드를 사용하는 경우 현재를 만드는 데 사용된 키워드의 특성 값은 **SAVEFILE** 키워드의 특성 값의 이름과 함께 .dsn 파일로 저장됩니다. **SAVEFILE** 키워드는 **DRIVER** 키워드, **FILEDSN** 키워드 또는 둘 다와 함께 사용하거나 SQLSTATE 01S09(잘못된 키워드)를 사용하여 SQL_SUCCESS_WITH_INFO 반환해야 합니다. **SAVEFILE** 키워드는 연결 문자열의 **DRIVER** 키워드 앞에 나타나야 하며 결과가 정의되지 않습니다.  
  
## <a name="driver-manager-guidelines"></a>드라이버 관리자 가이드라인  
 드라이버 관리자는 드라이버의 **SQLDriverConnect** 함수의 *InConnectionString* 인수에서 드라이버에 전달할 연결 문자열을 생성합니다. 드라이버 관리자는 응용 프로그램에서 전달된 *InConnectionString* 인수를 수정하지 않습니다.  
  
 드라이버 관리자의 작업은 *드라이버완료* 인수의 값을 기반으로 합니다.  
  
-   SQL_DRIVER_PROMPT: 연결 문자열에 **DRIVER,** **DSN**또는 **FILEDSN** 키워드가 없는 경우 드라이버 관리자는 데이터 원본 대화 상자가 표시됩니다. 대화 상자에서 반환되는 데이터 원본 이름과 응용 프로그램에서 전달된 다른 키워드에서 연결 문자열을 생성합니다. 대화 상자에서 반환된 데이터 원본 이름이 비어 있으면 드라이버 관리자는 키워드 값 쌍 DSN=Default를 지정합니다. 이 대화 상자에는 "기본값"이라는 이름의 데이터 원본이 표시되지 않습니다.  
  
-   SQL_DRIVER_COMPLETE 또는 SQL_DRIVER_COMPLETE_REQUIRED: 응용 프로그램에서 지정한 연결 문자열에 **DSN** 키워드가 포함된 경우 드라이버 관리자는 응용 프로그램에서 지정한 연결 문자열을 복사합니다. 그렇지 않으면 *DriverCompletion이* SQL_DRIVER_PROMPT 때와 동일한 작업을 수행합니다.  
  
-   SQL_DRIVER_NOPROMPT: 드라이버 관리자는 응용 프로그램에서 지정한 연결 문자열을 복사합니다.  
  
 응용 프로그램에서 지정한 연결 문자열에 **DRIVER** 키워드가 포함된 경우 드라이버 관리자는 응용 프로그램에서 지정한 연결 문자열을 복사합니다.  
  
 드라이버 관리자는 생성한 연결 문자열을 사용하여 사용할 드라이버를 결정하고 해당 드라이버에 연결하고 생성한 연결 문자열을 드라이버에 전달합니다. 드라이버 관리자와 드라이버의 상호 작용에 대한 자세한 내용은 [SQLConnect 함수의](../../../odbc/reference/syntax/sqlconnect-function.md)"주석" 섹션을 참조하십시오. 연결 문자열에 **DRIVER** 키워드가 없는 경우 드라이버 관리자는 다음과 같이 사용할 드라이버를 결정합니다.  
  
1.  연결 문자열에 **DSN** 키워드가 포함된 경우 드라이버 관리자는 시스템 정보에서 데이터 원본과 연결된 드라이버를 검색합니다.  
  
2.  연결 문자열에 **DSN** 키워드가 없거나 데이터 원본을 찾을 수 없는 경우 드라이버 관리자는 시스템 정보에서 기본 데이터 원본과 연결된 드라이버를 검색합니다. (자세한 내용은 [기본 하위 키를](../../../odbc/reference/install/default-subkey.md)참조하십시오.) 드라이버 관리자는 연결 문자열의 **DSN** 키워드 값을 "DEFAULT"로 변경합니다.  
  
3.  연결 문자열의 **DSN** 키워드가 "DEFAULT"로 설정된 경우 드라이버 관리자는 시스템 정보에서 기본 데이터 원본과 연결된 드라이버를 검색합니다.  
  
4.  데이터 원본을 찾을 수 없고 기본 데이터 원본을 찾을 수 없는 경우 드라이버 관리자는 SQLSTATE IM002(데이터 원본을 찾을 수 없고 기본 드라이버가 지정되지 않음)를 사용하여 SQL_ERROR 반환합니다.  
  
## <a name="file-data-sources"></a>파일 데이터 원본  
 **SQLDriverConnect** 호출에서 응용 프로그램에서 지정한 연결 문자열에 **FILEDSN** 키워드가 포함되어 있고 이 키워드가 **DSN** 또는 **DRIVER** 키워드로 대체되지 않는 경우 드라이버 관리자는 .dsn 파일 및 *InConnectionString* 인수의 정보를 사용하여 연결 문자열을 만듭니다. 드라이버 관리자는 다음과 같이 진행됩니다.  
  
1.  .dsn 파일의 파일 이름이 유효한지 확인합니다. 그렇지 않은 경우 SQLSTATE IM014(잘못된 파일 DSN 이름)를 사용하지 SQL_ERROR 반환합니다. 파일 이름이 빈 문자열(""")이고 SQL_DRIVER_NOPROMPT 지정되지 않은 경우 **파일 열기** 대화 상자가 표시됩니다. 파일 이름에 유효한 경로가 포함되어 있지만 파일 이름이나 잘못된 파일 이름이 없고 SQL_DRIVER_NOPROMPT 지정되지 않은 경우 **파일 열기** 대화 상자가 현재 디렉터리 집합과 함께 파일 이름에 지정된 대화 상자가 표시됩니다. 파일 이름이 빈 문자열(""")이거나 파일 이름에 유효한 경로가 포함되어 있지만 파일 이름이나 잘못된 파일 이름이 없고 SQL_DRIVER_NOPROMPT 지정되면 SQLSTATE IM014(파일 DSN의 잘못된 이름)와 함께 SQL_ERROR 반환됩니다.  
  
2.  .dsn 파일의 [ODBC] 섹션의 모든 키워드를 읽습니다. **DRIVER** 키워드가 없는 경우 .dsn 파일을 공유할 수 없고 **DSN** 키워드만 포함하는 경우를 제외하고 SQLSTATE im012(드라이버 키워드 구문 오류)가 있는 SQL_ERROR 반환합니다.  
  
     파일 데이터 원본을 공유할 수 없는 경우 드라이버 관리자는 **DSN** 키워드의 값을 읽고 공유할 수 없는 파일 데이터 원본이 가리키는 사용자 또는 시스템 데이터 원본에 필요에 따라 연결합니다. 3단계부터 5단계까지는 수행되지 않습니다.  
  
3.  드라이버에 대한 연결 문자열을 생성합니다. 드라이버 연결 문자열은 .dsn 파일에 지정된 키워드와 원래 응용 프로그램 연결 문자열에 지정된 키워드의 결합입니다. 키워드가 겹치는 드라이버 연결 문자열을 구성하기 위한 규칙은 다음과 같습니다.  
  
    -   **DRIVER** 키워드가 응용 프로그램 연결 문자열에 있고 **DRIVER** 키워드가 .dsn 파일 및 응용 프로그램 연결 문자열에서 동일하지 않은 경우 .dsn 파일의 드라이버 정보가 무시되고 응용 프로그램 연결 문자열의 드라이버 정보가 사용됩니다. **DRIVER** 키워드로 지정된 드라이버가 .dsn 파일과 응용 프로그램의 연결 문자열에서 동일하면 모든 키워드가 겹치는 경우 응용 프로그램 연결 문자열에 지정된 드라이버가 .dsn 파일에 지정된 드라이버보다 우선합니다.  
  
    -   새 연결 문자열에서 **FILEDSN** 키워드가 제거됩니다.  
  
4.  레지스트리 항목 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST를 보고 드라이버를 로드합니다. 드라이버\\ 이름>\>드라이버 \<키워드에 의해 지정 되는 INI<드라이버 이름 \드라이버입니다. **DRIVER**  
  
5.  드라이버에 새 연결 문자열을 전달합니다.  
  
 .dsn 파일의 예는 [파일 데이터 원본을 사용하여 연결](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)참조.  
  
## <a name="savefile-keyword"></a>저장 파일 키워드  
 응용 프로그램에서 지정한 연결 문자열에 **SAVEFILE** 키워드가 포함된 경우 드라이버 관리자는 연결 문자열을 .dsn 파일에 저장합니다. 드라이버 관리자는 다음과 같이 진행됩니다.  
  
1.  **SAVEFILE** 키워드의 특성 값으로 포함된 .dsn 파일의 파일 이름이 유효한지 확인합니다. 그렇지 않은 경우 SQLSTATE IM014(잘못된 파일 DSN 이름)를 사용하지 SQL_ERROR 반환합니다. 파일 이름의 유효성은 표준 시스템 이름 지정 규칙에 의해 결정됩니다. 파일 이름이 빈 문자열("")이고 *DriverCompletion* 인수가 SQL_DRIVER_NOPROMPT 않으면 파일 이름이 유효합니다. 파일 이름이 이미 있는 경우 *DriverCompletion이* SQL_DRIVER_NOPROMPT 파일이 덮어씁니다. *DriverCompletion이* SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE 또는 SQL_DRIVER_COMPLETE_REQUIRED 경우 대화 상자는 파일을 덮어쓸지 여부를 지정하라는 메시지를 사용자에게 표시합니다. 아니요를 입력하면 **파일 저장** 대화 상자가 나타납니다.  
  
2.  드라이버가 SQL_SUCCESS 반환하고 파일 이름이 빈 문자열이 아닌 경우 드라이버 관리자는 *OutConnectionString* 인수에서 반환된 연결 정보를 이 섹션의 "연결 문자열" 섹션에 지정된 형식으로 지정된 파일에 씁니다.  
  
3.  드라이버가 SQL_SUCCESS 반환하고 파일 이름이 빈 문자열("")인 경우 드라이버 관리자는 *hwnd가* 지정된 파일 **저장** 공통 대화 상자를 호출하고 이 섹션의 "연결 문자열" 섹션의 앞에 지정된 형식과 함께 File-Save 공통 대화 상자에 지정된 파일에 *OutConnectionString에* 반환된 연결 정보를 씁니다.  
  
4.  드라이버가 SQL_SUCCESS 반환하는 경우 연결 문자열을 포함하는 *OutConnectionString* 인수를 응용 프로그램에 반환합니다.  
  
5.  드라이버가 SQL_SUCCESS_WITH_INFO 반환하거나 SQL_ERROR 경우 드라이버 관리자는 SQLSTATE를 응용 프로그램에 반환합니다.  
  
## <a name="driver-guidelines"></a>드라이버 가이드라인  
 드라이버는 드라이버 관리자에 의해 전달 된 연결 문자열 **DSN** 또는 **DRIVER** 키워드를 포함 여부를 확인 합니다. 연결 문자열에 **DRIVER** 키워드가 포함된 경우 드라이버는 시스템 정보에서 데이터 원본에 대한 정보를 검색할 수 없습니다. 연결 문자열에 **DSN** 키워드가 포함되어 있거나 **DSN** 또는 **DRIVER** 키워드가 포함되어 있지 않은 경우 드라이버는 다음과 같이 시스템 정보에서 데이터 원본에 대한 정보를 검색할 수 있습니다.  
  
1.  연결 문자열에 **DSN** 키워드가 포함된 경우 드라이버는 지정된 데이터 원본에 대한 정보를 검색합니다.  
  
2.  연결 문자열에 **DSN** 키워드가 없거나 지정된 데이터 원본을 찾을 수 없거나 **DSN** 키워드가 "DEFAULT"로 설정된 경우 드라이버는 기본 데이터 원본에 대한 정보를 검색합니다.  
  
 드라이버는 시스템 정보에서 검색한 모든 정보를 사용하여 연결 문자열에서 전달된 정보를 보강합니다. 시스템 정보의 정보가 연결 문자열의 정보를 복제하는 경우 드라이버는 연결 문자열의 정보를 사용합니다.  
  
 *드라이버완성의*값에 따라 드라이버는 사용자에게 사용자 ID 및 암호와 같은 연결 정보를 묻고 데이터 원본에 연결합니다.  
  
-   SQL_DRIVER_PROMPT: 드라이버는 연결 문자열의 값과 시스템 정보(있는 경우)를 초기 값으로 사용하여 대화 상자를 표시합니다. 사용자가 대화 상자를 종료하면 드라이버가 데이터 원본에 연결됩니다. 또한 *InConnectionString의* **DSN** 또는 **DRIVER** 키워드 값과 \*대화 상자에서 반환된 정보에서 연결 문자열을 생성합니다. 이 연결 문자열을 * OutConnectionString 버퍼에*배치합니다.*  
  
-   SQL_DRIVER_COMPLETE 또는 SQL_DRIVER_COMPLETE_REQUIRED: 연결 문자열에 충분한 정보가 포함되어 있고 해당 정보가 올바른 경우 드라이버는 \*데이터 원본에 연결하고 *InConnectionString* \* *에*복사합니다. 정보가 없거나 올바르지 않은 경우 드라이버는 *DriverCompletion이* SQL_DRIVER_COMPLETE_REQUIRED 경우 데이터 원본에 연결하는 데 필요하지 않은 정보에 대한 제어를 비활성화한다는 점을 제외하면 *DriverCompletion가* SQL_DRIVER_PROMPT 때와 동일한 작업을 수행합니다.  
  
-   SQL_DRIVER_NOPROMPT: 연결 문자열에 충분한 정보가 포함된 경우 드라이버는 데이터 원본에 연결하고 \* *InConnectionString을* \* *OutConnectionString*에 복사합니다. 그렇지 않으면 드라이버는 **SQLDriverConnect**에 대한 SQL_ERROR 반환합니다.  
  
 데이터 원본에 성공적으로 연결하면 드라이버는 \***OutConnectionString에서*반환할 수 있는 출력 연결 문자열의 길이로 *StringLength2Ptr을* 설정합니다.  
  
 사용자가 드라이버 관리자 또는 드라이버에서 제공하는 대화 상자를 취소하면 **SQLDriverConnect는** SQL_NO_DATA 반환합니다.  
  
 연결 프로세스 중에 드라이버 관리자와 드라이버가 상호 작용하는 방법에 대한 자세한 내용은 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)를 참조하십시오.  
  
 드라이버가 **SQLDriverConnect를**지원하는 경우 드라이버에 대한 시스템 정보의 드라이버 키워드 섹션에는 두 번째 문자가 "Y"로 설정된 **ConnectFunctions** 키워드가 포함되어야 합니다.  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>연결 풀링이 활성화된 경우 연결  
 연결 풀링을 사용하면 응용 프로그램이 이미 생성된 연결을 다시 사용할 수 있습니다. **SQLDriverConnect가** 호출되면 드라이버 관리자는 연결 풀링을 위해 지정된 환경에서 연결 풀의 일부인 연결을 사용하여 연결을 시도합니다. 연결 풀링에 대한 자세한 내용은 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)를 참조하십시오.  
  
 응용 프로그램은 풀링이 활성화된 연결에서 SQLDisconnect를 호출하기 전에 SQL_ATTR_RESET_CONNECTION 설정할 수 있습니다. 자세한 내용은 [SQLSetConnectAttr 함수를](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)참조하십시오.  
  
 응용 프로그램이 **SQLDriverConnect를** 호출하여 풀된 연결에 연결할 때 다음 제한 사항이 적용됩니다.  
  
-   **SAVEFILE** 키워드가 연결 문자열에 지정되면 연결 풀링 처리가 수행되지 않습니다.  
  
-   연결 풀링을 사용하도록 설정한 경우 **SQLDriverConnect는** SQL_DRIVER_NOPROMPT *드라이버완성* 인수를 통해서만 호출할 수 있습니다. **SQLDriverConnect가** 다른 드라이버 *완료와*함께 호출되면 SQLSTATE HY110(잘못된 드라이버 완료)이 반환됩니다.  
  
## <a name="connection-attributes"></a>연결 특성  
 **SQLSetConnectAttr을**사용하여 설정된 SQL_ATTR_LOGIN_TIMEOUT 연결 특성은 응용 프로그램으로 돌아가기 전에 드라이버가 성공적인 연결을 완료할 때까지 로그인 요청이 완료될 때까지 기다리는 시간(초)을 정의합니다. 사용자에게 연결 문자열을 완료하라는 메시지가 표시되면 드라이버가 연결 프로세스를 시작할 때 각 로그인 요청에 대한 대기 기간이 시작됩니다.  
  
 드라이버는 기본적으로 SQL_MODE_READ_WRITE 액세스 모드에서 연결을 엽니다. 액세스 모드를 SQL_MODE_READ_ONLY 하려면 응용 프로그램은 **SQLDriverConnect**를 호출하기 전에 SQL_ATTR_ACCESS_MODE 특성을 사용하여 **SQLSetConnectAttr을** 호출해야 합니다.  
  
 데이터 원본의 시스템 정보에 기본 변환 라이브러리가 지정되면 드라이버가 로드합니다. **sqlSetConnectAttr을** SQL_ATTR_TRANSLATE_LIB 특성으로 호출하여 다른 번역 라이브러리를 로드할 수 있습니다. 변환 옵션은 SQL_ATTR_TRANSLATE_OPTION 옵션으로 **SQLSetConnectAttr을** 호출하여 지정할 수 있습니다.  
  
 자세한 내용은 [SQLDriverConnect 연결](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)을 참조하십시오.  
  
```cpp  
// SQLDriverConnect_ref.cpp  
// compile with: odbc32.lib user32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
  
   SQLCHAR OutConnStr[255];  
   SQLSMALLINT OutConnStrLen;  
  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            retcode = SQLDriverConnect( // SQL_NULL_HDBC  
               hdbc,   
               desktopHandle,   
               (SQLCHAR*)"driver=SQL Server",   
               _countof("driver=SQL Server"),  
               OutConnStr,  
               255,   
               &OutConnStrLen,  
               SQL_DRIVER_PROMPT );  
  
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
  
 또한 [샘플 ODBC 프로그램을](../../../odbc/reference/sample-odbc-program.md)참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|데이터 원본에 연결하는 데 필요한 값 검색 및 확대|[SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|데이터 원본에 연결|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|데이터 원본연결 해제|[SQLDisconnect 함수](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|드라이버 설명 및 특성 반환|[SQLDrivers 함수](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|손잡이 해제|[SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|연결 특성 설정|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
