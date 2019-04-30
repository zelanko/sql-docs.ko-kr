---
title: SQLFreeStmt Function | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeStmt
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFreeStmt
helpviewer_keywords:
- SQLFreeStmt function [ODBC]
ms.assetid: 03408162-8b63-4470-90c4-e6c7d8d33892
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f3cca214aeb63720e193f57f06a22481ae7d369f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259314"
---
# <a name="sqlfreestmt-function"></a>SQLFreeStmt 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLFreeStmt** 특정 문과 사용 하 여 연결 된 처리를 중지, 보류 중인 결과가 삭제 된 문과 연결 된 열려 있는 모든 커서가 닫히거나, 필요에 따라 문 핸들을 사용 하 여 연결 된 모든 리소스를 해제 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLFreeStmt(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Option);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들  
  
 *옵션*  
 [입력] 다음 옵션 중 하나입니다.  
  
 SQL_ CLOSE: 연관 된 커서를 닫고 *StatementHandle* (정의 된) 경우 모든 보류 중인 결과 무시 하 고 있습니다. 응용 프로그램을 다시 열 수이 커서 나중에 실행 하 여는 **선택** 동일 하거나 다른 매개 변수 값을 사용 하 여 다시 문입니다. 없음 커서를 연 경우이 옵션은 응용 프로그램에 대 한 영향을 주지 않습니다. **SQLCloseCursor** 커서 닫기 호출할 수도 있습니다. 자세한 내용은 [커서 닫기](../../../odbc/reference/develop-app/closing-the-cursor.md)합니다.  
  
 SQL_DROP: 이 옵션은 더 이상 사용되지 않습니다. 에 대 한 호출 **SQLFreeStmt** 사용 하 여는 *옵션* SQL_DROP의 드라이버 관리자에 매핑되어 [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)합니다.  
  
 SQL_UNBIND: 집합의 모든 열 버퍼를 해제 하는 0으로 카드가 SQL_DESC_COUNT 필드 구속 **SQLBindCol** 에 대 한는 주어진 *StatementHandle*. 책갈피 열; 연결을 끊지 않습니다이 이렇게 하려면 책갈피 열에 대 한 카드가의 SQL_DESC_DATA_PTR 필드가 NULL로 설정 됩니다. 둘 이상의 문에 의해 공유 되는 명시적으로 할당 된 설명자를에서이 작업을 수행 하는 경우 작업에는 영향이 설명자를 공유 하는 모든 문은의 바인딩을 확인할 수 있습니다. 자세한 내용은 [개요의 검색 결과 (기본)](../../../odbc/reference/develop-app/retrieving-results-basic.md)합니다.  
  
 SQL_RESET_PARAMS: APD의 SQL_DESC_COUNT 필드를 0으로 설정한 모든 매개 변수 버퍼를 해제 설정 **SQLBindParameter** 에 대 한는 주어진 *StatementHandle*합니다. 둘 이상의 문에 의해 공유 되는 명시적으로 할당 된 설명자를에서이 작업을 수행 하는 경우이 작업 설명자를 공유 하는 모든 문은의 바인딩을 적용 됩니다. 자세한 내용은 [매개 변수 바인딩](../../../odbc/reference/develop-app/binding-parameters-odbc.md)합니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLFreeStmt** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* SQL_의 HANDLE_STMT와 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLFreeStmt** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수가 계속 실행 될 때 **SQLFreeStmt** 호출 되었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수를 호출한 *옵션* 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 SQL_RESET_PARAMS로 설정 합니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY092|옵션 유형 범위를 벗어났습니다|인수에 지정 된 값 (DM) *옵션* 없습니다.<br /><br /> SQL_CLOSE SQL_DROP SQL_UNBIND SQL_RESET_PARAMS|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 호출 **SQLFreeStmt** 를 SQL_CLOSE with 옵션은 호출할 때와 동일한 **SQLCloseCursor**점을 제외 하 고 **SQLFreeStmt** SQL_CLOSE를 사용 하 여 영향을 주지 않습니다 응용 프로그램 커서가 없습니다 경우 문에서 엽니다. 커서가 없습니다 경우 열기, 호출 **SQLCloseCursor** SQLSTATE 24000 (잘못 된 커서 상태)를 반환 합니다.  
  
 응용 프로그램 해제; 된 후 문 핸들을 사용 하지 않아야 드라이버 관리자는 함수 호출에 대 한 핸들의 유효성을 검사 하지 않습니다.  
  
## <a name="example"></a>예제  
 핸들을 해제 하려면 바람직한 프로그래밍 관행을 것입니다. 그러나 간단히 하기 위해 다음 샘플 포함 되지 않습니다 핸들을 할당 해제 하는 코드. 핸들을 해제 하는 방법의 예제를 참조 하세요 [SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)합니다.  
  
```  
// SQLFreeStmt.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   // declare and initialize the environment, connection, statement handles  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR *)"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1024 + 1, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
   retCode = SQLFreeStmt(hstmt, SQL_UNBIND);  
   retCode = SQLFreeStmt(hstmt, SQL_RESET_PARAMS);  
}  
```  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|커서 닫기|[SQLCloseCursor 함수](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|핸들 해제|[SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|커서 이름을 설정합니다.|[SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
