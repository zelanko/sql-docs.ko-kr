---
description: ODBC 3.x 드라이버 작성
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
ms.openlocfilehash: c5fec9b94dbcf60868c44e49d92bddb4bb73e9cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421347"
---
# <a name="writing-odbc-3x-drivers"></a>ODBC 3.x 드라이버 작성
다음 표에서는 ODBC 3의 함수 지원을 보여 줍니다. *x* 드라이버와 odbc 응용 프로그램, 그리고 odbc 3에 대해 함수가 호출 될 때 드라이버 관리자에서 수행 하는 매핑 *x* 드라이버.  
  
|기능|지원됨<br /><br /> by<br /><br /> ODBC 3. *x*<br /><br /> 요소?|지원됨<br /><br /> by<br /><br /> ODBC 3. *x*<br /><br /> 프로그램별?|매핑/지원 됨<br /><br /> ODBC 3. *x*<br /><br /> 드라이버 관리자<br /><br /> ODBC 3. *x* 드라이버 인가요?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|예|아니요 [1]|예|  
|**SQLAllocEnv**|예|아니요 [1]|예|  
|**SQLAllocHandle**|예|예|예|  
|**SQLAllocStmt**|예|아니요 [1]|예|  
|**SQLBindCol**|예|예|예|  
|**Sqlbindparam 함수와**|예|예 [2]|예|  
|**SQLBindParameter**|예|예|예|  
|**SQLBrowseConnect**|예|예|예|  
|**SQLBulkOperations**|예|예|예|  
|**SQLCancel**|예|예|예|  
|**SQLCloseCursor**|예|예|예|  
|**SQLColAttribute**|예|예|예|  
|**SQLColAttributes**|아니요 [3]|예|예|  
|**SQLColumnPrivileges**|예|예|예|  
|**SQLColumns**|예|예|예|  
|**SQLConnect**|예|예|예|  
|**SQLCopyDesc**|예|예|예 [4]|  
|**SQLDataSources**|예|예|예|  
|**SQLDescribeCol**|예|예|예|  
|**SQLDescribeParam**|예|예|예|  
|**SQLDisconnect**|예|예|예|  
|**SQLDriverConnect**|예|예|예|  
|**SQLDrivers**|예|예|예|  
|**SQLEndTran**|예|예|예|  
|**SQLError**|예|아니요 [1]|예|  
|**SQLExecDirect**|예|예|예|  
|**SQLExecute**|예|예|예|  
|**SQLExtendedFetch**|예|예|예|  
|**SQLFetch**|예|예|예|  
|**SQLFetchScroll**|예|예|예|  
|**SQLForeignKeys**|예|예|예|  
|**SQLFreeConnect**|예|예 [1]|예|  
|**SQLFreeEnv**|예|예 [1]|예|  
|**SQLFreeHandle**|예|예|예|  
|**SQLFreeStmt**|예|예|예|  
|**SQLGetConnectAttr**|예|예|예|  
|**SQLGetConnectOption**|아니요 [5]|아니요 [1]|예|  
|**SQLGetCursorName**|예|예|예|  
|**SQLGetData**|예|예|예|  
|**SQLGetDescField**|예|예|예|  
|**SQLGetDescRec**|예|예|예|  
|**SQLGetDiagField**|예|예|예|  
|**SQLGetDiagRec**|예|예|예|  
|**SQLGetEnvAttr**|예|예|예|  
|**SQLGetFunctions**|아니요 [6]|예|예|  
|**SQLGetInfo**|예|예|예|  
|**SQLGetStmtAttr**|예|예|예|  
|**SQLGetStmtOption**|아니요 [5]|아니요 [1]|예|  
|**SQLGetTypeInfo**|예|예|예|  
|**SQLMoreResults**|예|예|예|  
|**SQLNativeSql**|예|예|예|  
|**SQLNumParams**|예|예|예|  
|**SQLNumResultCols**|예|예|예|  
|**SQLParamData**|예|예|예|  
|**SQLParamOptions**|예|예|예|  
|**SQLPrepare**|예|예|예|  
|**SQLPrimaryKeys**|예|예|예|  
|**SQLProcedureColumns**|예|예|예|  
|**SQLProcedures**|예|예|예|  
|**SQLPutData**|예|예|예|  
|**SQLRowCount**|예|예|예|  
|**SQLSetConnectAttr**|예|예|예|  
|**SQLSetConnectOption**|아니요 [5]|아니요 [1]|예|  
|**SQLSetCursorName**|예|예|예|  
|**SQLSetDescField**|예|예|예|  
|**SQLSetDescRec**|예|예|예|  
|**SQLSetEnvAttr**|예|예|예|  
|**SQLSetPos**|예|예|예|  
|**SQLSetParam**|예|예|예|  
|**SQLSetScrollOption**|예|예|예|  
|**SQLSetStmtAttr**|예|예|예|  
|**SQLSetStmtOption**|아니요 [5]|아니요 [1]|예|  
|**SQLSpecialColumns**|예|예|예|  
|**SQLStatistics**|예|예|예|  
|**SQLTablePrivileges**|예|예|예|  
|**SQLTables**|예|예|예|  
|**SQLTransact**|예|아니요 [1]|예|  
  
 [1]이 함수는 ODBC 3에서 더 이상 사용 되지 않습니다. *x*. ODBC 3. *x* 응용 프로그램은이 함수를 사용 하지 않아야 합니다. 그러나 개방형 그룹 또는 ISO CLI 규격 응용 프로그램은이 함수를 호출할 수 있습니다.  
  
 [2] ODBC 3. *x* 응용 프로그램은 **sqlbindparam 함수와**대신 **SQLBindParameter** 를 사용 해야 합니다. 그러나 개방형 그룹 또는 ISO CLI 규격 응용 프로그램은이 함수를 호출할 수 있습니다.  
  
 [3] 드라이버 작성자는 ODBC 2를 확인 해야 합니다. *x* 열 특성 SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE 및 SQL_COLUMN_LENGTH는 **sqlcolattribute**에서 지원 되어야 합니다.  
  
 [4]   **Sqlcopydesc** 는 다른 드라이버에 속하는 연결 간에 설명자를 복사할 때 드라이버 관리자에 의해 부분적으로 구현 됩니다. 드라이버는 자체 연결의 두 연결에서 **Sqlcopydesc** 를 지 원하는 데 필요 합니다. 드라이버 관리자만이 구현 하는 **Sqldrivers**와 같은 함수는이 목록에 표시 되지 않습니다.  
  
 [5] 특정 상황에서는 드라이버가이 기능을 지원 해야 할 수 있습니다. 자세한 내용은이 함수의 참조 페이지를 참조 하세요.  
  
 [6] 드라이버에서 지 원하는 함수 집합이 연결에 따라 달라 지는 경우 **SQLGetFunctions** 지원 하도록 선택할 수 있습니다.
