---
title: SQLFreeStmt 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d20a486a644a5608accef46a9558c1754efd975d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32920118"
---
# <a name="sqlfreestmt-function"></a>SQLFreeStmt 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLFreeStmt** 특정 문과 연결 된 처리를 중지를 보류 중인 결과가 삭제 된 문과 연결 된 열려 있는 모든 커서를 닫습니다 하거나 필요에 따라 문 핸들에 연결 된 모든 리소스를 해제 합니다.  
  
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
  
 SQL_ 닫기: 연결 된 커서를 닫아 *StatementHandle* (정의 된) 경우 모든 보류 중인 결과 삭제 합니다. 응용 프로그램을 다시 열 수이 커서 나중에 실행 하 여 한 **선택** 문을 다시 같거나 다른 데이터 집합 매개 변수 값입니다. 열려 있는 커서가 없습니다 없으면이 옵션은 응용 프로그램에 대 한 영향을 주지 않습니다. **SQLCloseCursor** 커서 닫기 호출할 수도 있습니다. 자세한 내용은 참조 [커서를 닫으면](../../../odbc/reference/develop-app/closing-the-cursor.md)합니다.  
  
 SQL_DROP:이 옵션은 사용 되지 않습니다. 에 대 한 호출 **SQLFreeStmt** 와 *옵션* SQL_DROP의 드라이버 관리자를 매핑되어 [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)합니다.  
  
 SQL_UNBIND: 설정의 모든 열 버퍼를 해제 하는 0으로 카드가 SQL_DESC_COUNT 필드 구속 **SQLBindCol** 에 대 한는 주어진 *StatementHandle*합니다. 이 책갈피 열; 연결이 끊어지지 않습니다. 이렇게 하려면 책갈피 열에 대 한 카드가의 SQL_DESC_DATA_PTR 필드가 NULL로 설정 됩니다. 둘 이상의 문에 의해 공유 되는 명시적으로 할당 된 설명자에이 작업을 수행 하는 경우 작업에 영향을 줍니다 설명자를 공유 하는 모든 문은 바인딩을 확인 합니다. 자세한 내용은 참조 [개요의 검색 결과 (기본)](../../../odbc/reference/develop-app/retrieving-results-basic.md)합니다.  
  
 SQL_RESET_PARAMS:을 0으로 설정 하 여 모든 매개 변수 버퍼를 해제 APD의 SQL_DESC_COUNT 필드를 설정 하 **SQLBindParameter** 에 대 한는 주어진 *StatementHandle*합니다. 둘 이상의 문에 의해 공유 되는 명시적으로 할당 된 설명자에이 작업을 수행 하는 경우이 작업 설명자를 공유 하는 모든 문은 데이터 소스의 영향을 줍니다. 자세한 내용은 참조 [매개 변수 바인딩](../../../odbc/reference/develop-app/binding-parameters-odbc.md)합니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLFreeStmt** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* SQL_의 HANDLE_STMT 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLFreeStmt** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. 이 비동기 함수 계속 실행 될 때 **SQLFreeStmt** 호출 되었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대 한 호출 된는 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수를 호출 했습니다 *옵션* 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 SQL_RESET_PARAMS로 설정 합니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY092|옵션 유형 범위를 벗어났습니다.|인수에 대해 지정 된 값 (DM) *옵션* 없습니다:<br /><br /> SQL_CLOSE SQL_DROP SQL_UNBIND SQL_RESET_PARAMS|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *StatementHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>설명  
 호출 **SQLFreeStmt** 는 SQL_CLOSE with 옵션은 호출에 해당 **SQLCloseCursor**제외 하 고 **SQLFreeStmt** SQL_CLOSE와 영향을 주지 않습니다 응용 프로그램 커서가 없는 경우 문에서 엽니다. 커서가 없는 경우를 열려면에 대 한 호출 **SQLCloseCursor** SQLSTATE 24000 (잘못 된 커서 상태)를 반환 합니다.  
  
 응용 프로그램 해제; 된 후 문 핸들을 사용 하지 않아야 드라이버 관리자는 함수 호출에 대 한 핸들의 유효성을 검사 하지 않습니다.  
  
## <a name="example"></a>예제  
 핸들을 확보 하는 바람직한 프로그래밍 관행은 그러나 편의상 다음 샘플 포함 되지 않습니다 핸들을 할당 하지 않아도 되도록 코드. 핸들을 해제 하는 방법의 예제를 보려면 [SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)합니다.  
  
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
|커서를 닫으면|[SQLCloseCursor 함수](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|핸들을 해제합니다.|[SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|커서 이름 설정|[SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
