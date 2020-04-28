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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 607b0d764a694098a23111e9d7f4ce9755ea982d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301343"
---
# <a name="sqlbrowseconnect-function"></a>SQLBrowseConnect 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ODBC  
  
 **요약**  
 **SQLBrowseConnect** 는 데이터 원본에 연결 하는 데 필요한 특성 및 특성 값을 검색 하 고 열거 하는 반복적인 방법을 지원 합니다. **SQLBrowseConnect** 에 대 한 각 호출은 연속 된 수준의 특성 및 특성 값을 반환 합니다. 모든 수준이 열거 되 면 데이터 원본에 대 한 연결이 완료 되 고 **SQLBrowseConnect**에서 전체 연결 문자열을 반환 합니다. SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO의 반환 코드는 모든 연결 정보가 지정 되었고 응용 프로그램이 데이터 원본에 연결 되었음을 나타냅니다.  
  
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
 입력 요청 연결 문자열을 찾습니다 ("Comments"의 "*Inconnectionstring* 인수" 참조).  
  
 *StringLength1*  
 입력 문자에서 **Inconnectionstring* 의 길이입니다.  
  
 *OutConnectionString*  
 출력 찾아보기 결과 연결 문자열을 반환할 문자 버퍼에 대 한 포인터입니다. "Comments"의 "*Outconnectionstring* 인수"를 참조 하십시오.  
  
 *Outconnectionstring* 이 NULL 인 경우 *StringLength2Ptr* 는 *outconnectionstring*에서 가리키는 버퍼에서 반환 하는 데 사용할 수 있는 문자 데이터의 NULL 종료 문자를 제외 하 고 전체 문자 수를 반환 합니다.  
  
 *BufferLength*  
 입력 **Outconnectionstring* 버퍼의 길이 (문자)입니다.  
  
 *StringLength2Ptr*  
 출력 \* *Outconnectionstring*에서 반환 하는 데 사용할 수 있는 총 문자 수 (null 종료 제외)입니다. 반환할 수 있는 문자 수가 *bufferlength*보다 크거나 같은 경우 \* *outconnectionstring* 의 연결 문자열은 *bufferlength* 에서 null 종료 문자의 길이를 뺀 값으로 잘립니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_ERROR, SQL_INVALID_HANDLE 또는 SQL_STILL_EXECUTING입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLBrowseConnect** 가 SQL_ERROR, SQL_SUCCESS_WITH_INFO 또는 SQL_NEED_DATA 반환 하는 경우 *HandleType* 의 SQL_HANDLE_STMT 및 *ConnectionHandle 핸들*을 사용 하 여 **SQLGETDIAGREC** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLBrowseConnect** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|버퍼 \* *outconnectionstring* 이 전체 찾아보기 결과 연결 문자열을 반환할 만큼 크지 않아 문자열이 잘렸습니다. Buffer **StringLength2Ptr* 에는 잘림 검색 결과 연결 문자열의 길이가 포함 됩니다. 함수는 SQL_NEED_DATA를 반환 합니다.|  
|01S00|잘못 된 연결 문자열 특성|*Inconnectionstring*(찾아보기 요청 연결 문자열)에 잘못 된 attribute 키워드를 지정 했습니다. 함수는 SQL_NEED_DATA를 반환 합니다.<br /><br /> 현재 연결 수준에 적용 되지 않는 찾아보기 요청 연결 문자열 (*Inconnectionstring*)에서 attribute 키워드를 지정 했습니다. 함수는 SQL_NEED_DATA를 반환 합니다.|  
|01 S 02|값 변경 됨|드라이버가 **SQLSetConnectAttr** 에서 *지정 된 값* 을 지원 하지 않아 유사한 값으로 대체 되었습니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08001|클라이언트에서 연결을 설정할 수 없음|드라이버가 데이터 원본과의 연결을 설정할 수 없습니다.|  
|08002|사용 중인 연결 이름|(DM) 지정 된 연결이 이미 데이터 원본과의 연결을 설정 하는 데 사용 되었으며 연결이 열려 있습니다.|  
|08004|서버에서 연결을 거부 했습니다.|데이터 소스에서 구현 정의 이유에 대 한 연결 설정을 거부 했습니다.|  
|08S01|통신 연결 오류|드라이버가 연결을 시도 하는 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|28000|잘못 된 권한 부여 사양|찾아보기 요청 연결 문자열 (*Inconnectionstring*)에 지정 된 사용자 id 또는 권한 부여 문자열이 나 둘 다에서 데이터 원본에 의해 정의 된 제한을 위반 했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|(DM) 드라이버 관리자가 함수의 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.<br /><br /> 드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|[Sqlcancelhandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md)를 호출 하 여 비동기 작업을 취소 했습니다. 그런 다음 *ConnectionHandle*에서 원래 함수를 다시 호출 했습니다.<br /><br /> 다중 스레드 응용 프로그램의 다른 스레드에서 *ConnectionHandle* **sqlcancelhandle** 을 호출 하 여 작업을 취소 했습니다.|  
|HY010|함수 시퀀스 오류|(DM) *ConnectionHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 인수 *StringLength1* 에 지정 된 값이 0 보다 작고 SQL_NTS와 같지 않습니다.<br /><br /> (DM) 인수 *Bufferlength* 에 지정 된 값이 0 보다 작은 경우|  
|HY114|드라이버가 연결 수준 비동기 함수 실행을 지원 하지 않습니다.|(DM) 연결을 만들기 전에 응용 프로그램에서 연결 핸들에 대해 비동기 작업을 사용 하도록 설정 했습니다. 그러나 드라이버는 연결 핸들에 대해 비동기 작업을 지원 하지 않습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에 대 한 연결이 완료 되기 전에 로그인 제한 시간이 만료 되었습니다. 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT을 통해 설정 됩니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) 지정 된 데이터 원본 이름에 해당 하는 드라이버에서 함수를 지원 하지 않습니다.|  
|IM002|데이터 원본을 찾을 수 없으며 기본 드라이버가 지정 되지 않았습니다.|(DM) 찾아보기 요청 연결 문자열 (*Inconnectionstring*)에 지정 된 데이터 원본 이름을 시스템 정보에서 찾을 수 없거나 기본 드라이버 사양이 없습니다.<br /><br /> (DM) ODBC 데이터 원본 및 기본 드라이버 정보를 시스템 정보에서 찾을 수 없습니다.|  
|IM003|지정한 드라이버를 로드할 수 없습니다.|(DM) 시스템 정보의 데이터 원본 사양에 나열 되었거나 **driver** 키워드에 의해 지정 된 드라이버를 찾을 수 없거나 다른 이유로 로드할 수 없습니다.|  
|IM004|SQL_HANDLE _ENV 드라이버의 **SQLAllocHandle** 가 실패 했습니다.|(DM) **SQLBrowseConnect**를 사용 하는 동안 드라이버 관리자는 *HandleType* SQL_HANDLE_ENV의 **SQLAllocHandle** 함수를 호출 하 고 드라이버에서 오류를 반환 했습니다.|  
|IM005|SQL_HANDLE_DBC에서 드라이버의 **SQLAllocHandle** 실패|(DM) **SQLBrowseConnect**를 사용 하는 동안 드라이버 관리자는 *HandleType* SQL_HANDLE_DBC의 **SQLAllocHandle** 함수를 호출 하 고 드라이버에서 오류를 반환 했습니다.|  
|IM006|드라이버의 **SQLSetConnectAttr** 실패|(DM) **SQLBrowseConnect**중에 드라이버 관리자가 드라이버의 **SQLSetConnectAttr** 함수를 호출 하 고 드라이버에서 오류를 반환 했습니다.|  
|IM009|변환 DLL을 로드할 수 없습니다.|드라이버가 데이터 원본 또는 연결에 대해 지정 된 변환 DLL을 로드할 수 없습니다.|  
|IM010|데이터 원본 이름이 너무 깁니다.|(DM) DSN 키워드에 대 한 특성 값이 SQL_MAX_DSN_LENGTH 자 보다 깁니다.|  
|IM011|드라이버 이름이 너무 깁니다.|(DM) DRIVER 키워드의 특성 값이 255 자 보다 깁니다.|  
|IM012|드라이버 키워드 구문 오류|(DM) DRIVER 키워드에 대 한 키워드-값 쌍에 구문 오류가 포함 되어 있습니다.|  
|IM014|지정 된 DSN에 드라이버와 응용 프로그램 간의 아키텍처가 일치 하지 않습니다.|(DM) 32 비트 응용 프로그램은 64 비트 드라이버에 연결 하는 DSN을 사용 합니다. 또는 그 반대의 경우도 마찬가지입니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
|S1118|드라이버가 비동기 알림을 지원 하지 않습니다.|드라이버가 비동기 알림을 지원 하지 않는 경우 SQL_ATTR_ASYNC_DBC_EVENT 또는 SQL_ATTR_ASYNC_DBC_RETCODE_PTR를 설정할 수 없습니다.|  
  
## <a name="inconnectionstring-argument"></a>InConnectionString 인수  
 찾아보기 요청 연결 문자열의 구문은 다음과 같습니다.  
  
 *연결 문자열* :: = *특성*[`;`] &#124; *특성* `;` *연결-문자열*;<br>
 *attribute* :: = *특성-키워드*`=`*특성-값* &#124; `DRIVER=`[`{`]*특성 값*[`}`]<br>
 *특성-keyword* :: = `DSN` &#124; `UID` &#124; `PWD` &#124; *드라이버 정의-키워드*<br>
 *특성-value* :: = *문자 문자열*<br>
 *드라이버 정의-키워드* :: = *식별자*<br>
  
 여기서 *문자 문자열* 에는 0 자 이상의 문자가 있습니다. *식별자* 에 하나 이상의 문자가 있습니다. *특성-키워드* 는 대/소문자를 구분 하지 않습니다. *특성-값* 은 대/소문자를 구분 합니다. 그리고 **DSN** 키워드 값은 공백으로만 구성 되지 않습니다. 연결 문자열 및 초기화 파일 문법을 포함 하 여 **[]{}(),;? 문자를 포함 하는 키워드 및 특성 값 = \*! @** 를 피해 야 합니다. 시스템 정보의 문법 때문에 키워드와 데이터 원본 이름에는 백슬래시 (\\) 문자를 사용할 수 없습니다. ODBC 2의 경우. *x* 드라이버 키워드에 대 한 특성 값 주위에는 중괄호를 입력 해야 합니다.  
  
 찾아보기 요청 연결 문자열에서 키워드가 반복 되는 경우 드라이버는 처음 발견 되는 키워드와 연결 된 값을 사용 합니다. **DSN** 및 **드라이버** 키워드가 동일한 찾아보기 요청 연결 문자열에 포함 된 경우 드라이버 관리자와 드라이버에서 가장 먼저 표시 되는 키워드를 사용 합니다.  
  
 응용 프로그램에서 데이터 원본 또는 드라이버를 선택 하는 방법에 대 한 자세한 내용은 [데이터 원본 또는 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)을 참조 하십시오.  
  
## <a name="outconnectionstring-argument"></a>OutConnectionString 인수  
 찾아보기 결과 연결 문자열은 연결 특성의 목록입니다. 연결 특성은 특성 키워드와 해당 특성 값으로 구성 됩니다. 찾아보기 결과 연결 문자열의 구문은 다음과 같습니다.  
  
 *연결 문자열* :: = *특성*[`;`] &#124; *특성* `;` *연결 문자열*<br>
 *attribute* :: = [`*`]*특성-키워드*`=`*특성-값*<br>
 *특성-keyword* :: = *ODBC-attribute* &#124; *드라이버 정의 특성-키워드*<br>
 *ODBC-keyword* =`UID` { `PWD`&#124;} [`:`*지역화 된 식별자*] 드라이버별- *keyword* :: = *식별자*[`:`*지역화*된 식별자] *특성-value* :: = `{` *특성* `}` -값 목록 &#124; `?` (중괄호는 literal 이며 드라이버에서 반환 됩니다.)<br>
 *특성-값-list* :: = *문자열* [`:`*지역화*된 문자열 *] &#124; 문자열* [`:`*지역화 된 문자열*] `,` *특성-값 목록*<br>
  
 여기서 *문자 문자열과* 지역화 된 *문자열* 은 0 개 이상의 문자를 포함 합니다. *식별자* 와 *지역화 된 식별자* 에는 하나 이상의 문자가 포함 되어 있습니다. *특성-키워드* 는 대/소문자를 구분 하지 않습니다. 및 *특성 값* 은 대/소문자를 구분 합니다. 연결 문자열 및 초기화 파일 문법, 키워드, 지역화 된 식별자 및 **[]{}(),;? 문자를 포함 하는 특성 값 = \*! @** 를 피해 야 합니다. 시스템 정보의 문법 때문에 키워드와 데이터 원본 이름에는 백슬래시 (\\) 문자를 사용할 수 없습니다.  
  
 찾아보기 결과 연결 문자열 구문은 다음 의미 체계 규칙에 따라 사용 됩니다.  
  
-   별표\*()가 *특성-키워드*앞에 오면 *특성* 은 선택 사항이 며 다음에 **SQLBrowseConnect**에 대 한 호출에서 생략 될 수 있습니다.  
  
-   **UID** 및 **PWD** 특성 키워드는 **SQLDriverConnect**에 정의 된 것과 동일한 의미를 갖습니다.  
  
-   *드라이버 정의 특성 키워드* 는 특성 값을 제공할 수 있는 특성 종류의 이름을 지정 합니다. 예를 들어 **서버**, **데이터베이스**, **호스트**또는 **DBMS**일 수 있습니다.  
  
-   *ODBC-특성-* 키워드 및 *드라이버 정의-키워드* 에는 지역화 되거나 사용자에 게 친숙 한 키워드 버전이 포함 되어 있습니다. 이는 응용 프로그램에서 대화 상자에 레이블로 사용할 수 있습니다. 그러나 검색 요청 문자열을 드라이버에 전달할 때에는 **UID**, **PWD**또는 *식별자* 만 사용 해야 합니다.  
  
-   {*특성-값-목록*}은 해당 *특성-키워드*에 유효한 실제 값의 열거형입니다. 중괄호 ({})는 선택 목록에 표시 되지 않습니다. 드라이버에서 반환 됩니다. 예를 들어 서버 이름이 나 데이터베이스 이름 목록 일 수 있습니다.  
  
-   *특성 값* 이 단일 물음표 (?) 이면 단일 값은 *특성-키워드*에 해당 합니다. 예: UID = 존스; PWD = Sesame.  
  
-   **SQLBrowseConnect** 에 대 한 각 호출은 연결 프로세스의 다음 수준을 충족 하는 데 필요한 정보만 반환 합니다. 드라이버는 상태 정보를 연결 핸들과 연결 하 여 각 호출에서 컨텍스트를 항상 확인할 수 있도록 합니다.  
  
## <a name="using-sqlbrowseconnect"></a>SQLBrowseConnect 사용  
 **SQLBrowseConnect** 에는 할당 된 연결이 필요 합니다. 드라이버 관리자는에 지정 되었거나 초기 찾아보기 요청 연결 문자열에 지정 된 데이터 원본 이름에 해당 하는 드라이버를 로드 합니다. 이 문제가 발생 하는 경우에 대 한 자세한 내용은 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)에서 "Comments" 섹션을 참조 하세요. 검색 프로세스 중에 드라이버는 데이터 원본에 대 한 연결을 설정할 수 있습니다. **SQLBrowseConnect** 가 SQL_ERROR을 반환 하는 경우 처리 되지 않은 연결이 종료 되 고 연결이 연결 되지 않은 상태로 반환 됩니다.  
  
> [!NOTE]  
>  **SQLBrowseConnect** 는 연결 풀링을 지원 하지 않습니다. 연결 풀링을 사용 하는 동안 **SQLBrowseConnect** 가 호출 되 면 SQLSTATE HY000 (일반 오류)가 반환 됩니다.  
  
 **SQLBrowseConnect** 가 연결에서 처음으로 호출 되는 경우 찾아보기 요청 연결 문자열에는 **DSN** 키워드나 **DRIVER** 키워드가 포함 되어야 합니다. 찾아보기 요청 연결 문자열에 **DSN** 키워드가 포함 된 경우 드라이버 관리자는 시스템 정보에서 해당 하는 데이터 원본 사양을 찾습니다.  
  
-   드라이버 관리자가 해당 데이터 원본 사양을 찾으면 연결 된 드라이버 DLL을 로드 합니다. 드라이버는 시스템 정보에서 데이터 원본에 대 한 정보를 검색할 수 있습니다.  
  
-   드라이버 관리자가 해당 데이터 원본 사양을 찾을 수 없는 경우 기본 데이터 원본 사양을 찾고 연결 된 드라이버 DLL을 로드 합니다. 드라이버는 시스템 정보에서 기본 데이터 원본에 대 한 정보를 검색할 수 있습니다. "DEFAULT"는 DSN에 대 한 드라이버에 전달 됩니다.  
  
-   드라이버 관리자가 해당 데이터 원본 사양을 찾을 수 없고 기본 데이터 원본 사양이 없는 경우 SQLSTATE IM002 (데이터 원본을 찾을 수 없으며 기본 드라이버가 지정 되지 않음)가 SQL_ERROR 반환 됩니다.  
  
 찾아보기 요청 연결 문자열에 **driver** 키워드가 포함 된 경우 드라이버 관리자는 지정 된 드라이버를 로드 합니다. 시스템 정보에서 데이터 원본을 찾으려고 시도 하지 않습니다. **Driver** 키워드는 시스템 정보의 정보를 사용 하지 않으므로 드라이버는 찾아보기 요청 연결 문자열의 정보만 사용 하 여 데이터 원본에 연결할 수 있도록 충분 한 키워드를 정의 해야 합니다.  
  
 **SQLBrowseConnect**에 대 한 각 호출에서 응용 프로그램은 찾아보기 요청 연결 문자열에 연결 특성 값을 지정 합니다. 드라이버는 찾아보기 결과 연결 문자열에서 연속 된 수준 특성 및 특성 값을 반환 합니다. 이 메서드는 찾아보기 요청 연결 문자열에 아직 열거 되지 않은 연결 특성이 있는 한 SQL_NEED_DATA를 반환 합니다. 응용 프로그램은 browse result 연결 문자열의 내용을 사용 하 여 **SQLBrowseConnect**에 대 한 다음 호출에 대 한 찾아보기 요청 연결 문자열을 작성 합니다. 모든 필수 특성 ( *Outconnectionstring* 인수에서 별표가 앞에 오지 않음)은 **SQLBrowseConnect**에 대 한 다음 호출에 포함 되어야 합니다. 현재 찾아보기 요청 연결 문자열을 빌드할 때 응용 프로그램은 이전 검색 결과 연결 문자열의 내용을 사용할 수 없습니다. 즉, 이전 수준에서 설정 된 특성에 대해 다른 값을 지정할 수 없습니다.  
  
 모든 수준의 연결 및 연결 된 특성이 열거 되 면 드라이버는 SQL_SUCCESS을 반환 하 고, 데이터 원본에 대 한 연결이 완료 되 고, 전체 연결 문자열이 응용 프로그램에 반환 됩니다. 연결 문자열은 **SQLDriverConnect**와 함께 다른 연결을 설정 하는 SQL_DRIVER_NOPROMPT 옵션과 함께 사용 하는 데 적합 합니다. 그러나 **SQLBrowseConnect**에 대 한 다른 호출에서는 전체 연결 문자열을 사용할 수 없습니다. **SQLBrowseConnect** 가 다시 호출 된 경우에는 전체 호출 시퀀스를 반복 해야 합니다.  
  
 **SQLBrowseConnect** 는 찾아보기 프로세스 중에 복구 가능 하 고 심각 하지 않은 오류가 있는 경우에도 SQL_NEED_DATA 반환 합니다. 예를 들어 응용 프로그램에서 제공 하는 잘못 된 암호 또는 특성 키워드입니다. SQL_NEED_DATA이 반환 되 고 찾아보기 결과 연결 문자열이 변경 되지 않은 경우 오류가 발생 하 고 응용 프로그램에서 **SQLGetDiagRec** 를 호출 하 여 찾아보기 시간 오류에 대 한 SQLSTATE를 반환할 수 있습니다. 이렇게 하면 응용 프로그램에서 특성을 수정 하 고 찾아보기를 계속할 수 있습니다.  
  
 응용 프로그램은 **Sqldisconnect**를 호출 하 여 언제 든 지 찾아보기 프로세스를 종료할 수 있습니다. 드라이버는 처리 중인 연결을 모두 종료 하 고 연결을 연결 되지 않은 상태로 되돌립니다.  
  
 연결 핸들에 대해 비동기 작업을 사용 하는 경우 **SQLBrowseConnect** 가 SQL_STILL_EXECUTING를 반환할 수도 있습니다. SQL_NEED_DATA 반환 될 때 응용 프로그램은 **Sqldisconnect** 를 사용 하 여 찾아보기 프로세스를 취소 해야 합니다. **SQLBrowseConnect** 가 SQL_STILL_EXECUTING을 반환 하는 경우 응용 프로그램은 **sqlcancelhandle** 을 사용 하 여 진행 중인 작업을 취소 해야 합니다. 함수가 SQL_NEED_DATA 반환한 후 **Sqlcancelhandle** 을 호출 해도 아무런 효과가 없습니다.  
  
 자세한 내용은 [SQLBrowseConnect를 사용 하 여 연결](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)을 참조 하세요.  
  
 드라이버에서 **SQLBrowseConnect**를 지 원하는 경우 드라이버의 시스템 정보에 있는 드라이버 키워드 섹션에는 "Y"로 세 번째 문자를 설정 하는 **connectfunctions** 키워드가 포함 되어야 합니다.  
  
## <a name="code-example"></a>코드 예  
  
> [!NOTE]  
>  Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는 경우 연결 문자열에 사용자 `Trusted_Connection=yes` ID 및 암호 정보를 지정 하는 대신를 지정 해야 합니다.  
  
 다음 예제에서 응용 프로그램은 **SQLBrowseConnect** 를 반복적으로 호출 합니다. **SQLBrowseConnect** 가 SQL_NEED_DATA를 반환할 때마다 \* *outconnectionstring*에서 필요한 데이터에 대 한 정보를 다시 전달 합니다. 응용 프로그램은 해당 루틴 **GetUserInput** (표시 되지 않음)에 *outconnectionstring* 을 전달 합니다. **GetUserInput** 는 정보를 구문 분석 하 고, 대화 상자를 작성 및 표시 하 고, \* *inconnectionstring*에 사용자가 입력 한 정보를 반환 합니다. 응용 프로그램은 다음에 **SQLBrowseConnect**에 대 한 호출에서 사용자 정보를 드라이버로 전달 합니다. 응용 프로그램에서 데이터 원본에 연결 하는 데 필요한 모든 정보를 제공 하 고 나면 **SQLBrowseConnect** 는 SQL_SUCCESS을 반환 하 고 응용 프로그램을 계속 진행 합니다.  
  
 **SQLBrowseConnect**를 호출 하 여 SQL Server 드라이버에 연결 하는 방법에 대 한 자세한 예제는 [SQL Server 검색 예](../../../odbc/reference/develop-app/sql-server-browsing-example.md)를 참조 하세요.  
  
 예를 들어 데이터 원본 판매에 연결 하기 위해 다음 작업이 발생할 수 있습니다. 먼저 응용 프로그램은 **SQLBrowseConnect**에 다음 문자열을 전달 합니다.  
  
```  
"DSN=Sales"  
```  
  
 드라이버 관리자는 데이터 원본 판매와 연결 된 드라이버를 로드 합니다. 그런 다음 응용 프로그램에서 받은 것과 동일한 인수를 사용 하 여 드라이버의 **SQLBrowseConnect** 함수를 호출 합니다. 드라이버는 **Outconnectionstring*에서 다음 문자열을 반환 합니다.  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 응용 프로그램은 사용자에 게 red, blue 또는 green 서버를 선택 하 고 사용자 ID와 암호를 입력 하도록 요청 하는 대화 상자를 작성 하는 **GetUserInput** 루틴에이 문자열을 전달 합니다. 루틴은 응용 프로그램이 \* **SQLBrowseConnect**에 전달 하는 *inconnectionstring*에서 다음 사용자 지정 정보를 다시 전달 합니다.  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect** 는이 정보를 사용 하 여 Sesame 암호를 사용 하 여 Smith로 red 서버에 연결한 다음 **outconnectionstring*에서 다음 문자열을 반환 합니다.  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 응용 프로그램은 사용자에 게 데이터베이스를 선택 하도록 요청 하는 대화 상자를 작성 하는 **GetUserInput** 루틴에이 문자열을 전달 합니다. 사용자가 empdata를 선택 하면 응용 프로그램에서이 문자열을 사용 하 여 마지막 시간 **SQLBrowseConnect** 를 호출 합니다.  
  
```  
"DATABASE=SalesOrders"  
```  
  
 드라이버에서 데이터 원본에 연결 하는 데 필요한 마지막 정보는 다음과 같습니다. **SQLBrowseConnect** 는 SQL_SUCCESS을 반환 하 고, **outconnectionstring* 은 완료 된 연결 문자열을 포함 합니다.  
  
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
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|연결 핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|데이터 원본에 연결|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|데이터 원본에서 연결 끊기|[SQLDisconnect 함수](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|연결 문자열 또는 대화 상자를 사용 하 여 데이터 원본에 연결|[SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|드라이버 설명 및 특성 반환|[SQLDrivers 함수](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|연결 핸들 해제|[SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
