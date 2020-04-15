---
title: SQLGetEnvAttr 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetEnvAttr
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLGetEnvAttr
helpviewer_keywords:
- SQLGetEnvAttr function [ODBC]
ms.assetid: 01f4590f-427a-4280-a1c3-18de9f7d86c1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 77cd24386a8eea6769aee59f3674b681c516d9ed
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285313"
---
# <a name="sqlgetenvattr-function"></a>SQLGetEnvAttr 함수
**규칙**  
 버전 출시: ODBC 3.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLGetEnvAttr** 환경 특성의 현재 설정을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLGetEnvAttr(  
     SQLHENV        EnvironmentHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>인수  
 *환경 핸들*  
 [입력] 환경 핸들입니다.  
  
 *특성*  
 [입력] 검색할 특성입니다.  
  
 *ValuePtr*  
 [출력] *특성*에 의해 지정된 특성의 현재 값을 반환하는 버퍼에 대한 포인터 .  
  
 *ValuePtr이* NULL인 경우 *StringLengthPtr은* *ValuePtr에서*가리키는 버퍼에서 반환할 수 있는 총 바이트 수(문자 데이터에 대한 null 종료 문자 제외)를 반환합니다.  
  
 *버퍼 길이*  
 [입력] *ValuePtr이* 문자 문자열을 가리키는 경우 이 인수는 \* *ValuePtr*의 길이여야 합니다. \* *ValuePtr이* 정수인 경우 *버퍼길이는* 무시됩니다. * \*ValuePtr이* 유니코드 문자열인 **경우(SQLGetEnvAttrW를**호출할 때) *버퍼길이* 인수는 짝수여야 합니다. 특성 값이 문자 문자열이 아닌 경우 *BufferLength는* 사용되지 않습니다.  
  
 *문자열길이Ptr*  
 [출력] * \*ValuePtr에서*반환할 수 있는 총 바이트 수(null-termination 문자 제외)를 반환하는 버퍼에 대한 포인터입니다. *ValuePtr이* null 포인터인 경우 길이가 반환되지 않습니다. 특성 값이 문자 문자열이고 반환할 수 있는 바이트 수가 *BufferLength보다*크거나 같으면 \* *ValuePtr의* 데이터는 *BufferLength에* 잘려null 종료 문자의 길이를 뺀 값으로 잘리며 드라이버에 의해 null-종료됩니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetEnvAttr** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 *경우,* SQL_HANDLE_ENV 핸들 유형 및 *환경 핸들*핸들을 사용하는 *Handle* **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 **SQLGetEnvAttr에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|\* *ValuePtr에서* 반환된 데이터는 null 종료 문자를 뺀 *버퍼길이로* 잘렸습니다. 잘린 문자열 값의 길이는 **StringLengthPtr에서*반환됩니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) **SQL_ATTR_ODBC_VERSION** 아직 **SQLSetEnvAttr을**통해 설정되지 않았습니다. **SQLAllocHandleStd**를 사용하는 경우 **SQL_ATTR_ODBC_VERSION** 명시적으로 설정할 필요가 없습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY092|잘못된 특성/옵션 식별자|인수 *특성에* 대해 지정된 값이 드라이버에서 지원하는 ODBC 버전에 대해 유효하지 않습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|인수 *특성에* 대해 지정된 값은 드라이버에서 지원하는 ODBC 버전에 대한 유효한 ODBC 환경 특성이지만 드라이버에서 지원되지 않았습니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *환경핸들에* 해당하는 드라이버가 기능을 지원하지 않습니다.|  
  
## <a name="comments"></a>주석  
 특성 목록은 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)을 참조하십시오. 드라이버 관련 환경 특성이 없습니다. *특성이* 문자열을 반환하는 특성을 지정하는 경우 *ValuePtr은* 문자열을 반환하는 버퍼에 대한 포인터여야 합니다. null-termination 바이트를 포함한 문자열의 최대 길이는 *BufferLength* 바이트입니다.  
  
 **SQLGetEnvAttr** 할당 및 환경 핸들 해제 사이에 언제든지 호출할 수 있습니다. **sqlFreeHandle SQL_HANDLE_ENV** *핸들 타입을* 사용 하 여 *환경 핸들에* 호출 될 때까지 환경에 대 한 응용 프로그램에 의해 성공적으로 설정 된 모든 환경 특성 유지 합니다. ODBC 3 *.x.* 한 환경의 환경 특성은 다른 환경이 할당된 경우 영향을 받지 않습니다.  
  
> [!NOTE]
>  SQL_ATTR_OUTPUT_NTS 환경 특성은 표준을 준수하는 응용 프로그램에서 지원됩니다. **SQLGetEnvAttr이** 호출될 때 ODBC 3 *.x* 드라이버 관리자는 항상 이 특성에 대해 SQL_TRUE 반환합니다. SQL_ATTR_OUTPUT_NTS **SQLSetEnvAttr에**대한 호출만 으로 SQL_TRUE 설정할 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|연결 특성의 설정 반환|[SQLGetConnectAttr 함수(SQLGetConnectAttr Function)](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|문 특성의 설정 반환|[SQLGetStmtAttr 함수](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|연결 특성 설정|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|환경 특성 설정|[SQLSetEnvAttr 함수](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
