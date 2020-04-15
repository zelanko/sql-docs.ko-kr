---
title: SQLGetCursorName 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetCursorName
helpviewer_keywords:
- SQLGetCursorName function [ODBC]
ms.assetid: e6e92199-7bb6-447c-8987-049a4c6ce05d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d3ac65dc07897ddc789ee03b06b1bc1f71d37c3c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285551"
---
# <a name="sqlgetcursorname-function"></a>SQLGetCursorName 함수(SQLGetCursorName Function)
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLGetCursorName** 지정된 명령문과 연관된 커서 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLGetCursorName(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CursorName,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   NameLengthPtr);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *커서 이름*  
 [출력] 커서 이름을 반환할 버퍼에 대한 포인터입니다.  
  
 *CursorName이* NULL인 경우 *NameLengthPtr은* *CursorName로*가리키는 버퍼에서 반환할 수 있는 총 문자 수(문자 데이터에 대한 null 종료 문자 제외)를 반환합니다.  
  
 *버퍼 길이*  
 [입력] \* *커서 이름의*길이 , 문자. CursorName의 값이 유니코드 문자열인 **경우(SQLGetCursorNameW를**호출할 때) *BufferLength* 인수는 짝수여야 합니다. * \**  
  
 *이름길이Ptr*  
 [출력] \* *CursorName에서*반환할 수 있는 총 문자 수(null-termination 문자 제외)를 반환하는 메모리에 대한 포인터입니다. 반환할 수 있는 문자 수가 *BufferLength보다*크거나 같으면 \* *CursorName의* 커서 이름이 *BufferLength에* 잘려null 종료 문자의 길이를 뺀 값입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetCursorName** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 관련 된 SQLSTATE 값 *SQL_HANDLE_STMT 핸들 유형* 및 문 *핸들*핸들을 호출 하 여 **가져올** 수 있습니다. *Handle* 다음 표에서는 **SQLGetCursorName에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|버퍼 \* *CursorName* 전체 커서 이름을 반환할 만큼 충분히 크지 않았기 때문에 커서 이름이 잘렸습니다. 잘린 커서 이름의 길이는 **NameLengthPtr에서*반환됩니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. 이 비동기 함수는 **SQLGetCursorName** 함수가 호출될 때 계속 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 *함수는 StatementHandle에* 대 한 호출 하 고이 함수를 호출 하는 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY015|사용할 수 있는 커서 이름이 없습니다.|(DM) 드라이버가 ODBC 2 *.x* 드라이버이고 문에 열린 커서가 없었으며 **SQLSetCursorName으로**커서 이름이 설정되지 않았습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) *인수 BufferLength에* 지정된 값이 0보다 적다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
  
## <a name="comments"></a>주석  
 커서 이름은 위치 가 있는 업데이트 및 삭제 문(예: **UPDATE** _테이블 이름)에서만_ 사용됩니다. 여기서 _커서 이름의_ **현재).** 자세한 내용은 [위치 업데이트 및 삭제 문을](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)참조하십시오. 응용 프로그램에서 **SQLSetCursorName을** 호출하지 않고 커서 이름을 정의하지 않으면 드라이버가 이름을 생성합니다. 이 이름은 SQL_CUR 문자로 시작합니다.  
  
> [!NOTE]
>  ODBC 2 *.x에서*열려 있는 커서가 없고 **SQLSetCursorName호출에**의해 이름이 설정되지 않은 경우 **SQLGetCursorName에** 대한 호출이 SQLSTATE HY015를 반환했습니다(사용 가능한 커서 이름 없음). ODBC 3 *.x에서는*더 이상 사실이 아닙니다. **SQLGetCursorName이** 호출되는 시기에 관계없이 드라이버는 커서 이름을 반환합니다.  
  
 **SQLGetCursorName** 이름이 명시적으로 또는 암시적으로 만들어졌는지 여부에 관계없이 커서의 이름을 반환합니다. **SQLSetCursorName이** 호출되지 않은 경우 커서 이름이 암시적으로 생성됩니다. **SQLSetCursorName커서가** 할당되거나 준비된 상태에 있는 한 명령문의 커서 이름을 바꾸기 위해 호출할 수 있습니다.  
  
 명시적으로 또는 암시적으로 설정된 커서 이름은 연결된 *StatementHandle이* 삭제될 때까지 설정된 상태로 유지되며, *핸들유형* SQL_HANDLE_STMT **있는 SQLFreeHandle을** 사용하여 사용됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비된 SQL 문 실행|[SQL실행 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|실행을 위한 명령문 준비|[SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|커서 이름 설정|[SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
