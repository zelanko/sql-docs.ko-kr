---
title: SQLBrowseConnect 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3af78971a17035091ab8a72bf0c9a8fe90250dd3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65538185"
---
# <a name="sqlbrowseconnect-function"></a>SQLBrowseConnect 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. ODBC  
  
 **요약**  
 **SQLBrowseConnect** 검색 하 고 특성 및 데이터 원본에 연결 하는 데 필요한 특성 값을 열거 하는 반복적인 방법을 지원 합니다. 호출할 때마다 **SQLBrowseConnect** 연속 수준의 특성 및 특성 값을 반환 합니다. 모든 수준 열거 된, 데이터 원본에 연결을 완료 된 후 전체 연결 문자열을 반환한 **SQLBrowseConnect**합니다. SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 반환 코드는 모든 연결 정보를 지정 하 고 응용 프로그램은 이제 데이터 원본에 연결을 나타냅니다.  
  
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
 *ConnectionHandle*  
 [Input] 연결 핸들입니다.  
  
 *InConnectionString*  
 [입력] 요청 연결 문자열을 찾습니다 (참조 "*InConnectionString* 인수"에서 "설명").  
  
 *StringLength1*  
 [입력] 길이 **InConnectionString* 문자에서입니다.  
  
 *OutConnectionString*  
 [출력] 찾아보기 결과 연결 문자열을 반환 하는 문자 버퍼에 대 한 포인터 (참조 "*OutConnectionString* 인수"에서 "설명").  
  
 하는 경우 *OutConnectionString* 가 null 인 경우 *StringLength2Ptr* (문자 데이터에 대 한 null 종료 문자를 제외한) 문자의 총 수를 반환 여전히는 버퍼에서 반환할 사용 가능한 가 가리키는 *OutConnectionString*합니다.  
  
 *BufferLength*  
 [입력] 문자에서 길이의 **OutConnectionString* 버퍼입니다.  
  
 *StringLength2Ptr*  
 [출력] 문자 (제외 null 종료)에서 반환할 사용 가능한 총 \* *OutConnectionString*합니다. 반환할 사용 가능한 문자 개수 보다 크거나 같은 경우 *BufferLength*에서 연결 문자열 \* *OutConnectionString* 잘립니다  *BufferLength* null 종료 문자 길이 뺀 값입니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_ERROR, SQL_INVALID_HANDLE, 또는 SQL_STILL_EXECUTING 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLBrowseConnect** SQL_ERROR, SQL_SUCCESS_WITH_INFO 또는 SQL_NEED_DATA 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여를 *HandleType* 호출의와 *ConnectionHandle 핸들*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLBrowseConnect** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|버퍼 \* *OutConnectionString* 충분히 잘렸습니다 하므로 전체 검색 결과 문자열을 반환할 수 없습니다. 버퍼 **StringLength2Ptr* 잘리지 않은 찾아보기 결과 문자열의 길이 포함 합니다. (함수는 SQL_NEED_DATA를 반환합니다.)|  
|01S00|잘못 된 연결 문자열 특성입니다.|잘못 된 특성 키워드 찾아보기 요청 연결 문자열에 지정 된 (*InConnectionString*). (함수는 SQL_NEED_DATA를 반환합니다.)<br /><br /> 특성 키워드 찾아보기 요청 연결 문자열에 지정 된 (*InConnectionString*)는 현재 연결 수준에 적용 되지 않습니다. (함수는 SQL_NEED_DATA를 반환합니다.)|  
|01S02|값이 변경 됨|드라이버의 지정된 된 값을 지원 하지 않았습니다 합니다 *ValuePtr* 에서 인수 **SQLSetConnectAttr** 유사한 값을 대체 합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08001|클라이언트를 연결할 수 없습니다.|드라이버는 데이터 원본과 연결을 설정할 수 없습니다.|  
|08002|연결 이름 사용|(DM) 지정된 된 연결 이미 사용한 데이터 원본에 연결 및 연결 되어 있습니다.|  
|08004|서버 연결을 거부 했습니다.|데이터 원본 연결의 설정 구현 시 정의 된 이유로 인해 거부 합니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 연결을 시도 된 드라이버는 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|28000|잘못 된 권한 부여 사양|사용자 id 나 권한 부여 문자열 또는 찾아보기에 지정 된 대로 둘 다 요청 연결 문자열 (*InConnectionString*), 데이터 원본에 의해 정의 된 제한을 위반 합니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|(DM) The Driver Manager 함수 완료 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.<br /><br /> 드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 작업을 호출 하 여 취소 되었습니다 [SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md)합니다. 그런 다음 원래 함수에서 다시 호출 된 합니다 *ConnectionHandle*합니다.<br /><br /> 작업을 호출 하 여 취소 되었습니다 **SQLCancelHandle** 에 *ConnectionHandle* 다중 스레드 응용 프로그램에서 다른 스레드에서 합니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *ConnectionHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|인수에 대 한 지정 된 값 (DM) *StringLength1* 0 보다 작은 및 SQL_NTS이 아닙니다.<br /><br /> 인수에 대 한 지정 된 값 (DM) *BufferLength* 0 보다 작습니다.|  
|HY114|드라이버는 연결 수준 비동기 함수 실행을 지원 하지 않습니다.|(DM) 응용 프로그램 연결 핸들에 연결 하기 전에 비동기 작업을 사용할 수 있습니다. 그러나 드라이버는 연결 핸들에서 비동기 작업을 지원 하지 않습니다.|  
|HYT00|제한 시간이 만료되었습니다.|완료 된 데이터 원본에 연결 하기 전에 로그인 제한 시간이 만료 되었습니다. 시간 제한 기간을 통해 설정 됩니다 **SQLSetConnectAttr**을 SQL_ATTR_LOGIN_TIMEOUT입니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 지정 된 데이터 원본 이름에 해당 하는 드라이버가 함수를 지원 하지 않습니다.|  
|IM002|데이터 원본을 찾을 수 없습니다 및 없습니다 지정 하지 않았습니다.|(DM) 데이터 원본 찾아보기 요청 연결 문자열에 지정 된 이름 (*InConnectionString*) 시스템 정보를 찾을 수 없습니다도 기본 드라이버 사양 없었습니다.<br /><br /> (DM) 시스템 정보에 ODBC 데이터 원본 및 기본 드라이버 정보를 찾을 수 없습니다.|  
|IM003|지정 된 드라이버를 로드할 수 없습니다.|(DM) 드라이버의 시스템 정보를 데이터 원본 사양에 나열 된 또는 지정 된 된 **드라이버** 키워드 찾을 수 없거나 다른 이유로 로드할 수 없습니다.|  
|IM004|운전 **SQLAllocHandle** SQL_HANDLE _ENV 실패에서|(DM) 하는 동안 **SQLBrowseConnect**, 드라이버 관리자가 드라이버를 호출 **SQLAllocHandle** 함수를 *HandleType* SQL_HANDLE_ENV 및 드라이버의 반환을 오류가 발생 했습니다.|  
|IM005|운전 **SQLAllocHandle** SQL_HANDLE_DBC 실패에서|(DM) 하는 동안 **SQLBrowseConnect**, 드라이버 관리자가 드라이버를 호출 **SQLAllocHandle** 함수를 *HandleType* SQL_HANDLE_DBC 및 드라이버의 반환을 오류가 발생 했습니다.|  
|IM006|운전 **SQLSetConnectAttr** 실패|(DM) 하는 동안 **SQLBrowseConnect**, 드라이버 관리자가 드라이버의 호출 **SQLSetConnectAttr** 함수 및 드라이버에서 오류를 반환 합니다.|  
|IM009|변환 DLL을 로드할 수 없습니다.|드라이버 변환 연결 또는 데이터 원본에 대 한 지정 된 DLL을 로드할 수 없습니다.|  
|IM010|데이터 원본 이름이 너무 깁니다.|(DM)는 DSN 키워드에 대 한 특성 값을 SQL_MAX_DSN_LENGTH 자를 초과 했습니다.|  
|IM011|드라이버 이름이 너무 깁니다.|(DM)는 DRIVER 키워드에 대 한 특성 값이 255 자 보다 긴 합니다.|  
|IM012|드라이버 키워드 구문 오류입니다.|(DM) DRIVER 키워드에 대 한 키워드-값 쌍에 구문 오류가 포함 되어 있습니다.|  
|IM014|지정 된 DSN은 드라이버와 응용 프로그램 간 아키텍처 불일치를 포함합니다.|64 비트 드라이버를;에 연결 하는 DSN을 사용 하 여 (DM) 32 비트 응용 프로그램 또는 그 반대의 경우도 마찬가지입니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
|S1118|드라이버 비동기 알림을 지원 하지 않습니다.|드라이버는 비동기 알림을 지원 하지 않습니다, SQL_ATTR_ASYNC_DBC_EVENT 또는 SQL_ATTR_ASYNC_DBC_RETCODE_PTR 설정할 수 없습니다.|  
  
## <a name="inconnectionstring-argument"></a>InConnectionString 인수  
 찾아보기 요청 연결 문자열에 다음 구문:  
  
 *연결 문자열* :: = *특성*[`;`] &#124; *특성* `;` *연결 문자열*;<br>
 *attribute* ::= *attribute-keyword*`=`*attribute-value* &#124; `DRIVER=`[`{`]*attribute-value*[`}`]<br>
 *attribute-keyword* ::= `DSN` &#124; `UID` &#124; `PWD` &#124; *driver-defined-attribute-keyword*<br>
 *attribute-value* ::= *character-string*<br>
 *driver-defined-attribute-keyword* ::= *identifier*<br>
  
 여기서 *문자열* 에 0 개 이상의 문자입니다. *식별자* 에 하나 이상의 문자입니다. *특성 키워드* 대/소문자 구분; 아닙니다 *특성-값* ; 대/소문자 구분 될 수 있습니다 및의 값을 **DSN** 키워드 공백 전적으로의 구성 되어 있지 않습니다. 연결 문자열 및 초기화 파일 문법, 키워드 및 특성 값의 문자를 포함 하는 때문 **{}(),? \*=! @** 하지 않아야 합니다. 시스템 정보에 대 한 문법, 인해 키워드 및 데이터 원본 이름은 백슬래시를 포함할 수 없습니다 (\\) 문자입니다. Odbc 2. *x* 드라이버를 드라이버 키워드에 대 한 특성 값을 묶는 중괄호 필요 합니다.  
  
 키워드는 찾아보기 요청 연결 문자열에서 반복 되는 경우 드라이버는 맨 처음 발견 되는 키워드를 사용 하 여 연결 된 값을 사용 합니다. 경우는 **DSN** 및 **드라이버** 키워드 동일한 찾아보기 요청 연결 문자열에 포함 된 드라이버 관리자와 드라이버 어떤 키워드가 나타나는 첫 번째를 사용 합니다.  
  
 응용 프로그램에서 데이터 원본 또는 드라이버를 선택 하는 방법에 대 한 자세한 내용은 [데이터 원본 또는 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)합니다.  
  
## <a name="outconnectionstring-argument"></a>OutConnectionString 인수  
 찾아보기 결과 문자열은 연결 특성의 목록입니다. 연결 특성을 특성 키워드와 해당 특성 값으로 구성 됩니다. 찾아보기 결과 문자열의 구문은:  
  
 *연결 문자열* :: = *특성*[`;`] &#124; *특성* `;` *연결 문자열*<br>
 *attribute* ::= [`*`]*attribute-keyword*`=`*attribute-value*<br>
 *attribute-keyword* ::= *ODBC-attribute-keyword* &#124; *driver-defined-attribute-keyword*<br>
 *ODBC 특성-키워드* = {`UID` &#124; `PWD`} [`:`*지역화 식별자*] *드라이버-정의-특성-키워드* :: = *식별자*[`:`*지역화 식별자*] *특성-값* :: = `{` *특성-값-목록* `}` &#124; `?` (중괄호는 리터럴; 드라이버에 의해 반환 됩니다.)<br>
 *특성 값 목록* :: = *문자열* [`:`*지역화 된 문자열*] &#124; *문자열* [`:` *지역화 된 문자열*] `,` *특성-값-목록*<br>
  
 여기서 *문자열* 하 고 *지역화 된 문자열* 0 개 이상의 자; *식별자* 하 고 *지역화 식별자* 하나 이상의 자; *특성 키워드* ; 대/소문자 구분 없는 및 *특성 값* 대/소문자 구분 될 수 있습니다. 연결으로 인해 문자열 초기화 파일 문법, 키워드, 지역화 된 식별자 및 문자를 포함 하는 값을 특성 **{}(),? \*=! @** 하지 않아야 합니다. 시스템 정보에 대 한 문법, 인해 키워드 및 데이터 원본 이름은 백슬래시를 포함할 수 없습니다 (\\) 문자입니다.  
  
 찾아보기 결과 연결 문자열 구문은 다음 의미 체계 규칙에 따라 사용 됩니다.  
  
-   경우에 별표 (\*) 앞에 *특성 키워드*의 *특성* 는 선택 사항이 며 다음 호출에서 생략할 수 있습니다 **SQLBrowseConnect**합니다.  
  
-   특성 키워드 **UID** 하 고 **PWD** 에 정의 된 대로 동일한 의미를 가집니다 **SQLDriverConnect**합니다.  
  
-   A *드라이버-정의-특성-키워드* 종류는 특성 값을 제공 되기도 하는 특성의 이름을 지정 합니다. 예를 들어, 수 있습니다 **SERVER**를 **데이터베이스**를 **호스트**, 또는 **DBMS**합니다.  
  
-   *ODBC 특성-키워드* 하 고 *드라이버-정의-특성-키워드* 키워드의 지역화 된 또는 친숙 한 버전을 포함 합니다. 이 대화 상자에서 레이블로 응용 프로그램에서 사용할 수 있습니다. 그러나 **UID**하십시오 **PWD**, 또는 *식별자* 단독으로 사용 해야 드라이버 찾아보기 요청 문자열을 전달 하는 경우.  
  
-   {0}*특성 값 목록*} 실제 값의 열거형을 해당 하는 것에 대 한 유효 *특성 키워드*합니다. 중괄호 ({}) 선택 목록에 나타내지 않습니다; 드라이버에 의해 반환 됩니다. 예를 들어, 데이터베이스 이름 목록을 또는 서버 이름 목록을 수 있습니다.  
  
-   경우는 *특성-값* 단일 물음표 (?)에 해당 하는 단일 값을 *특성 키워드*합니다. 예를 들어, UID JohnS; = PWD Sesame =.  
  
-   호출할 때마다 **SQLBrowseConnect** 연결 프로세스의 다음 수준을 충족 하는 데 필요한 정보만 반환 합니다. 드라이버는 각 호출에는 컨텍스트를 항상 확인할 수 있도록 연결 핸들을 사용 하 여 상태 정보를 연결 합니다.  
  
## <a name="using-sqlbrowseconnect"></a>SQLBrowseConnect를 사용 하 여  
 **SQLBrowseConnect** 할당 된 연결이 필요 합니다. 드라이버 관리자에서 지정 된 또는 초기 찾아보기 요청 연결 문자열에 지정 된 데이터 원본 이름에 해당 하는 드라이버를 로드 합니다. 이 경우에 대 한 내용은 "설명" 섹션을 참조 하세요. [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)합니다. 드라이버는 검색 프로세스 중에 데이터 소스를 사용 하 여 연결을 설정할 수 있습니다. 하는 경우 **SQLBrowseConnect** 연결이 종료 되 고 연결이 연결 되지 않은 상태로 반환 되는 처리 중인 SQL_ERROR를 반환 합니다.  
  
> [!NOTE]  
>  **SQLBrowseConnect** 연결 풀링을 지원 하지 않습니다. 하는 경우 **SQLBrowseConnect** 연결 풀링을 사용 하는 동안 호출 됩니다 SQLSTATE HY000 (일반 오류)를 반환 합니다.  
  
 때 **SQLBrowseConnect** 라고 찾아보기 요청 연결 문자열에서 연결을 처음으로 포함 해야 합니다는 **DSN** 키워드와 **드라이버** 키워드입니다. 찾아보기 요청 연결 문자열을 포함 하는 경우는 **DSN** 키워드를 드라이버 관리자 시스템 정보에 해당 하는 데이터 원본 설정을 찾습니다.  
  
-   드라이버 관리자에서 해당 데이터 원본 사양에 발견 하는 경우 관련된 드라이버 DLL; 로드 드라이버에서 시스템 정보를 데이터 원본에 대 한 정보를 검색할 수 있습니다.  
  
-   드라이버 관리자에서 해당 데이터 원본 사양을 찾을 수 없는 경우 해당 기본 데이터 원본 사양을 찾고 로드 관련된 드라이버 DLL; 드라이버는 시스템 정보에서 기본 데이터 원본에 대 한 정보를 검색할 수 있습니다. "DEFAULT" DSN에 대 한 드라이버에 전달 됩니다.  
  
-   드라이버 관리자는 해당 하는 데이터 원본 설정을 찾을 수 없습니다. 기본 데이터 원본 사양이 없으므로 SQLSTATE IM002 인 sql_error가 반환 (데이터 원본을 찾을 수 없습니다 및 지정 된 기본 드라이버가 없습니다).  
  
 찾아보기 요청 연결 문자열을 포함 하는 경우는 **드라이버** 지정한 드라이버를 로드 하는 키워드, 드라이버 관리자, 시스템 정보에는 데이터 소스를 찾으려고 시도 하지 않습니다. 때문에 합니다 **드라이버** 키워드 정보 시스템 정보를 사용 하지 않습니다, 드라이버를 드라이버 찾아보기 요청 연결 문자열에만 정보를 사용 하 여 데이터 원본에 연결할 수 있도록 충분 한 키워드를 정의 해야 합니다.  
  
 호출할 때마다 **SQLBrowseConnect**, 응용 프로그램 찾아보기 요청 연결 문자열의 연결 특성 값을 지정 합니다. 드라이버는 찾아보기 결과 연결 문자열에서는 연속 수준의 특성 및 특성 값을 반환합니다. 찾아보기 요청 연결 문자열의 열거 되지 아직 연결 특성은으로 SQL_NEED_DATA를 반환 합니다. 응용 프로그램 찾아보기 결과 문자열의 콘텐츠를 사용 하 여 다음 호출에 대 한 찾아보기 요청 연결 문자열을 빌드할 **SQLBrowseConnect**합니다. 모든 필수 특성 (별표가 앞에 오지 해당 합니다 *OutConnectionString* 인수) 다음 호출에 포함 되어야 합니다 **SQLBrowseConnect**합니다. 현재 찾아보기 요청 연결 문자열을 빌드할 때 응용 프로그램에서 이전 찾아보기 결과 연결 문자열의 콘텐츠를 사용할 수 없습니다는 note 즉, 이전 수준에서 설정 된 특성에 대해 다른 값을 지정할 수 없습니다.  
  
 연결과 연관 된 특성의 모든 수준을 열거와 관계 없이 SQL_SUCCESS를 반환 하는 드라이버, 데이터 원본에 대 한 연결이 완료 및 전체 연결 문자열은 응용 프로그램에 반환 됩니다. 연결 문자열을 함께에서 사용 하기에 적합 **SQLDriverConnect**, 다른 연결을 설정 하는 SQL_DRIVER_NOPROMPT 옵션을 사용 하 여 합니다. 전체 연결 문자열에 대 한 다른 호출에서 사용할 수 없습니다 **SQLBrowseConnect**하지만; 경우 **SQLBrowseConnect** 호출한 다시 전체 호출 시퀀스를 반복 해야 합니다.  
  
 **SQLBrowseConnect** 도 찾아보기 프로세스; 예를 들어는 잘못 된 암호 또는 응용 프로그램에서 제공 하는 특성 키워드 중 복구할 수, 치명적이 지 않은 오류가 있는 경우 SQL_NEED_DATA를 반환 합니다. 경우 SQL_NEED_DATA가 반환 하 고 찾아보기 결과 연결 문자열 변경 오류가 발생 했습니다 아니며 응용 프로그램에서 호출할 수 있습니다 **SQLGetDiagRec** SQLSTATE 탐색 시 오류를 반환 합니다. 이렇게 하면 응용 프로그램이 특성을 수정 하 고 탐색을 계속 합니다.  
  
 응용 프로그램 호출 하 여 언제 든 지 찾아보기 프로세스를 종료할 수 **SQLDisconnect**합니다. 드라이버는 모든 활성 연결을 종료 하 고 연결이 연결 되지 않은 상태로 반환 됩니다.  
  
 연결 핸들에 대해 비동기 작업을 사용 하면 **SQLBrowseConnect** SQL_STILL_EXECUTING을 반환할 수도 있습니다. SQL_NEED_DATA를 반환 하는 경우 응용 프로그램 사용 해야 합니다 **SQLDisconnect** 찾아보기 프로세스를 취소할 수 있습니다. 하는 경우 **SQLBrowseConnect** SQL_STILL_EXECUTING을 응용 프로그램 반환을 사용할지 **SQLCancelHandle** 진행 중인 작업을 취소 합니다. 호출 **SQLCancelHandle** 함수 반환 SQL_NEED_DATA 영향을 주지 않습니다.  
  
 자세한 내용은 [SQLBrowseConnect로 연결](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)합니다.  
  
 드라이버에서 지 원하는 경우 **SQLBrowseConnect**, 드라이버에 대 한 시스템 정보에서 드라이버 키워드 섹션을 포함 해야 합니다는 **ConnectFunctions** 키워드 세 번째 문자를 사용 하 여 설정에서 "Y"로 지정 합니다.  
  
## <a name="code-example"></a>코드 예  
  
> [!NOTE]  
>  지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, `Trusted_Connection=yes` 연결 문자열에 사용자 ID와 암호 정보 대신 합니다.  
  
 다음 예제에서는 응용 프로그램 호출 **SQLBrowseConnect** 반복적으로 합니다. 매번 **SQLBrowseConnect** SQL_NEED_DATA를 반환 합니다.에 필요한 데이터에 대 한 정보를 전달 하기 \* *OutConnectionString*합니다. 응용 프로그램 전달 *OutConnectionString* 해당 루틴 **GetUserInput** (표시 되지 않음). **GetUserInput** 정보를 구문 분석, 작성 및 대화 상자를 표시 및 사용자가 입력 한 정보를 반환 합니다 \* *InConnectionString*합니다. 다음 호출에서 드라이버에 사용자의 정보를 전달 하는 응용 프로그램 **SQLBrowseConnect**합니다. 응용 프로그램 데이터 원본에 연결할 드라이버에 필요한 모든 정보를 제공한 후 **SQLBrowseConnect** 관계 없이 SQL_SUCCESS를 반환 하는 응용 프로그램 진행 됩니다.  
  
 호출 하 여 SQL Server 드라이버에 연결 하는 자세한 예제 **SQLBrowseConnect**를 참조 하십시오 [SQL Server 찾아보기 예제](../../../odbc/reference/develop-app/sql-server-browsing-example.md)합니다.  
  
 예를 들어 데이터에 원본 Sales 연결 하려면 다음 작업을 발생할 수 있습니다. 응용 프로그램에 다음 문자열을 전달 하는 먼저 **SQLBrowseConnect**:  
  
```  
"DSN=Sales"  
```  
  
 드라이버 관리자 Sales 데이터 소스에 연결 된 드라이버를 로드 합니다. 그런 다음 드라이버를 호출 **SQLBrowseConnect** 응용 프로그램에서 수신한 동일한 인수를 사용 하 여 함수입니다. 드라이버에서 다음 문자열을 반환 합니다. **OutConnectionString*:  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 응용 프로그램 전달이 문자열을 해당 **GetUserInput** 일상적인, 대화 상자는 빌드되는 사용자에 게 묻는 빨강, 파랑 또는 녹색 서버를 선택 하 고 사용자 ID 및 암호를 입력 합니다. 다음 사용자 지정 정보를 다시 일상적인 전달 \* *InConnectionString*, 응용 프로그램에 전달 하는 **SQLBrowseConnect**:  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect** Sesame 암호로 Smith로 빨간색 서버에 연결 하려면이 정보를 사용 하 고 다음 문자열을 반환 합니다 **OutConnectionString*:  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 응용 프로그램 전달이 문자열을 해당 **GetUserInput** 루틴에 빌드 대화 상자를 묻는 메시지를 데이터베이스를 선택 합니다. 사용자 선택 empdata 및 응용 프로그램 호출 **SQLBrowseConnect** 를 마지막으로이 문자열을 사용 하 여:  
  
```  
"DATABASE=SalesOrders"  
```  
  
 이 마지막 부분 드라이버는 데이터 원본에 연결 하는 데 필요한 정보 **SQLBrowseConnect** 관계 없이 SQL_SUCCESS를 반환 하 고 **OutConnectionString* 완료 된 연결 문자열을 포함 합니다.  
  
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
  
|내용|참조 항목|  
|---------------------------|---------|  
|연결 핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|데이터 원본에 연결|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|데이터 원본에서 연결 끊기|[SQLDisconnect 함수](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|연결 문자열 또는 대화 상자를 사용 하 여 데이터 원본에 연결|[SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|드라이버 설명 및 특성을 반환합니다.|[SQLDrivers 함수](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|연결 핸들 해제|[SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
