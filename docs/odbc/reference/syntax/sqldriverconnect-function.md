---
title: "SQLDriverConnect 함수 | Microsoft Docs"
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
- SQLDriverConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDriverConnect
helpviewer_keywords:
- SQLDriverConnect function [ODBC]
ms.assetid: e299be1d-5c74-4ede-b6a3-430eb189134f
caps.latest.revision: 50
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8b9576bf21c922c1e8d223710210a1703f1cbec3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqldriverconnect-function"></a>SQLDriverConnect 함수(SQLDriverConnect Function)
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ODBC  
  
 **요약**  
 **SQLDriverConnect** 하는 대신 **SQLConnect**합니다. 에 세 가지 인수 보다 더 많은 연결 정보를 필요로 하는 데이터 원본 지원 **SQLConnect**, 모든 연결 정보 및 시스템에 정의 되어 있지 않은 데이터 원본에 대 한 사용자를 묻는 대화 상자 정보입니다.  
  
 **SQLDriverConnect** 다음 연결 특성을 제공 합니다.  
  
-   데이터 원본에서 데이터 원본 이름, 하나 이상의 사용자 Id, 하나 이상의 암호 및 필요한 기타 정보를 포함 하는 연결 문자열을 사용 하는 연결을 설정 합니다.  
  
-   추가 정보 없음 또는 부분 연결 문자열을 사용 하 여 연결 설정 이 경우 드라이버 관리자와 드라이버 표시할 수 있습니다 각 사용자에 게 연결 정보입니다.  
  
-   시스템 정보에 정의 되어 있지 않은 데이터 원본에 대 한 연결을 설정 합니다. 응용 프로그램이 부분 연결 문자열을 제공 하는 경우 드라이버는 연결 정보에 대 한 사용자를 표시할 수 있습니다.  
  
-   .Dsn 파일의 정보에서 생성 된 연결 문자열을 사용 하 여 데이터 원본에 대 한 연결을 설정 합니다.  
  
 연결 된 후 **SQLDriverConnect** 완료 된 연결 문자열을 반환 합니다. 응용 프로그램 이후의 연결 요청에 대 한이 문자열을 사용할 수 있습니다. 자세한 내용은 참조 [SQLDriverConnect를 사용 하 여 연결](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
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
 *ConnectionHandle*  
 [입력] 연결 핸들입니다.  
  
 *WindowHandle*  
 [입력] 창 핸들입니다. 해당 하는 경우 응용 프로그램의 부모 창 핸들을 전달할 수 또는 경우에 null 포인터 창 핸들은 적용 가능한 또는 **SQLDriverConnect** 대화 상자를 표시 하지 것입니다.  
  
 *InConnectionString*  
 [입력] 전체 연결 문자열 ("설명" 구문 참조), 부분 연결 문자열 또는 빈 문자열입니다.  
  
 *StringLength1*  
 [입력] 길이 **InConnectionString*, ANSI 또는 DBCS 문자열의 형식이 유니코드 또는 바이트 문자열은 경우에 문자에서입니다.  
  
 *OutConnectionString*  
 [출력] 완료 된 연결 문자열에 대 한 버퍼에 대 한 포인터입니다. 대상 데이터 원본에 연결 성공 시이 버퍼는 완료 된 연결 문자열을 포함합니다. 이 버퍼에 대 한 응용 프로그램 적어도 1, 024 자로 할당 해야 합니다.  
  
 경우 *OutConnectionString* 이 NULL 이면 *StringLength2Ptr* 여전히 문자 (문자 데이터에 대 한 null 종결 문자 제외)의 총 수를 반환 버퍼에서 반환할 수 가 가리키는 *OutConnectionString*합니다.  
  
 *BufferLength*  
 [입력] 길이 **OutConnectionString* 문자에서 버퍼입니다.  
  
 *StringLength2Ptr*  
 [출력] 문자 (null 종결 문자 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한 \* *OutConnectionString*합니다. 반환할 수 있는 문자 수는 보다 크거나 같은 경우 *BufferLength*, 연결 문자열에서 완료 \* *OutConnectionString* 잘립니다  *BufferLength* null 종결 문자 길이 뺀 값입니다.  
  
 *DriverCompletion*  
 [입력] 드라이버 관리자 또는 드라이버에 연결 하는 방법은 물어야 있는지 여부를 나타내는 플래그:  
  
 SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED 이면 또는 SQL_DRIVER_NOPROMPT 합니다.  
  
 (자세한 내용은 "설명" 참조)  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE, 또는 SQL_STILL_EXECUTING 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLDriverConnect** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 관련된 된 SQLSTATE 값을 가져올 수 있습니다 **SQLGetDiagRec** 와 *fHandleType*sql_handle_dbc 라는의 및 *hHandle* 의 *ConnectionHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLDriverConnect** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|버퍼 \* *OutConnectionString* 충분히 연결 문자열이 잘림 하므로 전체 연결 문자열을 반환할 수 없습니다. 잘리지 않은 연결 문자열의 길이에서 **StringLength2Ptr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S00|잘못 된 연결 문자열 특성입니다.|잘못 된 특성 키워드는 연결 문자열에 지정 되었습니다 (*InConnectionString*), 했지만 드라이버 그래도 데이터 원본에 연결할 수 있습니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01 S 02|옵션 값이 변경 됨|드라이버에서 가리키는 지정된 된 값을 지원 하지 않았습니다 고 *ValuePtr* 인수에 **SQLSetConnectAttr** 유사한 값을 대체 합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S08|파일 DSN을 저장할 수 없습니다.|문자열에  *\*InConnectionString* 포함 한 **FILEDSN** 키워드, 하지만.dsn 파일 저장 되지 않았습니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S09|잘못 된 키워드|(DM)에 있는 문자열  *\*InConnectionString* 포함 한 **SAVEFILE** 키워드 하지 않고는 **드라이버** 또는 **FILEDSN** 키워드입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08001|클라이언트 연결을 설정할 수 없습니다.|드라이버는 데이터 원본과 연결을 설정할 수 없습니다.|  
|08002|사용 중인 연결 이름|(DM) 지정 된 *ConnectionHandle* 이미를 사용한 데이터 원본과 연결을 설정 하 고 연결이 아직 열려 있습니다.|  
|08004|서버 연결을 거부 했습니다.|데이터 원본 구현에서 정의 된 이유로 연결 만들기를 거부 했습니다.|  
|08S01|통신 연결 오류|드라이버를 드라이버 하려고 했던 연결 데이터 원본 사이의 통신 연결 하기 전에 실패는 **SQLDriverConnect** 처리 함수는 완료 되었습니다.|  
|28000|잘못 된 권한 지정|사용자 식별자 또는 권한 부여 문자열 또는 연결 문자열에 지정 된 대로 둘 다 (*InConnectionString*), 데이터 원본에 정의 된 제한을 위반 합니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*szMessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY000|일반 오류 발생: 잘못 된 파일 dsn|(DM)에 있는 문자열 **InConnectionString* FILEDSN 키워드가 포함 되어 있지만.dsn 파일의 이름을 찾을 수 없습니다.|  
|HY000|일반 오류: 파일 버퍼를 만들 수 없습니다.|(DM)에 있는 문자열 **InConnectionString* FILEDSN 키워드가 포함 되어 있지만.dsn 파일을 읽을 수 없습니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버 관리자 완료 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.는 **SQLDriverConnect** 함수입니다.<br /><br /> 드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *ConnectionHandle*합니다. 함수를 호출 하 고, 실행을 완료 하기 전에 [SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md) 에서 호출 된는 *ConnectionHandle*, 한 다음은 **SQLDriverConnect** 다시 호출 된 함수는 *ConnectionHandle*합니다.<br /><br /> 또는 **SQLDriverConnect** 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancelHandle** 에서 호출 된는 *ConnectionHandle* 의 서로 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) 다른 비동기적으로 실행 중인 함수 (하지 **SQLDriverConnect**)에 대 한 호출 된는 *ConnectionHandle* 때 계속 실행 하 고는 **SQLDriverConnect** 함수가 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|**SQLDriverConnect** 기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|인수에 대해 지정 된 값 (DM) *StringLength1* 0 보다 작은 였으며 SQL_NTS이 아닙니다.<br /><br /> 인수에 대해 지정 된 값 (DM) *BufferLength* 0 보다 작습니다.|  
|HY092|잘못 된 특성/옵션 식별자|DM ()는 *DriverCompletion* SQL_DRIVER_PROMPT 되었습니다 및 *WindowHandle* 인수가 null 포인터입니다.|  
|HY110|잘못 된 드라이버 완료|인수에 대해 지정 된 값 (DM) *DriverCompletion* SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED 이면 또는 SQL_DRIVER_NOPROMPT 없습니다.<br /><br /> (DM) 연결 풀링을 사용 된 인수에 대해 지정 된 값 및 *DriverCompletion* SQL_DRIVER_NOPROMPT이 아닙니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|드라이버는 응용 프로그램이 요청 하는 ODBC 동작의 버전을 지원 하지 않습니다.|  
|HYT00|제한 시간이 만료되었습니다.|완료 된 데이터 원본에 연결 하기 전에 로그인 제한 시간이 만료 되었습니다. 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT 합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 지정 된 데이터 원본 이름에 해당 하는 드라이버가 함수를 지원 하지 않습니다.|  
|IM002|기본 드라이버를 지정 하 고 데이터 원본을 찾을 수 없습니다|DM ()는 데이터 원본 연결 문자열에 지정 된 이름 (*InConnectionString*)에서 시스템 정보를 찾을 수 없습니다 및 기본 드라이버 사양이 없는 했습니다.<br /><br /> (DM) 시스템 정보에 ODBC 데이터 원본 및 기본 드라이버 정보를 찾을 수 없습니다.|  
|IM003|지정 된 드라이버를 로드할 수 없습니다.|(DM)의 시스템 정보에 지정 된 데이터 원본에에서 나열 된 드라이버나로 지정 된는 **드라이버** 키워드를 찾을 수 없습니다 또는 다른 이유로 인해 로드할 수 없습니다.|  
|IM004|드라이버의 **SQLAllocHandle** 실패 SQL_HANDLE_ENV에|(DM) 중 **SQLDriverConnect**, 드라이버 관리자를 호출 했지만 드라이버의 **SQLAllocHandle** 작동는 *fHandleType* SQL_HANDLE_ENV와 드라이버의 반환 되는 오류가 발생 했습니다.|  
|IM005|드라이버의 **SQLAllocHandle** 에 sql_handle_dbc 라는 실패 했습니다.|(DM) 중 **SQLDriverConnect**, 드라이버 관리자를 호출 했지만 드라이버의 **SQLAllocHandle** 작동는 *fHandleType* sql_handle_dbc 라는 드라이버의 반환 되는 오류가 발생 했습니다.|  
|IM006|드라이버의 **SQLSetConnectAttr** 하지 못했습니다.|(DM) 중 **SQLDriverConnect**, 드라이버 관리자를 호출 했지만 드라이버의 **SQLSetConnectAttr** 함수 및 드라이버에서 오류를 반환 합니다.|  
|IM007|없는 데이터 원본이 나 드라이버를 지정 합니다. 금지 하는 대화 상자|데이터 원본 이름 또는 지정 되지 않은 드라이버를 연결 문자열에 및 *DriverCompletion* SQL_DRIVER_NOPROMPT 되었습니다.|  
|IM008|실패 대화 상자|드라이버는 로그인 대화 상자를 표시 하려고 하 고 실패 합니다.<br /><br /> *WindowHandle* 는 null 포인터 및 *DriverCompletion* SQL_DRIVER_NO_PROMPT 없습니다.|  
|IM009|변환 DLL을 로드할 수 없습니다.|드라이버 변환 데이터 원본에 대해 또는 연결에 대해 지정 된 DLL을 로드할 수 없습니다.|  
|IM010|데이터 원본 이름이 너무 깁니다.|DM ()는 DSN 키워드에 대 한 특성 값 SQL_MAX_DSN_LENGTH 자를 초과 했습니다.|  
|IM011|드라이버 이름이 너무 깁니다.|DM ()는 특성에 대 한 값은 **드라이버** 키워드 255 자를 초과 했습니다.|  
|IM012|드라이버 키워드 구문 오류입니다.|(DM)에 대 한 키워드-값 쌍으로 **드라이버** 키워드 구문 오류를 포함 합니다.<br /><br /> (DM)에 있는 문자열  *\*InConnectionString* 포함 된 한 **FILEDSN** .dsn 파일 있지만 키워드를 포함 하지 않은 한 **드라이버** 키워드 또는  **DSN** 키워드입니다.|  
|IM014|지정된 된 DSN 드라이버 및 응용 프로그램 사이 아키텍처 불일치가 포함|64 비트 드라이버;에 연결 하는 DSN을 사용 하 여 (DM) 32 비트 응용 프로그램 또는 그 반대의 경우도 마찬가지입니다.|  
|IM015|드라이버의 SQLDriverConnect SQL_HANDLE_DBC_INFO_HANDLE에 실패 했습니다.|드라이버가 SQL_ERROR를 반환 하면 드라이버 관리자 응용 프로그램에 sql_error가 반환 하 고 연결이 실패 합니다.<br /><br /> SQL_HANDLE_DBC_INFO_TOKEN에 대 한 자세한 내용은 참조 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)합니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
|S1118|드라이버는 비동기 알림을 지원 하지 않습니다.|드라이버는 비동기 알림을 지원 하지 않습니다, SQL_ATTR_ASYNC_DBC_EVENT 또는 SQL_ATTR_ASYNC_DBC_RETCODE_PTR 설정할 수 없습니다.|  
  
## <a name="comments"></a>설명  
 연결 문자열에는 다음 구문을 가집니다.  
  
 *연결 문자열* :: = *빈 문자열*[;] &#124; *특성*[;] &#124; *특성*; *연결 문자열*  
  
 *빈 문자열* :: =*특성* :: = *특성 키워드*=*특성-값* &#124; 드라이버 [{}] =*특성-값*[}]  
  
 *특성 키워드* :: = DSN &#124; UID &#124; PWD &#124; *드라이버-정의-속성-키워드*  
  
 *특성-값* :: = *문자열*  
  
 *드라이버-정의-속성-키워드* :: = *식별자*  
  
 여기서 *문자열* 에 0 개 이상의 문자가; *식별자* 에 하나 이상의 문자가; *특성 키워드*  /소문자를 구분 하지 않습니다 *특성-값* 대/소문자 구분; 수 있습니다의 값은 **DSN** 키워드 공백의로 구성 되어 있지 않습니다.  
  
 연결 문자열 및 초기화 파일 문법, 키워드 및 특성 값이 문자를 포함 하는 **{} (),? \*=! @** 묶지와 중괄호 피해 야 합니다. 값은 **DSN** 키워드는 공백으로 구성할 수 없습니다 및 선행 공백을 포함할 수 없습니다. 시스템 정보 문법, 인해 키워드 및 데이터 원본 이름은 백슬래시를 포함할 수 없습니다 (\\) 문자.  
  
 응용 프로그램 다음 특성 값은 주변에 중괄호가 추가할 필요가 없습니다는 **드라이버** 키워드 특성에 세미콜론 (;)를 포함 하지 않는 한이 경우 중괄호는 필수입니다. 특성 값을 수신 하는 중괄호를 포함 하는 경우 드라이버를 제거 하지 않아야 하지만 반환 된 연결 문자열의 일부 수 있어야 합니다.  
  
 묶은 중괄호 ({})는 문자를 포함 하는 DSN 또는 연결 문자열 값 **{} (),? \*=! @** 드라이버에 그대로 전달 됩니다. 키워드에 이러한 문자를 사용할 때 드라이버 관리자 파일 Dsn 사용 하는 경우 오류를 반환 하지만 일반 연결 문자열에 대 한 드라이버에는 연결 문자열에 전달 합니다. 키워드 값에 포함 된 중괄호를 사용 하지 마십시오.  
  
 연결 문자열에는 드라이버 정의 된 키워드를 개수에 관계 없이 포함 될 수 있습니다. 때문에 **드라이버** 키워드 시스템 정보에서 정보를 사용 하지 않으므로, 드라이버는 드라이버는 연결 문자열에 정보만 사용 하 여 데이터 원본에 연결할 수 있도록 충분 한 키워드를 정의 해야 합니다. (자세한 내용은 "드라이버," 나중에이 섹션의 지침 참조). 드라이버는 데이터 원본에 연결 하는 데 필요한 어떤 키워드를 정의 합니다.  
  
 특성 값을 설명 하는 다음 표에서 **DSN**, **FILEDSN**, **드라이버**, **UID**, **PWD**, 및 **SAVEFILE** 키워드입니다.  
  
|키워드|특성 값 설명|  
|-------------|---------------------------------|  
|**DSN**|반환 된 데이터 원본의 이름을 **SQLDataSources** 또는의 데이터 원본 대화 상자 **SQLDriverConnect**합니다.|  
|**FILEDSN**|데이터 원본에 대 한 연결 문자열을 빌드할 수.dsn 파일 이름입니다. 이러한 데이터 원본에는 파일 데이터 원본 이라고 합니다.|  
|**드라이버**|설명에서 반환 되는 드라이버의는 **SQLDrivers** 함수입니다. 예를 들어 Rdb 또는 SQL Server입니다.|  
|**UID**|사용자 id입니다.|  
|**PWD**|사용자 ID에 대 한 암호가 없는 경우 해당 사용자 ID 또는 빈 문자열 하는 암호 (PWD =;).|  
|**SAVEFILE**|특성 값, 성공적인 연결에 사용 되는 키워드를 저장 해야.dsn 파일의 파일 이름입니다.|  
  
 데이터 원본이 나 드라이버 응용 프로그램을 선택 하는 방법에 대 한 정보를 참조 하십시오. [데이터 원본이 나 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)합니다.  
  
 키워드는 연결 문자열에 반복 하는 경우 드라이버는 맨 처음 발견 되는 키워드와 연결 된 값을 사용 합니다. 경우는 **DSN** 및 **드라이버** 키워드 동일한 연결 문자열에 포함 된 드라이버 관리자와 드라이버 상관 없이 키워드에 첫 번째 표시를 사용 합니다.  
  
 **FILEDSN** 및 **DSN** 키워드는 함께 사용할 수 없습니다: 나오든 이들 키워드가 나타나는 첫 번째 사용 되 고 그 다음에 표시 된은 무시 됩니다. **FILEDSN** 및 **드라이버** 키워드, 반면에 배타적이 지 않습니다. Any 키워드 사용 연결 문자열에 표시 되 면 **FILEDSN**,.dsn 파일에 동일한 키워드의 특성 값이 아닌 연결 문자열 키워드의 특성 값이 사용 됩니다.  
  
 경우는 **FILEDSN** 키워드가 사용 되는지,.dsn 파일에 지정 된 키워드는 연결 문자열을 만드는 데 사용 됩니다. (자세한 내용은 파일 데이터 원본 ","이이 섹션의 뒷부분에 나오는 참조). **UID** 키워드는 선택 사항 이지만.dsn 파일와만 만들 수 있습니다는 **드라이버** 키워드입니다. **PWD** 키워드.dsn 파일에 저장 되지 않습니다. 기본 디렉터리를 저장 하 고.dsn 파일을 로드 하 여 지정 된 경로의 조합이 됩니다 **CommonFileDir** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ Windows\CurrentVersion 및 "ODBC\DataSources"입니다. (CommonFileDir "C:\Program Files\Common Files" 인 경우 기본 디렉터리 것 "C:\Program Files\Common Files\ODBC\Data 원본"입니다.)  
  
> [!NOTE]  
>  .Dsn 파일을 직접 호출 하 여 조작할 수 있습니다는 [SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md) 및 [SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md) installer DLL의에서 함수입니다.  
  
 경우는 **SAVEFILE** 키워드를 사용, 성공적인 연결에 사용 된 키워드의 특성 값의 특성 값의 이름으로.dsn 파일으로 저장 됩니다는 **SAVEFILE** 키워드입니다. **SAVEFILE** 키워드와 함께에서 사용 해야는 **드라이버** 키워드를는 **FILEDSN** 키워드 또는 둘 다 또는 함수를 SQL_SUCCESS_WITH_INFO를 반환 합니다. SQLSTATE 01S09 (잘못 된 키워드)입니다. **SAVEFILE** 키워드 앞에 나와야 합니다.는 **드라이버** 연결 문자열 또는 결과의 키워드 정의 되지 것입니다.  
  
## <a name="driver-manager-guidelines"></a>드라이버 관리자 지침  
 드라이버 관리자에서 드라이버를 전달 하려면 연결 문자열을 만듭니다는 *InConnectionString* 드라이버의의 인수 **SQLDriverConnect** 함수입니다. 드라이버 관리자를 수정 하지 않습니다는 *InConnectionString* 인수 응용 프로그램으로 전달 합니다.  
  
 드라이버 관리자의 작업의 값에 기반는 *DriverCompletion* 인수:  
  
-   SQL_DRIVER_PROMPT: 연결 문자열에 없는 경우 하나는 **드라이버**, **DSN**, 또는 **FILEDSN** 키워드를 드라이버 관리자는 데이터 원본 대화 상자를 표시 합니다. 대화 상자에서 반환 된 데이터 원본 이름 및 응용 프로그램에 의해 전달 하는 다른 모든 키워드에서 연결 문자열을 만듭니다. 드라이버 관리자는 DSN 키워드-값 쌍 지정 대화 상자에서 반환 된 데이터 원본 이름은 비어 있으면 = 기본값입니다. (이 대화 상자 "Default" 이름의 데이터 원본이 표시 되지 않습니다.)  
  
-   SQL_DRIVER_COMPLETE 또는 SQL_DRIVER_COMPLETE_REQUIRED: 응용 프로그램에서 지정 된 연결 문자열을 포함 하는 경우는 **DSN** 키워드를 드라이버 관리자가 응용 프로그램에서 지정 된 연결 문자열을 복사 합니다. 때와 동일한 동작을 수행, *DriverCompletion* SQL_DRIVER_PROMPT 됩니다.  
  
-   SQL_DRIVER_NOPROMPT: 드라이버 관리자는 응용 프로그램에서 지정 된 연결 문자열을 복사 합니다.  
  
 응용 프로그램에서 지정 된 연결 문자열을 포함 하는 경우는 **드라이버** 키워드를 드라이버 관리자가 응용 프로그램에서 지정 된 연결 문자열을 복사 합니다.  
  
 생성 하는 연결 문자열을 사용 하 여, 드라이버 관리자 드라이버를 사용 하 여 결정, 해당 드라이버에 연결 하 고 연결 문자열을 생성 하는 드라이버에 전달는; 드라이버 관리자와 드라이버의 상호 작용 하는 방법에 대 한 자세한 내용은의 "설명" 섹션을 참조 하십시오. [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)합니다. 연결 문자열에 없는 경우는 **드라이버** 키워드를 드라이버 관리자는 다음과 같이 사용 하는 드라이버를 결정 합니다.  
  
1.  연결 문자열을 포함 하는 경우는 **DSN** 키워드를 드라이버 관리자 시스템 정보를 데이터 소스와 연결 된 드라이버를 검색 합니다.  
  
2.  연결 문자열에 없는 경우는 **DSN** , 드라이버 관리자 시스템 정보에서 기본 데이터 원본과 관련 된 드라이버를 검색 하는 키워드 또는 데이터 원본을 찾을 수 없습니다. (자세한 내용은 참조 [기본 하위 키](../../../odbc/reference/install/default-subkey.md).) 값을 변경 하는 드라이버 관리자는 **DSN** 을 "DEFAULT" 연결 문자열 키워드입니다.  
  
3.  경우는 **DSN** , 드라이버 관리자 시스템 정보에서 기본 데이터 원본과 관련 된 드라이버를 검색 하 고 연결 문자열에서 키워드를 "DEFAULT"로 설정 합니다.  
  
4.  드라이버 관리자 SQLSTATE IM002 인 sql_error가 반환 데이터 원본을 찾을 수 없습니다 하는 경우의 기본 데이터 원본을 찾을 수 없습니다 (데이터 원본을 찾을 수 없습니다 및 기본 드라이버를 지정).  
  
## <a name="file-data-sources"></a>파일 데이터 원본  
 연결 문자열에 대 한 호출에서 응용 프로그램에서 지정 하는 경우 **SQLDriverConnect** 포함는 **FILEDSN** 키워드 및이 키워드 중 하나에 의해 교체 되지 않으면는 **DSN**또는 **드라이버** 키워드에 다음 드라이버 관리자.dsn 파일에 정보를 사용 하 여 연결 문자열을 만들기 및 *InConnectionString* 인수입니다. 드라이버 관리자는 다음과 같이 됩니다.  
  
1.  .Dsn 파일의 파일 이름이 올바른지 여부를 확인 합니다. Not, SQLSTATE IM014 포함 된 sql_error가 반환 하는 경우 (잘못 된 DSN 파일 이름). 파일 이름이 빈 문자열 ("") SQL_DRIVER_NOPROMPT 아니며를 지정 하면 **파일 열기** 대화 상자가 표시 됩니다. 올바른 경로 하지만 파일 이름이 없거나 잘못 된 파일 이름, 파일 이름에 포함 하 고 SQL_DRIVER_NOPROMPT를 지정 하지 않은 경우 **파일 열기** 파일 이름에 지정 된 1로 설정 하는 현재 디렉터리와 함께 대화 상자가 표시 됩니다. 파일 이름이 빈 문자열 ("") 또는 올바른 경로 하지만 파일 이름이 없거나 잘못 된 파일 이름, 파일 이름 포함 SQL_DRIVER_NOPROMPT를 지정 힙이고 SQLSTATE IM014와 SQL_ERROR가 반환 되 (잘못 된 DSN 파일 이름).  
  
2.  .Dsn 파일의 [ODBC] 섹션에 모든 키워드를 읽습니다. 경우는 **드라이버** 키워드 없다면, SQLSTATE IM012 포함 된 sql_error가 반환 (드라이버 키워드 구문 오류).dsn 파일을 공유할 수 있습니다 및 따라서만 들어 있는 제외 하 고는 **DSN** 키워드입니다.  
  
     파일 데이터 소스를 공유할 수 없는 경우 드라이버 관리자의 값을 읽습니다.는 **DSN** 키워드 하 고 공유할 수 없는 파일 데이터 원본이 가리키는 사용자 또는 시스템 데이터 원본에 필요에 따라 연결 합니다. 3-5 단계를 수행 하지 않습니다.  
  
3.  드라이버에 대 한 연결 문자열을 생성합니다. 드라이버 연결 문자열은.dsn 파일에 지정 된 키워드와 원래 응용 프로그램 연결 문자열에 지정 된 개체의 합집합입니다. 키워드 겹치는 드라이버 연결 문자열의 생성을 위한 규칙은 다음과 같습니다.  
  
    -   경우는 **드라이버** 로 지정 된 드라이버 및 응용 프로그램 연결 문자열에 있는 키워드는 **드라이버** 키워드.dsn 파일 및 응용 프로그램 연결 문자열에서 동일 하지 않은 경우 드라이버 정보.dsn 파일에는 무시 됩니다 하 고 응용 프로그램 연결 문자열에 드라이버 정보를 사용 합니다. 변수로 지정 된 드라이버는 **드라이버** 키워드.dsn 파일 및 응용 프로그램의 연결 문자열에서 동일 다음 모든 키워드 겹칠 경우 응용 프로그램 연결 문자열에 지정 된 우선 순위가 보다 .dsn 파일에 지정 합니다.  
  
    -   새 연결 문자열에는 **FILEDSN** 키워드를 제거 하는 합니다.  
  
4.  HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST 레지스트리 항목을 검색 하 여 드라이버를 로드 합니다. INI\\< 드라이버 이름\>\Driver 여기서 \<드라이버 이름 >에서 지정한는 **드라이버** 키워드입니다.  
  
5.  드라이버가 새 연결 문자열을 전달합니다.  
  
 .Dsn 파일의 예 참조 [를 사용 하 여 파일 데이터 원본 연결](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)합니다.  
  
## <a name="savefile-keyword"></a>SAVEFILE 키워드  
 응용 프로그램에서 지정 된 연결 문자열을 포함 하는 경우는 **SAVEFILE** 키워드에 다음 드라이버 관리자 연결 문자열을.dsn 파일에 저장 합니다. 드라이버 관리자는 다음과 같이 됩니다.  
  
1.  특성 값으로.dsn 파일의 파일 이름 포함 여부를 확인는 **SAVEFILE** 키워드는 사용할 수 있습니다. Not, SQLSTATE IM014 포함 된 sql_error가 반환 하는 경우 (잘못 된 DSN 파일 이름). 파일 이름의 유효성은 표준 시스템 명명 규칙에 의해 결정 됩니다. 파일 이름이 빈 문자열 ("") 및 *DriverCompletion* 인수 SQL_DRIVER_NOPROMPT 이면 않은 경우 파일 이름이 올바른지 합니다. 파일 이름에 이미 있으면 다음 경우 *DriverCompletion* 이 SQL_DRIVER_NOPROMPT 이면 파일을 덮어씁니다. 경우 *DriverCompletion* SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE 또는 SQL_DRIVER_COMPLETE_REQUIRED 이면은 파일을 덮어쓸 수 있는지 여부를 지정 하 라는 메시지를 대화 상자. 선택 하지 않으면를 입력 하면 **파일 저장** 대화 상자가 나타납니다.  
  
2.  드라이버 관계 없이 SQL_SUCCESS를 반환는 파일 이름이 설정 되지 않은 빈 문자열이 면 경우에 반환 된 연결 정보를 기록 하는 드라이버 관리자는 *OutConnectionString* 인수에 지정 된 형식으로 지정된 된 파일에 이 섹션의 앞부분에 나오는 "연결 문자열" 섹션.  
  
3.  드라이버 관계 없이 SQL_SUCCESS를 반환 하 고 파일 이름이 빈 문자열 ("")를 호출 하는 드라이버 관리자는 **파일 저장** 와 일반 대화 상자는 *hwnd* 지정 하 고 연결 정보를 기록 반환 된 *OutConnectionString* 이 섹션의 앞부분에 나오는 "연결 문자열" 섹션에 지정 된 형식으로 파일 저장 일반 대화 상자에 지정 된 파일에 있습니다.  
  
4.  반환 하는 경우 드라이버는 관계 없이 SQL_SUCCESS를 반환 합니다는 *OutConnectionString* 응용 프로그램에 연결 문자열을 포함 하는 인수입니다.  
  
5.  SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR를 반환 하는 드라이버, 드라이버 관리자 응용 프로그램에는 SQLSTATE을 반환 합니다.  
  
## <a name="driver-guidelines"></a>드라이버 지침  
 드라이버에 전달 된 드라이버 관리자에서 연결 문자열에 포함 되어 있는지 여부를 확인 하는 **DSN** 또는 **드라이버** 키워드입니다. 연결 문자열을 포함 하는 경우는 **드라이버** 키워드, 드라이버 시스템 정보에서 데이터 원본에 대 한 정보를 검색할 수 없습니다. 연결 문자열을 포함 하는 경우는 **DSN** 키워드 또는 포함 하지 않음은 **DSN** 또는 **드라이버** 키워드, 드라이버는 데이터 원본에 대 한 정보를 검색할 수 다음과 같은 시스템 정보:  
  
1.  연결 문자열을 포함 하는 경우는 **DSN** 키워드, 드라이버는 지정된 된 데이터 원본에 대 한 정보를 검색 합니다.  
  
2.  연결 문자열에 없는 경우는 **DSN** 키워드를 지정된 된 데이터 소스를 찾지 또는 **DSN** 키워드 "DEFAULT"로 설정 된 경우 드라이버는 기본 데이터 원본에 대 한 정보를 검색 합니다. .  
  
 드라이버에서 연결 문자열에 전달 된 정보를 보완할 시스템 정보를 검색 한 정보를 사용 합니다. 시스템 정보에 대 한 정보는 연결 문자열에 정보를 복제 하는 경우 드라이버는 연결 문자열에 정보를 사용 합니다.  
  
 값에 따라 *DriverCompletion*, 드라이버는 사용자 ID와 암호를 같은 연결 정보를 사용자를 데이터 원본에 연결:  
  
-   SQL_DRIVER_PROMPT: 드라이버 초기 값으로 (있는 경우)는 연결 문자열 및 시스템 정보 값을 사용 하는 대화 상자를 표시 합니다. 사용자 대화 상자를 종료 하는 경우 드라이버는 데이터 원본에 연결 합니다. 연결 문자열의 값을 생성 합니다는 **DSN** 또는 **드라이버** 키워드 \* *InConnectionString* 및에서 반환 된 정보는 대화 상자입니다. 이 연결 문자열에 배치 된 **OutConnectionString* 버퍼입니다.  
  
-   SQL_DRIVER_COMPLETE 또는 SQL_DRIVER_COMPLETE_REQUIRED: 드라이버 데이터 원본 및 복사본에 연결할 연결 문자열에 충분 한 정보를 포함 하는 경우 해당 내용이 정확한 \* *InConnectionString*를 \* *OutConnectionString*합니다. 모든 정보가 누락 되거나 잘못 된 경우 드라이버는 경우와 동일한 작업을 수행 하는 *DriverCompletion* SQL_DRIVER_PROMPT 되는 경우를 제외 하 고는 *DriverCompletion* SQL_DRIVER_COMPLETE_은 필요한 드라이버 데이터 원본에 연결 하지 않아도 모든 정보에 대 한 제어를 해제 합니다.  
  
-   SQL_DRIVER_NOPROMPT: 연결 문자열에 충분 한 정보를 드라이버에 연결 된 데이터 원본 및 복사본 \* *InConnectionString* 를 \* *OutConnectionString*. 드라이버에 대 한 SQL_ERROR를 반환 하는 그렇지 않은 경우 **SQLDriverConnect**합니다.  
  
 데이터 원본에 성공적으로 연결에서 드라이버 설정 \* *StringLength2Ptr* 반환에 사용할 수 있는 출력 연결 문자열의 길이 **OutConnectionString*합니다.  
  
 드라이버 관리자 또는 드라이버에서 제공 되는 대화 상자를 취소 하는 경우 **SQLDriverConnect** SQL_NO_DATA를 반환 합니다.  
  
 연결 하는 동안 드라이버 관리자와 드라이버 상호 작용 하는 방법에 대 한 정보를 참조 하십시오. [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)합니다.  
  
 드라이버에서 지 원하는 경우 **SQLDriverConnect**, 드라이버 키워드 섹션 드라이버에 대 한 시스템 정보를 포함 해야 합니다는 **ConnectFunctions** 키워드와 두 번째 문자 "Y"로 설정 합니다.  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>연결 풀링을 사용할 때 연결  
 연결 풀링은 응용을 프로그램을 이미 만들어져 있는 연결을 다시 사용할 수 있습니다. 때 **SQLDriverConnect** 호출 드라이버 관리자 연결 풀링에 대해 지정 된 환경에서 연결 풀의 일부인 연결을 사용 하 여 연결 하려고 합니다. 연결 풀링에 대 한 자세한 내용은 참조 하십시오. [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)합니다.  
  
 응용 프로그램 풀링이 설정 된 연결에서 SQLDisconnect를 호출 하기 전에 SQL_ATTR_RESET_CONNECTION를 설정할 수 있습니다. 자세한 내용은 참조 [SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)합니다.  
  
 응용 프로그램이 호출 하는 경우 다음과 같은 제한 사항이 적용 **SQLDriverConnect** 풀링된 연결에 연결 하려면:  
  
-   처리 풀링 연결을 수행 하는 경우는 **SAVEFILE** 키워드를 연결 문자열에 지정 합니다.  
  
-   연결 풀링을 사용 하는 경우 **SQLDriverConnect** 로 호출할 수는 *DriverCompletion* SQL_DRIVER_NOPROMPT에 있는 인수의 경우 **SQLDriverConnect** 라고 다른 *DriverCompletion*, SQLSTATE HY110 (잘못 된 드라이버 완료)이 반환 됩니다.  
  
## <a name="connection-attributes"></a>연결 특성  
 SQL_ATTR_LOGIN_TIMEOUT 연결 특성을 사용 하 여 설정 **SQLSetConnectAttr**, 로그인 요청을 응용 프로그램에 반환 하기 전에 드라이버에서 연결 된 완료 될 때까지 기다리는 시간 (초)의 수를 정의 합니다. 사용자는 연결 문자열을 완료 하 라는 메시지가 표시 됩니다, 드라이버는 연결 프로세스를 시작 하는 경우 각 로그인 요청에 대 한 대기 기간이 시작 됩니다.  
  
 드라이버는 기본적으로 SQL_MODE_READ_WRITE 액세스 모드에서 연결을 엽니다. 액세스 모드 SQL_MODE_READ_ONLY을 설정 하려면 응용 프로그램 호출 해야 **SQLSetConnectAttr** 호출 하기 전에 SQL_ATTR_ACCESS_MODE 특성으로 **SQLDriverConnect**합니다.  
  
 데이터 원본에 대 한 시스템 정보에는 기본 변환 라이브러리를 지정 하는 경우 드라이버 파일이 로드 됩니다. 호출 하 여 다른 변환 라이브러리를 로드할 수 **SQLSetConnectAttr** SQL_ATTR_TRANSLATE_LIB 특성을 사용 합니다. 번역 옵션을 호출 하 여 지정할 수 있습니다 **SQLSetConnectAttr** SQL_ATTR_TRANSLATE_OPTION 옵션을 사용 합니다.  
  
 자세한 내용은 참조 [SQLDriverConnect를 사용 하 여 연결](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)합니다.  
  
```  
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
  
 또한 참조 [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|검색 하 고 데이터 원본에 연결 하는 데 필요한 값을 열거|[SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|데이터 원본에 연결|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|데이터 원본에서 연결 끊기|[SQLDisconnect 함수](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|드라이버 설명 및 특성을 반환합니다.|[SQLDrivers 함수](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|핸들을 해제합니다.|[SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|연결 특성을 설정합니다.|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

