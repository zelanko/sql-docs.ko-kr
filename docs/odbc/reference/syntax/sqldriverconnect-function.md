---
description: SQLDriverConnect 함수(SQLDriverConnect Function)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6abdafe0a01d5c8182c5427c45545930c84e08e4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476146"
---
# <a name="sqldriverconnect-function"></a>SQLDriverConnect 함수(SQLDriverConnect Function)
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ODBC  
  
 **요약**  
 **SQLDriverConnect** 는 **SQLConnect**에 대 한 대안입니다. **SQLConnect**의 세 인수 보다 더 많은 연결 정보를 요구 하는 데이터 원본, 모든 연결 정보를 사용자에 게 표시 하는 대화 상자, 시스템 정보에 정의 되어 있지 않은 데이터 원본을 지원 합니다.  
  
 **SQLDriverConnect** 는 다음과 같은 연결 특성을 제공 합니다.  
  
-   데이터 원본 이름, 하나 이상의 사용자 Id, 하나 이상의 암호 및 데이터 원본에 필요한 기타 정보를 포함 하는 연결 문자열을 사용 하 여 연결을 설정 합니다.  
  
-   부분 연결 문자열 또는 추가 정보를 사용 하 여 연결을 설정 합니다. 이 경우 드라이버 관리자와 드라이버는 각각 사용자에 게 연결 정보를 묻는 메시지를 표시할 수 있습니다.  
  
-   시스템 정보에 정의 되어 있지 않은 데이터 원본에 대 한 연결을 설정 합니다. 응용 프로그램에서 부분 연결 문자열을 제공 하는 경우 드라이버는 사용자에 게 연결 정보를 묻는 메시지를 표시할 수 있습니다.  
  
-   Dsn 파일의 정보에서 생성 된 연결 문자열을 사용 하 여 데이터 원본에 대 한 연결을 설정 합니다.  
  
 연결이 설정 된 후 **SQLDriverConnect** 는 완료 된 연결 문자열을 반환 합니다. 응용 프로그램은 후속 연결 요청에이 문자열을 사용할 수 있습니다. 자세한 내용은 [SQLDriverConnect를 사용 하 여 연결](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)을 참조 하세요.  
  
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
 [Input] 연결 핸들입니다.  
  
 *WindowHandle*  
 입력 창 핸들입니다. 응용 프로그램은 부모 창의 핸들 (해당 되는 경우)을 전달 하거나, 창 핸들을 적용할 수 없거나 **SQLDriverConnect** 에서 대화 상자를 표시 하지 않을 경우 null 포인터를 전달할 수 있습니다.  
  
 *InConnectionString*  
 입력 전체 연결 문자열 ("주석"의 구문 참조), 부분 연결 문자열 또는 빈 문자열입니다.  
  
 *StringLength1*  
 입력 **Inconnectionstring*의 길이는 문자열이 Unicode 인 경우 문자이 고, 문자열은 ANSI 또는 DBCS 인 경우 바이트입니다.  
  
 *OutConnectionString*  
 출력 완료 된 연결 문자열의 버퍼에 대 한 포인터입니다. 대상 데이터 원본에 성공적으로 연결 되 면이 버퍼에는 완료 된 연결 문자열이 포함 됩니다. 응용 프로그램은이 버퍼에 대해 최소 1024 문자를 할당 해야 합니다.  
  
 *Outconnectionstring* 이 NULL 인 경우 *StringLength2Ptr* 는 *outconnectionstring*에서 가리키는 버퍼에서 반환 하는 데 사용할 수 있는 문자 데이터의 NULL 종료 문자를 제외 하 고 전체 문자 수를 반환 합니다.  
  
 *BufferLength*  
 입력 **Outconnectionstring* 버퍼의 길이 (문자)입니다.  
  
 *StringLength2Ptr*  
 출력 Outconnectionstring에서 반환 하는 데 사용할 수 있는 총 문자 수 (null 종결 문자 제외)를 반환할 버퍼에 대 한 포인터 \* *OutConnectionString*입니다. 반환할 수 있는 문자 수가 *Bufferlength*보다 크거나 같은 경우 outconnectionstring의 완료 된 연결 문자열은 \* *OutConnectionString* *bufferlength* 에서 null 종료 문자의 길이를 뺀 값으로 잘립니다.  
  
 *DriverCompletion*  
 입력 드라이버 관리자 또는 드라이버에서 추가 연결 정보를 확인 해야 하는지 여부를 나타내는 플래그입니다.  
  
 SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED 또는 SQL_DRIVER_NOPROMPT입니다.  
  
 자세한 내용은 "설명"을 참조 하십시오.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE 또는 SQL_STILL_EXECUTING입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLDriverConnect** 에서 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 SQLGetDiagRec의 SQL_HANDLE_DBC *fHandleType* 및 *ConnectionHandle*의 *hhandle* 으로 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLDriverConnect** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|버퍼 \* *outconnectionstring* 이 전체 연결 문자열을 반환할 만큼 크지 않아 연결 문자열이 잘렸습니다. 잘린 연결 문자열의 길이는 **StringLength2Ptr*에서 반환 됩니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01S00|잘못 된 연결 문자열 특성|연결 문자열 (*Inconnectionstring*)에 잘못 된 특성 키워드가 지정 되었지만 드라이버에서 데이터 원본에 연결할 수 있습니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01 S 02|옵션 값 변경 됨|드라이버에서 **SQLSetConnectAttr** 의 *valueptr* 인수가 가리키는 지정 된 값을 지원 하지 않고 유사한 값으로 대체 했습니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01S08|파일 DSN을 저장 하는 동안 오류 발생|* \* Inconnectionstring* 의 문자열은 **filedsn** 키워드를 포함 하지만 dsn 파일은 저장 되지 않았습니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01S09|잘못 된 키워드|(DM) * \* inconnectionstring* 의 문자열은 **SAVEFILE** 키워드를 포함 하지만 **드라이버** 또는 **filedsn** 키워드는 포함 하지 않습니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08001|클라이언트에서 연결을 설정할 수 없음|드라이버가 데이터 원본과의 연결을 설정할 수 없습니다.|  
|08002|사용 중인 연결 이름|(DM) 지정한 *ConnectionHandle* 는 이미 데이터 원본과의 연결을 설정 하는 데 사용 되었으며 연결이 아직 열려 있습니다.|  
|08004|서버에서 연결을 거부 했습니다.|데이터 소스에서 구현 정의 이유에 대 한 연결 설정을 거부 했습니다.|  
|08S01|통신 연결 오류|드라이버가 연결을 시도 하는 드라이버와 데이터 원본 간의 통신 연결이 **SQLDriverConnect** 함수 처리가 완료 되기 전에 실패 했습니다.|  
|28000|잘못 된 권한 부여 사양|연결 문자열 (*Inconnectionstring*)에 지정 된 사용자 id 또는 권한 부여 문자열 또는 둘 다가 데이터 원본에 의해 정의 된 제한을 위반 했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. * \* SzMessageText* 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY000|일반 오류: 파일 dsn이 잘못 되었습니다.|(DM) **Inconnectionstring* 의 문자열이 FILEDSN 키워드를 포함 하지만 dsn 파일의 이름을 찾을 수 없습니다.|  
|HY000|일반 오류: 파일 버퍼를 만들 수 없습니다.|(DM) **Inconnectionstring* 의 문자열이 FILEDSN 키워드를 포함 하지만 dsn 파일을 읽을 수 없습니다.|  
|HY001|메모리 할당 오류|드라이버 관리자가 **SQLDriverConnect** 함수의 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.<br /><br /> 드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*ConnectionHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 [Sqlcancelhandle 함수가](../../../odbc/reference/syntax/sqlcancelhandle-function.md) *ConnectionHandle*에서 호출 된 다음 *ConnectionHandle*에서 **SQLDriverConnect** 함수가 다시 호출 되었습니다.<br /><br /> 또는 **SQLDriverConnect** 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *ConnectionHandle* 에 대해 호출 되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) 비동기적으로 실행 되는 다른 함수 ( **SQLDriverConnect**아님)가 *ConnectionHandle* 에 대해 호출 되었으며 **SQLDriverConnect** 함수가 호출 될 때 계속 실행 중입니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없으므로 **SQLDriverConnect** 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 인수 *StringLength1* 에 지정 된 값이 0 보다 작고 SQL_NTS와 같지 않습니다.<br /><br /> (DM) 인수 *Bufferlength* 에 지정 된 값이 0 보다 작은 경우|  
|HY092|특성/옵션 식별자가 잘못 되었습니다.|(DM) *Drivercompletion* 인수가 SQL_DRIVER_PROMPT 되었고 *WindowHandle* 인수가 null 포인터입니다.|  
|HY110|드라이버 완료가 잘못 되었습니다.|(DM) 인수 *Drivercompletion* 에 지정 된 값이 SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED 또는 SQL_DRIVER_NOPROMPT와 같지 않습니다.<br /><br /> (DM) 연결 풀링이 사용 하도록 설정 되어 있고 인수 *Drivercompletion* 에 지정 된 값이 SQL_DRIVER_NOPROMPT와 같지 않습니다.|  
|HYC00|선택적 기능이 구현 되지 않음|드라이버가 응용 프로그램이 요청한 ODBC 동작의 버전을 지원 하지 않습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에 대 한 연결이 완료 되기 전에 로그인 제한 시간이 만료 되었습니다. 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT을 통해 설정 됩니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) 지정 된 데이터 원본 이름에 해당 하는 드라이버에서 함수를 지원 하지 않습니다.|  
|IM002|데이터 원본을 찾을 수 없으며 기본 드라이버가 지정 되지 않았습니다.|(DM) 연결 문자열 (*Inconnectionstring*)에 지정 된 데이터 원본 이름을 시스템 정보에서 찾을 수 없으며 기본 드라이버 사양이 없습니다.<br /><br /> (DM) ODBC 데이터 원본 및 기본 드라이버 정보를 시스템 정보에서 찾을 수 없습니다.|  
|IM003|지정한 드라이버를 로드할 수 없습니다.|(DM) 시스템 정보의 데이터 원본 사양에 나열 되었거나 **driver** 키워드에 의해 지정 된 드라이버를 찾을 수 없거나 다른 이유로 로드할 수 없습니다.|  
|IM004|SQL_HANDLE_ENV에서 드라이버의 **SQLAllocHandle** 실패|(DM) **SQLDriverConnect**를 사용 하는 동안 드라이버 관리자는 *fHandleType* SQL_HANDLE_ENV의 드라이버 **SQLAllocHandle** 함수를 호출 하 고 드라이버에서 오류를 반환 했습니다.|  
|IM005|SQL_HANDLE_DBC에서 드라이버의 **SQLAllocHandle** 가 실패 했습니다.|(DM) **SQLDriverConnect**를 사용 하는 동안 드라이버 관리자는 *fHandleType* SQL_HANDLE_DBC의 드라이버 **SQLAllocHandle** 함수를 호출 하 고 드라이버에서 오류를 반환 했습니다.|  
|IM006|드라이버의 **SQLSetConnectAttr** 실패|(DM) **SQLDriverConnect**중에 드라이버 관리자가 드라이버의 **SQLSetConnectAttr** 함수를 호출 하 고 드라이버에서 오류를 반환 했습니다.|  
|IM007|데이터 원본 또는 드라이버를 지정 하지 않았습니다. 대화 금지 됨|연결 문자열에 지정 된 데이터 원본 이름 또는 드라이버가 없으며 *Drivercompletion* 가 SQL_DRIVER_NOPROMPT 되었습니다.|  
|IM008|대화 상자 실패|드라이버가 로그인 대화 상자를 표시 하려고 했지만 실패 했습니다.<br /><br /> *WindowHandle* 가 null 포인터이 고 *drivercompletion* 가 SQL_DRIVER_NO_PROMPT 되지 않았습니다.|  
|IM009|변환 DLL을 로드할 수 없습니다.|드라이버가 데이터 원본 또는 연결에 대해 지정 된 변환 DLL을 로드할 수 없습니다.|  
|IM010|데이터 원본 이름이 너무 깁니다.|(DM) DSN 키워드에 대 한 특성 값이 SQL_MAX_DSN_LENGTH 자 보다 깁니다.|  
|IM011|드라이버 이름이 너무 깁니다.|(DM) **DRIVER** 키워드의 특성 값이 255 자 보다 깁니다.|  
|IM012|드라이버 키워드 구문 오류|(DM) **DRIVER** 키워드에 대 한 키워드-값 쌍에 구문 오류가 포함 되어 있습니다.<br /><br /> (DM) * \* inconnectionstring* 의 문자열이 **filedsn** 키워드를 포함 하 고 있지만 Dsn 파일에 **드라이버** 키워드나 **dsn** 키워드가 포함 되지 않았습니다.|  
|IM014|지정 된 DSN에 드라이버와 응용 프로그램 간의 아키텍처가 일치 하지 않습니다.|(DM) 32 비트 응용 프로그램은 64 비트 드라이버에 연결 하는 DSN을 사용 합니다. 또는 그 반대의 경우도 마찬가지입니다.|  
|IM015|SQL_HANDLE_DBC_INFO_HANDLE에서 드라이버의 SQLDriverConnect 실패|드라이버가 SQL_ERROR을 반환 하는 경우 드라이버 관리자는 응용 프로그램에 SQL_ERROR을 반환 하 고 연결에 실패 합니다.<br /><br /> SQL_HANDLE_DBC_INFO_TOKEN에 대 한 자세한 내용은 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)을 참조 하세요.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
|S1118|드라이버가 비동기 알림을 지원 하지 않습니다.|드라이버가 비동기 알림을 지원 하지 않는 경우 SQL_ATTR_ASYNC_DBC_EVENT 또는 SQL_ATTR_ASYNC_DBC_RETCODE_PTR를 설정할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 연결 문자열의 구문은 다음과 같습니다.  
  
 *연결 문자열* :: = *빈 문자열*[;] &#124; *특성*[;] &#124; *특성*; *연결 문자열*  
  
 *빈 문자열* :: =*attribute* :: = *특성-키워드* = *특성-값* &#124; DRIVER = [{]*특성-값*[}]  
  
 *특성-keyword* :: = DSN &#124; UID &#124; PWD &#124; *드라이버-정의 된 특성-키워드*  
  
 *특성-value* :: = *문자 문자열*  
  
 *드라이버 정의-키워드* :: = *식별자*  
  
 여기서 *문자 문자열* 에는 0 자 이상의 문자가 있습니다. *식별자* 에 하나 이상의 문자가 있습니다. *특성-키워드* 는 대/소문자를 구분 하지 않습니다. *특성-값* 은 대/소문자를 구분 합니다. 그리고 **DSN** 키워드 값은 공백으로만 구성 되지 않습니다.  
  
 연결 문자열 및 초기화 파일 문법을 포함 하 여 **[] {} (),;? \* 문자를 포함 하는 키워드 및 특성 값 =! @** 중괄호로 묶지 않아야 합니다. **DSN** 키워드의 값은 공백으로만 구성 될 수 없으며 선행 공백을 포함할 수 없습니다. 시스템 정보의 문법 때문에 키워드와 데이터 원본 이름에는 백슬래시 () 문자를 사용할 수 없습니다 \\ .  
  
 특성에 세미콜론 (;)이 포함 된 경우를 제외 하 고, 응용 프로그램에서는 **드라이버** 키워드 뒤에 중괄호를 추가할 필요가 없습니다. 단,이 경우에는 중괄호가 필요 합니다. 드라이버가 수신 하는 특성 값에 중괄호가 포함 된 경우 드라이버는 제거 하지 않아야 하지만 반환 된 연결 문자열의 일부 여야 합니다.  
  
 {} **[] {} (),;? \* 문자를 포함 하는 중괄호 ()로 묶인 DSN 또는 연결 문자열 값입니다. =! @** 은 드라이버에 그대로 전달 됩니다. 그러나 키워드에 이러한 문자를 사용 하는 경우 드라이버 관리자는 파일 Dsn을 사용할 때 오류를 반환 하지만 일반 연결 문자열의 경우 연결 문자열을 드라이버에 전달 합니다. 키워드 값에는 포함 된 중괄호를 사용 하지 마십시오.  
  
 연결 문자열에는 원하는 수의 드라이버 정의 키워드가 포함 될 수 있습니다. **Driver** 키워드는 시스템 정보의 정보를 사용 하지 않으므로 드라이버가 연결 문자열의 정보만 사용 하 여 데이터 원본에 연결할 수 있도록 충분 한 키워드를 정의 해야 합니다. 자세한 내용은이 섹션의 뒷부분에 나오는 "드라이버 지침"을 참조 하십시오. 드라이버는 데이터 원본에 연결 하는 데 필요한 키워드를 정의 합니다.  
  
 다음 표에서는 **DSN**, **filedsn**, **DRIVER**, **UID**, **PWD**및 **SAVEFILE** 키워드의 특성 값에 대해 설명 합니다.  
  
|키워드|특성 값 설명|  
|-------------|---------------------------------|  
|**DSN**|**Sqldatasources** 원본 또는 **SQLDriverConnect**의 데이터 원본 대화 상자에서 반환 되는 데이터 원본의 이름입니다.|  
|**FILEDSN**|데이터 원본에 대해 연결 문자열을 작성 하는 dsn 파일의 이름입니다. 이러한 데이터 소스를 파일 데이터 원본 이라고 합니다.|  
|**요소**|**Sqldrivers** 함수에서 반환 하는 드라이버에 대 한 설명입니다. 예를 들어 Rdb 또는 SQL Server입니다.|  
|**UID**|사용자 ID입니다.|  
|**PWD**|사용자 ID에 해당 하는 암호 이거나, 사용자 ID (PWD =;)의 암호가 없는 경우 빈 문자열입니다.|  
|**SAVEFILE**|존재 하는 연결을 설정 하는 데 사용 된 키워드의 특성 값을 저장 해야 하는 dsn 파일의 파일 이름입니다.|  
  
 응용 프로그램에서 데이터 원본 또는 드라이버를 선택 하는 방법에 대 한 자세한 내용은 [데이터 원본 또는 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)을 참조 하십시오.  
  
 연결 문자열에서 키워드가 반복 되는 경우 드라이버는 키워드의 첫 번째 항목과 연결 된 값을 사용 합니다. **DSN** 및 **드라이버** 키워드가 동일한 연결 문자열에 포함 되어 있으면 드라이버 관리자와 드라이버에서 가장 먼저 표시 되는 키워드를 사용 합니다.  
  
 **Filedsn** 및 **DSN** 키워드는 함께 사용할 수 없습니다. 첫 번째로 표시 되는 키워드가 사용 되며, 두 번째 표시 되는 키워드가 무시 됩니다. 반면 **Filedsn** 및 **드라이버** 키워드는 함께 사용할 수 없습니다. **Filedsn**을 사용 하 여 연결 문자열에 키워드가 나타나는 경우 dsn 파일에 있는 동일한 키워드의 특성 값 대신 연결 문자열에 있는 키워드의 특성 값이 사용 됩니다.  
  
 **Filedsn** 키워드를 사용 하는 경우 dsn 파일에 지정 된 키워드를 사용 하 여 연결 문자열을 만듭니다. 자세한 내용은이 섹션의 뒷부분에 나오는 "파일 데이터 원본"을 참조 하십시오. **UID** 키워드는 선택 사항입니다. dsn 파일은 **DRIVER** 키워드를 사용 하 여 만들 수 있습니다. **PWD** 키워드는 dsn 파일에 저장 되지 않습니다. Dsn 파일을 저장 하 고 로드 하는 기본 디렉터리는 HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\ Windows\CurrentVersion 및 "ODBC\DataSources"에서 **CommonFileDir** 에 지정 된 경로의 조합입니다. CommonFileDir가 "C:\Program Files\Common Files" 인 경우 기본 디렉터리는 "C:\Program Files\Common Files\ODBC\Data Sources"입니다.  
  
> [!NOTE]  
>  설치 관리자 DLL에서 [Sqlreadfiledsn](../../../odbc/reference/syntax/sqlreadfiledsn-function.md) 및 [sqlreadfiledsn](../../../odbc/reference/syntax/sqlwritefiledsn-function.md) 함수를 호출 하 여 dsn 파일을 직접 조작할 수 있습니다.  
  
 **SAVEFILE** 키워드를 사용 하는 경우 현재 연결을 만드는 데 사용 된 키워드의 특성 값이 **SAVEFILE** 키워드의 특성 값 이름으로 dsn 파일로 저장 됩니다. **SAVEFILE** 키워드는 **DRIVER** 키워드, **filedsn** 키워드 또는 둘 다와 함께 사용 해야 합니다. 그렇지 않으면 함수는 SQLSTATE 01S09 (잘못 된 키워드)를 사용 하 여 SQL_SUCCESS_WITH_INFO을 반환 합니다. **SAVEFILE** 키워드는 연결 문자열에서 **DRIVER** 키워드 앞에 나와야 합니다. 그렇지 않으면 결과가 정의 되지 않습니다.  
  
## <a name="driver-manager-guidelines"></a>드라이버 관리자 지침  
 드라이버 관리자는 드라이버의 **SQLDriverConnect** 함수에서 *inconnectionstring* 인수에 있는 드라이버에 전달할 연결 문자열을 생성 합니다. 드라이버 관리자는 응용 프로그램에 의해 전달 된 *Inconnectionstring* 인수를 수정 하지 않습니다.  
  
 드라이버 관리자의 작업은 *Drivercompletion* 인수의 값을 기준으로 합니다.  
  
-   SQL_DRIVER_PROMPT: 연결 문자열에 **driver**, **DSN**또는 **filedsn** 키워드가 포함 되지 않은 경우 드라이버 관리자는 데이터 원본 대화 상자를 표시 합니다. 대화 상자에서 반환 된 데이터 소스 이름과 응용 프로그램에 의해 전달 되는 다른 모든 키워드에서 연결 문자열을 생성 합니다. 대화 상자에서 반환 된 데이터 원본 이름이 비어 있는 경우 드라이버 관리자는 키워드-값 쌍 DSN = 기본값을 지정 합니다. 이 대화 상자에는 "Default" 라는 이름의 데이터 원본이 표시 되지 않습니다.  
  
-   SQL_DRIVER_COMPLETE 또는 SQL_DRIVER_COMPLETE_REQUIRED: 응용 프로그램에 지정 된 연결 문자열에 **DSN** 키워드가 포함 된 경우 드라이버 관리자는 응용 프로그램에 지정 된 연결 문자열을 복사 합니다. 그렇지 않으면 *Drivercompletion* 가 SQL_DRIVER_PROMPT 때와 동일한 작업을 수행 합니다.  
  
-   SQL_DRIVER_NOPROMPT: 드라이버 관리자는 응용 프로그램에 지정 된 연결 문자열을 복사 합니다.  
  
 응용 프로그램에 지정 된 연결 문자열에 **driver** 키워드가 포함 된 경우 드라이버 관리자는 응용 프로그램에 지정 된 연결 문자열을 복사 합니다.  
  
 구성 된 연결 문자열을 사용 하 여 드라이버 관리자는 사용할 드라이버를 결정 하 고, 해당 드라이버에 연결 하 고, 생성 된 연결 문자열을 드라이버로 전달 합니다. 드라이버 관리자와 드라이버의 상호 작용에 대 한 자세한 내용은 [SQLConnect Function](../../../odbc/reference/syntax/sqlconnect-function.md)의 "Comments" 섹션을 참조 하십시오. 연결 문자열에 **driver** 키워드가 포함 되지 않은 경우 드라이버 관리자는 다음과 같이 사용할 드라이버를 결정 합니다.  
  
1.  연결 문자열에 **DSN** 키워드가 포함 된 경우 드라이버 관리자는 시스템 정보에서 데이터 원본과 연결 된 드라이버를 검색 합니다.  
  
2.  연결 문자열이 **DSN** 키워드를 포함 하지 않거나 데이터 원본을 찾을 수 없는 경우 드라이버 관리자는 시스템 정보에서 기본 데이터 원본과 연결 된 드라이버를 검색 합니다. 자세한 내용은 [기본 하위 키](../../../odbc/reference/install/default-subkey.md)를 참조 하세요. 드라이버 관리자는 연결 문자열에서 **DSN** 키워드의 값을 "DEFAULT"로 변경 합니다.  
  
3.  연결 문자열의 **DSN** 키워드가 "default"로 설정 된 경우 드라이버 관리자는 시스템 정보에서 기본 데이터 원본과 연결 된 드라이버를 검색 합니다.  
  
4.  데이터 원본을 찾을 수 없고 기본 데이터 원본을 찾을 수 없는 경우 드라이버 관리자는 SQLSTATE IM002 (데이터 원본을 찾을 수 없으며 기본 드라이버가 지정 되지 않음)와 SQL_ERROR를 반환 합니다.  
  
## <a name="file-data-sources"></a>파일 데이터 원본  
 **SQLDriverConnect** 에 대 한 호출에서 응용 프로그램에 지정 된 연결 문자열에 **filedsn** 키워드가 포함 되어 있고이 키워드가 **dsn** 또는 **DRIVER** 키워드로 대체 되지 않는 경우 드라이버 관리자는 dsn 파일 및 *inconnectionstring* 인수에 있는 정보를 사용 하 여 연결 문자열을 만듭니다. 드라이버 관리자는 다음과 같이 진행 됩니다.  
  
1.  Dsn 파일의 파일 이름이 유효한 지 확인 합니다. 그렇지 않으면 SQLSTATE IM014를 사용 하 여 SQL_ERROR을 반환 합니다 (파일 DSN의 이름이 잘못 됨). 파일 이름이 빈 문자열 ("")이 고 SQL_DRIVER_NOPROMPT 지정 되지 않은 경우에는 **파일 열기** 대화 상자가 표시 됩니다. 파일 이름에 올바른 경로가 포함 되어 있지만 파일 이름 또는 파일 이름이 잘못 되었거나 SQL_DRIVER_NOPROMPT 지정 되지 않은 경우 파일 **열기** 대화 상자가 표시 됩니다 .이 대화 상자에는 현재 디렉터리가 파일 이름에 지정 된 것으로 설정 되어 있습니다. 파일 이름이 빈 문자열 ("") 이거나 파일 이름에 올바른 경로가 포함 되어 있지만 파일 이름이 나 잘못 된 파일 이름을 포함 하 고 SQL_DRIVER_NOPROMPT를 지정 하는 경우 SQLSTATE IM014 (파일 DSN의 잘못 된 이름)를 사용 하 여 SQL_ERROR 반환 됩니다.  
  
2.  Dsn 파일의 [ODBC] 섹션에 있는 모든 키워드를 읽습니다. **Driver** 키워드가 없으면 IM012 (드라이버 키워드 구문 오류)와 함께 SQL_ERROR 반환 합니다. 단, dsn 파일은 unshareable이 고 **dsn** 키워드만 포함 합니다.  
  
     파일 데이터 원본이 unshareable 인 경우 드라이버 관리자는 **DSN** 키워드의 값을 읽고 필요에 따라 unshareable 파일 데이터 원본에서 가리키는 사용자 또는 시스템 데이터 원본에 연결 합니다. 3 ~ 5 단계는 수행 되지 않습니다.  
  
3.  드라이버에 대 한 연결 문자열을 생성 합니다. 드라이버 연결 문자열은 dsn 파일에 지정 된 키워드와 원본 응용 프로그램 연결 문자열에 지정 된 키워드의 합집합입니다. 키워드가 겹치는 드라이버 연결 문자열의 생성에 대 한 규칙은 다음과 같습니다.  
  
    -   **드라이버** 키워드가 응용 프로그램 연결 문자열에 있고 **드라이버** 키워드로 지정 된 드라이버가 dsn 파일 및 응용 프로그램 연결 문자열에서 동일 하지 않은 경우 dsn 파일의 드라이버 정보는 무시 되 고 응용 프로그램 연결 문자열의 드라이버 정보가 사용 됩니다. **드라이버** 키워드에서 지정 된 드라이버가 dsn 파일 및 응용 프로그램의 연결 문자열에서 동일한 경우 모든 키워드가 겹치면 응용 프로그램 연결 문자열에 지정 된 드라이버가 dsn 파일에 지정 된 것 보다 우선 적용 됩니다.  
  
    -   새 연결 문자열에서 **Filedsn** 키워드를 제거 합니다.  
  
4.  <드라이버 이름 \Driver HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST.INI레지스트리 항목을 확인 하 여 드라이버를 로드 합니다 \\ \> \<Driver Name> . 여기서은 **driver** 키워드에 의해 지정 됩니다.  
  
5.  드라이버에 새 연결 문자열을 전달 합니다.  
  
 Dsn 파일의 예는 [파일 데이터 원본을 사용 하 여 연결](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)을 참조 하세요.  
  
## <a name="savefile-keyword"></a>SAVEFILE 키워드  
 응용 프로그램에 지정 된 연결 문자열에 **SAVEFILE** 키워드가 포함 된 경우 드라이버 관리자는 연결 문자열을 dsn 파일에 저장 합니다. 드라이버 관리자는 다음과 같이 진행 됩니다.  
  
1.  **SAVEFILE** 키워드의 특성 값으로 포함 된 dsn 파일의 파일 이름이 유효한 지 확인 합니다. 그렇지 않으면 SQLSTATE IM014를 사용 하 여 SQL_ERROR을 반환 합니다 (파일 DSN의 이름이 잘못 됨). 파일 이름의 유효성은 표준 시스템 명명 규칙에 따라 결정 됩니다. 파일 이름이 빈 문자열 ("")이 고 *Drivercompletion* 인수가 SQL_DRIVER_NOPROMPT 되지 않은 경우 파일 이름이 유효 합니다. 파일 이름이 이미 존재 하는 경우에는 *Drivercompletion* 가 SQL_DRIVER_NOPROMPT 되 면 파일을 덮어씁니다. *Drivercompletion* 가 SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE 또는 SQL_DRIVER_COMPLETE_REQUIRED 인 경우 대화 상자에서 파일을 덮어쓸지 여부를 지정 하 라는 메시지를 표시 합니다. 을 입력 하지 않으면 **파일-저장** 대화 상자가 나타납니다.  
  
2.  드라이버가 SQL_SUCCESS을 반환 하 고 파일 이름이 빈 문자열이 아닌 경우 드라이버 관리자는이 섹션의 앞부분에 나오는 "연결 문자열" 섹션에 지정 된 형식을 사용 하 여 *Outconnectionstring* 인수에서 반환 된 연결 정보를 지정 된 파일에 씁니다.  
  
3.  드라이버가 SQL_SUCCESS을 반환 하 고 파일 이름이 빈 문자열 ("") 인 경우 드라이버 관리자는 *hwnd* 를 지정 하 여 **파일-** 일반 저장 대화 상자를 호출 하 고 *outconnectionstring* 에서 반환 된 연결 정보를이 섹션의 앞부분에 있는 "연결 문자열" 섹션에 지정 된 형식으로 파일-공용 대화 상자에 지정 된 파일에 씁니다.  
  
4.  드라이버가 SQL_SUCCESS 반환 하는 경우 응용 프로그램에 대 한 연결 문자열을 포함 하는 *Outconnectionstring* 인수를 반환 합니다.  
  
5.  드라이버가 SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR를 반환 하는 경우 드라이버 관리자는 SQLSTATE를 응용 프로그램에 반환 합니다.  
  
## <a name="driver-guidelines"></a>드라이버 지침  
 드라이버는 드라이버 관리자에 의해 전달 된 연결 문자열에 **DSN** 또는 **driver** 키워드가 포함 되어 있는지 여부를 확인 합니다. 연결 문자열에 **driver** 키워드가 포함 된 경우 드라이버는 시스템 정보에서 데이터 원본에 대 한 정보를 검색할 수 없습니다. 연결 문자열에 **dsn** 키워드나 **driver** 키워드가 포함 되지 않은 경우 드라이버는 다음과 **DSN** 같이 시스템 정보에서 데이터 원본에 대 한 정보를 검색할 수 있습니다.  
  
1.  연결 문자열에 **DSN** 키워드가 포함 된 경우 드라이버는 지정 된 데이터 원본에 대 한 정보를 검색 합니다.  
  
2.  연결 문자열이 **dsn** 키워드를 포함 하지 않거나 지정 된 데이터 원본을 찾을 수 없는 경우 또는 **DSN** 키워드가 "default"로 설정 된 경우 드라이버는 기본 데이터 원본에 대 한 정보를 검색 합니다.  
  
 드라이버는 시스템 정보에서 검색 하는 정보를 사용 하 여 연결 문자열에 전달 된 정보를 보강 합니다. 시스템 정보의 정보가 연결 문자열의 정보를 중복 하는 경우 드라이버는 연결 문자열의 정보를 사용 합니다.  
  
 드라이버는 *Drivercompletion*값을 기준으로 사용자 ID 및 암호와 같은 연결 정보를 묻는 메시지를 표시 하 고 데이터 원본에 연결 합니다.  
  
-   SQL_DRIVER_PROMPT: 드라이버는 연결 문자열 및 시스템 정보 (있는 경우)의 값을 초기 값으로 사용 하 여 대화 상자를 표시 합니다. 사용자가 대화 상자를 종료 하면 드라이버가 데이터 원본에 연결 됩니다. 또한 inconnectionstring의 **DSN** 또는 **DRIVER** 키워드 값에서 연결 문자열을 생성 \* *InConnectionString* 하 고 대화 상자에서 반환 되는 정보를 생성 합니다. 이 연결 문자열을 **Outconnectionstring* 버퍼에 배치 합니다.  
  
-   SQL_DRIVER_COMPLETE 또는 SQL_DRIVER_COMPLETE_REQUIRED: 연결 문자열이 충분 한 정보를 포함 하 고 해당 정보가 올바르면 드라이버는 데이터 원본에 연결 하 고 \* *inconnectionstring* 을 \* *outconnectionstring*에 복사 합니다. 누락 되거나 잘못 된 정보가 있는 경우 드라이버는 *drivercompletion* 이 SQL_DRIVER_PROMPT 때와 동일한 작업을 수행 합니다. 단, *drivercompletion* 이 SQL_DRIVER_COMPLETE_REQUIRED 경우 드라이버는 데이터 원본에 연결 하는 데 필요 하지 않은 정보에 대 한 컨트롤을 사용 하지 않도록 설정 합니다.  
  
-   SQL_DRIVER_NOPROMPT: 연결 문자열에 충분 한 정보가 포함 된 경우 드라이버는 데이터 원본에 연결 하 고 \* *inconnectionstring* 을 \* *outconnectionstring*에 복사 합니다. 그렇지 않으면 드라이버는 **SQLDriverConnect**에 대 한 SQL_ERROR를 반환 합니다.  
  
 데이터 원본에 성공적으로 연결 되 면 드라이버는 \* *StringLength2Ptr* 를 **outconnectionstring*에서 반환 하는 데 사용할 수 있는 출력 연결 문자열의 길이로 설정 합니다.  
  
 사용자가 드라이버 관리자 또는 드라이버에서 제공 하는 대화 상자를 취소 하면 **SQLDriverConnect** 는 SQL_NO_DATA을 반환 합니다.  
  
 연결 프로세스 중에 드라이버 관리자와 드라이버가 상호 작용 하는 방법에 대 한 자세한 내용은 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)를 참조 하세요.  
  
 드라이버에서 **SQLDriverConnect**를 지 원하는 경우 드라이버에 대 한 시스템 정보의 드라이버 키워드 섹션에는 두 번째 문자를 "Y"로 설정 하는 **connectfunctions** 키워드가 포함 되어야 합니다.  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>연결 풀링을 사용 하는 경우 연결  
 연결 풀링을 사용 하면 응용 프로그램에서 이미 생성 된 연결을 다시 사용할 수 있습니다. **SQLDriverConnect** 가 호출 되 면 드라이버 관리자는 연결 풀링을 위해 지정 된 환경의 연결 풀에 속하는 연결을 사용 하 여 연결을 시도 합니다. 연결 풀링에 대 한 자세한 내용은 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)를 참조 하세요.  
  
 풀링을 사용 하는 연결에서 SQLDisconnect를 호출 하기 전에 응용 프로그램에서 SQL_ATTR_RESET_CONNECTION 설정할 수 있습니다. 자세한 내용은 [SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)를 참조 하세요.  
  
 응용 프로그램에서 **SQLDriverConnect** 를 호출 하 여 풀링된 연결에 연결 하는 경우 다음 제한 사항이 적용 됩니다.  
  
-   연결 문자열에 **SAVEFILE** 키워드가 지정 된 경우 연결 풀링 처리가 수행 되지 않습니다.  
  
-   연결 풀링을 사용 하는 경우 SQL_DRIVER_NOPROMPT의 *Drivercompletion* 인수를 사용 하 여 **SQLDriverConnect** 를 호출할 수 있습니다. 다른 **Drivercompletion** 를 사용 하 여 *DriverCompletion*를 호출 하면 SQLSTATE HY110 (잘못 된 드라이버 완료)가 반환 됩니다.  
  
## <a name="connection-attributes"></a>연결 특성  
 **SQLSetConnectAttr**를 사용 하 여 설정 된 SQL_ATTR_LOGIN_TIMEOUT 연결 특성은 응용 프로그램으로 반환 하기 전에 드라이버가 성공적으로 연결 되어 로그인 요청이 완료 될 때까지 대기 하는 시간 (초)을 정의 합니다. 사용자에 게 연결 문자열을 입력 하 라는 메시지가 표시 되 면 드라이버에서 연결 프로세스를 시작할 때 각 로그인 요청에 대 한 대기 기간이 시작 됩니다.  
  
 드라이버는 기본적으로 SQL_MODE_READ_WRITE 액세스 모드로 연결을 엽니다. 액세스 모드를 SQL_MODE_READ_ONLY로 설정 하려면 **SQLDriverConnect**를 호출 하기 전에 응용 프로그램에서 SQL_ATTR_ACCESS_MODE 특성을 사용 하 여 **SQLSetConnectAttr** 를 호출 해야 합니다.  
  
 데이터 원본에 대 한 시스템 정보에 기본 번역 라이브러리가 지정 된 경우 드라이버에서 해당 라이브러리를 로드 합니다. SQL_ATTR_TRANSLATE_LIB 특성을 사용 하 여 **SQLSetConnectAttr** 를 호출 하 여 다른 번역 라이브러리를 로드할 수 있습니다. SQLSetConnectAttr 옵션을 사용 SQL_ATTR_TRANSLATE_OPTION 하 여 **SQLSetConnectAttr** 를 호출 하면 translation 옵션을 지정할 수 있습니다.  
  
 자세한 내용은 [SQLDriverConnect를 사용 하 여 연결](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)을 참조 하세요.  
  
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
  
 [예제 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md)도 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|데이터 원본에 연결 하는 데 필요한 값 검색 및 열거|[SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|데이터 원본에 연결|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|데이터 원본에서 연결 끊기|[SQLDisconnect 함수](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|드라이버 설명 및 특성 반환|[SQLDrivers 함수](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|핸들 해제|[SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|연결 특성 설정|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
