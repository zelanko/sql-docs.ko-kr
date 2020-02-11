---
title: SQLSetCursorName 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 842d21bc36b9360826b4b85aa7da2798782995c6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68092994"
---
# <a name="sqlsetcursorname-function"></a>SQLSetCursorName 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLSetCursorName** 는 커서 이름을 활성 문과 연결 합니다. 응용 프로그램에서 **SQLSetCursorName**를 호출 하지 않는 경우 드라이버는 SQL 문 처리를 위해 필요에 따라 커서 이름을 생성 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들입니다.  
  
 *CursorName*  
 입력 커서 이름입니다. 효율적인 처리를 위해 커서 이름은 커서 이름에 선행 또는 후행 공백을 포함 하지 않아야 하며 커서 이름에 구분 식별자가 포함 된 경우에는 구분 기호를 커서 이름의 첫 문자로 배치 해야 합니다.  
  
 *NameLength*  
 입력 **CursorName*의 문자 길이입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLSetCursorName** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLSetCursorName** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|커서 이름이 최대 제한을 초과 하 여 허용 되는 최대 문자 수만 사용 되었습니다.|  
|24000|잘못된 커서 상태|*StatementHandle* 에 해당 하는 문은 이미 실행 되었거나 커서 위치에 배치 된 상태입니다.|  
|34000|잘못된 커서 이름|**CursorName* 에 지정 된 커서 이름이 드라이버에서 정의한 최대 길이를 초과 했거나 "sqlcur" 또는 "SQL_CUR"로 시작 되었으므로 잘못 되었습니다.|  
|3C000|중복 된 커서 이름|**CursorName* 에 지정 된 커서 이름이 이미 있습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY009|Null 포인터 사용이 잘못 되었습니다.|(DM) *CursorName* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLSetCursorName** 함수가 호출 될 때이 aynchronous 함수는 계속 실행 중입니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수가 호출 되었으며이 함수가 호출 될 때 여전히 실행 되 고 있습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 인수 *NameLength* 가 0 보다 작지만 SQL_NTS와 같지 않습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 커서 이름은 위치 지정 update 및 delete 문에서만 사용 됩니다. 예를 들어 **update** _table-name_ ... **WHERE CURRENT OF** _cursor name_). 자세한 내용은 [위치 지정 Update 및 Delete 문](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)을 참조 하세요. 응용 프로그램에서 **SQLSetCursorName** 를 호출 하 여 커서 이름을 정의 하지 않는 경우 쿼리 문 실행 시 드라이버는 SQL_CUR 문자로 시작 하는 이름을 생성 하 고 길이가 18 자를 초과 하지 않습니다.  
  
 연결 내의 모든 커서 이름은 고유 해야 합니다. 커서 이름의 최대 길이는 드라이버에 의해 정의 됩니다. 최대 상호 운용성을 위해 응용 프로그램에서 커서 이름을 18 자 이하로 제한 하는 것이 좋습니다. ODBC 3.x에서 커서 이름이 따옴표 붙은 식별자 인 경우에는 대/소문자를 구분 하는 방식으로 처리 되며, SQL 구문에서 공백 또는 예약 된 키워드와 같이 특수 하 게 허용 하거나 처리 하지 않는 문자를 포함할 수*있습니다.* 커서 이름을 대/소문자를 구분 하는 방식으로 처리 해야 하는 경우 따옴표 붙은 식별자로 전달 해야 합니다.  
  
 명시적으로 설정 되거나 암시적으로 설정 된 커서 이름은 **Sqlfreehandle**을 사용 하 여 연결 된 문을 삭제할 때까지 설정 된 상태로 유지 됩니다. 커서가 할당 된 상태 이거나 준비 된 상태에 있는 경우 **SQLSetCursorName** 를 호출 하 여 문에 커서의 이름을 바꿀 수 있습니다.  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서 응용 프로그램은 **SQLSetCursorName** 를 사용 하 여 문의 커서 이름을 설정 합니다. 그런 다음 해당 문을 사용 하 여 CUSTOMERS 테이블에서 결과를 검색 합니다. 마지막으로, 위치 지정 업데이트를 수행 하 여 John Smith의 전화 번호를 변경 합니다. 응용 프로그램은 **SELECT** 및 **UPDATE** 문에 대해 다른 문 핸들을 사용 합니다.  
  
 다른 코드 예제를 보려면 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)를 참조 하십시오.  
  
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
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문 실행|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|커서 이름 반환|[SQLGetCursorName 함수(SQLGetCursorName Function)](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|커서 스크롤 옵션 설정|[SQLSetScrollOptions 함수](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
