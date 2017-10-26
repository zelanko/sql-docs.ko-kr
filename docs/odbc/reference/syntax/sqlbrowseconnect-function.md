---
title: "SQLBrowseConnect 함수 | Microsoft Docs"
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
- SQLBrowseConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBrowseConnect
helpviewer_keywords:
- SQLBrowseConnect function [ODBC]
ms.assetid: b7f1be66-e6c7-4790-88ec-62b7662103c0
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9f8117cc5238576f840cdb98f5ffaded38aed0d6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlbrowseconnect-function"></a>SQLBrowseConnect 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ODBC  
  
 **요약**  
 **SQLBrowseConnect** 검색 하 고 특성 및 데이터 원본에 연결 하는 데 필요한 특성 값을 열거 하는 반복 메서드를 지원 합니다. 호출할 때마다 **SQLBrowseConnect** 연속적인 수준의 특성 및 특성 값을 반환 합니다. 모든 수준 열거, 데이터 원본에 대 한 연결 완성 되 고 전체 연결 문자열을 반환한 **SQLBrowseConnect**합니다. SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 반환 코드는 모든 연결 정보를 지정 하 고 응용 프로그램은 이제 데이터 원본에 연결을 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
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
 [입력] 연결 핸들입니다.  
  
 *InConnectionString*  
 [입력] 요청 연결 문자열을 찾아보기 (참조 "*InConnectionString* 인수" "설명").  
  
 *StringLength1*  
 [입력] 길이 **InConnectionString* 문자 수입니다.  
  
 *OutConnectionString*  
 [출력] 찾아보기 결과 연결 문자열을 반환 하는 문자 버퍼에 대 한 포인터 (참조 "*OutConnectionString* 인수"에서 "설명").  
  
 경우 *OutConnectionString* 이 NULL 이면 *StringLength2Ptr* 여전히 문자 (문자 데이터에 대 한 null 종결 문자 제외)의 총 수를 반환 버퍼에서 반환할 수 가 가리키는 *OutConnectionString*합니다.  
  
 *BufferLength*  
 [입력] 길이 문자의는 **OutConnectionString* 버퍼입니다.  
  
 *StringLength2Ptr*  
 [출력] 총 수 (제외 null 종료) 사용할 수 있는 문자를 반환 하려면 \* *OutConnectionString*합니다. 반환할 수 있는 문자 수는 보다 크거나 같은 경우 *BufferLength*, 연결 문자열을 \* *OutConnectionString* 잘립니다 * BufferLength* null 종결 문자 길이 뺀 값입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_ERROR, SQL_INVALID_HANDLE, 또는 SQL_STILL_EXECUTING 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLBrowseConnect** SQL_ERROR, SQL_SUCCESS_WITH_INFO 또는 관련된 된 SQLSTATE 값 sql_need_data가 반환 되는 호출 하 여 경우가 **SQLGetDiagRec** 와 *HandleType* 여의 및 *ConnectionHandle의 핸들*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLBrowseConnect** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|버퍼 \* *OutConnectionString* 충분히 문자열이 잘렸습니다 하므로 전체 검색 결과 연결 문자열을 반환할 수 없습니다. 버퍼 **StringLength2Ptr* 잘리지 않은 찾아보기 결과 연결 문자열의 길이 포함 합니다. (함수는 SQL_NEED_DATA를 반환합니다.)|  
|01S00|잘못 된 연결 문자열 특성입니다.|잘못 된 특성 키워드 찾아보기 요청 연결 문자열에 지정 된 (*InConnectionString*). (함수는 SQL_NEED_DATA를 반환합니다.)<br /><br /> 특성 키워드 찾아보기 요청 연결 문자열에 지정 된 (*InConnectionString*) 현재 연결 수준에 적용 되지 않습니다. (함수는 SQL_NEED_DATA를 반환합니다.)|  
|01 S 02|값이 변경 됨|드라이버의 지정된 된 값을 지원 하지 않았습니다 고 *ValuePtr* 인수에 **SQLSetConnectAttr** 유사한 값을 대체 합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08001|클라이언트 연결을 설정할 수 없습니다.|드라이버는 데이터 원본과 연결을 설정할 수 없습니다.|  
|08002|사용 중인 연결 이름|(DM) 지정된 된 연결 이미를 사용한 데이터 원본과 연결을 설정 하 고 연결 되어 있는 합니다.|  
|08004|서버 연결을 거부 했습니다.|데이터 원본 구현에서 정의 된 이유로 연결 만들기를 거부 했습니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버를 드라이버 하려고 했던 연결 데이터 원본 사이의 통신 링크 하지 못했습니다.|  
|28000|잘못 된 권한 지정|사용자 식별자 또는 권한 부여 문자열 또는 찾아보기에 지정 된 대로 둘 다 요청 연결 문자열 (*InConnectionString*), 데이터 원본에 정의 된 제한을 위반 합니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에 * \*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버 관리자에서 (DM) 함수는 완료 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.<br /><br /> 드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|호출 하 여 비동기 작업이 취소 되었습니다 [SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md)합니다. 그런 다음 원래 함수에서 다시 호출 된는 *ConnectionHandle*합니다.<br /><br /> 호출 하 여는 작업이 취소 되었습니다 **SQLCancelHandle** 에 *ConnectionHandle* 다중 스레드 응용 프로그램에서 다른 스레드에서 합니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *ConnectionHandle* 호출 되었을 때 계속 실행 하 고 있습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|인수에 대해 지정 된 값 (DM) *StringLength1* 0 보다 작은 였으며 SQL_NTS이 아닙니다.<br /><br /> 인수에 대해 지정 된 값 (DM) *BufferLength* 0 보다 작습니다.|  
|HY114|드라이버는 연결 수준 비동기 함수 실행을 지원 하지 않습니다.|(DM) 응용 프로그램 연결 핸들에 연결 하기 전에 비동기 작업을 사용할 수 있습니다. 그러나, 드라이버는 연결 핸들에서 비동기 작업을 지원 하지 않습니다.|  
|HYT00|제한 시간이 만료되었습니다.|완료 된 데이터 원본에 연결 하기 전에 로그인 제한 시간이 만료 되었습니다. 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT 합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 지정 된 데이터 원본 이름에 해당 하는 드라이버가 함수를 지원 하지 않습니다.|  
|IM002|기본 드라이버를 지정 하 고 데이터 원본을 찾을 수 없습니다|DM ()는 데이터 원본 찾아보기 요청 연결 문자열에 지정 된 이름 (*InConnectionString*) 시스템 정보에서 찾을 수 없습니다도 기본 드라이버 사양 없었습니다.<br /><br /> (DM) 시스템 정보에 ODBC 데이터 원본 및 기본 드라이버 정보를 찾을 수 없습니다.|  
|IM003|지정 된 드라이버를 로드할 수 없습니다.|(DM)의 시스템 정보에 지정 된 데이터 원본에에서 나열 된 드라이버나로 지정 된는 **드라이버** 키워드를 찾을 수 없습니다 또는 다른 이유로 인해 로드할 수 없습니다.|  
|IM004|드라이버의 **SQLAllocHandle** 실패 SQL_HANDLE _ENV에|(DM) 중 **SQLBrowseConnect**, 드라이버 관리자를 호출 했지만 드라이버의 **SQLAllocHandle** 작동는 *HandleType* SQL_HANDLE_ENV와 드라이버의 반환 되는 오류가 발생 했습니다.|  
|IM005|드라이버의 **SQLAllocHandle** 실패 sql_handle_dbc 라는에|(DM) 중 **SQLBrowseConnect**, 드라이버 관리자를 호출 했지만 드라이버의 **SQLAllocHandle** 작동는 *HandleType* sql_handle_dbc 라는 드라이버의 반환 되는 오류가 발생 했습니다.|  
|IM006|드라이버의 **SQLSetConnectAttr** 하지 못했습니다.|(DM) 중 **SQLBrowseConnect**, 드라이버 관리자를 호출 했지만 드라이버의 **SQLSetConnectAttr** 함수 및 드라이버에서 오류를 반환 합니다.|  
|IM009|변환 DLL을 로드할 수 없습니다.|드라이버 변환 데이터 원본에 대해 또는 연결에 대해 지정 된 DLL을 로드할 수 없습니다.|  
|IM010|데이터 원본 이름이 너무 깁니다.|DM ()는 DSN 키워드에 대 한 특성 값 SQL_MAX_DSN_LENGTH 자를 초과 했습니다.|  
|IM011|드라이버 이름이 너무 깁니다.|DM ()는 DRIVER 키워드에 대 한 특성 값이 255 자 보다 긴지 않습니다.|  
|IM012|드라이버 키워드 구문 오류입니다.|DM ()는 DRIVER 키워드에 대 한 키워드-값 쌍에 구문 오류가 포함 되어 있습니다.|  
|IM014|지정된 된 DSN 드라이버 및 응용 프로그램 사이 아키텍처 불일치가 포함|64 비트 드라이버;에 연결 하는 DSN을 사용 하 여 (DM) 32 비트 응용 프로그램 또는 그 반대의 경우도 마찬가지입니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
|S1118|드라이버는 비동기 알림을 지원 하지 않습니다.|드라이버는 비동기 알림을 지원 하지 않습니다, SQL_ATTR_ASYNC_DBC_EVENT 또는 SQL_ATTR_ASYNC_DBC_RETCODE_PTR 설정할 수 없습니다.|  
  
## <a name="inconnectionstring-argument"></a>InConnectionString 인수  
 찾아보기 요청 연결 문자열에는 다음 구문을 가집니다.  
  
 *연결 문자열* :: = *특성*[;] &#124; *특성*; *연결 stringattribute* :: = *특성 키워드*=*특성-값* &#124; 드라이버 [{}] =*특성-값 [*}]*특성 키워드* :: = DSN &#124; UID &#124; PWD &#124; *드라이버-정의 된 특성-keywordattribute-값* :: = *문자-stringdriver-정의-속성-키워드* :: = *식별자*  
  
 여기서 *문자열* 에 0 개 이상의 문자가; *식별자* 에 하나 이상의 문자가; *특성 키워드 * /소문자를 구분 하지 않습니다 *특성-값* 대/소문자 구분; 수 있습니다의 값은 **DSN** 키워드 공백의로 구성 되어 있지 않습니다. 연결 문자열 및 초기화 파일 문법, 키워드 및 특성 값이 문자를 포함 하는 **{} (),? \*=! @** 피해 야 합니다. 시스템 정보에 대 한 문법, 인해 키워드 및 데이터 원본 이름은 백슬래시를 포함할 수 없습니다 (\\) 문자. Odbc 2. *x* 드라이버를 중괄호로 묶어야 DRIVER 키워드에 대 한 특성 값입니다.  
  
 키워드는 찾아보기 요청 연결 문자열에 반복 하는 경우 드라이버는 맨 처음 발견 되는 키워드와 연결 된 값을 사용 합니다. 경우는 **DSN** 및 **드라이버** 키워드 동일한 찾아보기 요청 연결 문자열에 포함 된 드라이버 관리자와 드라이버 상관 없이 키워드에 첫 번째 표시를 사용 합니다.  
  
 데이터 원본이 나 드라이버 응용 프로그램을 선택 하는 방법에 대 한 정보를 참조 하십시오. [데이터 원본이 나 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)합니다.  
  
## <a name="outconnectionstring-argument"></a>OutConnectionString 인수  
 찾아보기 결과 연결 문자열은 연결 특성의 목록. 연결 특성 특성 키워드와 해당 특성 값으로 구성 됩니다. 찾아보기 결과 연결 문자열에는 다음 구문을 가집니다.  
  
 *연결 문자열* :: = *특성*[;] &#124; *특성*; *연결 stringattribute* :: = [\*]*특성 키워드 특성 valueattribute 키워드가 =* :: = *ODBC 특성-키워드* &#124; *driver-defined-attribute-keywordODBC-attribute-keyword* = {UID &#124; PWD} [:*지역화 식별자*]*드라이버-정의-속성-키워드* :: = *식별자*[:*지역화 id*]*특성-값* :: = {*특성 값 목록*} &#124;? (중괄호는 리터럴, 드라이버에 의해 반환 됩니다.) *특성 값 목록* :: = *문자열* [:*지역화 된 문자열*] &#124; *문자열* [:*지역화 된 문자열*], *특성-값-목록*  
  
 여기서 *문자열* 및 *지역화 된 문자열* 0 개 이상의 문자가; *식별자* 및 *지역화 식별자* 하나 이상의 문자가; *특성 키워드* 를 구분 하 고 *특성-값* 대/소문자 구분 될 수 있습니다. 연결으로 인해 문자열 및 초기화 파일 문법, 키워드, 지역화 된 식별자 및 특성 값을 문자를 포함 하는 **{} (),? \*=! @** 피해 야 합니다. 시스템 정보에 대 한 문법, 인해 키워드 및 데이터 원본 이름은 백슬래시를 포함할 수 없습니다 (\\) 문자.  
  
 찾아보기 결과 연결 문자열 구문은 다음 의미 체계 규칙에 따라 사용 됩니다.  
  
-   별표 (\*) 앞에 *특성 키워드*, *특성* 는 선택 사항이 며 다음 호출에서 생략할 수 **SQLBrowseConnect**합니다.  
  
-   특성 키워드 **UID** 및 **PWD** 에 정의 된 의미가 동일한 **SQLDriverConnect**합니다.  
  
-   A *드라이버-정의-속성-키워드* 종류 특성 값 제공 될 수 있습니다는 특성의 이름을 지정 합니다. 예를 들어, 수 있습니다 **서버**, **데이터베이스**, **호스트**, 또는 **DBMS**합니다.  
  
-   *ODBC 특성-키워드* 및 *드라이버-정의-특성-키워드* 키워드의 지역화 된 또는 친숙 한 버전을 포함 합니다. 이 대화 상자에서 레이블로 응용 프로그램에서 사용할 수 있습니다. 그러나 **UID**, **PWD**, 또는 *식별자* 단독 때 사용 해야 드라이버에 찾아보기 요청 문자열을 전달 합니다.  
  
-   {*특성 값 목록*} 실제 값의 열거형을 해당 하는 것에 대 한 유효 *특성 키워드*합니다. 참고 중괄호 ({}); 선택 목록에 나타내지 않습니다 드라이버에서 반환 됩니다. 예를 들어 서버 이름의 목록을 또는 데이터베이스 이름 목록을 수 있습니다.  
  
-   경우는 *특성-값* 단일 물음표 (?), 단일 값에 해당 하는 *특성 키워드*합니다. 예를 들어 UID = JohnS; PWD Sesame = 합니다.  
  
-   호출할 때마다 **SQLBrowseConnect** 연결 프로세스의 다음 수준에 만족 하는 데 필요한 정보만 반환 합니다. 드라이버는 각 호출에서 항상 컨텍스트를 확인할 수 있도록 연결 핸들와 상태 정보를 연결 합니다.  
  
## <a name="using-sqlbrowseconnect"></a>SQLBrowseConnect를 사용 하 여  
 **SQLBrowseConnect** 할당 된 연결이 필요 합니다. 드라이버 관리자에서 지정한 또는; 초기 찾아보기 요청 연결 문자열에 지정 된 데이터 원본 이름에 해당 하는 드라이버를 로드 합니다. 이 경우에 대 한 내용은의 "설명" 섹션을 참조 하십시오. [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)합니다. 드라이버는 검색 프로세스 중에 데이터 소스와 연결을 설정할 수 있습니다. 경우 **SQLBrowseConnect** 연결이 종료 되 고 연결 되지 않은 상태로 반환 되는 처리 중인 SQL_ERROR를 반환 합니다.  
  
> [!NOTE]  
>  **SQLBrowseConnect** 연결 풀링을 지원 하지 않습니다. 경우 **SQLBrowseConnect** 연결 풀링을 사용 하는 동안 SQLSTATE HY000 (일반 오류)이 반환 됩니다.  
  
 때 **SQLBrowseConnect** 라고 연결에서 처음으로 찾아보기 요청 연결 문자열을 포함 해야 합니다는 **DSN** 키워드 또는 **드라이버** 키워드입니다. 찾아보기 요청 연결 문자열을 포함 하는 경우는 **DSN** 키워드를 드라이버 관리자 시스템 정보에 해당 하는 데이터 원본 설정을 찾습니다.  
  
-   드라이버 관리자는 해당 하는 데이터 원본 설정을 발견 하면 관련된 드라이버 DLL; 로드 드라이버는 시스템 정보를 데이터 원본에 대 한 정보를 검색할 수 있습니다.  
  
-   관련된 드라이버 DLL; 로드를 찾아 지정 된 기본 데이터 원본 드라이버 관리자가 해당 하는 데이터 원본 설정을 찾을 수 없는 경우 드라이버에서 시스템 정보 기본 데이터 원본에 대 한 정보를 검색할 수 있습니다. "DEFAULT"는 DSN에 대 한 드라이버에 전달 됩니다.  
  
-   드라이버 관리자는 해당 하는 데이터 원본 설정을 찾을 수 없습니다. 기본 데이터 원본 사양이 없으므로 SQLSTATE IM002 포함 된 sql_error가 반환 (데이터 원본을 찾을 수 없습니다 및 기본 드라이버를 지정).  
  
 찾아보기 요청 연결 문자열을 포함 하는 경우는 **드라이버** 지정된 된 드라이버를 로드 하는 키워드, 드라이버 관리자, 시스템 정보에는 데이터 소스를 찾으려고 시도 하지 않습니다. 때문에 **드라이버** 키워드 시스템 정보에서 정보를 사용 하지 않으므로, 드라이버는 드라이버 찾아보기 요청 연결 문자열에 정보만 사용 하 여 데이터 원본에 연결할 수 있도록 충분 한 키워드를 정의 해야 합니다.  
  
 호출할 때마다 **SQLBrowseConnect**, 응용 프로그램 찾아보기 요청 연결 문자열에 연결 특성 값을 지정 합니다. 찾아보기 결과 연결 문자열;에 연속적인 수준의 특성 및 특성 값을 반환 하는 드라이버 찾아보기 요청 연결 문자열에서 열거 되지 아직 연결 특성은으로 SQL_NEED_DATA를 반환 합니다. 응용 프로그램 찾아보기 결과 연결 문자열의 내용을 사용 하 여 다음 호출에 대 한 찾아보기 요청 연결 문자열을 작성할 **SQLBrowseConnect**합니다. 모든 필수 특성 (앞에 별표 하는 것은 *OutConnectionString* 인수)에 대 한 다음 호출에 포함 되어야 합니다 **SQLBrowseConnect**합니다. Note 현재 찾아보기 요청 연결 문자열; 빌드할 때 응용 프로그램이 이전 찾아보기 결과 연결 문자열의 내용의 사용할 수 없습니다 즉, 이전 수준에서 설정 하는 특성에 대 한 서로 다른 값을 지정할 수 없습니다.  
  
 연결과 연관 된 특성의 모든 수준을 열거 관계 없이 SQL_SUCCESS를 반환 하는 드라이버, 데이터 원본에 대 한 연결이 완료 및 전체 연결 문자열을 응용 프로그램에 반환 됩니다. 연결 문자열은 함께 사용 하기에 적합 한 **SQLDriverConnect**, 다른 연결을 SQL_DRIVER_NOPROMPT 옵션을 사용 합니다. 전체 연결 문자열에 대 한 다른 호출에서 사용할 수 없습니다 **SQLBrowseConnect**그러나; 경우 **SQLBrowseConnect** 전체를 다시 호출 호출의 시퀀스를 반복 해야 합니다.  
  
 **SQLBrowseConnect** 도 찾아보기 프로세스; 예를 들어 잘못 된 암호 또는 하는 동안 응용 프로그램에서 제공 하는 특성 키워드 복구할 수, 치명적이 지 않은 오류가 있는 경우 SQL_NEED_DATA를 반환 합니다. 때 SQL_NEED_DATA가 반환 하 고 찾아보기 결과 연결 문자열 변경 오류가 발생 했습니다 아니며 응용 프로그램에서 호출할 수 **SQLGetDiagRec** 탐색 시 오류에 대 한 SQLSTATE 돌아갑니다. 이렇게 하면 특성을 수정 하 고 찾아보기 계속 하려면 응용 프로그램이 있습니다.  
  
 응용 프로그램 호출 하 여 언제 든 지 찾아보기 프로세스를 종료할 수 **SQLDisconnect**합니다. 드라이버는 모든 활성 연결을 종료 하 고 연결이 연결 되지 않은 상태로 반환 됩니다.  
  
 연결 핸들에 비동기 작업을 사용 하면 **SQLBrowseConnect** SQL_STILL_EXECUTING도 반환할 수 있습니다. SQL_NEED_DATA를 반환 하는 경우 응용 프로그램 사용 해야 **SQLDisconnect** 찾아보기 프로세스를 취소 합니다. 경우 **SQLBrowseConnect** 반환 SQL_STILL_EXECUTING을 응용 프로그램을 사용할지 **SQLCancelHandle** 진행 중인 작업을 취소 합니다. 호출 **SQLCancelHandle** 함수에서 반환 하는 SQL_NEED_DATA 아무 효과가 없습니다.  
  
 자세한 내용은 참조 [SQLBrowseConnect 연결과](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)합니다.  
  
 드라이버에서 지 원하는 경우 **SQLBrowseConnect**, 드라이버 키워드 섹션 드라이버에 대 한 시스템 정보에 포함 해야 합니다는 **ConnectFunctions** 키워드와 세 번째 문자 "Y"로 설정  
  
## <a name="code-example"></a>코드 예  
  
> [!NOTE]  
>  지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, `Trusted_Connection=yes` 연결 문자열에 사용자 ID와 암호 정보 대신 합니다.  
  
 다음 예제에서는 응용 프로그램 호출 **SQLBrowseConnect** 반복 합니다. 때마다 **SQLBrowseConnect** sql_need_data가 반환에 필요한 데이터에 대 한 정보를 전달 하기 \* *OutConnectionString*합니다. 응용 프로그램 전달 *OutConnectionString* 해당 루틴에 **GetUserInput** (표시 되지 않음). **GetUserInput** 정보를 구문 분석, 빌드 및 대화 상자를 표시 및에서 사용자가 입력 한 정보를 반환 \* *InConnectionString*합니다. 다음 호출에서 드라이버를 사용자의 정보를 전달 하는 응용 프로그램 **SQLBrowseConnect**합니다. 응용 프로그램에서 데이터 원본에 연결 하는 드라이버에 필요한 모든 정보를 제공 하는 후 **SQLBrowseConnect** 관계 없이 SQL_SUCCESS를 반환 하는 응용 프로그램 진행 됩니다.  
  
 SQL Server 드라이버에 연결 하 여 호출 하 여 더 자세한 예제를 보려면 **SQLBrowseConnect**, 참조 [SQL Server 검색 예](../../../odbc/reference/develop-app/sql-server-browsing-example.md)합니다.  
  
 예를 들어 원본 판매 데이터에 연결, 다음 작업이 발생할 수 있습니다. 응용 프로그램에 다음 문자열을 전달 하는 첫째, **SQLBrowseConnect**:  
  
```  
"DSN=Sales"  
```  
  
 드라이버 관리자는 영업 데이터 원본과 관련 된 드라이버를 로드 합니다. 그런 다음 드라이버의 연속 호출 **SQLBrowseConnect** 함수 응용 프로그램에서 받은 동일한 인수를 사용 합니다. 드라이버에서 다음 문자열을 반환 합니다 **OutConnectionString*:  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 응용 프로그램이이 문자열을 전달 해당 **GetUserInput** 일반적인 어떤 빌드가 대화 상자를 사용자에 게 요청 빨간색, 파란색 또는 녹색 서버를 선택 하 고 사용자 ID와 암호를 입력 합니다. 다음 사용자 지정 정보를에서 다시 라우팅 전달 \* *InConnectionString*, 응용 프로그램에 전달 하는 **SQLBrowseConnect**:  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect** Sesame 암호로 Smith로 빨간색 서버에 연결 하려면이 정보를 사용 하 고 다음에서 다음 문자열을 반환 **OutConnectionString*:  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 응용 프로그램이이 문자열을 전달 해당 **GetUserInput** 일반적인 어떤 빌드가 대화 상자를 묻는 메시지를 데이터베이스를 선택 합니다. 사용자가 선택 되어 empdata 및 응용 프로그램 호출 **SQLBrowseConnect** 를 마지막으로이 문자열을 사용 합니다.  
  
```  
"DATABASE=SalesOrders"  
```  
  
 이 드라이버; 데이터 원본에 연결 하는 데 필요한 정보가의 마지막 부분 **SQLBrowseConnect** 관계 없이 SQL_SUCCESS를 반환 하 고 **OutConnectionString* 완료 된 연결 문자열을 포함 합니다.  
  
```  
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
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

