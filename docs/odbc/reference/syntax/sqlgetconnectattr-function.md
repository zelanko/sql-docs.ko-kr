---
title: SQLGetConnectAttr 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectAttr
helpviewer_keywords:
- SQLGetConnectAttr function [ODBC]
ms.assetid: 2cb4ffa8-19d3-4664-8c2f-6682cdcc3f33
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6076f14ff0c33fec38b99e9c43b8a688970a7a9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285633"
---
# <a name="sqlgetconnectattr-function"></a>SQLGetConnectAttr 함수(SQLGetConnectAttr Function)
**규칙**  
 버전 출시: ODBC 3.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLGetConnectAttr** 연결 특성의 현재 설정을 반환 합니다.  
  
> [!NOTE]
>  ODBC 3 *.x* 응용 프로그램이 ODBC 2 *.x* 드라이버로 작업할 때 드라이버 관리자가 이 함수를 매핑하는 작업에 대한 자세한 내용은 [응용 프로그램의 이전 버전과의 호환성에 대한 매핑 교체 함수를](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLGetConnectAttr(  
     SQLHDBC        ConnectionHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>인수  
 *연결 핸들*  
 [Input] 연결 핸들입니다.  
  
 *특성*  
 [입력] 검색할 특성입니다.  
  
 *ValuePtr*  
 [출력] *특성에*의해 지정된 특성의 현재 값을 반환하는 메모리에 대한 포인터 . 정수 형식 특성의 경우 일부 드라이버는 버퍼의 하위 32비트 또는 16비트만 작성하고 상위 순서의 비트를 변경하지 않고 그대로 둘 수 있습니다. 따라서 응용 프로그램은 SQLULEN 버퍼를 사용하고 이 함수를 호출하기 전에 값을 0으로 초기화해야 합니다.  
  
 *ValuePtr이* NULL인 경우 *StringLengthPtr은* *ValuePtr에서*가리키는 버퍼에서 반환할 수 있는 총 바이트 수(문자 데이터에 대한 null 종료 문자 제외)를 반환합니다.  
  
 *버퍼 길이*  
 [입력] *특성이* ODBC 정의 특성이고 *ValuePtr이* 문자 문자열 또는 이진 버퍼를 가리키는 \*경우 이 인수는 *ValuePtr*의 길이여야 합니다. *특성이* ODBC 정의 특성이고 \* *ValuePtr이* 정수인 경우 *버퍼길이무시됩니다.* ValuePtr의 값이 유니코드 문자열인 **경우(SQLGetConnectAttrW를**호출할 때) *버퍼길이* 인수는 짝수여야 합니다. * \**  
  
 *특성이* 드라이버 정의 특성인 경우 응용 프로그램은 *BufferLength* 인수를 설정하여 드라이버 관리자에 대한 특성의 특성을 나타냅니다. *BufferLength에는* 다음 값이 있을 수 있습니다.  
  
-   * \*ValuePtr이* 문자 문자열에 대한 포인터인 경우 *BufferLength는* 문자열의 길이입니다.  
  
-   * \*ValuePtr이* 이진 버퍼에 대한 포인터인 경우 응용 프로그램은*SQL_LEN_BINARY_ATTR(길이)* 매크로의 결과를 *BufferLength*에 배치합니다. 이렇게 하면 *버퍼길이에*음수 값이 배치됩니다.  
  
-   * \*ValuePtr이* 문자열 문자열 이나 이진 문자열 이외의 값에 대 한 포인터 인 경우 *BufferLength* 값 SQL_IS_POINTER 있어야 합니다.  
  
-   * \*ValuePtr* 고정 길이 데이터 형식이 포함 된 경우 *BufferLength는* SQL_IS_INTEGER 또는 SQL_IS_UINTEGER 적절 하 게.  
  
 *문자열길이Ptr*  
 [출력] \* *ValuePtr에서*반환할 수 있는 총 바이트 수(null-termination 문자 제외)를 반환하는 버퍼에 대한 포인터입니다. \* *ValuePtr이* null 포인터인 경우 길이가 반환되지 않습니다. 특성 값이 문자 문자열이고 반환할 수 있는 바이트 수가 *bufferLength에서* null 종료 문자의 길이를 뺀 값인 경우 * \*ValuePtr의* 데이터는 Null 종료 문자의 길이를 뺀 *BufferLength로* 잘리고 드라이버에 의해 null-종료됩니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetConnectAttr** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우, 연결 된 SQLSTATE 값 SQL_HANDLE_DBC *핸들 SQL_HANDLE_DBC* 및 *연결 핸들의* **핸들을** 호출 하 여 진단 데이터 구조에서 가져올 수 있습니다. *Handle* 다음 표에서는 **SQLGetConnectAttr에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|\* *ValuePtr에서* 반환된 데이터는 Null 종료 문자의 길이를 뺀 *버퍼길이로* 잘렸습니다. 잘린 문자열 값의 길이는 **StringLengthPtr에서*반환됩니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08003|연결이 열려 있지 않음|(DM) 열린 연결이 필요한 *특성* 값이 지정되었습니다.|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. **SQLGetDiagField의** *MessageText* 인수로 진단 데이터 구조에서 반환된 오류 메시지는 오류와 그 원인을 설명합니다.|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) **SQLBrowseConnect는** *연결 핸들에* 대 한 호출 하 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 **SQLBrowseConnect가** SQL_SUCCESS_WITH_INFO 또는 SQL_SUCCESS 반환하기 전에 호출되었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *연결 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) * \*ValuePtr은* 문자 문자열이며 버퍼길이는 0보다 작지만 SQL_NTS 같지는 않습니다.|  
|HY092|잘못된 특성/옵션 식별자|인수 *특성에* 대해 지정된 값이 드라이버에서 지원하는 ODBC 버전에 대해 유효하지 않습니다.|  
|HY14|드라이버는 연결 수준 비동기 함수 실행을 지원하지 않습니다.|(DM) 응용 프로그램이 비동기 연결 작업을 지원하지 않는 드라이버에 대해 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 사용하여 비동기 함수 실행을 사용하도록 설정하려고 했습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|인수 *특성에* 대해 지정된 값은 드라이버에서 지원하는 ODBC 버전에 대한 유효한 ODBC 연결 특성이지만 드라이버에서 지원되지 않았습니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *연결 핸들에* 해당하는 드라이버는 기능을 지원하지 않습니다.|  
  
## <a name="comments"></a>주석  
 연결 특성에 대한 일반 정보는 [연결 특성 을](../../../odbc/reference/develop-app/connection-attributes.md)참조하십시오.  
  
 설정할 수 있는 특성 목록은 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)을 참조하십시오. *특성이* 문자열을 반환하는 특성을 지정하는 경우 *ValuePtr은* 문자열에 대한 버퍼에 대한 포인터여야 합니다. null-termination 문자를 포함 하 여 반환 된 문자열의 최대 길이 *BufferLength* 바이트 됩니다.  
  
 특성에 따라 응용 프로그램은 **SQLGetConnectAttr**을 호출하기 전에 연결을 설정할 필요가 없습니다. 그러나 **SQLGetConnectAttr이** 호출되고 지정된 특성에 기본값이 없으며 **SQLSetConnectAttr에**대한 사전 호출에 의해 설정되지 않은 경우 **SQLGetConnectAttr은** SQL_NO_DATA 반환합니다.  
  
 *특성이* trace 또는 SQL_ATTR_ traceFILE과 SQL_ATTR_ 경우 *연결 핸들이* 유효할 필요가 없으며 **SQLGetConnectAttr은** SQL_ERROR 반환하거나 *연결 핸들이* 잘못된 경우 SQL_INVALID_HANDLE 반환하지 않습니다. 이러한 특성은 모든 연결에 적용됩니다. **SQLGetConnectAttr** 다른 인수가 잘못되면 SQL_ERROR 반환하거나 SQL_INVALID_HANDLE.  
  
 응용 프로그램이 **SQLSetConnectAttr을**사용하여 문 특성을 설정할 수 있지만 응용 프로그램은 **SQLGetConnectAttr을** 사용하여 문 특성 값을 검색할 수 없습니다. 문 특성 설정을 검색하려면 **SQLGetStmtAttr을** 호출해야 합니다.  
  
 SQL_ATTR_AUTO_IPD 및 SQL_ATTR_CONNECTION_DEAD 연결 특성은 **SQLGetConnectAttr** 호출로 반환할 수 있지만 **SQLSetConnectAttr**에 대한 호출로 설정할 수 없습니다.  
  
> [!NOTE]  
>  **SQLGetConnectAttr에**대한 비동기 지원은 없습니다. **SQLGetConnectAttr을**구현할 때 드라이버는 서버에서 정보를 보내거나 요청하는 횟수를 최소화하여 성능을 향상시킬 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|문 특성의 설정 반환|[SQLGetStmtAttr 함수](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|연결 특성 설정|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|환경 특성 설정|[SQLSetEnvAttr 함수](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
