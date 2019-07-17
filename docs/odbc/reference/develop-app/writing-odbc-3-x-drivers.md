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
ms.openlocfilehash: fb403cef47f901cdb43bbb32c669ba68aa34913d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078900"
---
# <a name="writing-odbc-3x-drivers"></a>ODBC 3.x 드라이버 작성
다음 표에서 ODBC 3에서 함수 지원 합니다. *x* 드라이버 및 ODBC 응용 프로그램 및 매핑을 함수는 ODBC 3에 대해 호출 될 때 드라이버 관리자에 의해 수행 됩니다. *x* 드라이버입니다.  
  
|함수|지원됨<br /><br /> 여는<br /><br /> ODBC 3.*x*<br /><br /> 드라이버?|지원됨<br /><br /> 여는<br /><br /> ODBC 3.*x*<br /><br /> 응용 프로그램이 있나요?|매핑된/지원<br /><br /> ODBC 3에서. *x*<br /><br /> 드라이버 관리자<br /><br /> ODBC 3입니다. *x* 드라이버?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|아니요|[1]|예|  
|**SQLAllocEnv**|아니요|[1]|예|  
|**SQLAllocHandle**|예|예|아니요|  
|**SQLAllocStmt**|아니요|[1]|예|  
|**SQLBindCol**|예|예|아니요|  
|**SQLBindParam**|아니요|예 [2]|예|  
|**SQLBindParameter**|예|예|아니요|  
|**SQLBrowseConnect**|예|예|아니요|  
|**SQLBulkOperations**|예|예|아니요|  
|**SQLCancel**|예|예|아니요|  
|**SQLCloseCursor**|예|예|아니요|  
|**SQLColAttribute**|예|예|아니요|  
|**SQLColAttributes**|[3]|아니요|예|  
|**SQLColumnPrivileges**|예|예|아니요|  
|**SQLColumns**|예|예|아니요|  
|**SQLConnect**|예|예|아니요|  
|**SQLCopyDesc**|예|예|예 [4]|  
|**SQLDataSources**|아니요|예|예|  
|**SQLDescribeCol**|예|예|아니요|  
|**SQLDescribeParam**|예|예|아니요|  
|**SQLDisconnect**|예|예|아니요|  
|**SQLDriverConnect**|예|예|아니요|  
|**SQLDrivers**|아니요|예|예|  
|**SQLEndTran**|예|예|아니요|  
|**SQLError**|아니요|[1]|예|  
|**SQLExecDirect**|예|예|아니요|  
|**SQLExecute**|예|예|아니요|  
|**SQLExtendedFetch**|예|아니오|아니요|  
|**SQLFetch**|예|예|아니요|  
|**SQLFetchScroll**|예|예|아니요|  
|**SQLForeignKeys**|예|예|아니요|  
|**SQLFreeConnect**|아니요|예 [1]|예|  
|**SQLFreeEnv**|아니요|예 [1]|예|  
|**SQLFreeHandle**|예|예|아니요|  
|**SQLFreeStmt**|예|예|아니요|  
|**SQLGetConnectAttr**|예|예|아니요|  
|**SQLGetConnectOption**|No[5]|[1]|예|  
|**SQLGetCursorName**|예|예|아니요|  
|**SQLGetData**|예|예|아니요|  
|**SQLGetDescField**|예|예|아니요|  
|**SQLGetDescRec**|예|예|아니요|  
|**SQLGetDiagField**|예|예|아니요|  
|**SQLGetDiagRec**|예|예|아니요|  
|**SQLGetEnvAttr**|예|예|아니요|  
|**SQLGetFunctions**|[6]|예|예|  
|**SQLGetInfo**|예|예|아니요|  
|**SQLGetStmtAttr**|예|예|아니요|  
|**SQLGetStmtOption**|No[5]|[1]|예|  
|**SQLGetTypeInfo**|예|예|아니요|  
|**SQLMoreResults**|예|예|아니요|  
|**SQLNativeSql**|예|예|아니요|  
|**SQLNumParams**|예|예|아니요|  
|**SQLNumResultCols**|예|예|아니요|  
|**SQLParamData**|예|예|아니요|  
|**SQLParamOptions**|아니요|아니요|예|  
|**SQLPrepare**|예|예|아니요|  
|**SQLPrimaryKeys**|예|예|아니요|  
|**SQLProcedureColumns**|예|예|아니요|  
|**SQLProcedures**|예|예|아니요|  
|**SQLPutData**|예|예|아니요|  
|**SQLRowCount**|예|예|아니요|  
|**SQLSetConnectAttr**|예|예|아니요|  
|**SQLSetConnectOption**|No[5]|[1]|예|  
|**SQLSetCursorName**|예|예|아니요|  
|**SQLSetDescField**|예|예|아니요|  
|**SQLSetDescRec**|예|예|아니요|  
|**SQLSetEnvAttr**|예|예|아니요|  
|**SQLSetPos**|예|예|아니요|  
|**SQLSetParam**|아니요|아니요|예|  
|**SQLSetScrollOption**|예|예|아니요|  
|**SQLSetStmtAttr**|예|예|아니요|  
|**SQLSetStmtOption**|No[5]|[1]|예|  
|**SQLSpecialColumns**|예|예|아니요|  
|**SQLStatistics**|예|예|아니요|  
|**SQLTablePrivileges**|예|예|아니요|  
|**SQLTables**|예|예|아니요|  
|**SQLTransact**|아니요|[1]|예|  
  
 [1]이이 함수는 ODBC 3에서 사용 되지 않습니다. *x*합니다. ODBC 3입니다. *x* 응용 프로그램 해야이 함수를 사용 하지 않습니다. 그러나는 Open Group 또는 ISO CLI 호환 응용 프로그램이 함수를 호출할 수 있습니다.  
  
 [2] ODBC 3입니다. *x* 응용 프로그램을 사용할지 **SQLBindParameter** 대신 **SQLBindParam**합니다. 그러나는 Open Group 또는 ISO CLI 호환 응용 프로그램이 함수를 호출할 수 있습니다.  
  
 [3] 드라이버 작성자 한다는 점에 유의 해야 ODBC 2. *x* SQL_COLUMN_LENGTH SQL_COLUMN_PRECISION 고 SQL_COLUMN_SCALE를 사용 하 여 지원 해야 하는 열 특성 **SQLColAttribute**합니다.  
  
 [4] **SQLCopyDesc** 다른 드라이버에 속하는 연결 설명자를 복사할 때 드라이버 관리자에 의해 부분적으로 구현 됩니다. 드라이버 지원에 필요한 **SQLCopyDesc** 대 한 자체 연결의 두 개의. 와 같은 함수 **SQLDrivers**전적으로 드라이버 관리자에 의해 구현 되는 경우,이 목록에 표시 되지 않습니다.  
  
 [5] 특정 상황에서 드라이버를이 함수를 지원 해야 합니다. 자세한 내용은이 함수의 참조 페이지를 참조 하세요.  
  
 [6]의 드라이버 지원 하도록 선택할 수 **SQLGetFunctions** 드라이버에서 지 원하는 함수 집합이 다릅니다 연결에서 연결 하는 경우.
