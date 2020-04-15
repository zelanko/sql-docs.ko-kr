---
title: SQL브라우오커커 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBrowseConnect
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBrowseConnect
helpviewer_keywords:
- SQLBrowseConnect function [ODBC]
ms.assetid: b7f1be66-e6c7-4790-88ec-62b7662103c0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 607b0d764a694098a23111e9d7f4ce9755ea982d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301343"
---
# <a name="sqlbrowseconnect-function"></a>SQLBrowseConnect 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ODBC  
  
 **요약**  
 **SQLBrowseConnect는** 데이터 원본에 연결하는 데 필요한 특성 및 특성 값을 검색하고 등록하는 반복적인 방법을 지원합니다. **SQLBrowseConnect에** 대한 각 호출은 연속적인 수준의 특성 및 특성 값을 반환합니다. 모든 수준이 등록되면 데이터 원본에 대한 연결이 완료되고 **SQLBrowseConnect**에서 전체 연결 문자열이 반환됩니다. SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 반환 코드는 모든 연결 정보가 지정되었으며 응용 프로그램이 이제 데이터 원본에 연결되어 있음을 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLBrowseConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr);  
```  
  
## <a name="arguments"></a>인수  
 *연결 핸들*  
 [Input] 연결 핸들입니다.  
  
 *인커넥션 스트링*  
 [입력] 요청 연결 문자열을 찾아봅니다("주석"의 *"InConnectionString* 인수"참조).  
  
 *문자열 길이1*  
 [입력] * 문자의*연결 문자열의* 길이입니다.  
  
 *아웃커넥션 스트링*  
 [출력] 찾아보기 결과 연결 문자열을 반환할 문자 버퍼에 대한 포인터("주석"의 *"OutConnectionString* 인수" 참조).  
  
 *OutConnectionString이* NULL인 경우 *StringLength2Ptr은* *OutConnectionString에서*가리키는 버퍼에서 반환할 수 있는 총 문자 수(문자 데이터에 대한 null 종료 문자 제외)를 반환합니다.  
  
 *버퍼 길이*  
 [입력] **OutConnectionString* 버퍼의 길이(문자)입니다.  
  
 *문자열길이2Ptr*  
 [출력] \* *OutConnectionString에서*반환할 수 있는 총 문자 수(널 종료 제외)입니다. 반환할 수 있는 문자 수가 *BufferLength보다*크거나 같으면 \* *OutConnectionString의* 연결 문자열이 *BufferLength에* 잘려null 종료 문자의 길이를 뺀 값입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_ERROR, SQL_INVALID_HANDLE 또는 SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>진단  
 **SQLBrowseConnect** SQL_ERROR, SQL_SUCCESS_WITH_INFO 또는 SQL_NEED_DATA 반환하는 경우 *SQL_HANDLE_STMT 핸들 유형* 및 연결 *핸들*핸들을 사용하는 **SQLGetDiagRec을** 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 **SQLBrowseConnect에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|버퍼 \* *OutConnectionString* 전체 찾아보기 결과 연결 문자열을 반환 하기에 충분 하지 않은 문자열이 잘렸습니다. 버퍼 **StringLength2Ptr에는* 잘린 찾아보기 결과 연결 문자열의 길이가 포함되어 있습니다. (함수는 SQL_NEED_DATA 반환합니다.)|  
|01S00|잘못된 연결 문자열 특성|잘못된 특성 키워드가 찾아보기 요청 연결*문자열(InConnectionString)에*지정되었습니다. (함수는 SQL_NEED_DATA 반환합니다.)<br /><br /> 현재 연결 수준에 적용되지 않는 찾아보기 요청 연결*문자열(InConnectionString)에*특성 키워드가 지정되었습니다. (함수는 SQL_NEED_DATA 반환합니다.)|  
|01S02|값이 변경되었습니다.|드라이버는 **SQLSetConnectAttr에서** *ValuePtr* 인수의 지정된 값을 지원 하지 않고 비슷한 값을 대체 했습니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08001|연결을 설정할 수 없는 클라이언트|드라이버가 데이터 원본과 연결을 설정할 수 없습니다.|  
|08002|사용 중 연결 이름|(DM) 지정된 연결이 이미 데이터 원본과의 연결을 설정하는 데 사용되었으며 연결이 열려 있습니다.|  
|08004|서버가 연결을 거부했습니다.|데이터 원본은 구현 정의 이유로 연결 의 설치를 거부했습니다.|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결을 시도하려는 데이터 원본 간의 통신 링크가 실패했습니다.|  
|28000|잘못된 권한 부여 사양|찾아보기 요청 연결*문자열(InConnectionString)에*지정된 사용자 식별자 또는 권한 부여 문자열 또는 둘 다 데이터 원본에서 정의한 제한을 위반했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|(DM) 드라이버 관리자가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.<br /><br /> 드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|[SQLCancelHandle 함수를](../../../odbc/reference/syntax/sqlcancelhandle-function.md)호출하여 비동기 작업이 취소되었습니다. 그런 다음 원래 함수가 *연결 핸들*에서 다시 호출되었습니다.<br /><br /> 다중 스레드 응용 프로그램의 다른 스레드에서 *ConnectionHandle에서* **SQLCancelHandle을** 호출하여 작업이 취소되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) 비동기적으로 실행 되는 함수 (이 하나) *연결 핸들에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) *인수 StringLength1에* 대해 지정된 값은 0보다 크고 SQL_NTS 같지 않았습니다.<br /><br /> (DM) 인수 *BufferLength에* 대해 지정된 값이 0보다 적습니다.|  
|HY14|드라이버 연결 수준 비동기 함수 실행을 지원 하지 않습니다.|(DM) 응용 프로그램은 연결을 하기 전에 연결 핸들에서 비동기 작업을 사용하도록 설정했습니다. 그러나 드라이버는 연결 핸들에서 비동기 작업을 지원하지 않습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에 대한 연결이 완료되기 전에 로그인 시간 시간 만료 기간이 만료되었습니다. 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT 통해 설정됩니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) 지정된 데이터 원본 이름에 해당하는 드라이버가 함수를 지원하지 않습니다.|  
|IM002|데이터 원본을 찾을 수 없으며 기본 드라이버가 지정되지 않았습니다.|(DM) 찾아보기 요청 연결 문자열 *(InConnectionString)에*지정된 데이터 원본 이름이 시스템 정보에서 찾을 수 없으며 기본 드라이버 사양이 없습니다.<br /><br /> (DM) ODBC 데이터 원본 및 기본 드라이버 정보를 시스템 정보에서 찾을 수 없습니다.|  
|IM003|지정된 드라이버를 로드할 수 없습니다.|(DM) 시스템 정보의 데이터 원본 사양에 나열되거나 **DRIVER** 키워드에 의해 지정된 드라이버를 찾을 수 없거나 다른 이유로 로드할 수 없습니다.|  
|IM004|SQL_HANDLE _ENV 드라이버의 **SQLAllocHandle** 실패|(DM) **SQLBrowseConnect**동안 드라이버 관리자는 *핸들 유형SQL_HANDLE_ENV* 드라이버의 **SQLAllocHandle** 함수를 호출하고 드라이버가 오류를 반환했습니다.|  
|IM005|SQL_HANDLE_DBC 드라이버의 **SQLAllocHandle실패**|(DM) **SQLBrowseConnect**동안 드라이버 관리자는 *핸들 유형* SQL_HANDLE_DBC 드라이버의 **SQLAllocHandle** 함수를 호출하고 드라이버가 오류를 반환했습니다.|  
|IM006|드라이버의 **SQLSetConnectAttr** 실패|(DM) **SQLBrowseConnect**동안 드라이버 관리자는 드라이버의 **SQLSetConnectAttr** 함수를 호출하고 드라이버가 오류를 반환했습니다.|  
|IM009|번역 DLL을 로드할 수 없음|드라이버가 데이터 원본 또는 연결에 대해 지정된 변환 DLL을 로드할 수 없습니다.|  
|IM010|데이터 원본 이름이 너무 깁니다.|(DM) DSN 키워드의 특성 값이 SQL_MAX_DSN_LENGTH 문자보다 길다.|  
|IM011|드라이버 이름이 너무 깁니다.|(DM) DRIVER 키워드의 속성 값이 255자보다 길다.|  
|IM012|DRIVER 키워드 구문 오류|(DM) DRIVER 키워드의 키워드 값 쌍에는 구문 오류가 포함되어 있습니다.|  
|IM014|지정된 DSN에는 드라이버와 응용 프로그램 간의 아키텍처 불일치가 포함되어 있습니다.|(DM) 32비트 애플리케이션은 64비트 드라이버에 연결하는 DSN을 사용합니다. 또는 그 반대의 경우도 마찬가지입니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
|S1118|드라이버가 비동기 알림을 지원하지 않습니다.|드라이버가 비동기 알림을 지원하지 않는 경우 SQL_ATTR_ASYNC_DBC_EVENT 설정할 수 없습니다 SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="inconnectionstring-argument"></a>인커넥션스트링 인수  
 찾아보기 요청 연결 문자열에는 다음과 같은 구문이 있습니다.  
  
 *연결 문자열* ::=`;` *특성*[ ] &#124; *특성* `;` *연결 문자열;*<br>
 *속성* ::= *속성-키워드*`=`*속성-값* `DRIVER=`&#124;`{`[ ] 속성*값*[ ]`}`<br>
 *속성 키워드* ::= `DSN` `UID` &#124; `PWD` &#124; *드라이버 정의-속성-키워드&#124;*<br>
 *특성 값* ::= *문자 문자열*<br>
 *드라이버 정의-특성-키워드* ::= *식별자*<br>
  
 *여기서 문자 문자열에* 문자가 0개 이상인 경우; *식별자에* 하나 이상의 문자가 있습니다. *특성 키워드는* 대/소문자를 구분하지 않습니다. *특성 값은* 대/소문자를 구분할 수 있습니다. **DSN** 키워드의 값은 공백으로만 구성되지 않습니다. 연결 문자열 및 초기화 파일 문법, 문자 **[]{}(;)를 포함하는 키워드 및 특성 값으로 인해? \*=!@은** 피해야 합니다. 시스템 정보의 문법때문에 키워드와 데이터 원본 이름은 백슬래시()\\문자를 포함할 수 없습니다. ODBC 2. *x* 드라이버, 중괄호는 DRIVER 키워드의 특성 값 주위에 필요합니다.  
  
 찾아보기 요청 연결 문자열에서 키워드가 반복되는 경우 드라이버는 키워드의 첫 번째 발생과 관련된 값을 사용합니다. **DSN** 및 **DRIVER** 키워드가 동일한 찾아보기 요청 연결 문자열에 포함된 경우 드라이버 관리자와 드라이버는 어떤 키워드가 먼저 나타나는지 사용합니다.  
  
 응용 프로그램이 데이터 원본 또는 드라이버를 선택하는 방법에 대한 자세한 내용은 [데이터 원본 또는 드라이버 선택을](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)참조하십시오.  
  
## <a name="outconnectionstring-argument"></a>아웃커넥션스트링 인수  
 찾아보기 결과 연결 문자열은 연결 특성 목록입니다. 연결 특성은 특성 키워드와 해당 특성 값으로 구성됩니다. 찾아보기 결과 연결 문자열에는 다음과 같은 구문이 있습니다.  
  
 *연결 문자열* ::=`;` *특성*[ ] &#124; *특성* `;` *연결 문자열*<br>
 *속성* :=[`*`]*속성 키워드*`=`*특성-값*<br>
 *속성 키워드* ::= *ODBC-특성 키워드* &#124; 드라이버 *정의-속성-키워드*<br>
 *ODBC-attribute-keyword* =`UID` `PWD`{&#124;`:`}[*지역화 식별자]* *드라이버 정의-특성-키워드* ::= *식별자*`:`*[지역화 식별자]* *특성 값* ::= `{` *특성-값-목록* `}` &#124; `?` (중괄호는 리터럴이며 드라이버에 의해 반환됩니다.)<br>
 *속성 값 목록* ::= 문자`:` *문자열* [*지역화된 문자 문자열]*&#124; *문자 문자열* [`:`*지역화된 문자 문자열]* `,` *특성 값 목록*<br>
  
 *여기서 문자 문자열* 및 *지역화된 문자 문자열에* 0 개 이상의 문자가 있습니다. *식별자* 및 *지역화된 식별자에는* 하나 이상의 문자가 있습니다. *특성 키워드는* 대/소문자를 구분하지 않습니다. 및 *특성 값은* 대/소문자를 구분할 수 있습니다. 연결 문자열 및 초기화 파일 문법, 키워드, 지역화된 식별자 및 문자가 포함된 특성 값으로 인해 **[]{}(;;)? \*=!@은** 피해야 합니다. 시스템 정보의 문법때문에 키워드와 데이터 원본 이름은 백슬래시()\\문자를 포함할 수 없습니다.  
  
 찾아보기 결과 연결 문자열 구문은 다음 의미 체계 규칙에 따라 사용됩니다.  
  
-   별표 ()\*앞에 특성 *키워드가*앞에 오면 *특성은* 선택 사항이며 **SQLBrowseConnect**에 대한 다음 호출에서 생략할 수 있습니다.  
  
-   속성 키워드 **UID** 및 **PWD는** **SQLDriverConnect**에 정의된 것과 동일한 의미를 갖습니다.  
  
-   *드라이버 정의 특성 키워드는* 특성 값이 제공될 수 있는 특성의 종류를 지정합니다. 예를 들어 **서버,** **데이터베이스,** **호스트**또는 **DBMS**일 수 있습니다.  
  
-   *ODBC-속성 키워드* 및 *드라이버 정의-속성-키워드에는* 지역화된 또는 사용자 친화적인 키워드 버전이 포함됩니다. 응용 프로그램에서 대화 상자의 레이블로 사용할 수 있습니다. 그러나 검색 요청 문자열을 드라이버에 전달할 때 **UID,** **PWD**또는 *식별자만* 사용해야 합니다.  
  
-   *{특성-값-목록*}는 해당 *특성 키워드에*유효한 실제 값의 열거형입니다. 중괄호 (){}는 선택 사항 목록을 나타내지 않습니다. 드라이버가 반환합니다. 예를 들어 서버 이름 목록 또는 데이터베이스 이름 목록일 수 있습니다.  
  
-   특성 *값이* 단일 물음표(?)인 경우 단일 값은 *속성 키워드에*해당합니다. 예를 들어, UID=JohnS; PWD = 참깨.  
  
-   **SQLBrowseConnect에** 대한 각 호출은 연결 프로세스의 다음 수준을 충족하는 데 필요한 정보만 반환합니다. 드라이버는 상태 정보를 연결 핸들과 연결하여 각 호출에서 항상 컨텍스트를 결정할 수 있도록 합니다.  
  
## <a name="using-sqlbrowseconnect"></a>SQL브라우지커넥트 사용  
 **SQLBrowseConnect는** 할당된 연결이 필요합니다. Driver Manager는 초기 찾아보기 요청 연결 문자열에 지정된 데이터 원본 이름에 해당하는 드라이버를 로드합니다. 이 발생 시기에 대 한 자세한 내용은 [SQLConnect 함수의](../../../odbc/reference/syntax/sqlconnect-function.md)"주석" 섹션을 참조 하십시오. 드라이버는 브라우징 과정에서 데이터 원본과 연결을 설정할 수 있습니다. **SQLBrowseConnect가** SQL_ERROR 반환하면 미해결 연결이 종료되고 연결이 연결되지 않은 상태로 반환됩니다.  
  
> [!NOTE]  
>  **SQLBrowseConnect는** 연결 풀링을 지원하지 않습니다. 연결 풀링을 사용하도록 설정한 상태에서 **SQLBrowseConnect가** 호출되면 SQLSTATE HY000(일반 오류)이 반환됩니다.  
  
 **SQLBrowseConnect가** 연결에서 처음으로 호출되는 경우 찾아보기 요청 연결 문자열에는 **DSN** 키워드 또는 **DRIVER** 키워드가 포함되어야 합니다. 찾아보기 요청 연결 문자열에 **DSN** 키워드가 포함된 경우 드라이버 관리자는 시스템 정보에서 해당 데이터 원본 사양을 찾습니다.  
  
-   드라이버 관리자가 해당 데이터 원본 사양을 찾으면 연결된 드라이버 DLL을 로드합니다. 드라이버는 시스템 정보에서 데이터 원본에 대한 정보를 검색할 수 있습니다.  
  
-   드라이버 관리자가 해당 데이터 원본 사양을 찾을 수 없는 경우 기본 데이터 원본 사양을 찾고 관련 드라이버 DLL을 로드합니다. 드라이버는 시스템 정보에서 기본 데이터 원본에 대한 정보를 검색할 수 있습니다. "기본값"은 DSN의 드라이버에 전달됩니다.  
  
-   드라이버 관리자가 해당 데이터 원본 사양을 찾을 수 없고 기본 데이터 원본 사양이 없는 경우 SQLSTATE IM002(데이터 원본을 찾을 수 없고 기본 드라이버가 지정되지 않음)를 사용하여 SQL_ERROR 반환합니다.  
  
 찾아보기 요청 연결 문자열에 **DRIVER** 키워드가 포함된 경우 드라이버 관리자는 지정된 드라이버를 로드합니다. 시스템 정보에서 데이터 원본을 찾으려고 시도하지 않습니다. **DRIVER** 키워드는 시스템 정보의 정보를 사용하지 않으므로 드라이버는 찾아보기 요청 연결 문자열의 정보만 사용하여 데이터 원본에 연결할 수 있도록 충분한 키워드를 정의해야 합니다.  
  
 **SQLBrowseConnect에**대한 각 호출에서 응용 프로그램은 찾아보기 요청 연결 문자열의 연결 특성 값을 지정합니다. 드라이버는 찾아보기 결과 연결 문자열에서 연속적인 수준의 특성 및 특성 값을 반환합니다. 찾아보기 요청 연결 문자열에 아직 기거되지 않은 연결 특성이 있는 한 SQL_NEED_DATA 반환합니다. 응용 프로그램은 찾아보기 결과 연결 문자열의 내용을 사용하여 **다음 SQLBrowseConnect**에 대한 다음 호출에 대한 찾아보기 요청 연결 문자열을 작성합니다. 모든 필수 *특성(OutConnectionString* 인수의 별표 앞에 있지 않은 특성)은 **SQLBrowseConnect**에 대한 다음 호출에 포함되어야 합니다. 응용 프로그램은 현재 찾아보기 요청 연결 문자열을 빌드할 때 이전 찾아보기 결과 연결 문자열의 내용을 사용할 수 없습니다. 즉, 이전 수준에서 설정된 특성에 대해 다른 값을 지정할 수 없습니다.  
  
 모든 연결 수준과 관련 특성이 등록되면 드라이버는 SQL_SUCCESS 반환하고 데이터 원본에 대한 연결이 완료되고 전체 연결 문자열이 응용 프로그램에 반환됩니다. 연결 문자열은 **SQLDriverConnect와**함께 다른 연결을 설정하는 SQL_DRIVER_NOPROMPT 옵션과 함께 사용하기에 적합합니다. 그러나 전체 연결 문자열은 **SQLBrowseConnect에**대한 다른 호출에서 사용할 수 없습니다. **SQLBrowseConnect가** 다시 호출된 경우 전체 호출 시퀀스를 반복해야 합니다.  
  
 **또한 SQLBrowseConnect는** 찾아보기 프로세스 중에 복구 할 수있는 치명적이지 않은 오류가있는 경우 SQL_NEED_DATA 반환합니다. 예를 들어 응용 프로그램에서 제공하는 잘못된 암호 또는 특성 키워드입니다. SQL_NEED_DATA 반환되고 찾아보기 결과 연결 문자열이 변경되지 않으면 오류가 발생했으며 응용 프로그램에서 **SQLGetDiagRec을** 호출하여 SQLSTATE를 호출하여 찾아보기 시간 오류에 대해 반환할 수 있습니다. 이렇게 하면 응용 프로그램이 특성을 수정하고 찾아보기를 계속할 수 있습니다.  
  
 응용 프로그램은 **SQLDisconnect**를 호출하여 언제든지 찾아보기 프로세스를 종료할 수 있습니다. 드라이버는 미해결 연결을 종료하고 연결이 연결되지 않은 상태로 연결됩니다.  
  
 연결 핸들에서 비동기 작업을 사용하도록 설정하면 **SQLBrowseConnect가** SQL_STILL_EXECUTING 반환할 수도 있습니다. SQL_NEED_DATA 반환하는 경우 응용 프로그램은 **SQLDisconnect를** 사용하여 찾아보기 프로세스를 취소해야 합니다. **SQLBrowseConnect가** SQL_STILL_EXECUTING 반환하는 경우 응용 프로그램은 **SQLCancelHandle을** 사용하여 진행 중인 작업을 취소해야 합니다. 함수가 반환된 후 **SQLCancelHandle을** 호출하면 SQL_NEED_DATA 영향을 주지 않습니다.  
  
 자세한 내용은 [SQLBrowseConnect 연결](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)을 참조하십시오.  
  
 드라이버가 **SQLBrowseConnect를**지원하는 경우 드라이버의 시스템 정보의 드라이버 키워드 섹션에는 세 번째 문자가 "Y"로 설정된 **ConnectFunctions** 키워드가 포함되어야 합니다.  
  
## <a name="code-example"></a>코드 예  
  
> [!NOTE]  
>  Windows 인증을 지원하는 데이터 원본 공급자에 연결하는 경우 `Trusted_Connection=yes` 연결 문자열에서 사용자 ID 및 암호 정보 대신 지정해야 합니다.  
  
 다음 예제에서 응용 프로그램은 **SQLBrowseConnect를** 반복적으로 호출합니다. **SQLBrowseConnect가** SQL_NEED_DATA 반환할 때마다 \* *OutConnectionString*에 필요한 데이터에 대한 정보를 다시 전달합니다. 응용 프로그램은 *OutConnectionString을* 일상적인 **GetUserInput(표시되지** 않음)에 전달합니다. **GetUserInput** 정보를 구문 분석, 빌드 하 고 대화 상자를 표시 하 고 \* *InConnectionString에서*사용자가 입력 한 정보를 반환 합니다. 응용 프로그램은 **SQLBrowseConnect**에 대한 다음 호출에서 드라이버에 사용자의 정보를 전달합니다. 응용 프로그램이 드라이버가 데이터 원본에 연결하는 데 필요한 모든 정보를 제공한 후 **SQLBrowseConnect는** SQL_SUCCESS 반환하고 응용 프로그램이 진행됩니다.  
  
 **SQLBrowseConnect를**호출하여 SQL Server 드라이버에 연결하는 자세한 예제는 [SQL Server 브라우징 예제를](../../../odbc/reference/develop-app/sql-server-browsing-example.md)참조하십시오.  
  
 예를 들어 데이터 원본 Sales에 연결하려면 다음 작업이 발생할 수 있습니다. 첫째, 응용 프로그램은 다음 문자열을 **SQLBrowseConnect에**전달합니다.  
  
```  
"DSN=Sales"  
```  
  
 드라이버 관리자는 데이터 원본 Sales와 연결된 드라이버를 로드합니다. 그런 다음 응용 프로그램에서 받은 것과 동일한 인수로 드라이버의 **SQLBrowseConnect** 함수를 호출합니다. 드라이버는 **OutConnectionString에서*다음 문자열을 반환합니다.  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 응용 프로그램은 이 문자열을 **GetUserInput** 루틴에 전달하여 사용자에게 빨간색, 파란색 또는 녹색 서버를 선택하고 사용자 ID와 암호를 입력하도록 요청하는 대화 상자를 빌드합니다. 루틴은 응용 프로그램이 \* **SQLBrowseConnect에**전달하는 *InConnectionString에서*다음 사용자 지정 정보를 다시 전달합니다.  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect** 는 이 정보를 사용하여 암호 참깨를 사용하여 스미스로 빨간색 서버에 연결한 다음 **OutConnectionString:*  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 응용 프로그램은 이 문자열을 **GetUserInput** 루틴에 전달하여 사용자에게 데이터베이스를 선택하도록 요청하는 대화 상자를 빌드합니다. 사용자는 empdata를 선택하고 응용 프로그램은 이 문자열을 사용하여 **SQLBrowseConnect를** 마지막으로 호출합니다.  
  
```  
"DATABASE=SalesOrders"  
```  
  
 이것은 드라이버가 데이터 원본에 연결하는 데 필요한 마지막 정보입니다. **SQLBrowseConnect는** SQL_SUCCESS 반환하고 **OutConnectionString에는* 완료된 연결 문자열이 포함되어 있습니다.  
  
```cpp  
// SQLBrowseConnect_Function.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define BRWS_LEN 100  
SQLHENV henv;  
SQLHDBC hdbc;  
SQLHSTMT hstmt;  
SQLRETURN retcode;  
SQLCHAR szConnStrIn[BRWS_LEN], szConnStrOut[BRWS_LEN];  
SQLSMALLINT cbConnStrOut;  
  
void GetUserInput(SQLCHAR * szConnStrOut, SQLCHAR * szConnStrIn) {}  
  
int main() {  
   // Allocate the environment handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);        
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
      // Set the version environment attribute.  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
         // Allocate the connection handle.  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            // Call SQLBrowseConnect until it returns a value other than SQL_NEED_DATA   
            // (pass data source name the first time).  If SQL_NEED_DATA is returned, call GetUserInput   
            // (not shown) to build a dialog from the values in szConnStrOut.  The user-supplied values   
            // are returned in szConnStrIn, which is passed in the next call to SQLBrowseConnect.  
  
            strcpy_s((char*)szConnStrIn, _countof(szConnStrIn), "DSN=Sales");  
            do {  
               retcode = SQLBrowseConnect(hdbc, szConnStrIn, SQL_NTS,  
                  szConnStrOut, BRWS_LEN, &cbConnStrOut);  
               if (retcode == SQL_NEED_DATA)  
                  GetUserInput(szConnStrOut, szConnStrIn);  
            } while (retcode == SQL_NEED_DATA);  
  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
               // Allocate the statement handle.  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                  // Process data after successful connection  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               SQLDisconnect(hdbc);  
            }  
         }  
         SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
      }  
   }  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|연결 핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|데이터 원본에 연결|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|데이터 원본연결 해제|[SQLDisconnect 함수](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|연결 문자열 또는 대화 상자를 사용하여 데이터 원본에 연결|[SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|드라이버 설명 및 특성 반환|[SQLDrivers 함수](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|연결 핸들 해제|[SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
