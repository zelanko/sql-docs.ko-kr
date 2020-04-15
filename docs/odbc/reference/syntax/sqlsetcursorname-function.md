---
title: SQLSetCursorName 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetCursorName
helpviewer_keywords:
- SQLSetCursorName function [ODBC]
ms.assetid: 4e055946-12d4-4589-9891-41617a50f34e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a3bcd07a39401d49be04d141e50c671179efb16
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287343"
---
# <a name="sqlsetcursorname-function"></a>SQLSetCursorName 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLSetCursorName** 활성 문과 커서 이름을 연결 합니다. 응용 프로그램이 **SQLSetCursorName을**호출하지 않으면 드라이버는 SQL 문 처리에 필요한 커서 이름을 생성합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *커서 이름*  
 [입력] 커서 이름입니다. 효율적인 처리를 위해 커서 이름에는 커서 이름에 선행 또는 후행 공백이 포함되어서는 안 되며 커서 이름에 구분된 식별자가 포함된 경우 구분 기호를 커서 이름의 첫 번째 문자로 배치해야 합니다.  
  
 *NameLength*  
 [입력] **커서 이름의*문자 길이 .  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLSetCursorName** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 관련 된 SQLSTATE 값 SQL_HANDLE_STMT *핸들 유형* 및 문 *핸들* *핸들을* 호출 하 여 가져올 수 **있습니다.** 다음 표에서는 **SQLSetCursorName에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|커서 이름이 최대 제한을 초과하므로 허용되는 최대 문자 수만 사용되었습니다.|  
|24000|잘못된 커서 상태|*StatementHandle에* 해당하는 문은 이미 실행되거나 커서 위치 가 있는 상태입니다.|  
|34000|잘못된 커서 이름|**CursorName에* 지정된 커서 이름이 드라이버에서 정의한 최대 길이를 초과했거나 "SQLCUR" 또는 "SQL_CUR"로 시작했기 때문에 잘못된 것입니다.|  
|3C000|중복 커서 이름|**커서이름에* 지정된 커서 이름이 이미 있습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY09|null 포인터의 잘못된 사용|(DM) *인수 CursorName은* null 포인터였습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. **SQLSetCursorName** 함수가 호출될 때 이 aynchronous 함수는 여전히 실행 중이었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 *함수는 StatementHandle에* 대 한 호출 하 고이 함수를 호출 하는 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) 인수 *NameLength가* 0보다 작지만 SQL_NTS 같지 않았습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
  
## <a name="comments"></a>주석  
 커서 이름은 위치 가 있는 업데이트 및 삭제 문(예: **UPDATE** _테이블 이름)에서만_ 사용됩니다. 여기서 _커서 이름의_ **현재).** 자세한 내용은 [위치 업데이트 및 삭제 문을](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)참조하십시오. 응용 프로그램이 **SQLSetCursorName을** 호출하지 않고 커서 이름을 정의하지 않으면 쿼리 문이 실행될 때 드라이버는 SQL_CUR 문자로 시작하여 길이가 18자를 초과하지 않는 이름을 생성합니다.  
  
 연결 내의 모든 커서 이름은 고유해야 합니다. 커서 이름의 최대 길이는 드라이버에 의해 정의됩니다. 최대 상호 운용성을 위해 응용 프로그램은 커서 이름을 18자 이하로 제한하는 것이 좋습니다. ODBC 3 *.x에서*커서 이름이 따옴표로 된 식별자인 경우 대/소문자를 구분하는 방식으로 처리되며 SQL 구문이 공백 또는 예약된 키워드와 같이 특별히 허용하지 않거나 처리하지 않는 문자를 포함할 수 있습니다. 커서 이름을 대/소문자 구분 방식으로 처리해야 하는 경우 인용된 식별자로 전달되어야 합니다.  
  
 **SQLFreeHandle**을 사용하여 연결된 문이 삭제될 때까지 명시적으로 또는 암시적으로 설정된 커서 이름은 설정된 상태로 유지됩니다. **SQLSetCursorName커서가** 할당되거나 준비된 상태에 있는 한 명령문의 커서 이름을 바꾸기 위해 호출할 수 있습니다.  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서 응용 프로그램은 **SQLSetCursorName을** 사용하여 명령문에 대한 커서 이름을 설정합니다. 그런 다음 해당 문을 사용하여 CUSTOMERS 테이블에서 결과를 검색합니다. 마지막으로, 존 스미스의 전화 번호를 변경 하려면 위치 된 업데이트를 수행 합니다. 응용 프로그램은 **SELECT** 및 **UPDATE** 문에 대해 서로 다른 명령문 핸들을 사용합니다.  
  
 다른 코드 예제는 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)를 참조하십시오.  
  
```cpp  
#define NAME_LEN 50  
#define PHONE_LEN 10  
  
SQLHSTMT     hstmtSelect,  
SQLHSTMT     hstmtUpdate;  
SQLRETURN    retcode;  
SQLHDBC      hdbc;  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   cbName, cbPhone;  
  
/* Allocate the statements and set the cursor name. */  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmtSelect);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmtUpdate);  
SQLSetCursorName(hstmtSelect, "C1", SQL_NTS);  
  
/* SELECT the result set and bind its columns to local buffers. */  
  
SQLExecDirect(hstmtSelect,  
      "SELECT NAME, PHONE FROM CUSTOMERS",  
      SQL_NTS);  
SQLBindCol(hstmtSelect, 1, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
SQLBindCol(hstmtSelect, 2, SQL_C_CHAR, szPhone, PHONE_LEN, &cbPhone);  
  
/* Read through the result set until the cursor is */  
/* positioned on the row for John Smith. */  
  
do  
 retcode = SQLFetch(hstmtSelect);  
while ((retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) &&  
   (strcmp(szName, "Smith, John") != 0));  
  
/* Perform a positioned update of John Smith's name. */  
  
if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
   SQLExecDirect(hstmtUpdate,  
   "UPDATE EMPLOYEE SET PHONE=\"2064890154\" WHERE CURRENT OF C1",  
   SQL_NTS);  
}  
```  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비된 SQL 문 실행|[SQL실행 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|커서 이름 반환|[SQLGetCursorName 함수](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|커서 스크롤 옵션 설정|[SQLSetScrollOptions 함수](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
