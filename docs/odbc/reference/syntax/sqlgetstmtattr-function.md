---
title: SQLGetStmtAttr 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetStmtAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetStmtAttr
helpviewer_keywords:
- SQLGetStmtAttr function [ODBC]
ms.assetid: e321d460-e997-4527-aee6-207cf5a498e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89e7c75b412a6358806017102915989a8370dd43
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303307"
---
# <a name="sqlgetstmtattr-function"></a>SQLGetStmtAttr 함수
**규칙**  
 버전 출시: ODBC 3.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLGetStmtAttr** 는 문 특성의 현재 설정을 반환합니다.  
  
> [!NOTE]  
>  드라이버 관리자가 이 함수를 ODBC 3에 매핑하는 기능에 대한 자세한 내용을 참조하십시오. *x* 응용 프로그램이 ODBC 2로 작동합니다. *x* 드라이버, [응용 프로그램의 이전 버전과의 호환성에 대한 매핑 교체 함수를](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLGetStmtAttr(  
     SQLHSTMT        StatementHandle,  
     SQLINTEGER      Attribute,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *특성*  
 [입력] 검색할 특성입니다.  
  
 *ValuePtr*  
 [출력] *특성*에 지정된 특성의 값을 반환하는 버퍼에 대한 포인터 .  
  
 *ValuePtr이* NULL인 경우 *StringLengthPtr은* *ValuePtr에서*가리키는 버퍼에서 반환할 수 있는 총 바이트 수(문자 데이터에 대한 null 종료 문자 제외)를 반환합니다.  
  
 *버퍼 길이*  
 [입력] *특성이* ODBC 정의 특성이고 *ValuePtr이* 문자 문자열 또는 이진 버퍼를 가리키는 \*경우 이 인수는 *ValuePtr*의 길이여야 합니다. *특성이* ODBC 정의 특성이고 \* *ValuePtr이* 정수인 경우 *버퍼길이무시됩니다.* * \*ValuePtr에서* 반환되는 값이 유니코드 문자열인 **경우(SQLGetStmtAttrW를**호출할 때) *BufferLength* 인수는 짝수여야 합니다.  
  
 *특성이* 드라이버 정의 특성인 경우 응용 프로그램은 *BufferLength* 인수를 설정하여 드라이버 관리자에 대한 특성의 특성을 나타냅니다. *BufferLength에는* 다음 값이 있을 수 있습니다.  
  
-   * \*ValuePtr이* 문자 문자열에 대한 포인터인 경우 *BufferLength는* 문자열의 길이 또는 SQL_NTS.  
  
-   * \*ValuePtr이* 이진 버퍼에 대한 포인터인 경우 응용 프로그램은 *버퍼길이*에 SQL_LEN_BINARY_ATTR(길이) 매크로의 결과를 배치합니다.*length* 이렇게 하면 *버퍼길이에*음수 값이 배치됩니다.  
  
-   * \*ValuePtr이* 문자열 문자열 이나 이진 문자열 이외의 값에 대 한 포인터 인 경우 *BufferLength* 값 SQL_IS_POINTER 있어야 합니다.  
  
-   * \*ValuePtr* 고정 길이 데이터 형식이 포함되어 있는 경우 *BufferLength는* 적절하게 SQL_IS_INTEGER 또는 SQL_IS_UINTEGER.  
  
 *문자열길이Ptr*  
 [출력] * \*ValuePtr에서*반환할 수 있는 총 바이트 수(null-termination 문자 제외)를 반환하는 버퍼에 대한 포인터입니다. *ValuePtr이* null 포인터인 경우 길이가 반환되지 않습니다. 특성 값이 문자 문자열이고 반환할 수 있는 바이트 수가 *BufferLength보다*크거나 같으면 * \*ValuePtr의* 데이터는 *BufferLength에* 잘려null 종료 문자의 길이를 뺀 값으로 잘리며 드라이버에 의해 null-종료됩니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetStmtAttr** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *핸들 유형* SQL_HANDLE_STMT 및 *명령문* *핸들* 핸들을 사용하는 **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 **SQLGetStmtAttr에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|* \*ValuePtr에서* 반환된 데이터는 Null 종료 문자의 길이를 뺀 *버퍼길이로* 잘렸습니다. 잘린 문자열 값의 길이는 **StringLengthPtr에서*반환됩니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|24000|잘못된 커서 상태|인수 *특성이* SQL_ATTR_ROW_NUMBER 커서가 열리지 않았거나 결과 집합이 시작되기 전이나 결과 집합이 끝난 후에 커서가 배치되었습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. 인수 *MessageText에서* **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류및 그 원인을 설명합니다.|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. **SQLGetStmtAttr** 함수가 호출될 때 이 비동기 함수는 여전히 실행 중이었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 *함수는 StatementHandle에* 대 한 호출 하 고이 함수를 호출 하는 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|*(DM) \*ValuePtr은* 문자 문자열이며 BufferLength는 0보다 작지만 SQL_NTS 같지는 않습니다.|  
|HY092|잘못된 특성/옵션 식별자|인수 *특성에* 대해 지정된 값이 드라이버에서 지원하는 ODBC 버전에 대해 유효하지 않습니다.|  
|HY109|잘못된 커서 위치|*특성* 인수가 SQL_ATTR_ROW_NUMBER 행이 삭제되었거나 가져올 수 없습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|인수 *특성에* 대해 지정된 값은 드라이버에서 지원하는 ODBC 버전에 대한 유효한 ODBC 문 특성이지만 드라이버에서 지원되지 않았습니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle에* 해당하는 드라이버는 기능을 지원하지 않습니다.|  
  
## <a name="comments"></a>주석  
 명령문 특성에 대한 일반 정보는 [명령문 특성 을](../../../odbc/reference/develop-app/statement-attributes.md)참조하십시오.  
  
 **SQLGetStmtAttr에** 대한 호출은 * \*ValuePtr에서* *특성*에 지정된 명령문 특성의 값을 반환합니다. 이 값은 SQLULEN 값 또는 null 종료 된 문자 문자열일 수 있습니다. 값이 SQLULEN 값인 경우 일부 드라이버는 버퍼의 하위 32비트 또는 16비트만 작성하고 상위 순서의 비트를 변경하지 않고 그대로 둘 수 있습니다. 따라서 응용 프로그램은 SQLULEN 버퍼를 사용하고 이 함수를 호출하기 전에 값을 0으로 초기화해야 합니다. 또한 *버퍼 길이* 및 *StringLengthPtr* 인수는 사용 되지 않습니다. 값이 null-terminated 문자열인 경우 응용 프로그램은 *BufferLength* 인수에서 해당 문자열의 최대 길이를 지정하고 드라이버는 * \*StringLengthPtr* 버퍼에서 해당 문자열의 길이를 반환합니다.  
  
 **SQLGetStmtAttr을** 호출하는 응용 프로그램이 ODBC 2와 함께 작동하도록 허용합니다. *x* 드라이버, **SQLGetStmtAttr에** 대한 호출은 드라이버 관리자에서 **SQLGetStmt옵션에**매핑됩니다.  
  
 다음 문 특성은 읽기 전용이므로 **SQLGetStmtAttr에서**검색할 수 있지만 **SQLSetStmtAttr에서**설정하지는 않습니다.  
  
-   SQL_ATTR_IMP_PARAM_DESC  
  
-   SQL_ATTR_IMP_ROW_DESC  
  
-   SQL_ATTR_ROW_NUMBER  
  
 설정하고 검색할 수 있는 특성 목록은 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)을 참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|연결 특성의 설정 반환|[SQLGetConnectAttr 함수(SQLGetConnectAttr Function)](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|연결 특성 설정|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
