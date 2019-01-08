---
title: SQLSetEnvAttr 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61b83ee255e580c557bfae9923d67735c63c3912
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53202162"
---
# <a name="sqlsetenvattr-function"></a>SQLSetEnvAttr 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수 합니다. ISO 92  
  
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
 [입력] 특성을 설정 하려면 "주석입니다."에 나열 된  
  
 *ValuePtr*  
 [입력] 와 연결할 값에 대 한 포인터 *특성*합니다. 값에 따라 *특성*하십시오 *ValuePtr* 는 32 비트 정수 값 이어야 하거나 null로 끝나는 문자열을 가리킵니다.  
  
 *StringLength*  
 [입력] 하는 경우 *ValuePtr* 문자열 또는 이진 버퍼를 가리키는,이 인수 길이 여야 합니다 **ValuePtr*합니다. 문자 문자열 데이터의 경우이 인수는 문자열의 바이트 수를 포함 해야 합니다.  
  
 하는 경우 *ValuePtr* 정수 이면 *StringLength* 무시 됩니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLSetEnvAttr** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* SQL_의 HANDLE_ENV와 *처리할* 의 *EnvironmentHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLSetEnvAttr** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다. 드라이버는 환경 특성을 지원 하지 않으면, 연결 시간 동안에 오류를 반환할 수 있습니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S02|옵션 값이 변경 됨|드라이버에서 지정 된 값을 지원 하지 않았습니다 *ValuePtr* 유사한 값을 대체 합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|특성 인수는 문자열 값이 필요한 환경 특성을 식별 하며 *ValuePtr* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)에 할당 된 연결 핸들 *EnvironmentHandle*합니다.<br /><br /> (DM) **SQL_ATTR_ODBC_VERSION** 으로 설정 되어 있으면 **SQLSetEnvAttr** 하 고 *특성* 같지 **SQL_ATTR_ODBC_VERSION**합니다. 설정할 필요가 없습니다 **SQL_ATTR_ODBC_VERSION** 사용 하는 경우에 명시적으로 **SQLAllocHandleStd**합니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY024|잘못 된 특성 값|지정 된 주어진 *특성* 값을 잘못 된 값에 지정 된 *ValuePtr*합니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|합니다 *StringLength* 인수가 0 보다 작은 하지만 SQL_NTS 없습니다.|  
|HY092|잘못 된 특성/옵션 식별자입니다.|인수에 지정 된 값 (DM) *특성* ODBC 드라이버에서 지 원하는 버전에 올바르지 않습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|인수에 지정 된 값 *특성* ODBC의 버전 드라이버에서 지원 되지만 드라이버에서 지원 되지에 대 한 유효한 ODBC 환경 특성을 했습니다.<br /><br /> (DM)는 *특성* 인수가 SQL_ATTR_OUTPUT_NTS, 및 *ValuePtr* SQL_FALSE 되었습니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램에서 호출할 수 있습니다 **SQLSetEnvAttr** 환경에 없는 연결 핸들 할당 되는 경우에 합니다. 모든 환경 특성을 환경에 대 한 응용 프로그램에서 성공적으로 설정 될 때까지 지속 **SQLFreeHandle** 환경에서 호출 됩니다. 둘 이상의 환경 핸들이 ODBC 3에 동시에 할당할 수 있습니다 *.x*합니다.  
  
 정보의 형식을 통해 설정할 *ValuePtr* 지정 된 종속 *특성*합니다. **SQLSetEnvAttr** 두 가지 형식 중 하나에 대 한 특성 정보를 수락할: null로 끝나는 문자열 또는 32 비트 정수 값입니다. 형식에 대해 특성의 설명에 표시 됩니다.  
  
 드라이버 관련 환경 특성이 없는 합니다.  
  
 호출 하 여 연결 특성을 설정할 수 없습니다 **SQLSetEnvAttr**합니다. 이 작업을 수행 하려고 하면 SQLSTATE HY092 반환 됩니다 (잘못 된 특성/옵션 식별자)입니다.  
  
|*특성*|*ValuePtr* 내용|  
|-----------------|-------------------------|  
|SQL_ATTR_CONNECTION_POOLING (ODBC 3.8)|환경 수준에서 연결 풀링을 사용 하지 않도록 설정 하는 32 비트 SQLUINTEGER 값입니다. 다음 값이 사용 됩니다.<br /><br /> SQL_CP_OFF = 연결 풀링을 해제 됩니다. 기본값입니다.<br /><br /> SQL_CP_ONE_PER_DRIVER 단일 = 연결 풀은 각 드라이버에 대해 지원 됩니다. 풀의 모든 연결은 하나의 드라이버와 관련이 있습니다.<br /><br /> SQL_CP_ONE_PER_HENV 단일 = 각 환경에 대 한 연결 풀 지원 됩니다. 풀의 모든 연결은 하나의 환경 연관 되어 있습니다.<br /><br /> SQL_CP_DRIVER_AWARE 가능 하다 면 = 드라이버의 연결 풀 인식 기능을 사용 합니다. 드라이버는 연결 풀 인식을 지원 하지 않으면, SQL_CP_DRIVER_AWARE 무시 되 고 SQL_CP_ONE_PER_HENV 사용 됩니다. 자세한 내용은 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)합니다. 여기서 일부 드라이버를 지원 하 고 일부 드라이버는 연결 풀 인식을 지원 하지 않는 환경에서 SQL_CP_DRIVER_AWARE에 드라이버를 지 원하는 연결 풀 인식 기능을 사용할 수 있지만 SQL_CP_ONE_PER_HENV에서 설정 하는 것과 동일 연결 풀 인식 기능을 지원 하지 않는 드라이버.<br /><br /> 연결 풀링을 사용 하는 호출 하 여 **SQLSetEnvAttr** SQL_CP_ONE_PER_DRIVER 또는 SQL_CP_ONE_PER_HENV로 SQL_ATTR_CONNECTION_POOLING 특성을 설정 합니다. 이 호출은 응용 프로그램은 연결 풀링이 사용 하도록 설정 하는 공유 환경에서 할당 전에 수행 되어야 합니다. 호출에서 환경 핸들 **SQLSetEnvAttr** SQL_ATTR_CONNECTION_POOLING 프로세스 수준 특성을 사용 하면 null로 설정 됩니다. 그런 다음 응용 프로그램 호출 하 여 암시적 공유 환경에서 할당 연결 풀링을 사용 하도록 설정한 후 **SQLAllocHandle** 사용 하 여 합니다 *InputHandle* 인수를 SQL_HANDLE_ENV로 설정 합니다.<br /><br /> 때문에 해당 환경에 대 한 SQL_ATTR_CONNECTION_POOLING 연결 풀링을 사용 하도록 설정한 후 응용 프로그램에 대 한 공유 환경 선정 된 다시 설정할 수 없습니다 **SQLSetEnvAttr** null 환경을 사용 하 여 호출 됩니다 이 특성을 설정 하는 경우를 처리 합니다. 연결 풀링을 사용 될 때 이미 공유 환경에서이 특성이 설정 되어 특성 이후에 할당 되는 공유 환경을 영향을 줍니다.<br /><br /> 환경에서 연결 풀링을 사용 하도록 설정할 수 이기도 합니다. 환경 연결 풀링에 대 한 다음 note:<br /><br /> -연결 풀링에서 NULL 핸들을 사용 하도록 설정 하면 프로세스 수준 특성입니다. 이후에 할당 된 환경에서는 공유 환경 됩니다 및 프로세스 수준 연결 풀링 설정을 상속 합니다.<br />-Environment 할당 된 후 응용 프로그램 해당 연결 풀 설정을 변경할 수 있습니다.<br />-환경 연결 풀링을 사용 하는 연결의 드라이버는 드라이버 풀링을 사용 하 고 있으면 기본 설정을 사용 환경 풀링 합니다.<br /><br /> SQL_ATTR_CONNECTION_POOLING은 드라이버 관리자 내에서 구현 됩니다. 드라이버는 SQL_ATTR_CONNECTION_POOLING 구현할 필요가 없습니다. ODBC 2.0 및 3.0 응용 프로그램이 환경 특성을 설정할 수 있습니다.<br /><br /> 자세한 내용은 [ODBC 연결 풀링](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)을 참조하세요.|  
|SQL_ATTR_CP_MATCH (ODBC 3.0)|연결 풀에서 연결을 선택 하는 방법을 결정 하는 32 비트 SQLUINTEGER 값입니다. 때 **SQLConnect** 하거나 **SQLDriverConnect** 는 호출 드라이버 관리자 결정 연결 풀에서 다시 사용 됩니다. 드라이버 관리자 연결 옵션을 호출 및 풀의 응용 프로그램에 키워드 및 연결의 연결 특성을 설정 하는 연결 특성을 찾으려고 합니다. 이 특성의 값에 일치 하는 조건의 전체 자릿수 수준이 결정합니다.<br /><br /> 다음 값이이 특성의 값을 설정 하는 데 사용 됩니다.<br /><br /> SQL_CP_STRICT_MATCH = 호출에서 연결 옵션을 정확 하 게 일치 하는 연결만 및 응용 프로그램에 의해 설정 된 특성은 다시 연결 합니다. 기본값입니다.<br /><br /> SQL_CP_RELAXED_MATCH 연결 = 일치 연결 문자열 키워드를 사용할 수 있습니다. 키워드와 일치 해야 하지만 일부 연결 특성 일치 해야 합니다.<br /><br /> 드라이버 관리자에서 어떻게 수행 일치 하는 풀링된 연결에 연결 하는 방법에 대 한 자세한 내용은 참조 하십시오 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)합니다. 연결 풀링에 대 한 자세한 내용은 참조 하세요. [ODBC 연결 풀링](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)합니다.|  
|SQL_ATTR_ODBC_VERSION (ODBC 3.0)|특정 기능은 ODBC 2 보여 여부를 결정 하는 32 비트 정수 *.x* 동작 또는 ODBC 3 *.x* 동작 합니다. 다음 값이이 특성의 값을 설정 하는 데 사용 됩니다.<br /><br /> SQL_OV_ODBC3_80 The Driver Manager and 드라이버가 다음 ODBC 3.8 별첨 동작:<br /><br /> -드라이버는 반환 하 고 ODBC 3 개 필요한 데. *x* 날짜, 시간 및 타임 스탬프에 대 한 코드입니다.<br />-드라이버는 ODBC 3을 반환합니다. *x* SQLSTATE 코드 시기 **SQLError**, **SQLGetDiagField**, 또는 **SQLGetDiagRec** 라고 합니다.<br />- *CatalogName* 호출에서 인수 **SQLTables** 검색 패턴을 허용 합니다.<br />-드라이버 관리자는 C 데이터 형식 확장성을 지원합니다. C 데이터 형식 확장성에 대 한 자세한 내용은 참조 하세요. [odbc에서 C 데이터 형식](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)합니다.<br /><br /> 자세한 내용은 [What's New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)합니다.<br /><br /> SQL_OV_ODBC3 The Driver Manager and 드라이버가 다음 ODBC 3 별첨 *.x* 동작:<br /><br /> -드라이버는 반환 하 고 ODBC 3 개 필요한 데 *.x* 날짜, 시간 및 타임 스탬프에 대 한 코드입니다.<br />-드라이버는 ODBC 3를 반환 *.x* SQLSTATE 코드 때 **SQLError**, **SQLGetDiagField**, 또는 **SQLGetDiagRec** 라고 합니다.<br />- *CatalogName* 호출에서 인수 **SQLTables** 검색 패턴을 허용 합니다.<br />-드라이버 관리자에서 C 데이터 형식 확장성을 지원 하지 않습니다.<br /><br /> SQL_OV_ODBC2 The 드라이버 관리자와 드라이버 별첨 다음 ODBC 2 =*.x* 동작 합니다. ODBC 2에 특히 유용 *.x* 는 ODBC 3을 사용 하는 응용 프로그램 *.x* 드라이버입니다.<br /><br /> -드라이버는 반환 하며 ODBC 2 *.x* 날짜, 시간 및 타임 스탬프에 대 한 코드입니다.<br />-드라이버는 ODBC 2를 반환 *.x* SQLSTATE 코드 시기 **SQLError**, **SQLGetDiagField**, 또는 **SQLGetDiagRec** 라고 합니다.<br />- *CatalogName* 호출에서 인수 **SQLTables** 검색 패턴을 허용 하지 않습니다.<br />-드라이버 관리자에서 C 데이터 형식 확장성을 지원 하지 않습니다.<br /><br /> 응용 프로그램을 SQLHENV 인수가 있는 함수를 호출 하기 전에이 환경 특성을 설정 해야 합니다 또는 SQLSTATE HY010 반환 됩니다 (함수 시퀀스 오류). 이러한 환경 플래그에 대 한 추가 동작이 있는지 드라이버 관련 됩니다.<br /><br /> -자세한 내용은 참조 하십시오 [응용 프로그램의 ODBC 버전 선언](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) 하 고 [동작 변경 내용](../../../odbc/reference/develop-app/behavioral-changes.md)합니다.|  
|SQL_ATTR_OUTPUT_NTS (ODBC 3.0)|드라이버에서 문자열 데이터를 반환 하는 방법을 결정 하는 32 비트 정수입니다. SQL_TRUE, 드라이버 null로 끝나는 문자열 데이터를 반환 합니다. SQL_FALSE, 드라이버는 null로 끝나는 문자열 데이터를 반환 하지 않으면.<br /><br /> 이 특성 SQL_TRUE 기본값으로 사용 됩니다. 에 대 한 호출 **SQLSetEnvAttr** SQL_TRUE로 설정에 관계 없이 SQL_SUCCESS를 반환 합니다. 에 대 한 호출 **SQLSetEnvAttr** SQL_FALSE 반환 하 고 SQLSTATE HYC00 SQL_ERROR로 설정 하려면 (선택적 기능이 구현 되지 않음).|  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|환경 특성의 설정을 반환합니다.|[SQLGetEnvAttr 함수](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 3.8의 새로운 기능](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
