---
title: 규칙 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], function
- function conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: bb5d68cf-d238-481e-babc-2e9401b4700e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b6cb2f56113487922866573caf3b5f8b67fff7c4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47740081"
---
# <a name="function-conformance"></a>함수 적합성
다음 표에서이 방법이 잘 정의 된 규칙 수준은 각 ODBC 함수를 나타냅니다.  
  
|기능|적합성 수준|  
|--------------|-----------------------|  
|**SQLAllocHandle**|핵심|  
|**SQLBindCol**|핵심|  
|**SQLBindParameter**|Core [1]|  
|**SQLBrowseConnect**|수준 1|  
|**SQLBulkOperations**|수준 1|  
|**SQLCancel**|Core [1]|  
|**SQLCloseCursor**|핵심|  
|**SQLColAttribute**|Core [1]|  
|**SQLColumnPrivileges**|수준 2|  
|**SQLColumns**|핵심|  
|**SQLConnect**|핵심|  
|**SQLCopyDesc**|핵심|  
|**SQLDataSources**|핵심|  
|**SQLDescribeCol**|Core [1]|  
|**SQLDescribeParam**|수준 2|  
|**SQLDisconnect**|핵심|  
|**SQLDriverConnect**|핵심|  
|**SQLDrivers**|핵심|  
|**SQLEndTran**|Core [1]|  
|**SQLExecDirect**|핵심|  
|**SQLExecute**|핵심|  
|**SQLFetch**|핵심|  
|**SQLFetchScroll**|Core [1]|  
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
|**SQLSetConnectAttr**|Core [2]|  
|**SQLSetCursorName**|핵심|  
|**SQLSetDescField**|Core [1]|  
|**SQLSetDescRec**|핵심|  
|**SQLSetEnvAttr**|Core [2]|  
|**SQLSetPos**|수준 1 [1]|  
|**SQLSetStmtAttr**|Core [2]|  
|**SQLSpecialColumns**|Core [1]|  
|**SQLStatistics**|핵심|  
|**SQLTablePrivileges**|수준 2|  
|**SQLTables**|핵심|  
  
 [이 함수의 1] 중요 한 기능은 더 높은 적합성 수준 에서만 제공 됩니다.  
  
 [2] 기본이 아닌 값으로 특정 특성을 설정 합니다. 규칙 수준에 따라 달라 집니다. 자세한 내용은 다음 섹션을 참조 하세요 [특성 적합성](../../../odbc/reference/develop-app/attribute-conformance.md)합니다.
