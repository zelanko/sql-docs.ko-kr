---
title: "ODBC 3.x 드라이버 작성 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading drivers [ODBC]
- ODBC drivers [ODBC], upgrading
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 9b75f59b-623f-4711-9ca2-e751b3622e00
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 41ca6ddf1535899ed8e5e0f065cf2f5f0ca19dca
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="writing-odbc-3x-drivers"></a>쓰기 ODBC 3.x 드라이버
다음 표에서 ODBC 3에서 함수 지원을 보여 줍니다. *x* 드라이버 및 ODBC 응용 프로그램 및 ODBC 3에 대해 함수를 호출할 때 드라이버 관리자에 의해 수행 매핑. *x* 드라이버입니다.  
  
|함수|지원됨<br /><br /> 여는<br /><br /> ODBC 3입니다. *x*<br /><br /> 드라이버?|지원됨<br /><br /> 여는<br /><br /> ODBC 3입니다. *x*<br /><br /> 응용 프로그램?|매핑된/지원<br /><br /> ODBC 3. *x*<br /><br /> 드라이버 관리자를<br /><br /> ODBC 3입니다. *x* 드라이버?|  
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
|**SQLGetConnectOption**|[5]|[1]|예|  
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
|**SQLGetStmtOption**|[5]|[1]|예|  
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
|**SQLSetConnectOption**|[5]|[1]|예|  
|**SQLSetCursorName**|예|예|아니요|  
|**SQLSetDescField**|예|예|아니요|  
|**SQLSetDescRec**|예|예|아니요|  
|**SQLSetEnvAttr**|예|예|아니요|  
|**SQLSetPos**|예|예|아니요|  
|**SQLSetParam**|아니요|아니요|예|  
|**SQLSetScrollOption**|예|예|아니요|  
|**SQLSetStmtAttr**|예|예|아니요|  
|**SQLSetStmtOption**|[5]|[1]|예|  
|**SQLSpecialColumns**|예|예|아니요|  
|**SQLStatistics**|예|예|아니요|  
|**SQLTablePrivileges**|예|예|아니요|  
|**SQLTables**|예|예|아니요|  
|**SQLTransact**|아니요|[1]|예|  
  
 [ODBC 3에서 1]이이 함수는 사용 되지 않습니다. *x*합니다. ODBC 3입니다. *x* 응용 프로그램은이 기능을 사용 하지 않아야 합니다. 그러나는 Open Group 또는 ISO CLI 호환 응용 프로그램이이 함수를 호출할 수 있습니다.  
  
 [2] ODBC 3입니다. *x* 응용 프로그램 사용 해야 **SQLBindParameter** 대신 **SQLBindParam**합니다. 그러나는 Open Group 또는 ISO CLI 호환 응용 프로그램이이 함수를 호출할 수 있습니다.  
  
 [3] 드라이버 작성자 한다는 점에 유의 해야 ODBC 2. *x* SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE, 및 SQL_COLUMN_LENGTH를 지원 해야 하는 열 특성 **SQLColAttribute**합니다.  
  
 [4] **SQLCopyDesc** 다른 드라이버에 속해 있는 연결을 통해 한 설명자를 복사할 때 드라이버 관리자에서 부분적으로 구현 됩니다. 드라이버 지원에 필요한 **SQLCopyDesc** 두 자체 연결에 걸쳐 있습니다. 와 같은 함수가 **SQLDrivers**, 드라이버 관리자에서 전적으로 구현 되는,이 목록에 표시 되지 않습니다.  
  
 [특정 상황에서 5] 드라이버 해야이 기능을 지원 합니다. 자세한 내용은이 함수의 참조 페이지를 참조 하세요.  
  
 [6]의 드라이버 지원 하도록 선택할 수 **SQLGetFunctions** 드라이버에서 지 원하는 기능 집합은 달라 연결에서 연결 하는 경우.

