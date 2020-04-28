---
title: SQLSetEnvAttr 함수 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetEnvAttr
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetEnvAttr
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC]
ms.assetid: 0343241c-4b15-4d4b-aa2b-2e8ab5215cd2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 640b1e6947d67b92e2b7f8e623597e1d99d4a877
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299543"
---
# <a name="sqlsetenvattr-function"></a>SQLSetEnvAttr 함수
**규칙**  
 소개 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLSetEnvAttr** 는 환경의 여러 측면을 제어 하는 특성을 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLSetEnvAttr(  
     SQLHENV      EnvironmentHandle,  
     SQLINTEGER   Attribute,  
     SQLPOINTER   ValuePtr,  
     SQLINTEGER   StringLength);  
```  
  
## <a name="arguments"></a>인수  
 *EnvironmentHandle*  
 입력 환경 핸들.  
  
 *특성도*  
 입력 설정할 특성입니다. "Comments"에 나열 되어 있습니다.  
  
 *ValuePtr*  
 입력 *특성과*연결 될 값에 대 한 포인터입니다. *특성*의 값에 *따라, 요소는 32* 비트 정수 값 이거나 null로 끝나는 문자열을 가리킵니다.  
  
 *StringLength*  
 입력 *Valueptr* 이 문자열 또는 이진 버퍼를 가리키는 경우이 인수는 **valueptr*의 길이 여야 합니다. 문자열 데이터의 경우이 인수는 문자열의 바이트 수를 포함 해야 합니다.  
  
 *Valueptr* 이 정수 이면 *stringlength* 는 무시 됩니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLSetEnvAttr** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_ENV의 *HandleType* 및 *EnvironmentHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLSetEnvAttr** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다. 드라이버가 환경 특성을 지원 하지 않는 경우 연결 시간 동안에만 오류를 반환할 수 있습니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01 S 02|옵션 값 변경 됨|드라이버가 *Valueptr* 에 지정 된 값을 지원 하지 않고 유사한 값으로 대체 되었습니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY009|Null 포인터 사용이 잘못 되었습니다.|특성 인수는 문자열 값을 요구 하는 환경 특성을 식별 하 고, 값 *Eptr* 인수는 null 포인터입니다.|  
|HY010|함수 시퀀스 오류|(DM) *EnvironmentHandle*에 연결 핸들이 할당 되었습니다.<br /><br /> (DM) **SQL_ATTR_ODBC_VERSION** **SQLSetEnvAttr** 를 사용 하 여 설정 되지 않았습니다. *특성* 은 **SQL_ATTR_ODBC_VERSION**와 같지 않습니다. **SQLAllocHandleStd**를 사용 하는 경우 **SQL_ATTR_ODBC_VERSION** 를 명시적으로 설정할 필요가 없습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY024|잘못 된 특성 값|지정 된 *특성* 값이 지정 된 경우에는 잘못 된 값이 *valueptr*에 지정 되었습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|*Stringlength* 인수가 0 보다 작지만 SQL_NTS 되지 않았습니다.|  
|HY092|특성/옵션 식별자가 잘못 되었습니다.|(DM) 인수 *특성* 에 지정 된 값이 드라이버에서 지 원하는 ODBC 버전에 적합 하지 않습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|인수 *특성* 에 지정 된 값이 드라이버에서 지원 되는 odbc 버전에 대 한 올바른 odbc 환경 특성 이지만 드라이버에서 지원 하지 않습니다.<br /><br /> (DM) *특성* 인수가 SQL_ATTR_OUTPUT_NTS 되었으며,이는 *SQL_FALSE 되었습니다.*|  
  
## <a name="comments"></a>주석  
 응용 프로그램은 환경에 연결 핸들이 할당 되지 않은 경우에만 **SQLSetEnvAttr** 를 호출할 수 있습니다. 환경에 대해 응용 프로그램에서 설정 하는 모든 환경 특성은 **Sqlfreehandle** 이 환경에서 호출 될 때까지 지속 됩니다. 두 개 이상의 환경 핸들 *을 ODBC 3.x*에서 동시에 할당할 수 있습니다.  
  
 *Valueptr* 을 통해 설정 된 정보 형식은 지정 된 *특성*에 따라 다릅니다. **SQLSetEnvAttr** 는 null로 끝나는 문자열 또는 32 비트 정수 값의 두 가지 형식 중 하나로 특성 정보를 허용 합니다. 각의 형식은 특성의 설명에 설명 되어 있습니다.  
  
 드라이버별 환경 특성은 없습니다.  
  
 **SQLSetEnvAttr**를 호출 하 여 연결 특성을 설정할 수 없습니다. 이 작업을 수행 하려고 하면 SQLSTATE HY092 (잘못 된 특성/옵션 식별자)가 반환 됩니다.  
  
|*특성도*|*ValuePtr* 이상 내용|  
|-----------------|-------------------------|  
|SQL_ATTR_CONNECTION_POOLING (ODBC 3.8)|환경 수준에서 연결 풀링을 사용 하거나 사용 하지 않도록 설정 하는 32 비트 SQLUINTEGER 값입니다. 사용 되는 값은 다음과 같습니다.<br /><br /> SQL_CP_OFF = 연결 풀링이 해제 되어 있습니다. 기본값입니다.<br /><br /> SQL_CP_ONE_PER_DRIVER = 각 드라이버에 대해 단일 연결 풀이 지원 됩니다. 풀의 모든 연결은 하나의 드라이버와 연결 됩니다.<br /><br /> SQL_CP_ONE_PER_HENV = 단일 연결 풀이 각 환경에 대해 지원 됩니다. 풀의 모든 연결은 하나의 환경에 연결 됩니다.<br /><br /> SQL_CP_DRIVER_AWARE = 사용 가능한 경우 드라이버의 연결 풀 인식 기능을 사용 합니다. 드라이버가 연결 풀 인식을 지원 하지 않는 경우 SQL_CP_DRIVER_AWARE 무시 되 고 SQL_CP_ONE_PER_HENV 사용 됩니다. 자세한 내용은 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)을 참조 하세요. 일부 드라이버에서 및 일부 드라이버를 지 원하는 환경에서 연결 풀 인식을 지원 하지 않는 경우 해당 지원 드라이버에 대 한 연결 풀 인식 기능을 사용 하도록 설정할 수 SQL_CP_DRIVER_AWARE 있지만 연결 풀 인식 기능을 지원 하지 않는 드라이버에서 SQL_CP_ONE_PER_HENV로 설정 하는 것과 같습니다.<br /><br /> **SQLSetEnvAttr** 를 호출 하 여 SQL_ATTR_CONNECTION_POOLING 특성을 SQL_CP_ONE_PER_DRIVER 또는 SQL_CP_ONE_PER_HENV로 설정 하면 연결 풀링이 활성화 됩니다. 응용 프로그램에서 연결 풀링을 사용 하도록 설정할 공유 환경을 할당 하기 전에이 호출을 수행 해야 합니다. **SQLSetEnvAttr** 에 대 한 호출의 환경 핸들은 null로 설정 되며,이를 통해 프로세스 수준 특성을 SQL_ATTR_CONNECTION_POOLING 합니다. 연결 풀링을 사용 하도록 설정한 후에는 응용 프로그램에서 *InputHandle* 인수가 SQL_HANDLE_ENV로 설정 된 **SQLAllocHandle** 를 호출 하 여 암시적 공유 환경을 할당 합니다.<br /><br /> 연결 풀링을 사용 하도록 설정 하 고 응용 프로그램에 대해 공유 환경을 선택한 후에는이 특성을 설정할 때 null 환경 핸들을 사용 하 여 **SQLSetEnvAttr** 를 호출 하므로 해당 환경에 대해 SQL_ATTR_CONNECTION_POOLING를 다시 설정할 수 없습니다. 공유 환경에서 연결 풀링을 이미 사용 하도록 설정 하는 동안이 특성이 설정 된 경우이 특성은 나중에 할당 된 공유 환경에만 영향을 줍니다.<br /><br /> 환경에서 연결 풀링을 사용 하도록 설정할 수도 있습니다. 환경 연결 풀링을 위한 다음 사항에 유의 하세요.<br /><br /> -NULL 핸들에서 연결 풀링을 사용 하도록 설정 하는 것은 프로세스 수준 특성입니다. 이후에 할당 된 환경은 공유 환경이 되며 프로세스 수준 연결 풀링 설정을 상속 합니다.<br />-환경이 할당 된 후에도 응용 프로그램에서 연결 풀 설정을 변경할 수 있습니다.<br />-환경 연결 풀링이 사용 하도록 설정 되어 있고 연결의 드라이버가 드라이버 풀링을 사용 하는 경우 환경 풀링이 우선적으로 적용 됩니다.<br /><br /> SQL_ATTR_CONNECTION_POOLING는 드라이버 관리자 내에서 구현 됩니다. 드라이버는 SQL_ATTR_CONNECTION_POOLING를 구현할 필요가 없습니다. ODBC 2.0 및 3.0 응용 프로그램은이 환경 특성을 설정할 수 있습니다.<br /><br /> 자세한 내용은 [ODBC 연결 풀링](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)을 참조하세요.|  
|SQL_ATTR_CP_MATCH (ODBC 3.0)|연결 풀에서 연결을 선택 하는 방법을 결정 하는 32 비트 SQLUINTEGER 값입니다. **SQLConnect** 또는 **SQLDriverConnect** 가 호출 되 면 드라이버 관리자는 풀에서 다시 사용 되는 연결을 결정 합니다. 드라이버 관리자는 호출의 연결 옵션과 응용 프로그램에서 설정 하는 연결 특성을 풀에 있는 연결의 키워드 및 연결 특성에 일치 시 키 려 고 합니다. 이 특성의 값은 일치 조건의 전체 자릿수 수준을 결정 합니다.<br /><br /> 이 특성의 값을 설정 하는 데 사용 되는 값은 다음과 같습니다.<br /><br /> SQL_CP_STRICT_MATCH = 호출의 연결 옵션과 정확히 일치 하는 연결과 응용 프로그램에 설정 된 연결 특성이 다시 사용 됩니다. 기본값입니다.<br /><br /> SQL_CP_RELAXED_MATCH = 연결 문자열 키워드가 일치 하는 연결을 사용할 수 있습니다. 키워드가 일치 해야 하지만 일부 연결 특성이 일치 해야 합니다.<br /><br /> 풀 연결에 대 한 연결에서 드라이버 관리자가 일치를 수행 하는 방법에 대 한 자세한 내용은 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)를 참조 하세요. 연결 풀링에 대 한 자세한 내용은 [ODBC 연결 풀링](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)을 참조 하세요.|  
|SQL_ATTR_ODBC_VERSION (ODBC 3.0)|특정 *기능이 odbc 2.x* *동작 또는 odbc 2.x* 동작을 보여 주는 지 여부를 결정 하는 32 비트 정수입니다. 이 특성의 값을 설정 하는 데 사용 되는 값은 다음과 같습니다.<br /><br /> SQL_OV_ODBC3_80 = 드라이버 관리자와 드라이버는 다음과 같은 ODBC 3.8 동작을 나타냅니다.<br /><br /> -드라이버는를 반환 하 고 날짜, 시간 및 타임 스탬프에 대 *한 ODBC 2.x* 코드를 예상 합니다.<br />- **SQLError**, **SQLGetDiagField**또는 **SQLGetDiagRec** 를 호출 하면 드라이버 *에서 ODBC 3.x* SQLSTATE 코드를 반환 합니다.<br />- **Sqltables** 호출의 *CatalogName* 인수는 검색 패턴을 허용 합니다.<br />-드라이버 관리자는 C 데이터 형식 확장성을 지원 합니다. C 데이터 형식 확장성에 대 한 자세한 내용은 [ODBC의 c 데이터 형식](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)을 참조 하세요.<br /><br /> 자세한 내용은 [ODBC 3.8의 새로운 기능](../../../odbc/reference/what-s-new-in-odbc-3-8.md)을 참조 하세요.<br /><br /> SQL_OV_ODBC3 = 드라이버 관리자와 드라이버는 다음과 같은 ODBC 2.x 동작을 *나타냅니다* .<br /><br /> -드라이버는를 반환 하 고 날짜, 시간 및 타임 스탬프에 대 *한 ODBC 2.x* 코드를 예상 합니다.<br />- **SQLError**, **SQLGetDiagField**또는 **SQLGetDiagRec** 를 호출 하면 드라이버 *에서 ODBC 3.x* SQLSTATE 코드를 반환 합니다.<br />- **Sqltables** 호출의 *CatalogName* 인수는 검색 패턴을 허용 합니다.<br />-드라이버 관리자는 C 데이터 형식 확장성을 지원 하지 않습니다.<br /><br /> SQL_OV_ODBC2 = 드라이버 관리자와 드라이버는 다음과 *같은 ODBC 2.x* 동작을 나타냅니다. 이 기능은 odbc 2.x *드라이버를* 사용 하 여 작업 하는 odbc *2.x 응용 프로그램* 에 특히 유용 합니다.<br /><br /> -드라이버는를 반환 하 고 날짜, 시간 및 타임 스탬프에 대 *한 ODBC 2.x* 코드를 예상 합니다.<br />- **SQLError**, **SQLGetDiagField**또는 **SQLGetDiagRec** 를 호출 하면 드라이버 *에서 ODBC 2.x* SQLSTATE 코드를 반환 합니다.<br />- **Sqltables** 호출의 *CatalogName* 인수는 검색 패턴을 허용 하지 않습니다.<br />-드라이버 관리자는 C 데이터 형식 확장성을 지원 하지 않습니다.<br /><br /> 응용 프로그램은 SQLHENV 인수가 있는 함수를 호출 하기 전에이 환경 특성을 설정 해야 합니다. 그렇지 않으면 호출에서 SQLSTATE HY010 (함수 시퀀스 오류)가 반환 됩니다. 이러한 환경 플래그에 대 한 추가 동작이 있는지 여부에 대 한 드라이버 전용입니다.<br /><br /> -자세한 내용은 [응용 프로그램의 ODBC 버전 선언](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) 및 [동작 변경](../../../odbc/reference/develop-app/behavioral-changes.md)을 참조 하세요.|  
|SQL_ATTR_OUTPUT_NTS (ODBC 3.0)|드라이버가 문자열 데이터를 반환 하는 방법을 결정 하는 32 비트 정수입니다. SQL_TRUE 경우 드라이버는 null로 끝나는 문자열 데이터를 반환 합니다. SQL_FALSE 경우 드라이버는 null로 끝나는 문자열 데이터를 반환 하지 않습니다.<br /><br /> 이 특성의 기본값은 SQL_TRUE입니다. **SQLSetEnvAttr** 를 호출 하 SQL_TRUE로 설정 하 SQL_SUCCESS를 반환 합니다. **SQLSetEnvAttr** 를 호출 하 SQL_FALSE로 설정 하면 SQL_ERROR 및 SQLSTATE HYC00 (선택적 기능이 구현 되지 않음)를 반환 합니다.|  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|환경 특성의 설정 반환|[SQLGetEnvAttr 함수](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 3.8의 새로운 기능](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
