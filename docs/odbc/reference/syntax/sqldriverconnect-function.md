---
title: SQLDriverConnect 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 225b882a6c48900e9a15a23e4073910315848985
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537649"
---
# <a name="sqldriverconnect-function"></a>SQLDriverConnect 함수(SQLDriverConnect Function)
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. ODBC  
  
 **요약**  
 **SQLDriverConnect** 대안인 **SQLConnect**합니다. 에 세 가지 인수 보다 더 많은 연결 정보를 필요로 하는 데이터 원본을 지 원하는 **SQLConnect**, 모든 연결 정보 및 시스템에 정의 되어 있지 않은 데이터 원본에 대 한 사용자에 게 프롬프트 대화 상자 정보입니다.  
  
 **SQLDriverConnect** 다음 연결 특성을 제공 합니다.  
  
-   데이터 원본에서 데이터 원본 이름, 하나 이상의 사용자 Id, 하나 이상의 암호 및 필요한 기타 정보를 포함 하는 연결 문자열을 사용 하는 연결을 설정 합니다.  
  
-   부분 연결 문자열 또는 추가 정보 없음;를 사용 하 여 연결 이 경우 드라이버 관리자 및 드라이버 수 각 프롬프트 연결 정보에 대 한 사용자.  
  
-   시스템 정보에 정의 되지 않은 데이터 원본에 연결 합니다. 부분 연결 문자열을 제공 하는 응용 프로그램을 하는 경우 드라이버 연결 정보에 대 한 사용자를 표시 수 있습니다.  
  
-   .Dsn 파일의 정보에서 생성 된 연결 문자열을 사용 하 여 데이터 원본에 연결 합니다.  
  
 연결이 설정 되 면 **SQLDriverConnect** 완료 된 연결 문자열을 반환 합니다. 응용 프로그램 이후의 연결 요청에 대 한이 문자열을 사용할 수 있습니다. 자세한 내용은 [SQLDriverConnect를 사용 하 여 연결](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)합니다.  
  
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
 *ConnectionHandle*  
 [입력] 연결 핸들입니다.  
  
 *WindowHandle*  
 [입력] 창 핸들입니다. 해당 하는 경우 응용 프로그램의 부모 창 핸들을 전달할 수 없거나 null 포인터인 경우 창 핸들을 적용 하거나 **SQLDriverConnect** 대화 상자를 표시 하지 것입니다.  
  
 *InConnectionString*  
 [입력] 전체 연결 문자열 ("설명" 구문을 참조), 부분 연결 문자열 또는 빈 문자열입니다.  
  
 *StringLength1*  
 [입력] 길이 **InConnectionString*, 인지 문자열을 유니코드 또는 바이트 문자열은 ANSI 또는 DBCS 문자에서입니다.  
  
 *OutConnectionString*  
 [출력] 완료 된 연결 문자열에 대 한 버퍼에 대 한 포인터입니다. 연결에 성공 하면 대상 데이터 원본에이 버퍼는 완료 된 연결 문자열을 포함합니다. 응용 프로그램에는이 버퍼에 대 한 최소 1,024 자 할당 해야 합니다.  
  
 하는 경우 *OutConnectionString* 가 null 인 경우 *StringLength2Ptr* (문자 데이터에 대 한 null 종료 문자를 제외한) 문자의 총 수를 반환 여전히는 버퍼에서 반환할 사용 가능한 가 가리키는 *OutConnectionString*합니다.  
  
 *BufferLength*  
 [입력] 길이 **OutConnectionString* 문자에서 버퍼입니다.  
  
 *StringLength2Ptr*  
 [출력] 문자 (null 종결 문자가 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한 \* *OutConnectionString*합니다. 반환할 사용 가능한 문자 개수 보다 크거나 같은 경우 *BufferLength*의 연결 문자열에서 완료 \* *OutConnectionString* 잘립니다  *BufferLength* null 종료 문자 길이 뺀 값입니다.  
  
 *DriverCompletion*  
 [입력] 드라이버를 드라이버 관리자 연결 자세한 물어야 하는지 여부를 나타내는 플래그.  
  
 SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED 이면 또는 SQL_DRIVER_NOPROMPT를 선택 합니다.  
  
 (자세한 내용은 "설명입니다." 참조)  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE, 또는 SQL_STILL_EXECUTING 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLDriverConnect** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 연관된 된 SQLSTATE 값을 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *fHandleType*SQL_HANDLE_DBC의 및는 *hHandle* 의 *ConnectionHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLDriverConnect** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|버퍼 \* *OutConnectionString* 충분 하므로 연결 문자열 잘렸습니다. 전체 연결 문자열을 반환할 수 없습니다. 잘리지 않은 연결 문자열의 길이에서 **StringLength2Ptr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S00|잘못 된 연결 문자열 특성입니다.|잘못 된 특성 키워드는 연결 문자열에 지정 된 (*InConnectionString*), 드라이버 했지만 그래도 데이터 원본에 연결할 수 있습니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S02|옵션 값이 변경 됨|드라이버에서 가리키는 지정된 된 값을 지원 하지 않았습니다 합니다 *ValuePtr* 인수에 **SQLSetConnectAttr** 유사한 값을 대체 합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S08|파일 DSN 저장 중 오류 발생|문자열  *\*InConnectionString* 포함 된를 **FILEDSN** 키워드 되지만.dsn 파일이 저장 되지 않았습니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S09|잘못 된 키워드|(DM)의 문자열이  *\*InConnectionString* 포함 된를 **SAVEFILE** 키워드 아닌를 **드라이버** 또는 **FILEDSN** 키워드입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08001|클라이언트를 연결할 수 없습니다.|드라이버는 데이터 원본과 연결을 설정할 수 없습니다.|  
|08002|연결 이름 사용|(DM) 지정 된 *ConnectionHandle* 이미 사용한 데이터 원본에 연결 및 연결이 열려 있습니다.|  
|08004|서버 연결을 거부 했습니다.|데이터 원본 연결의 설정 구현 시 정의 된 이유로 인해 거부 합니다.|  
|08S01|통신 연결 오류|드라이버 및 연결을 시도 된 드라이버는 데이터 원본 간의 통신 링크 실패 하기 전에 합니다 **SQLDriverConnect** 함수 완료 처리 합니다.|  
|28000|잘못 된 권한 부여 사양|사용자 식별자 또는 권한 부여 문자열 또는 연결 문자열에 지정 된 대로 둘 다 (*InConnectionString*), 데이터 원본에 의해 정의 된 제한을 위반 합니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*szMessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY000|일반 오류: 잘못 된 파일 dsn|(DM) 문자열에서 **InConnectionString* FILEDSN 키워드를 포함 하지만.dsn 파일의 이름을 찾을 수 없습니다.|  
|HY000|일반 오류: 파일 버퍼를 만들 수 없습니다.|(DM) 문자열에서 **InConnectionString* FILEDSN 키워드를 포함 하지만.dsn 파일을 읽을 수 없습니다.|  
|HY001|메모리 할당 오류|드라이버 관리자를 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다는 **SQLDriverConnect** 함수입니다.<br /><br /> 드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *ConnectionHandle*합니다. 함수 호출 및 실행을 완료 하기 전에 [SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md) 에서 호출 된 합니다 *ConnectionHandle*, 차례로 합니다 **SQLDriverConnect** 다시 호출 된 함수는 *ConnectionHandle*합니다.<br /><br /> 또는 **SQLDriverConnect** 함수가 호출 되 고 실행을 완료 하기 전에 **SQLCancelHandle** 에서 호출한 합니다 *ConnectionHandle* 의 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) 비동기적으로 실행 하는 또 다른 함수 (되지 **SQLDriverConnect**)에 대해 호출 된 합니다 *ConnectionHandle* 때 계속 실행 하 고는 **SQLDriverConnect** 함수가 호출 되었습니다.|  
|HY013|메모리 관리 오류|합니다 **SQLDriverConnect** 기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 했으므로 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|인수에 대 한 지정 된 값 (DM) *StringLength1* 0 보다 작은 및 SQL_NTS이 아닙니다.<br /><br /> 인수에 대 한 지정 된 값 (DM) *BufferLength* 0 보다 작습니다.|  
|HY092|잘못 된 특성/옵션 식별자입니다.|(DM)는 *DriverCompletion* 인수가 SQL_DRIVER_PROMPT 하며 *WindowHandle* 인수가 null 포인터입니다.|  
|HY110|잘못 된 드라이버 완료|인수에 지정 된 값 (DM) *DriverCompletion* 가 SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED 이면 또는 SQL_DRIVER_NOPROMPT 없습니다.<br /><br /> (DM) 연결 풀링을 사용 하 고 인수에 지정 된 값 *DriverCompletion* SQL_DRIVER_NOPROMPT 같음 없습니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|드라이버는 응용 프로그램이 요청 하는 ODBC 동작의 버전을 지원 하지 않습니다.|  
|HYT00|제한 시간이 만료되었습니다.|완료 된 데이터 원본에 연결 하기 전에 로그인 제한 시간이 만료 되었습니다. 시간 제한 기간을 통해 설정 됩니다 **SQLSetConnectAttr**을 SQL_ATTR_LOGIN_TIMEOUT입니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 지정 된 데이터 원본 이름에 해당 하는 드라이버가 함수를 지원 하지 않습니다.|  
|IM002|데이터 원본을 찾을 수 없습니다 및 없습니다 지정 하지 않았습니다.|(DM) 데이터 원본 연결 문자열에 지정 된 이름 (*InConnectionString*)에서 시스템 정보를 찾을 수 없습니다 및 기본 드라이버 사양이 없는 했습니다.<br /><br /> (DM) 시스템 정보에 ODBC 데이터 원본 및 기본 드라이버 정보를 찾을 수 없습니다.|  
|IM003|지정 된 드라이버를 로드할 수 없습니다.|(DM) 드라이버의 시스템 정보를 데이터 원본 사양에 나열 된 또는 지정 된 된 **드라이버** 키워드 찾을 수 없거나 다른 이유로 로드할 수 없습니다.|  
|IM004|운전 **SQLAllocHandle** SQL_HANDLE_ENV 실패에서|(DM) 중 **SQLDriverConnect**, 드라이버 관리자가 드라이버를 호출 **SQLAllocHandle** 함수를 *fHandleType* 반환 SQL_HANDLE_ENV 및 드라이버는 오류가 발생 했습니다.|  
|IM005|운전 **SQLAllocHandle** 에서 SQL_HANDLE_DBC 실패 했습니다.|(DM) 중 **SQLDriverConnect**, 드라이버 관리자가 드라이버를 호출 **SQLAllocHandle** 함수를 *fHandleType* 반환 SQL_HANDLE_DBC 및 드라이버는 오류가 발생 했습니다.|  
|IM006|운전 **SQLSetConnectAttr** 실패|(DM) 하는 동안 **SQLDriverConnect**, 드라이버 관리자가 드라이버의 호출 **SQLSetConnectAttr** 함수 및 드라이버에서 오류를 반환 합니다.|  
|IM007|없는 데이터 원본 또는 드라이버 지정 금지 하는 대화 상자|없는 데이터 원본 이름 또는 드라이버 연결 문자열에 지정 된 하 고 *DriverCompletion* SQL_DRIVER_NOPROMPT 되었습니다.|  
|IM008|실패 대화 상자|드라이버는 해당 로그인 대화 상자를 표시 하려고를 실패 했습니다.<br /><br /> *WindowHandle* 가 null 포인터 및 *DriverCompletion* SQL_DRIVER_NO_PROMPT 없습니다.|  
|IM009|변환 DLL을 로드할 수 없습니다.|드라이버 변환 연결 또는 데이터 원본에 대 한 지정 된 DLL을 로드할 수 없습니다.|  
|IM010|데이터 원본 이름이 너무 깁니다.|(DM)는 DSN 키워드에 대 한 특성 값을 SQL_MAX_DSN_LENGTH 자를 초과 했습니다.|  
|IM011|드라이버 이름이 너무 깁니다.|(DM) 특성 값을 **드라이버** 키워드가 255 자입니다.|  
|IM012|드라이버 키워드 구문 오류입니다.|에 대 한 (DM) 키워드-값 쌍을 **드라이버** 키워드 구문 오류가 포함 합니다.<br /><br /> (DM)의 문자열이  *\*InConnectionString* 포함 된를 **FILEDSN** 키워드 되지만.dsn 파일이 포함 되지 않은 **드라이버** 키워드 또는  **DSN** 키워드입니다.|  
|IM014|지정 된 DSN은 드라이버와 응용 프로그램 간 아키텍처 불일치를 포함합니다.|64 비트 드라이버를;에 연결 하는 DSN을 사용 하 여 (DM) 32 비트 응용 프로그램 또는 그 반대의 경우도 마찬가지입니다.|  
|IM015|드라이버의 SQLDriverConnect SQL_HANDLE_DBC_INFO_HANDLE에 실패 했습니다.|SQL_ERROR를 반환 하는 드라이버를 드라이버 관리자에서 응용 프로그램에 SQL_ERROR를 반환 하 고 연결이 실패 합니다.<br /><br /> SQL_HANDLE_DBC_INFO_TOKEN에 대 한 자세한 내용은 참조 하세요. [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)합니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
|S1118|드라이버 비동기 알림을 지원 하지 않습니다.|드라이버는 비동기 알림을 지원 하지 않습니다, SQL_ATTR_ASYNC_DBC_EVENT 또는 SQL_ATTR_ASYNC_DBC_RETCODE_PTR 설정할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 연결 문자열에 다음 구문:  
  
 *연결 문자열* :: = *빈 문자열*[;] &#124; *특성*[;] &#124; *특성*; *연결 문자열*  
  
 *empty-string* ::=*attribute* ::= *attribute-keyword*=*attribute-value* &#124; DRIVER=[{]*attribute-value*[}]  
  
 *특성-키워드* :: DSN = &#124; UID &#124; PWD &#124; *드라이버-정의-특성-키워드*  
  
 *attribute-value* ::= *character-string*  
  
 *driver-defined-attribute-keyword* ::= *identifier*  
  
 여기서 *문자열* 에 0 개 이상의 문자입니다. *식별자* 에 하나 이상의 문자입니다. *특성 키워드* 대/소문자 구분; 아닙니다 *특성-값* ; 대/소문자 구분 될 수 있습니다 및의 값을 **DSN** 키워드 공백 전적으로의 구성 되어 있지 않습니다.  
  
 연결 문자열 및 초기화 파일 문법, 키워드 및 특성 값의 문자를 포함 하는 때문 **{}(),? \*=! @** 묶지 사용 하 여 중괄호를 피해 야 합니다. 값을 **DSN** 키워드를 공백으로 구성할 수 없습니다 및 선행 공백을 포함 하지 않아야 합니다. 시스템 정보 문법을 인해 키워드 및 데이터 원본 이름은 백슬래시를 포함할 수 없습니다 (\\) 문자입니다.  
  
 응용 프로그램 뒤의 특성 값 주위에 중괄호를 추가 하지 않아도 합니다 **드라이버** 키워드 특성을 세미콜론 (;)를 포함 하지 않는 한 경우에 중괄호가 필요 합니다. 드라이버를 수신 하는 특성 값이 중괄호에 포함 된 경우 드라이버를 제거 하지 않아야 하지만 반환 된 연결 문자열의 일부가 되어야 합니다.  
  
 중괄호를 사용 하 여 포함 하는 DSN 또는 연결 문자열 값 ({}) 문자를 포함 하 **{}(),? \*=! @** 드라이버에 그대로 전달 됩니다. 그러나 키워드에서 이러한 문자를 사용할 때 드라이버 관리자 파일 Dsn 사용 하는 경우 오류를 반환 하지만 일반 연결 문자열에 대 한 드라이버 연결 문자열을 전달 합니다. 키워드 값이 포함 된 중괄호를 사용 하지 마십시오.  
  
 연결 문자열에는 드라이버에서 정의 된 키워드를 개수에 관계 없이 포함할 수 있습니다. 때문에 합니다 **드라이버** 키워드 정보 시스템 정보를 사용 하지 않습니다, 드라이버를 드라이버 연결 문자열에만 정보를 사용 하 여 데이터 원본에 연결할 수 있도록 충분 한 키워드를 정의 해야 합니다. (자세한 내용은 "드라이버에서" 나중에이 섹션의 지침 참조). 드라이버는 데이터 원본에 연결 하는 데 필요한는 키워드를 정의 합니다.  
  
 다음 표에서 특성 값을 **DSN**, **FILEDSN**, **드라이버**, **UID**, **PWD**, 및 **SAVEFILE** 키워드입니다.  
  
|키워드|특성 값 설명|  
|-------------|---------------------------------|  
|**DSN**|반환 된 데이터 원본의 이름을 **SQLDataSources** 또는 데이터 원본 대화 상자의 **SQLDriverConnect**합니다.|  
|**FILEDSN**|데이터 원본에 대 한 연결 문자열을 빌드할 수.dsn 파일의 이름입니다. 이러한 데이터 원본에 파일 데이터 원본 이라고 합니다.|  
|**드라이버**|드라이버에서 반환 된 대로 설명은 합니다 **SQLDrivers** 함수입니다. 예를 들어, Rdb 또는 SQL Server입니다.|  
|**UID**|사용자 id입니다.|  
|**PWD**|사용자 ID에 대 한 암호가 없는 경우 해당 사용자 ID 또는 빈 문자열 하는 암호 (PWD =;).|  
|**SAVEFILE**|성공한 경우 연결에 사용 된 키워드의 특성 값을 저장할 수.dsn 파일의 파일 이름입니다.|  
  
 응용 프로그램에서 데이터 원본 또는 드라이버를 선택 하는 방법에 대 한 자세한 내용은 [데이터 원본 또는 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)합니다.  
  
 키워드는 연결 문자열에서 반복 되는 경우 드라이버는 맨 처음 발견 되는 키워드를 사용 하 여 연결 된 값을 사용 합니다. 경우는 **DSN** 하 고 **드라이버** 키워드 동일한 연결 문자열에 포함 된, 드라이버 및 드라이버 관리자를 사용 하 여 어떤 키워드가 나타나는 첫 번째입니다.  
  
 합니다 **FILEDSN** 하 고 **DSN** 키워드는 함께 사용할 수 없습니다: 어떤 키워드가 나타나는 첫 번째를 사용 하 고 두 번째 나타나는 것은 무시 됩니다. 합니다 **FILEDSN** 하 고 **드라이버** 키워드, 다른 한편으로 배타적이 지 않습니다. 키워드는 연결 문자열에 있으면 **FILEDSN**,.dsn 파일에서 동일한 키워드가의 특성 값이 아닌 연결 문자열 키워드의 특성 값이 사용 됩니다.  
  
 경우는 **FILEDSN** 키워드가 사용 되는지,.dsn 파일에 지정 된 키워드는 연결 문자열을 만드는 데 사용 됩니다. (자세한 내용은 파일 데이터 원본 ","이 단원의 뒷부분 참조). 합니다 **UID** 키워드는 선택 사항 이지만.dsn 파일을 만들 수 있습니다만 합니다 **드라이버** 키워드입니다. 합니다 **PWD** 키워드.dsn 파일에 저장 되지 않습니다. 기본 디렉터리를 저장 하 고.dsn 파일을 로드 하 여 지정 된 경로의 조합 됩니다 **CommonFileDir** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ Windows\CurrentVersion 및 "ODBC\DataSources"입니다. (CommonFileDir "C:\Program Files\Common Files" 인 경우 기본 디렉터리 것 "C:\Program Files\Common Files\ODBC\Data Sources"입니다.)  
  
> [!NOTE]  
>  .Dsn 파일을 호출 하 여 직접 조작할 수 있습니다 합니다 [SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md) 하 고 [SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md) 설치 관리자 DLL의에서 함수입니다.  
  
 경우는 **SAVEFILE** 키워드가 사용 되는지, 특성 값의 이름 사용 하 여.dsn 파일로 저장할 경우 성공적인 연결에 사용 된 키워드의 특성 값을 합니다 **SAVEFILE** 키워드입니다. **SAVEFILE** 키워드와 함께에서 사용 해야 합니다는 **드라이버** 키워드는 **FILEDSN** 키워드 또는 둘 다 함수를 사용 하 여 SQL_SUCCESS_WITH_INFO를 반환 합니다. 또는 SQLSTATE 01S09 (잘못 된 키워드). 합니다 **SAVEFILE** 키워드 앞에 나타나야 합니다. 합니다 **드라이버** 키워드는 연결 문자열이 나 결과에서 정의 되지 것입니다.  
  
## <a name="driver-manager-guidelines"></a>드라이버 관리자 지침  
 드라이버 관리자에서 드라이버에 전달할 연결 문자열을 생성 합니다 *InConnectionString* 드라이버의 인수의 **SQLDriverConnect** 함수입니다. 드라이버 관리자를 수정 하지는 않습니다 합니다 *InConnectionString* 인수 응용 프로그램으로 전달 합니다.  
  
 값을 기준으로 드라이버 관리자의 작업은는 *DriverCompletion* 인수:  
  
-   SQL_DRIVER_PROMPT: 연결 문자열에 없는 경우 하나는 **드라이버**를 **DSN**, 또는 **FILEDSN** 키워드를 드라이버 관리자는 데이터 원본 대화 상자를 표시 합니다. 대화 상자에서 반환 된 데이터 원본 이름 및 응용 프로그램으로 전달 하는 다른 모든 키워드에서 연결 문자열을 생성 합니다. 드라이버 관리자는 DSN 키워드-값 쌍 지정 대화 상자에서 반환 된 데이터 원본 이름은 비어 있으면 = Default입니다. (이 대화 상자 이름 "Default"를 사용 하 여 데이터 원본 표시 되지 않습니다.)  
  
-   SQL_DRIVER_COMPLETE 또는 SQL_DRIVER_COMPLETE_REQUIRED: 응용 프로그램에서 지정 된 연결 문자열에 포함 된 경우는 **DSN** 키워드 드라이버 관리자 응용 프로그램에서 지정 된 연결 문자열을 복사 합니다. 때와 동일한 작업을 수행 하는 고, 그렇지 *DriverCompletion* SQL_DRIVER_PROMPT 됩니다.  
  
-   SQL_DRIVER_NOPROMPT: 드라이버 관리자는 응용 프로그램에서 지정 된 연결 문자열을 복사 합니다.  
  
 응용 프로그램에서 지정 된 연결 문자열을 포함 하는 경우는 **드라이버** 키워드 드라이버 관리자 응용 프로그램에서 지정 된 연결 문자열을 복사 합니다.  
  
 생성 된 연결 문자열을 사용 하 여, 드라이버 관리자를 사용할 드라이버를 확인, 해당 드라이버에 연결 및 드라이버;에 생성 된 연결 문자열을 전달 드라이버 관리자와 드라이버의 상호 작용 하는 방법에 대 한 자세한 내용은의 "설명" 섹션을 참조 하세요 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)합니다. 연결 문자열에 없는 경우는 **드라이버** 키워드를 드라이버 관리자는 다음과 같이 사용할 드라이버를 결정 합니다.  
  
1.  연결 문자열을 포함 하는 경우는 **DSN** 키워드 드라이버 관리자에서 시스템 정보를 데이터 소스에 연결 된 드라이버를 검색 합니다.  
  
2.  연결 문자열에 없는 경우는 **DSN** 시스템 정보에서 기본 데이터 소스에 연결 된 드라이버를 검색 하는 드라이버 관리자, 키워드 또는 데이터 소스를 찾을 수 없습니다. (자세한 내용은 [기본 하위 키](../../../odbc/reference/install/default-subkey.md).) 드라이버 관리자의 값을 변경 합니다 **DSN** "기본" 연결 문자열 키워드입니다.  
  
3.  경우는 **DSN** "DEFAULT"로 설정 된 연결 문자열 키워드, 드라이버 관리자 시스템 정보에서 기본 데이터 소스에 연결 된 드라이버를 검색 합니다.  
  
4.  드라이버 관리자 SQLSTATE IM002 인 sql_error가 반환 데이터 원본에 없는 경우 기본 데이터 원본을 찾을 수 없습니다 (데이터 원본을 찾을 수 없습니다 및 지정 된 기본 드라이버가 없습니다).  
  
## <a name="file-data-sources"></a>파일 데이터 원본  
 응용 프로그램에 대 한 호출에서 연결 문자열을 지정 하는 경우 **SQLDriverConnect** 포함 된 **FILEDSN** 키워드와이 키워드 중 하나에 의해 교체 되지 않으면를 **DSN**나 **드라이버** 키워드를 다음 드라이버 관리자.dsn 파일에서 정보를 사용 하 여 연결 문자열을 만듭니다 및 *InConnectionString* 인수입니다. 드라이버 관리자는 다음과 같이 진행 됩니다.  
  
1.  .Dsn 파일의 파일 이름이 올바른지 여부를 확인 합니다. 그렇지 않으면 SQLSTATE IM014 인 sql_error가 반환 하는 경우 (파일 DSN의 잘못 된 이름). 파일 이름이 빈 문자열 ("") SQL_DRIVER_NOPROMPT 아니며 지정 하면 **파일 열기** 대화 상자가 표시 됩니다. 파일 이름에 올바른 경로 하지만 파일 이름이 없거나는 잘못 된 파일 이름을 포함 하 고 SQL_DRIVER_NOPROMPT를 지정 하지 않은 경우 해당 **파일 열기** 로 파일 이름에 지정 된 현재 디렉터리를 사용 하 여 대화 상자가 표시 됩니다. 파일 이름이 빈 문자열 ("") 또는 파일 이름에 올바른 경로 하지만 파일 이름이 없거나 잘못 된 파일 이름을, SQL_DRIVER_NOPROMPT를 지정 하 고 SQLSTATE IM014를 사용 하 여 SQL_ERROR가 반환 됩니다 (잘못 된 파일 DSN 이름).  
  
2.  .Dsn 파일의 [ODBC] 섹션에서 모든 키워드를 읽습니다. 경우는 **드라이버** 키워드 없는, SQLSTATE IM012 인 sql_error가 반환 (드라이버 키워드 구문 오류), 제외한.dsn 파일을 공유할 수 있는 되지 않았고만 포함 합니다 **DSN** 키워드입니다.  
  
     드라이버 관리자의 값을 읽고 파일 데이터 소스를 공유할 수 없는 경우는 **DSN** 키워드는 공유할 수 없는 파일 데이터 원본을 가리키는 사용자 또는 시스템 데이터 원본에 필요에 따라 연결 합니다. 3-5 단계를 수행 되지 않습니다.  
  
3.  드라이버에 대 한 연결 문자열을 생성합니다. 드라이버 연결 문자열은.dsn 파일에 지정 된 키워드와 원래 응용 프로그램 연결 문자열에 지정 된 통합 합니다. 키워드 겹치는 드라이버 연결 문자열의 생성에 대 한 규칙 아래와 같습니다.  
  
    -   경우는 **드라이버** 로 지정 된 드라이버 및 응용 프로그램 연결 문자열에 있는 키워드는 **드라이버** 키워드 동일 하지 않은.dsn 파일 및 응용 프로그램 연결 문자열에는 .dsn 파일에서 드라이버 정보는 무시 됩니다 하 고 응용 프로그램 연결 문자열에서 드라이버 정보를 사용 합니다. 지정 하면 드라이버는 **드라이버** 키워드.dsn 파일 및 응용 프로그램의 연결 문자열에서 동일 하 게 됩니다 보다 우선 순위가 응용 프로그램 연결 문자열에 지정 된 모든 키워드 겹치는 경우 .dsn 파일에 지정 합니다.  
  
    -   새 연결 문자열에는 **FILEDSN** 키워드 제거 됩니다.  
  
4.  HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST 레지스트리 항목을 확인 하 여 드라이버를 로드 합니다. INI\\< 드라이버 이름\>\Driver 위치 \<드라이버 이름 >으로 지정 된 합니다 **드라이버** 키워드입니다.  
  
5.  드라이버가 새 연결 문자열을 전달합니다.  
  
 .Dsn 파일의 예제를 참조 하세요 [를 사용 하 여 파일 데이터 원본 연결](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)합니다.  
  
## <a name="savefile-keyword"></a>SAVEFILE 키워드  
 응용 프로그램에서 지정 된 연결 문자열을 포함 하는 경우는 **SAVEFILE** 키워드에 다음 드라이버 관리자 연결 문자열을.dsn 파일에 저장 합니다. 드라이버 관리자는 다음과 같이 진행 됩니다.  
  
1.  특성 값으로.dsn 파일의 파일 이름 포함 여부를 확인 합니다 **SAVEFILE** 키워드는 유효 합니다. 그렇지 않으면 SQLSTATE IM014 인 sql_error가 반환 하는 경우 (파일 DSN의 잘못 된 이름). 파일 이름의 유효성은 표준 시스템 명명 규칙에 의해 결정 됩니다. 파일 이름이 빈 문자열 ("") 및 *DriverCompletion* 인수가 SQL_DRIVER_NOPROMPT 이면 경우 파일 이름이 잘못 되었습니다. 파일 이름이 이미 있는 경우 다음 경우 *DriverCompletion* 이 SQL_DRIVER_NOPROMPT 이면 파일을 덮어씁니다. 하는 경우 *DriverCompletion* SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE 또는 SQL_DRIVER_COMPLETE_REQUIRED 이면는 파일을 덮어쓸지 여부를 지정 하 라는 메시지를 대화 상자. 선택 하지 않으면를 입력 하면 **파일 저장** 대화 상자가 나타납니다.  
  
2.  드라이버와 관계 없이 SQL_SUCCESS를 반환 및 파일 이름을 빈 문자열로 없습니다 경우 드라이버 관리자에서 반환 되는 연결 정보를 기록 합니다 *OutConnectionString* 인수에 지정 된 형식으로 지정된 된 파일에 이 섹션 앞부분의 "연결 문자열" 섹션입니다.  
  
3.  드라이버와 관계 없이 SQL_SUCCESS를 반환 하 고 파일 이름을 빈 문자열 (""), 드라이버 관리자를 호출 하는 **파일 저장** 와 일반 대화 상자를 *hwnd* 연결 정보를 쓰고 지정 반환 된 *OutConnectionString* 이 섹션 앞부분에 나오는 "연결 문자열" 섹션에 지정 된 형식으로 파일 저장 일반 대화 상자에서 지정 된 파일입니다.  
  
4.  반환 하는 경우 드라이버는 관계 없이 SQL_SUCCESS를 반환 합니다는 *OutConnectionString* 응용 프로그램에 연결 문자열을 포함 하는 인수입니다.  
  
5.  드라이버는 SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR를 반환 하는 경우 드라이버 관리자 SQLSTATE 응용 프로그램에 반환 합니다.  
  
## <a name="driver-guidelines"></a>드라이버 지침  
 드라이버를 드라이버 관리자에 의해 전달 된 연결 문자열에 포함 되는지 여부를 확인 합니다 **DSN** 하거나 **드라이버** 키워드입니다. 연결 문자열을 포함 하는 경우는 **드라이버** 키워드 드라이버 시스템 정보에서 데이터 원본에 대 한 정보를 검색할 수 없습니다. 연결 문자열을 포함 하는 경우는 **DSN** 키워드 하나 포함 되어 있지는 **DSN** 또는 **드라이버** 키워드, 드라이버는 데이터 원본에 대 한 정보를 검색할 수 있습니다 다음과 같은 시스템 정보:  
  
1.  연결 문자열을 포함 하는 경우는 **DSN** 키워드, 드라이버는 지정 된 데이터 원본에 대 한 정보를 검색 합니다.  
  
2.  연결 문자열에 없는 경우는 **DSN** 키워드를 지정된 된 데이터 소스는 찾을 수 없습니다, 또는 **DSN** 키워드 "DEFAULT"로 설정 된, 드라이버는 기본 데이터 원본에 대 한 정보를 검색 합니다. .  
  
 드라이버에서 연결 문자열에 전달 된 정보를 보강 하 여 시스템 정보를 검색 하는 모든 정보를 사용 합니다. 시스템 정보에 정보를 연결 문자열에는 정보를 복제 하는 경우 드라이버는 연결 문자열에 정보를 사용 합니다.  
  
 값을 기반으로 *DriverCompletion*, 드라이버는 사용자 ID 및 암호와 같은 연결 정보를 사용자를 데이터 원본에 연결 합니다.  
  
-   SQL_DRIVER_PROMPT: 드라이버를 사용 하 여 연결 문자열 및 시스템 정보 값 (있는 경우) 초기 값으로는 대화 상자를 표시 합니다. 대화 상자를 종료 하는 사용자, 드라이버는 데이터 원본에 연결 합니다. 값에서 연결 문자열도 생성 합니다 **DSN** 또는 **드라이버** 키워드 \* *InConnectionString* 및에서 반환 된 정보는 대화 상자입니다. 이 연결 문자열을 사용 하 여 배치를 **OutConnectionString* 버퍼입니다.  
  
-   SQL_DRIVER_COMPLETE 또는 SQL_DRIVER_COMPLETE_REQUIRED: 연결 문자열에 충분 한 정보를 포함 하는 경우 해당 정보가 올바른지 드라이버에 연결할 데이터 원본 및 복사본 \* *InConnectionString* 하려면 \* *OutConnectionString* . 모든 정보가 누락 되었거나 잘못 된 경우 드라이버는 경우와 동일한 작업을 수행 하는 *DriverCompletion* 단 SQL_DRIVER_PROMPT 됩니다 *DriverCompletion* SQL_DRIVER_COMPLETE_는 필요한 드라이버 하지 데이터 원본에 연결 하는 데 필요한 모든 정보에 대 한 제어를 해제 합니다.  
  
-   SQL_DRIVER_NOPROMPT: 충분 한 정보를 포함 하는 연결 문자열을 하는 경우 드라이버는 데이터 원본 및 복사본에 연결 \* *InConnectionString* 하려면 \* *OutConnectionString*합니다. 드라이버에 대 한 SQL_ERROR를 반환 하는 고, 그렇지 **SQLDriverConnect**합니다.  
  
 데이터 원본에 성공적으로 연결에서 드라이버 설정 \* *StringLength2Ptr* 에서 반환할 수 있는 출력 연결 문자열의 길이 **OutConnectionString*합니다.  
  
 드라이버 관리자 또는 드라이버에서 제공 되는 대화 상자를 취소 하면 **SQLDriverConnect** SQL_NO_DATA를 반환 합니다.  
  
 연결 프로세스 중 드라이버 관리자와 드라이버 상호 작용 하는 방법에 대 한 자세한 내용은 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)합니다.  
  
 드라이버에서 지 원하는 경우 **SQLDriverConnect**, 드라이버 키워드 부분 드라이버에 대 한 시스템 정보를 포함 해야 합니다는 **ConnectFunctions** 두 번째 문자를 사용 하 여 키워드 "Y"로 설정 합니다.  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>연결 풀링을 사용할 때 연결  
 연결 풀링을 통해 응용 프로그램을을 이미 만든 연결을 다시 사용할 수 있습니다. 때 **SQLDriverConnect** 라고, 드라이버 관리자 하려고 연결 풀링에 대해 지정 된 환경에서 연결 풀의 일부인 연결을 사용 하 여 연결 합니다. 연결 풀링에 대 한 자세한 내용은 참조 하세요. [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)합니다.  
  
 응용 프로그램 풀링이 활성화 되어 연결에서 SQLDisconnect를 호출 하기 전에 SQL_ATTR_RESET_CONNECTION를 설정할 수 있습니다. 자세한 내용은 [SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)합니다.  
  
 응용 프로그램을 호출 하는 경우 다음 제한 사항이 적용 **SQLDriverConnect** 풀링된 연결으로 연결 합니다.  
  
-   처리 풀링 연결을 수행 하는 경우는 **SAVEFILE** 연결 문자열 키워드가 지정 된 합니다.  
  
-   연결 풀링을 사용 하는 경우 **SQLDriverConnect** 에서만 호출할 수는 *DriverCompletion* SQL_DRIVER_NOPROMPT 인수의 같으면 **SQLDriverConnect** 라고 모든 다른 *DriverCompletion*, SQLSTATE HY110 (잘못 된 드라이버 완료가) 반환 됩니다.  
  
## <a name="connection-attributes"></a>연결 특성  
 SQL_ATTR_LOGIN_TIMEOUT 연결 특성을 사용 하 여 설정할 **SQLSetConnectAttr**, 로그인 요청을 성공적으로 연결을 사용 하 여 응용 프로그램에 반환 하기 전에 드라이버에서 완료 될 때까지 기다리는 시간 (초) 수를 정의 합니다. 연결 문자열을 완료 하려면 사용자를 사용 하는 메시지가 표시 되 면 드라이버는 연결 프로세스를 시작 하는 경우 각 로그인 요청에 대 한 대기 기간 시작 합니다.  
  
 드라이버는 기본적으로 SQL_MODE_READ_WRITE 액세스 모드에서 연결을 엽니다. SQL_MODE_READ_ONLY에 대 한 액세스 모드를 설정 하려면 응용 프로그램 호출 해야 합니다 **SQLSetConnectAttr** 호출 하기 전에 SQL_ATTR_ACCESS_MODE 특성과 **SQLDriverConnect**합니다.  
  
 데이터 원본에 대 한 시스템 정보에는 기본 변환 라이브러리를 지정 하는 경우 드라이버 파일이 로드 됩니다. 호출 하 여 다른 변환 라이브러리를 로드할 수 있습니다 **SQLSetConnectAttr** SQL_ATTR_TRANSLATE_LIB 특성을 사용 합니다. 변환 옵션을 호출 하 여 지정할 수 있습니다 **SQLSetConnectAttr** SQL_ATTR_TRANSLATE_OPTION 옵션을 사용 합니다.  
  
 자세한 내용은 [SQLDriverConnect를 사용 하 여 연결](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)합니다.  
  
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
  
 도 참조 하세요 [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|검색 및 데이터 원본에 연결 하는 데 필요한 값을 열거|[SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|데이터 원본에 연결|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|데이터 원본에서 연결 끊기|[SQLDisconnect 함수](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|드라이버 설명 및 특성을 반환합니다.|[SQLDrivers 함수](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|핸들 해제|[SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|연결 특성을 설정합니다.|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
