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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62f2a701fd5ac94c92d41494a4fd1ab023edaf25
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300363"
---
# <a name="writing-odbc-3x-drivers"></a>ODBC 3.x 드라이버 작성
다음 표에서는 ODBC 3의 함수 지원을 보여 줍니다. *x* 드라이버와 odbc 응용 프로그램, 그리고 odbc 3에 대해 함수가 호출 될 때 드라이버 관리자에서 수행 하는 매핑 *x* 드라이버.  
  
|기능|지원됨<br /><br /> by<br /><br /> ODBC 3. *x*<br /><br /> 요소?|지원됨<br /><br /> by<br /><br /> ODBC 3. *x*<br /><br /> 프로그램별?|매핑/지원 됨<br /><br /> ODBC 3. *x*<br /><br /> 드라이버 관리자<br /><br /> ODBC 3. *x* 드라이버 인가요?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|아니요|아니요 [1]|예|  
|**SQLAllocEnv**|아니요|아니요 [1]|예|  
|**SQLAllocHandle**|예|예|아니요|  
|**SQLAllocStmt**|아니요|아니요 [1]|예|  
|**SQLBindCol**|예|예|아니요|  
|**Sqlbindparam 함수와**|아니요|예 [2]|예|  
|**SQLBindParameter**|예|예|아니요|  
|**SQLBrowseConnect**|예|예|아니요|  
|**SQLBulkOperations**|예|예|아니요|  
|**SQLCancel**|예|예|아니요|  
|**SQLCloseCursor**|예|예|아니요|  
|**SQLColAttribute**|예|예|아니요|  
|**SQLColAttributes**|아니요 [3]|아니요|예|  
|**SQLColumnPrivileges**|예|예|아니요|  
|**SQLColumns**|예|예|아니요|  
|**SQLConnect**|예|예|아니요|  
|**SQLCopyDesc**|예|예|예 [4]|  
|**SQLDataSources**|아니요|예|예|  
|**SQLDescribeCol**|예|예|아니요|  
|**SQLDescribeParam**|예|예|아니요|  
|**SQLDisconnect**|예|예|아니요|  
|**SQLDriverConnect**|예|예|아니요|  
|**SQLDrivers**|예|예|예|  
|**SQLEndTran**|예|예|아니요|  
|**SQLError**|아니요|아니요 [1]|예|  
|**SQLExecDirect**|예|예|아니요|  
|**SQLExecute**|예|예|아니요|  
|**SQLExtendedFetch**|예|아니요|아니요|  
|**SQLFetch**|예|예|아니요|  
|**SQLFetchScroll**|예|예|아니요|  
|**SQLForeignKeys**|예|예|아니요|  
|**SQLFreeConnect**|아니요|예 [1]|예|  
|**SQLFreeEnv**|아니요|예 [1]|예|  
|**SQLFreeHandle**|예|예|아니요|  
|**SQLFreeStmt**|예|예|아니요|  
|**SQLGetConnectAttr**|예|예|아니요|  
|**SQLGetConnectOption**|아니요 [5]|아니요 [1]|예|  
|**SQLGetCursorName**|예|예|아니요|  
|**SQLGetData**|예|예|아니요|  
|**SQLGetDescField**|예|예|아니요|  
|**SQLGetDescRec**|예|예|아니요|  
|**SQLGetDiagField**|예|예|아니요|  
|**SQLGetDiagRec**|예|예|아니요|  
|**SQLGetEnvAttr**|예|예|아니요|  
|**SQLGetFunctions**|아니요 [6]|예|예|  
|**SQLGetInfo**|예|예|아니요|  
|**SQLGetStmtAttr**|예|예|아니요|  
|**SQLGetStmtOption**|아니요 [5]|아니요 [1]|예|  
|**SQLGetTypeInfo**|예|예|아니요|  
|**SQLMoreResults**|예|예|아니요|  
|**SQLNativeSql**|예|예|아니요|  
|**SQLNumParams**|예|예|아니요|  
|**SQLNumResultCols**|예|예|아니요|  
|**SQLParamData**|예|예|아니요|  
|**SQLParamOptions**|아니요|예|예|  
|**SQLPrepare**|예|예|아니요|  
|**SQLPrimaryKeys**|예|예|아니요|  
|**SQLProcedureColumns**|예|예|아니요|  
|**SQLProcedures**|예|예|아니요|  
|**SQLPutData**|예|예|아니요|  
|**SQLRowCount**|예|예|아니요|  
|**SQLSetConnectAttr**|예|예|아니요|  
|**SQLSetConnectOption**|아니요 [5]|아니요 [1]|예|  
|**SQLSetCursorName**|예|예|아니요|  
|**SQLSetDescField**|예|예|아니요|  
|**SQLSetDescRec**|예|예|아니요|  
|**SQLSetEnvAttr**|예|예|아니요|  
|**SQLSetPos**|예|예|아니요|  
|**SQLSetParam**|아니요|예|예|  
|**SQLSetScrollOption**|예|예|아니요|  
|**SQLSetStmtAttr**|예|예|아니요|  
|**SQLSetStmtOption**|아니요 [5]|아니요 [1]|예|  
|**SQLSpecialColumns**|예|예|아니요|  
|**SQLStatistics**|예|예|아니요|  
|**SQLTablePrivileges**|예|예|아니요|  
|**SQLTables**|예|예|아니요|  
|**SQLTransact**|아니요|아니요 [1]|예|  
  
 [1]이 함수는 ODBC 3에서 더 이상 사용 되지 않습니다. *x*. ODBC 3. *x* 응용 프로그램은이 함수를 사용 하지 않아야 합니다. 그러나 개방형 그룹 또는 ISO CLI 규격 응용 프로그램은이 함수를 호출할 수 있습니다.  
  
 [2] ODBC 3. *x* 응용 프로그램은 **sqlbindparam 함수와**대신 **SQLBindParameter** 를 사용 해야 합니다. 그러나 개방형 그룹 또는 ISO CLI 규격 응용 프로그램은이 함수를 호출할 수 있습니다.  
  
 [3] 드라이버 작성자는 ODBC 2를 확인 해야 합니다. *x* 열 특성 SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE 및 SQL_COLUMN_LENGTH는 **sqlcolattribute**에서 지원 되어야 합니다.  
  
 [4] **Sqlcopydesc** 는 다른 드라이버에 속하는 연결 간에 설명자를 복사할 때 드라이버 관리자에 의해 부분적으로 구현 됩니다. 드라이버는 자체 연결의 두 연결에서 **Sqlcopydesc** 를 지 원하는 데 필요 합니다. 드라이버 관리자만이 구현 하는 **Sqldrivers**와 같은 함수는이 목록에 표시 되지 않습니다.  
  
 [5] 특정 상황에서는 드라이버가이 기능을 지원 해야 할 수 있습니다. 자세한 내용은이 함수의 참조 페이지를 참조 하세요.  
  
 [6] 드라이버에서 지 원하는 함수 집합이 연결에 따라 달라 지는 경우 **SQLGetFunctions** 지원 하도록 선택할 수 있습니다.
