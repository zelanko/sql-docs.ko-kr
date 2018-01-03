---
title: "SQLSetCursorName 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLSetCursorName
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLSetCursorName
helpviewer_keywords: SQLSetCursorName function [ODBC]
ms.assetid: 4e055946-12d4-4589-9891-41617a50f34e
caps.latest.revision: "18"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e9f416827e5f192599b35027d2a203b011b844f6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetcursorname-function"></a>SQLSetCursorName 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLSetCursorName** 활성 문을 커서 이름을 연결 합니다. 응용 프로그램을 호출 하지 않는 **SQLSetCursorName**, 드라이버는 SQL 문 처리에 필요에 따라 커서 이름을 생성 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *M e*  
 [입력] 커서 이름입니다. 효율적인 처리 커서 이름을 커서 이름에 선행 또는 후행 공백을 모두 묶지 말아야 하 고 커서 이름에서 첫 번째 문자로 구분 기호를 배치 하도록 커서 이름이 구분된 식별자가 포함 된 경우.  
  
 *NameLength*  
 [입력] 문자 길이 **m e*합니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLSetCursorName** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* 의 여는 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLSetCursorName** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|커서 이름이 하므로 최대 한도 초과 문자의 최대 허용 수만 사용 했습니다.|  
|24000|잘못된 커서 상태|에 해당 하는 문을 *StatementHandle* 이 이미 실행 된 또는 커서가 위치 합니다.|  
|34000|잘못된 커서 이름|에 지정 된 커서 이름을 **m e* 드라이버에 의해 정의 된 대로 최대 길이 초과 하거나 "SQLCUR" 또는 "SQL_CUR"로 시작 하므로 잘못 되었습니다.|  
|3C000|중복 된 커서 이름입니다.|에 지정 된 커서 이름을 **m e* 이미 있습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|(DM) 인수 *m e* 는 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. 이 aynchronous 함수 계속 실행 될 때는 **SQLSetCursorName** 함수를 호출 했습니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM) 인수 *NameLength* 같지 않음 SQL_NTS 하지만 0 보다 작습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *StatementHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 커서 이름은 위치 지정된 업데이트에만 사용 되며 및 delete 문 (예를 들어 **업데이트** *테이블 이름* ... **WHERE CURRENT OF** *커서 이름을*). 자세한 내용은 참조 [배치 Update 및 Delete 문이](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)합니다. 응용 프로그램을 호출 하지 않는 **SQLSetCursorName** 드라이버 SQL_CUR 문자로 시작 하 고 길이가 18 자를 초과 하지 않는 추가 하는 이름을 생성 하는 쿼리 문 실행에 커서 이름을 정의할 수 있습니다.  
  
 연결 내에서 모든 커서 이름은 고유 해야 합니다. 커서 이름의 최대 길이 드라이버에 의해 정의 됩니다. 상호 운용성을 극대화 응용 프로그램 커서 이름은 최대 18 자로 제한 하는 좋습니다. ODBC 3에서*.x*, 커서 이름을 따옴표 붙은 식별자는 대/소문자 구분 방식으로 처리 됩니다 및 문자는 SQL 구문을 허용 합니다 또는 공백 같은 특수, 취급 또는 예약 된 키워드를 포함할 수 있습니다. 커서 이름은 대/소문자 구분 방식으로 취급 되어야, 따옴표 붙은 식별자로 전달 되어야 합니다.  
  
 와 관련 된 문을 사용 하 여 삭제 될 때까지 설정 명시적으로 또는 암시적으로 상태를 유지 하는 커서 이름을 설정 **SQLFreeHandle**합니다. **SQLSetCursorName** 으로 커서가 할당 또는 준비 된 상태에 있는 문에서 커서의 이름을 바꾸려면 호출할 수 있습니다.  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서는 응용 프로그램에서 사용 **SQLSetCursorName** 문에 대 한 커서 이름을 설정 합니다. 그런 다음 해당 문을 사용 하 여 CUSTOMERS 테이블에서 결과 검색 합니다. 마지막으로, John Smith의 전화 번호를 변경 하려면 현재 위치 업데이트를 수행 합니다. 응용 프로그램에 대 한 다른 문 핸들을 사용 한다는 점에 유의 **선택** 및 **업데이트** 문.  
  
 다른 코드 예제를 보려면 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)합니다.  
  
```  
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
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|커서 이름 반환|[SQLGetCursorName 함수](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|커서 스크롤 옵션 설정|[SQLSetScrollOptions 함수](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
