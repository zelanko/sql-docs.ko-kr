---
title: "규칙에 따라 작동 | Microsoft Docs"
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
helpviewer_keywords:
- conformance levels [ODBC], function
- function conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: bb5d68cf-d238-481e-babc-2e9401b4700e
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fb178c2359ee9b1df4754615316f80b8284e84a6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="function-conformance"></a>기능 규칙
다음 표에서이 잘 정의 된 규칙 수준과 각 ODBC 함수를 나타냅니다.  
  
|함수|규칙 수준|  
|--------------|-----------------------|  
|**SQLAllocHandle**|핵심|  
|**SQLBindCol**|핵심|  
|**SQLBindParameter**|코어 [1]|  
|**SQLBrowseConnect**|수준 1|  
|**SQLBulkOperations**|수준 1|  
|**SQLCancel**|코어 [1]|  
|**SQLCloseCursor**|핵심|  
|**SQLColAttribute**|코어 [1]|  
|**SQLColumnPrivileges**|수준 2|  
|**SQLColumns**|핵심|  
|**SQLConnect**|핵심|  
|**SQLCopyDesc**|핵심|  
|**SQLDataSources**|핵심|  
|**SQLDescribeCol**|코어 [1]|  
|**SQLDescribeParam**|수준 2|  
|**SQLDisconnect**|핵심|  
|**SQLDriverConnect**|핵심|  
|**SQLDrivers**|핵심|  
|**SQLEndTran**|코어 [1]|  
|**SQLExecDirect**|핵심|  
|**SQLExecute**|핵심|  
|**SQLFetch**|핵심|  
|**SQLFetchScroll**|코어 [1]|  
|**SQLForeignKeys**|수준 2|  
|**SQLFreeHandle**|핵심|  
|**SQLFreeStmt**|핵심|  
|**SQLGetConnectAttr**|핵심|  
|**SQLGetCursorName**|핵심|  
|**SQLGetData**|핵심|  
|**SQLGetDescField**|핵심|  
|**SQLGetDescRec**|핵심|  
|**SQLGetDiagField**|핵심|  
|**SQLGetDiagRec**|핵심|  
|**SQLGetEnvAttr**|핵심|  
|**SQLGetFunctions**|핵심|  
|**SQLGetInfo**|핵심|  
|**SQLGetStmtAttr**|핵심|  
|**SQLGetTypeInfo**|핵심|  
|**SQLMoreResults**|수준 1|  
|**SQLNativeSql**|핵심|  
|**SQLNumParams**|핵심|  
|**SQLNumResultCols**|핵심|  
|**SQLParamData**|핵심|  
|**SQLPrepare**|핵심|  
|**SQLPrimaryKeys**|수준 1|  
|**SQLProcedureColumns**|수준 1|  
|**SQLProcedures**|수준 1|  
|**SQLPutData**|핵심|  
|**SQLRowCount**|핵심|  
|**SQLSetConnectAttr**|코어 [2]|  
|**SQLSetCursorName**|핵심|  
|**SQLSetDescField**|코어 [1]|  
|**SQLSetDescRec**|핵심|  
|**SQLSetEnvAttr**|코어 [2]|  
|**SQLSetPos**|수준 1 [1]|  
|**SQLSetStmtAttr**|코어 [2]|  
|**SQLSpecialColumns**|코어 [1]|  
|**SQLStatistics**|핵심|  
|**SQLTablePrivileges**|수준 2|  
|**SQLTables**|핵심|  
  
 [이 함수는 1] 중요 한 기능이 높은 받는 규칙 수준에만 사용할 수입니다.  
  
 [2]을 기본이 아닌 값으로 특정 특성을 설정 합니다. 규칙 수준에 따라 달라 집니다. 자세한 내용은 다음 섹션을 참조 하십시오. [특성 규칙](../../../odbc/reference/develop-app/attribute-conformance.md)합니다.
