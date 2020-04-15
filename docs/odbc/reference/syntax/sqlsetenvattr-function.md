---
title: SQLSetEnvAttr 함수 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299543"
---
# <a name="sqlsetenvattr-function"></a>SQLSetEnvAttr 함수
**규칙**  
 버전 출시: ODBC 3.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLSetEnvAttr환경의** 측면을 제어하는 특성을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLSetEnvAttr(  
     SQLHENV      EnvironmentHandle,  
     SQLINTEGER   Attribute,  
     SQLPOINTER   ValuePtr,  
     SQLINTEGER   StringLength);  
```  
  
## <a name="arguments"></a>인수  
 *환경 핸들*  
 [입력] 환경 핸들입니다.  
  
 *특성*  
 [입력] "주석"에 나열된 설정 특성입니다.  
  
 *ValuePtr*  
 [입력] *속성에*연결할 값에 대한 포인터 . *특성값에*따라 *ValuePtr은* 32비트 정수 값또는 null 종료된 문자 문자열을 가리킵니다.  
  
 *문자열 길이*  
 [입력] *ValuePtr이* 문자 문자열 또는 이진 버퍼를 가리키는 경우 이 인수는 **ValuePtr*의 길이여야 합니다. 문자열 데이터의 경우 이 인수에는 문자열의 바이트 수가 포함되어야 합니다.  
  
 *ValuePtr이* 정수인 경우 *StringLength는* 무시됩니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLSetEnvAttr** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 SQL_HANDLE_ENV *핸들 유형* 및 *환경 핸들*핸들을 호출 *Handle* 하 여 관련 된 **SQLSTATE** 값을 가져올 수 있습니다. 다음 표에서는 **SQLSetEnvAttr에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR. 드라이버가 환경 특성을 지원하지 않는 경우 연결 시간 동안에만 오류를 반환할 수 있습니다.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01S02|옵션 값이 변경되었습니다.|드라이버는 *ValuePtr에* 지정된 값을 지원하지 않고 유사한 값을 대체했습니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY09|null 포인터의 잘못된 사용|특성 인수는 문자열 값이 필요한 환경 특성을 식별했으며 *ValuePtr* 인수는 null 포인터였습니다.|  
|HY010|함수 시퀀스 오류|(DM) *환경 핸들에*연결 핸들이 할당되었습니다.<br /><br /> (DM) **SQL_ATTR_ODBC_VERSION** **SQLSetEnvAttr로** 설정되지 않았으며 *특성이* **SQL_ATTR_ODBC_VERSION**같지 않습니다. **SQLAllocHandleStd**를 사용하는 경우 **SQL_ATTR_ODBC_VERSION** 명시적으로 설정할 필요가 없습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY024|잘못된 특성 값|지정된 *특성* 값이 주어지면 *값Ptr*에 잘못된 값이 지정되었습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|*StringLength* 인수는 0보다 작지만 SQL_NTS 않았습니다.|  
|HY092|잘못된 특성/옵션 식별자|(DM) 인수 *특성에* 대해 지정된 값이 드라이버에서 지원하는 ODBC 버전에 대해 유효하지 않습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|인수 *특성에* 대해 지정된 값은 드라이버에서 지원하는 ODBC 버전에 대한 유효한 ODBC 환경 특성이지만 드라이버에서 지원되지 않았습니다.<br /><br /> (DM) *특성* 인수가 SQL_ATTR_OUTPUT_NTS *값Ptr이* SQL_FALSE.|  
  
## <a name="comments"></a>주석  
 응용 프로그램은 환경에 연결 핸들이 할당되지 않은 경우에만 **SQLSetEnvAttr을** 호출할 수 있습니다. **SQLFreeHandle** 환경에서 호출 될 때까지 환경에 대 한 응용 프로그램에 의해 성공적으로 설정 된 모든 환경 특성 유지 합니다. ODBC *3.x에서*두 개 이상의 환경 핸들을 동시에 할당할 수 있습니다.  
  
 *ValuePtr을* 통해 설정 된 정보의 형식은 지정 된 *특성에*따라 달라 집니다. **SQLSetEnvAttr는** null 종료 된 문자 문자열 또는 32 비트 정수 값의 두 가지 형식 중 하나에서 특성 정보를 허용합니다. 각 형식은 특성 설명에 기록됩니다.  
  
 드라이버 관련 환경 특성이 없습니다.  
  
 연결 특성은 **SQLSetEnvAttr**에 대한 호출로 설정할 수 없습니다. 이렇게 하면 SQLSTATE HY092(잘못된 특성/옵션 식별자)가 반환됩니다.  
  
|*특성*|*밸류Ptr* 내용|  
|-----------------|-------------------------|  
|SQL_ATTR_CONNECTION_POOLING (ODBC 3.8)|환경 수준에서 연결 풀링을 활성화하거나 사용하지 않도록 설정하는 32비트 SQLUINTEGER 값입니다. 다음 값이 사용됩니다.<br /><br /> SQL_CP_OFF = 연결 풀링이 꺼져 있습니다. 이것이 기본값입니다.<br /><br /> SQL_CP_ONE_PER_DRIVER = 각 드라이버에 대해 단일 연결 풀이 지원됩니다. 풀의 모든 연결은 하나의 드라이버와 연결됩니다.<br /><br /> SQL_CP_ONE_PER_HENV = 각 환경에 대해 단일 연결 풀이 지원됩니다. 풀의 모든 연결은 하나의 환경과 연결됩니다.<br /><br /> SQL_CP_DRIVER_AWARE = 사용 가능한 경우 드라이버의 연결 풀 인식 기능을 사용합니다. 드라이버가 연결 풀 인식을 지원하지 않으면 SQL_CP_DRIVER_AWARE 무시되고 SQL_CP_ONE_PER_HENV 사용됩니다. 자세한 내용은 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)을 참조하십시오. 일부 드라이버가 지원하고 일부 드라이버가 연결 풀 인식을 지원하지 않는 환경에서는 SQL_CP_DRIVER_AWARE 지원 드라이버에서 연결 풀 인식 기능을 사용하도록 설정할 수 있지만 연결 풀 인식 기능을 지원하지 않는 드라이버에 대한 SQL_CP_ONE_PER_HENV 설정하는 것과 같습니다.<br /><br /> 연결 풀링은 **SQLSetEnvAttr을** 호출하여 SQL_ATTR_CONNECTION_POOLING 특성을 SQL_CP_ONE_PER_DRIVER 또는 SQL_CP_ONE_PER_HENV 설정하여 사용할 수 있습니다. 응용 프로그램에서 연결 풀링을 사용하도록 설정할 공유 환경을 할당하기 전에 이 호출을 수행해야 합니다. **SQLSetEnvAttr에** 대 한 호출에서 환경 핸들 null로 설정 됩니다., SQL_ATTR_CONNECTION_POOLING 프로세스 수준 특성을 만듭니다. 연결 풀링을 사용하도록 설정한 후 응용 프로그램은 SQL_HANDLE_ENV 설정된 *InputHandle* 인수로 **SQLAllocHandle을** 호출하여 암시적 공유 환경을 할당합니다.<br /><br /> 이 특성을 설정할 때 **SQLSetEnvAttr이** null 환경 핸들을 사용 하 여 호출 되므로 연결 풀링을 사용 하 고 응용 프로그램에 대 한 공유 환경을 선택한 후 해당 환경에 대 한 SQL_ATTR_CONNECTION_POOLING 다시 설정할 수 없습니다. 공유 환경에서 연결 풀링이 이미 활성화되어 있는 동안 이 특성이 설정된 경우 이 특성은 나중에 할당된 공유 환경에만 영향을 줍니다.<br /><br /> 환경에서 연결 풀링을 활성화할 수도 있습니다. 환경 연결 풀링에 대한 다음 사항<br /><br /> - NULL 핸들에서 연결 풀링을 활성화하는 것은 프로세스 수준 특성입니다. 이후에 할당된 환경은 공유 환경이 되며 프로세스 수준 연결 풀링 설정을 상속합니다.<br />- 환경이 할당된 후에도 응용 프로그램은 연결 풀 설정을 변경할 수 있습니다.<br />- 환경 연결 풀링을 사용하도록 설정하고 연결 드라이버가 드라이버 풀링을 사용하는 경우 환경 풀링을 선호합니다.<br /><br /> SQL_ATTR_CONNECTION_POOLING 드라이버 관리자 내부에서 구현됩니다. 드라이버는 SQL_ATTR_CONNECTION_POOLING 구현할 필요가 없습니다. ODBC 2.0 및 3.0 응용 프로그램은 이 환경 특성을 설정할 수 있습니다.<br /><br /> 자세한 내용은 [ODBC 연결 풀링](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)을 참조하세요.|  
|SQL_ATTR_CP_MATCH (ODBC 3.0)|연결 풀에서 연결이 선택되는 방법을 결정하는 32비트 SQLUINTEGER 값입니다. **SQLConnect** 또는 **SQLDriverConnect가** 호출되면 드라이버 관리자는 풀에서 다시 사용되는 연결을 결정합니다. 드라이버 관리자는 호출의 연결 옵션과 응용 프로그램에서 설정한 연결 특성을 풀의 연결의 키워드 및 연결 특성과 일치시키려고 합니다. 이 특성의 값은 일치하는 조건의 정밀도 수준을 결정합니다.<br /><br /> 다음 값은 이 특성의 값을 설정하는 데 사용됩니다.<br /><br /> SQL_CP_STRICT_MATCH = 호출의 연결 옵션과 정확히 일치하는 연결과 응용 프로그램에서 설정한 연결 특성만 다시 사용됩니다. 이것이 기본값입니다.<br /><br /> SQL_CP_RELAXED_MATCH = 일치하는 연결 문자열 키워드가 있는 연결을 사용할 수 있습니다. 키워드는 일치해야 하지만 모든 연결 특성이 일치하는 것은 아닙니다.<br /><br /> 드라이버 관리자가 풀린 연결에 연결하여 일치를 수행하는 방법에 대한 자세한 내용은 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)를 참조하십시오. 연결 풀링에 대한 자세한 내용은 [ODBC 연결 풀링을](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)참조하십시오.|  
|SQL_ATTR_ODBC_VERSION (ODBC 3.0)|특정 기능이 ODBC *2.x* 동작 또는 ODBC *3.x* 동작을 나타내는지 여부를 결정하는 32비트 정수입니다. 다음 값은 이 특성의 값을 설정하는 데 사용됩니다.<br /><br /> SQL_OV_ODBC3_80 = 드라이버 관리자 및 드라이버는 다음과 같은 ODBC 3.8 동작을 나타낸다.<br /><br /> - 드라이버가 반환하고 날짜, 시간 및 타임 스탬프에 대한 ODBC *3.x* 코드를 기대합니다.<br />- 드라이버는 **SQLError,** **SQLGetDiagField**또는 **SQLGetDiagRec가** 호출 될 때 ODBC *3.x* SQLSTATE 코드를 반환합니다.<br />- **SQLTables** 호출의 *CatalogName* 인수는 검색 패턴을 허용합니다.<br />- 드라이버 관리자는 C 데이터 형식 확장성을 지원합니다. C 데이터 형식 확장성에 대한 자세한 내용은 [ODBC의 C 데이터 유형을](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)참조하십시오.<br /><br /> 자세한 내용은 [ODBC 3.8의 새로운 내용을](../../../odbc/reference/what-s-new-in-odbc-3-8.md)참조하십시오.<br /><br /> SQL_OV_ODBC3 = 드라이버 관리자 및 드라이버는 다음과 같은 ODBC *3.x* 동작을 나타낸다.<br /><br /> - 드라이버가 반환하고 날짜, 시간 및 타임 스탬프에 대한 ODBC *3.x* 코드를 기대합니다.<br />- 드라이버는 **SQLError,** **SQLGetDiagField**또는 **SQLGetDiagRec가** 호출 될 때 ODBC *3.x* SQLSTATE 코드를 반환합니다.<br />- **SQLTables** 호출의 *CatalogName* 인수는 검색 패턴을 허용합니다.<br />- 드라이버 관리자는 C 데이터 형식 확장성을 지원하지 않습니다.<br /><br /> SQL_OV_ODBC2 = 드라이버 관리자와 드라이버는 다음과 같은 ODBC *2.x* 동작을 나타낸다. 이 기능은 ODBC *3.x* 드라이버로 작업하는 ODBC *2.x* 응용 프로그램에 특히 유용합니다.<br /><br /> - 드라이버가 반환하고 날짜, 시간 및 타임 스탬프에 대한 ODBC *2.x* 코드를 기대합니다.<br />- 드라이버는 **SQLError,** **SQLGetDiagField**또는 **SQLGetDiagRec가** 호출 될 때 ODBC *2.x* SQLSTATE 코드를 반환합니다.<br />- **SQLTables** 호출의 *CatalogName* 인수는 검색 패턴을 허용하지 않습니다.<br />- 드라이버 관리자는 C 데이터 형식 확장성을 지원하지 않습니다.<br /><br /> 응용 프로그램은 SQLHENV 인수가 있는 함수를 호출하기 전에 이 환경 특성을 설정해야 하며, 호출은 SQLSTATE HY010(함수 시퀀스 오류)을 반환합니다. 이러한 환경 플래그에 대해 추가 동작이 있는지 여부는 드라이버에 따라 다릅니다.<br /><br /> - 자세한 내용은 [응용 프로그램의 ODBC 버전](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) 및 [동작 변경](../../../odbc/reference/develop-app/behavioral-changes.md)선언을 참조하십시오.|  
|SQL_ATTR_OUTPUT_NTS (ODBC 3.0)|드라이버가 문자열 데이터를 반환하는 방법을 결정하는 32비트 정수입니다. SQL_TRUE 경우 드라이버는 null-terminated 문자열 데이터를 반환합니다. SQL_FALSE 경우 드라이버는 null-terminated 문자열 데이터를 반환하지 않습니다.<br /><br /> 이 특성은 기본적으로 SQL_TRUE. **sqlSetEnvAttr에** 대 한 호출 SQL_TRUE 반환 SQL_SUCCESS 설정 합니다. SQL_ERROR 및 SQLSTATE HYC00(선택적 기능이 구현되지 않음)을 반환하는 SQL_FALSE 설정하려면 **SQLSetEnvAttr에** 대한 호출입니다.|  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|환경 특성 설정 반환|[SQLGetEnvAttr 함수](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 3.8의 새로운 기능](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
