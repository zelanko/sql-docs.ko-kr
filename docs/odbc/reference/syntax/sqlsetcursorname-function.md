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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68092994"
---
# <a name="sqlsetcursorname-function"></a>SQLSetCursorName 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLSetCursorName** 활성 문을 사용 하 여 커서 이름을 연결 합니다. 응용 프로그램을 호출 하지 않습니다 **SQLSetCursorName**, 드라이버는 SQL 문 처리에 대 한 필요에 따라 커서 이름을 생성 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *cursorName*  
 [입력] 커서 이름입니다. 효율적인 처리를 위해 커서 이름 커서 이름에 선행 또는 후행 공백을 모두를 포함 하지 않아야 하 고 커서 이름에서 첫 번째 문자로 구분 기호를 배치 해야 커서 이름이 구분된 식별자에 포함 된 경우.  
  
 *NameLength*  
 [입력] 문자 길이 **CursorName*합니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLSetCursorName** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* 의 호출 및 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLSetCursorName** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|커서 이름 이므로, 최대 한도 초과 합니다만 허용 되는 최대 문자 사용 되었습니다.|  
|24000|잘못된 커서 상태|에 해당 하는 문을 *StatementHandle* 이미 상태의 실행 또는 커서가 위치 합니다.|  
|34000|잘못된 커서 이름|에 지정 된 커서 이름을 **CursorName* 드라이버에 의해 정의 된 대로 최대 길이 초과 하거나 "SQLCUR" 또는 "SQL_CUR."로 시작 하므로 잘못 되었습니다.|  
|3C000|커서 이름이 중복 됩니다.|에 지정 된 커서 이름을 **CursorName* 이미 있습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|(DM) 인수 *CursorName* 가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 aynchronous 함수가 여전히 실행 시기를 **SQLSetCursorName** 함수를 호출 했습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM) 인수 *NameLength* 0 보다 작지만 같지 않음 SQL_NTS 되었습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 커서 이름은 현재 위치 업데이트에만 사용 됩니다 및 delete 문 (예를 들어 **업데이트할** _테이블 이름_ ... **WHERE CURRENT OF** _커서 이름을_). 자세한 내용은 [배치 업데이트 및 삭제 문을](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)합니다. 응용 프로그램을 호출 하지 않습니다 **SQLSetCursorName** 드라이버 SQL_CUR 문자로 시작 하 고 길이가 18 자를 초과 하지 않는지 여부를 지정 하는 이름을 생성 쿼리 문 실행 커서 이름을 정의 합니다.  
  
 연결 내에서 모든 커서 이름은 고유 해야 합니다. 커서 이름의 최대 길이 드라이버에 의해 정의 됩니다. 최대 상호 운용성을 위해 응용 프로그램 커서 이름은 개 이하의 18 자로 제한 하는 좋습니다. ODBC 3에서 *.x*, 커서 이름을 따옴표 붙은 식별자는 대/소문자 구분 방식으로 처리 됩니다 및 문자는 SQL의 구문과 허용 하지는 공백 같은 특수, 취급 하는 또는 예약 된 키워드를 포함할 수 있습니다. 커서 이름을 대/소문자 구분 방식으로 취급 되어야, 따옴표 붙은 식별자로 전달 되어야 합니다.  
  
 명시적으로 설정 됩니다 또는 암시적으로 유지 하는 커서 이름을 설정와 관련 된 문을 사용 하 여 삭제 될 때까지 **SQLFreeHandle**합니다. **SQLSetCursorName** 커서가 할당 또는 준비 된 상태와 문에서 커서 이름을 바꾸려면 호출할 수 있습니다.  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서는 응용 프로그램 사용 **SQLSetCursorName** 문에 대 한 커서 이름을 설정 합니다. 그런 다음 해당 문을 사용 하 여 CUSTOMERS 테이블에서 결과 검색 합니다. 마지막으로, John Smith의 전화 번호를 변경 하려면 현재 위치 업데이트를 수행 합니다. 응용 프로그램에 대 한 다른 문 핸들을 사용 한다는 점에 유의 합니다 **선택** 및 **업데이트** 문입니다.  
  
 다른 코드 예제를 보려면 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)합니다.  
  
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
  
|내용|참조 항목|  
|---------------------------|---------|  
|SQL 문을 실행합니다.|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|커서 이름을 반환합니다.|[SQLGetCursorName 함수](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|커서 스크롤 옵션 설정|[SQLSetScrollOptions 함수](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
