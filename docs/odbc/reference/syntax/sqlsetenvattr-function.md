---
title: SQLSetEnvAttr 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLSetEnvAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetEnvAttr
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC]
ms.assetid: 0343241c-4b15-4d4b-aa2b-2e8ab5215cd2
caps.latest.revision: 38
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1355ec6fc86872547019cc0dda74fc356b5680c9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetenvattr-function"></a>SQLSetEnvAttr 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLSetEnvAttr** 환경의 측면을 제어 하는 특성을 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLSetEnvAttr(  
     SQLHENV      EnvironmentHandle,  
     SQLINTEGER   Attribute,  
     SQLPOINTER   ValuePtr,  
     SQLINTEGER   StringLength);  
```  
  
## <a name="arguments"></a>인수  
 *EnvironmentHandle*  
 [입력] 환경 핸들입니다.  
  
 *특성*  
 [입력] 특성을 설정 하려면 "설명"에 나열 된  
  
 *ValuePtr*  
 [입력] 연결 된 값에 대 한 포인터 *특성*합니다. 값에 따라 *특성*, *ValuePtr* 에서 32 비트 정수 값 이어야 하거나 null로 끝나는 문자열을 가리킵니다.  
  
 *stringLength*  
 [입력] 경우 *ValuePtr* 문자열 또는 이진 버퍼를 가리키거나,이 인수 길이 여야 합니다 **ValuePtr*합니다. 문자 문자열 데이터에 대 한이 인수는 문자열의 바이트 수를 포함 해야 합니다.  
  
 경우 *ValuePtr* 정수 이면 *StringLength* 는 무시 됩니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLSetEnvAttr** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* SQL_의 HANDLE_ENV 및 *처리* 의 *EnvironmentHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLSetEnvAttr** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다. 드라이버 환경 특성을 지원 하지 않으면 연결 시간 중에 오류를 반환할 수 있습니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S02|옵션 값이 변경 됨|드라이버에 지정 된 값을 지원 하지 않았습니다 *ValuePtr* 유사한 값을 대체 합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|특성 인수는 문자열 값을 필요한 환경 특성을 식별 및 *ValuePtr* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)에 할당 된 연결 핸들 *EnvironmentHandle*합니다.<br /><br /> (DM) **SQL_ATTR_ODBC_VERSION** 으로 설정 되지 않은 **SQLSetEnvAttr** 및 *특성* 과 같지 않은 **SQL_ATTR_ODBC_VERSION**합니다. 설정할 필요가 없습니다 **SQL_ATTR_ODBC_VERSION** 사용 하는 경우에 명시적으로 **SQLAllocHandleStd**합니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY024|잘못 된 특성 값|지정 된 주어진 *특성* 값에 잘못 된 값을 지정 된 *ValuePtr*합니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|*StringLength* 에 인수가 0 보다 작지 않음 SQL_NTS 없습니다.|  
|HY092|잘못 된 특성/옵션 식별자|인수에 대해 지정 된 값 (DM) *특성* ODBC 드라이버에서 지 원하는 버전에 대해 올바르지 않습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|인수에 대해 지정 된 값 *특성* ODBC의 버전은 드라이버에서 지원 되지만 드라이버에서 지원 하지 않아 유효한 ODBC 환경 특성을 했습니다.<br /><br /> DM ()는 *특성* SQL_ATTR_OUTPUT_NTS, 되었습니다 및 *ValuePtr* SQL_FALSE 되었습니다.|  
  
## <a name="comments"></a>설명  
 응용 프로그램에서 호출할 수 **SQLSetEnvAttr** 환경에 없는 연결 핸들을 할당 한 경우에 합니다. 모든 환경 특성 환경에 대 한 응용 프로그램에 의해 성공적으로 설정 될 때까지 지속 **SQLFreeHandle** 환경에서 호출 됩니다. ODBC 3에서 개 이상의 환경 핸들을 동시에 할당 될 수 *.x*합니다.  
  
 정보의 형식을 통해 설정 *ValuePtr* 했는지에 따라 지정 된 *특성*합니다. **SQLSetEnvAttr** 두 가지 형식 중 하나에 대 한 특성 정보를 수락할: null로 끝나는 문자열 또는 32 비트 정수 값입니다. 각각의 형식 특성의 설명에 표시 됩니다.  
  
 드라이버 관련 환경 특성이 없는 합니다.  
  
 호출 하 여 연결 특성을 설정할 수 없습니다 **SQLSetEnvAttr**합니다. 이 작업을 수행 하려고 하면 SQLSTATE HY092 반환 됩니다 (잘못 된 특성/옵션 식별자)입니다.  
  
|*특성*|*ValuePtr* 내용|  
|-----------------|-------------------------|  
|SQL_ATTR_CONNECTION_POOLING (ODBC 3.8)|환경 수준에서 연결 풀링을 사용 하지 않도록 설정 하거나 사용 하는 32 비트 SQLUINTEGER 값입니다. 다음 값을 사용 합니다.<br /><br /> SQL_CP_OFF = 연결 풀링이 해제 되어 있습니다. 기본값입니다.<br /><br /> SQL_CP_ONE_PER_DRIVER 단일 = 연결 풀은 각 드라이버에 대해 지원 됩니다. 모든 연결 풀에서 하나의 드라이버와 관련이 있습니다.<br /><br /> SQL_CP_ONE_PER_HENV 단일 = 연결 풀은 각 환경에 대해 지원 됩니다. 모든 연결 풀에서 하나의 환경와 관련이 있습니다.<br /><br /> SQL_CP_DRIVER_AWARE 가능 하다 면 = 연결 풀 인식 기능의 드라이버를 사용 합니다. 드라이버 인식 연결 풀을 지원 하지 않으면 SQL_CP_DRIVER_AWARE 무시 되 고 SQL_CP_ONE_PER_HENV 사용 됩니다. 자세한 내용은 참조 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)합니다. 일부 드라이버를 지원 하 고 일부 드라이버 인식 연결 풀을 지원 하지 않는 있는 환경에서는 SQL_CP_DRIVER_AWARE 드라이버를 지 원하는 항목에 연결 풀 인식 기능을 사용할 수 있지만에 SQL_CP_ONE_PER_HENV 하는 설정에 해당 하는 연결 풀 인식 기능을 지원 하지 않는 해당 드라이버입니다.<br /><br /> 연결 풀링을 사용 하는 호출 하 여 **SQLSetEnvAttr** SQL_CP_ONE_PER_DRIVER 또는 SQL_CP_ONE_PER_HENV로 SQL_ATTR_CONNECTION_POOLING 특성을 설정 합니다. 이 호출 응용 프로그램에서 사용 하도록 설정 하는 연결에 대 한 풀링는 공유 환경 할당 되기 전에 수행 되어야 합니다. 환경 핸들에 대 한 호출에서 **SQLSetEnvAttr** SQL_ATTR_CONNECTION_POOLING 프로세스 수준 특성을 낮추는 null로 설정 됩니다. 그런 다음 응용 프로그램 호출 하 여 암시적 공유 환경에서 할당 연결 풀링을 사용 하도록 설정한 후 **SQLAllocHandle** 와 *InputHandle* 인수를 SQL_HANDLE_ENV로 설정 합니다.<br /><br /> 연결 풀링이 사용 된 후 응용 프로그램에 대 한 공유 환경 선택 SQL_ATTR_CONNECTION_POOLING 다시 설정할 수 없습니다 해당 환경에 대 한 때문에 **SQLSetEnvAttr** null 환경으로 호출 이 특성을 설정 하는 경우를 처리 합니다. 이 특성은 연결 풀링을 공유 환경에서 이미 사용 되는 동안 설정, 특성 이후에 할당 되는 공유 환경을 영향을 받습니다.<br /><br /> 환경에 대해 연결 풀링을 설정도 가능 합니다. 환경 연결 풀링에 대 한 다음 note:<br /><br /> -연결 풀링 NULL 핸들에 대해 사용 하도록 설정 프로세스 수준 특성입니다. 이후에 할당 된 공유 환경 됩니다 환경과 프로세스 수준의 연결 풀링 설정을 상속 합니다.<br />-환경을 할당 된 후 응용 프로그램에 해당 연결 풀 설정을 변경할 수 있습니다.<br />-환경 연결 풀링을 사용 하 고 연결의 드라이버 드라이버 풀링을 사용 하 여, 환경 풀링 내용이 기본 설정 됩니다.<br /><br /> SQL_ATTR_CONNECTION_POOLING은 드라이버 관리자 내부 구현 됩니다. 드라이버는 SQL_ATTR_CONNECTION_POOLING 구현할 필요는 없습니다. ODBC 2.0 및 3.0 응용 프로그램이 환경 특성을 설정할 수 있습니다.<br /><br /> 자세한 내용은 참조 [ODBC 연결 풀링](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)합니다.|  
|SQL_ATTR_CP_MATCH (ODBC 3.0)|연결 풀에서 연결을 선택 하는 방법을 결정 하는 32 비트 SQLUINTEGER 값입니다. 때 **SQLConnect** 또는 **SQLDriverConnect** 은 호출 드라이버 관리자 결정는 연결 풀에서 다시 사용 됩니다. 드라이버 관리자 연결 옵션 호출 및 풀의 키워드 및 연결의 연결 특성을 응용 프로그램이 설정한 연결 특성에 일치 시 키 려 합니다. 이 특성의 값에 일치 하는 조건의 전체 자릿수 수준을 결정합니다.<br /><br /> 다음 값을 사용 하 여이 특성의 값을 설정 합니다.<br /><br /> SQL_CP_STRICT_MATCH = 호출에는 연결 옵션을 정확 하 게 일치 하는 전용 연결 및 응용 프로그램에 의해 설정 된 특성을 다시 사용 된 연결입니다. 기본값입니다.<br /><br /> SQL_CP_RELAXED_MATCH 연결 = 일치 연결 문자열 키워드를 사용할 수 있습니다. 키워드와 일치 해야 하지만 일부 연결 특성이 일치 해야 합니다.<br /><br /> 드라이버 관리자 풀링된 연결에 대 한 연결에 일치를 수행 하는 방법에 대 한 자세한 내용은 참조 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)합니다. 연결 풀링에 대 한 자세한 내용은 참조 [ODBC 연결 풀링](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)합니다.|  
|SQL_ATTR_ODBC_VERSION (ODBC 3.0)|특정 기능 ODBC 2에서는 있는지 여부를 결정 하는 32 비트 정수 *.x* 동작이 나 ODBC 3 *.x* 동작 합니다. 다음 값을 사용 하 여이 특성의 값을 설정 합니다.<br /><br /> SQL_OV_ODBC3_80 = The 드라이버 관리자, 드라이버 우리 다음 ODBC 3.8 동작:<br /><br /> -ODBC 3 드라이버를 반환 합니다. *x* 날짜, 시간 및 타임 스탬프에 대 한 코드입니다.<br />-드라이버는 ODBC 3을 반환합니다. *x* 경우 SQLSTATE 코드 **SQLError**, **SQLGetDiagField**, 또는 **SQLGetDiagRec** 호출 됩니다.<br />- *CatalogName* 인수에 대 한 호출에 **SQLTables** 검색 패턴을 허용 합니다.<br />드라이버 관리자-C 데이터 형식 확장성을 지원합니다. C 데이터 형식 확장성에 대 한 자세한 내용은 참조 [odbc에서 C 데이터 형식을](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)합니다.<br /><br /> 자세한 내용은 참조 [What's New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)합니다.<br /><br /> SQL_OV_ODBC3 The 드라이버 관리자와 드라이버 우리는 다음과 같은 ODBC 3 =*.x* 동작:<br /><br /> -드라이버 반환 하 고 ODBC 3에서는 *.x* 날짜, 시간 및 타임 스탬프에 대 한 코드입니다.<br />-드라이버 ODBC 3을 반환 합니다.*.x* 경우 SQLSTATE 코드 **SQLError**, **SQLGetDiagField**, 또는 **SQLGetDiagRec** 호출 됩니다.<br />- *CatalogName* 인수에 대 한 호출에 **SQLTables** 검색 패턴을 허용 합니다.<br />-드라이버 관리자에서 C 데이터 형식 확장성을 지원 하지 않습니다.<br /><br /> SQL_OV_ODBC2 The 드라이버 관리자와 드라이버 우리 다음 ODBC 2 =*.x* 동작 합니다. ODBC 2에 특히 유용 *.x* ODBC 3을 사용 하는 응용 프로그램 *.x* 드라이버입니다.<br /><br /> -드라이버 반환 하 고 ODBC 2에서는 *.x* 날짜, 시간 및 타임 스탬프에 대 한 코드입니다.<br />-하면 드라이버는 ODBC 2 반환 *.x* 경우 SQLSTATE 코드 **SQLError**, **SQLGetDiagField**, 또는 **SQLGetDiagRec** 호출 됩니다.<br />- *CatalogName* 인수에 대 한 호출에 **SQLTables** 검색 패턴을 사용할 수 없습니다.<br />-드라이버 관리자에서 C 데이터 형식 확장성을 지원 하지 않습니다.<br /><br /> 응용 프로그램 SQLHENV 인수에 있는 모든 함수를 호출 하기 전에이 환경 특성을 설정 해야 합니다 또는 호출이 SQLSTATE HY010 반환 됩니다 (함수 시퀀스 오류). 이러한 환경 플래그에 대 한 추가 동작이 존재 하는지 여부 드라이버 관련 됩니다.<br /><br /> -자세한 내용은 참조 [응용 프로그램의 ODBC 버전 선언](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) 및 [변경 된 동작](../../../odbc/reference/develop-app/behavioral-changes.md)합니다.|  
|SQL_ATTR_OUTPUT_NTS (ODBC 3.0)|드라이버에서 문자열 데이터를 반환 하는 방법을 결정 하는 32 비트 정수입니다. SQL_TRUE, 드라이버 null로 끝나는 문자열 데이터를 반환 합니다. 경우 SQL_FALSE, 드라이버는 null로 끝나는 문자열 데이터를 반환 하지 않습니다.<br /><br /> 이 특성 SQL_TRUE 기본값으로 사용 됩니다. 에 대 한 호출 **SQLSetEnvAttr** SQL_TRUE로 설정에 관계 없이 SQL_SUCCESS를 반환 합니다. 에 대 한 호출 **SQLSetEnvAttr** SQL_FALSE 반환 하 고 SQLSTATE HYC00 SQL_ERROR로 설정 하려면 (선택 사항 기능이 구현 되지 않았습니다)입니다.|  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|환경 특성의 설정을 반환합니다.|[SQLGetEnvAttr 함수](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 3.8의 새로운 기능](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
