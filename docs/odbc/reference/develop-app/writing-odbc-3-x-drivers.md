---
title: ODBC 3.x 드라이버 작성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading drivers [ODBC]
- ODBC drivers [ODBC], upgrading
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 9b75f59b-623f-4711-9ca2-e751b3622e00
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f548e1496ce45d9fdb4677fd9659de349e5c5cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62636108"
---
# <a name="writing-odbc-3x-drivers"></a>ODBC 3.x 드라이버 작성
다음 표에서 ODBC 3에서 함수 지원 합니다. *x* 드라이버 및 ODBC 응용 프로그램 및 매핑을 함수는 ODBC 3에 대해 호출 될 때 드라이버 관리자에 의해 수행 됩니다. *x* 드라이버입니다.  
  
|기능|지원됨<br /><br /> 여는<br /><br /> ODBC 3.*x*<br /><br /> 드라이버?|지원됨<br /><br /> 여는<br /><br /> ODBC 3.*x*<br /><br /> 응용 프로그램이 있나요?|매핑된/지원<br /><br /> ODBC 3에서. *x*<br /><br /> 드라이버 관리자<br /><br /> ODBC 3입니다. *x* 드라이버?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|아니요|[1]|사용자 계정 컨트롤|  
|**SQLAllocEnv**|아니요|[1]|사용자 계정 컨트롤|  
|**SQLAllocHandle**|사용자 계정 컨트롤|예|아니요|  
|**SQLAllocStmt**|아니요|[1]|사용자 계정 컨트롤|  
|**SQLBindCol**|사용자 계정 컨트롤|예|아니요|  
|**SQLBindParam**|아니요|예 [2]|사용자 계정 컨트롤|  
|**SQLBindParameter**|사용자 계정 컨트롤|예|아니요|  
|**SQLBrowseConnect**|사용자 계정 컨트롤|예|아니요|  
|**SQLBulkOperations**|사용자 계정 컨트롤|예|아니요|  
|**SQLCancel**|사용자 계정 컨트롤|예|아니요|  
|**SQLCloseCursor**|사용자 계정 컨트롤|예|아니요|  
|**SQLColAttribute**|사용자 계정 컨트롤|예|아니요|  
|**SQLColAttributes**|No[3]|아니요|사용자 계정 컨트롤|  
|**SQLColumnPrivileges**|사용자 계정 컨트롤|예|아니요|  
|**SQLColumns**|사용자 계정 컨트롤|예|아니요|  
|**SQLConnect**|사용자 계정 컨트롤|예|아니요|  
|**SQLCopyDesc**|사용자 계정 컨트롤|사용자 계정 컨트롤|예 [4]|  
|**SQLDataSources**|아니요|예|사용자 계정 컨트롤|  
|**SQLDescribeCol**|사용자 계정 컨트롤|예|아니요|  
|**SQLDescribeParam**|사용자 계정 컨트롤|예|아니요|  
|**SQLDisconnect**|사용자 계정 컨트롤|예|아니요|  
|**SQLDriverConnect**|사용자 계정 컨트롤|예|아니요|  
|**SQLDrivers**|아니요|예|사용자 계정 컨트롤|  
|**SQLEndTran**|사용자 계정 컨트롤|예|아니요|  
|**SQLError**|아니요|[1]|사용자 계정 컨트롤|  
|**SQLExecDirect**|사용자 계정 컨트롤|예|아니요|  
|**SQLExecute**|사용자 계정 컨트롤|예|아니요|  
|**SQLExtendedFetch**|사용자 계정 컨트롤|아니오|아니요|  
|**SQLFetch**|사용자 계정 컨트롤|예|아니요|  
|**SQLFetchScroll**|사용자 계정 컨트롤|예|아니요|  
|**SQLForeignKeys**|사용자 계정 컨트롤|예|아니요|  
|**SQLFreeConnect**|아니요|예 [1]|사용자 계정 컨트롤|  
|**SQLFreeEnv**|아니요|예 [1]|사용자 계정 컨트롤|  
|**SQLFreeHandle**|사용자 계정 컨트롤|예|아니요|  
|**SQLFreeStmt**|사용자 계정 컨트롤|예|아니요|  
|**SQLGetConnectAttr**|사용자 계정 컨트롤|예|아니요|  
|**SQLGetConnectOption**|No[5]|[1]|사용자 계정 컨트롤|  
|**SQLGetCursorName**|사용자 계정 컨트롤|예|아니요|  
|**SQLGetData**|사용자 계정 컨트롤|예|아니요|  
|**SQLGetDescField**|사용자 계정 컨트롤|예|아니요|  
|**SQLGetDescRec**|사용자 계정 컨트롤|예|아니요|  
|**SQLGetDiagField**|사용자 계정 컨트롤|예|아니요|  
|**SQLGetDiagRec**|사용자 계정 컨트롤|예|아니요|  
|**SQLGetEnvAttr**|사용자 계정 컨트롤|예|아니요|  
|**SQLGetFunctions**|No[6]|사용자 계정 컨트롤|사용자 계정 컨트롤|  
|**SQLGetInfo**|사용자 계정 컨트롤|예|아니요|  
|**SQLGetStmtAttr**|사용자 계정 컨트롤|예|아니요|  
|**SQLGetStmtOption**|No[5]|[1]|사용자 계정 컨트롤|  
|**SQLGetTypeInfo**|사용자 계정 컨트롤|예|아니요|  
|**SQLMoreResults**|사용자 계정 컨트롤|예|아니요|  
|**SQLNativeSql**|사용자 계정 컨트롤|예|아니요|  
|**SQLNumParams**|사용자 계정 컨트롤|예|아니요|  
|**SQLNumResultCols**|사용자 계정 컨트롤|예|아니요|  
|**SQLParamData**|사용자 계정 컨트롤|예|아니요|  
|**SQLParamOptions**|아니요|아니요|사용자 계정 컨트롤|  
|**SQLPrepare**|사용자 계정 컨트롤|예|아니요|  
|**SQLPrimaryKeys**|사용자 계정 컨트롤|예|아니요|  
|**SQLProcedureColumns**|사용자 계정 컨트롤|예|아니요|  
|**SQLProcedures**|사용자 계정 컨트롤|예|아니요|  
|**SQLPutData**|사용자 계정 컨트롤|예|아니요|  
|**SQLRowCount**|사용자 계정 컨트롤|예|아니요|  
|**SQLSetConnectAttr**|사용자 계정 컨트롤|예|아니요|  
|**SQLSetConnectOption**|No[5]|[1]|사용자 계정 컨트롤|  
|**SQLSetCursorName**|사용자 계정 컨트롤|예|아니요|  
|**SQLSetDescField**|사용자 계정 컨트롤|예|아니요|  
|**SQLSetDescRec**|사용자 계정 컨트롤|예|아니요|  
|**SQLSetEnvAttr**|사용자 계정 컨트롤|예|아니요|  
|**SQLSetPos**|사용자 계정 컨트롤|예|아니요|  
|**SQLSetParam**|아니요|아니요|사용자 계정 컨트롤|  
|**SQLSetScrollOption**|사용자 계정 컨트롤|예|아니요|  
|**SQLSetStmtAttr**|사용자 계정 컨트롤|예|아니요|  
|**SQLSetStmtOption**|No[5]|[1]|사용자 계정 컨트롤|  
|**SQLSpecialColumns**|사용자 계정 컨트롤|예|아니요|  
|**SQLStatistics**|사용자 계정 컨트롤|예|아니요|  
|**SQLTablePrivileges**|사용자 계정 컨트롤|예|아니요|  
|**SQLTables**|사용자 계정 컨트롤|예|아니요|  
|**SQLTransact**|아니요|[1]|사용자 계정 컨트롤|  
  
 [1]이이 함수는 ODBC 3에서 사용 되지 않습니다. *x*합니다. ODBC 3입니다. *x* 응용 프로그램 해야이 함수를 사용 하지 않습니다. 그러나는 Open Group 또는 ISO CLI 호환 응용 프로그램이 함수를 호출할 수 있습니다.  
  
 [2] ODBC 3입니다. *x* 응용 프로그램을 사용할지 **SQLBindParameter** 대신 **SQLBindParam**합니다. 그러나는 Open Group 또는 ISO CLI 호환 응용 프로그램이 함수를 호출할 수 있습니다.  
  
 [3] 드라이버 작성자 한다는 점에 유의 해야 ODBC 2. *x* SQL_COLUMN_LENGTH SQL_COLUMN_PRECISION 고 SQL_COLUMN_SCALE를 사용 하 여 지원 해야 하는 열 특성 **SQLColAttribute**합니다.  
  
 [4] **SQLCopyDesc** 다른 드라이버에 속하는 연결 설명자를 복사할 때 드라이버 관리자에 의해 부분적으로 구현 됩니다. 드라이버 지원에 필요한 **SQLCopyDesc** 대 한 자체 연결의 두 개의. 와 같은 함수 **SQLDrivers**전적으로 드라이버 관리자에 의해 구현 되는 경우,이 목록에 표시 되지 않습니다.  
  
 [5] 특정 상황에서 드라이버를이 함수를 지원 해야 합니다. 자세한 내용은이 함수의 참조 페이지를 참조 하세요.  
  
 [6]의 드라이버 지원 하도록 선택할 수 **SQLGetFunctions** 드라이버에서 지 원하는 함수 집합이 다릅니다 연결에서 연결 하는 경우.
