---
title: 함수 규칙 | Microsoft Docs
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
ms.openlocfilehash: 45eb427b660496430334633b5d43ee8989211c0f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069750"
---
# <a name="function-conformance"></a>함수 적합성
다음 표에서는 잘 정의 된 각 ODBC 함수의 규칙 수준을 나타냅니다.  
  
|함수|규칙 수준|  
|--------------|-----------------------|  
|**SQLAllocHandle**|코어|  
|**SQLBindCol**|코어|  
|**SQLBindParameter**|코어 [1]|  
|**SQLBrowseConnect**|수준 1|  
|**SQLBulkOperations**|수준 1|  
|**SQLCancel**|코어 [1]|  
|**SQLCloseCursor**|코어|  
|**SQLColAttribute**|코어 [1]|  
|**SQLColumnPrivileges**|Level 2|  
|**SQLColumns**|코어|  
|**SQLConnect**|코어|  
|**SQLCopyDesc**|코어|  
|**SQLDataSources**|코어|  
|**SQLDescribeCol**|코어 [1]|  
|**SQLDescribeParam**|Level 2|  
|**SQLDisconnect**|코어|  
|**SQLDriverConnect**|코어|  
|**SQLDrivers**|코어|  
|**SQLEndTran**|코어 [1]|  
|**SQLExecDirect**|코어|  
|**SQLExecute**|코어|  
|**SQLFetch**|코어|  
|**SQLFetchScroll**|코어 [1]|  
|**SQLForeignKeys**|Level 2|  
|**SQLFreeHandle**|코어|  
|**SQLFreeStmt**|코어|  
|**SQLGetConnectAttr**|코어|  
|**SQLGetCursorName**|코어|  
|**SQLGetData**|코어|  
|**SQLGetDescField**|코어|  
|**SQLGetDescRec**|코어|  
|**SQLGetDiagField**|코어|  
|**SQLGetDiagRec**|코어|  
|**SQLGetEnvAttr**|코어|  
|**SQLGetFunctions**|코어|  
|**SQLGetInfo**|코어|  
|**SQLGetStmtAttr**|코어|  
|**SQLGetTypeInfo**|코어|  
|**SQLMoreResults**|수준 1|  
|**SQLNativeSql**|코어|  
|**SQLNumParams**|코어|  
|**SQLNumResultCols**|코어|  
|**SQLParamData**|코어|  
|**SQLPrepare**|코어|  
|**SQLPrimaryKeys**|수준 1|  
|**SQLProcedureColumns**|수준 1|  
|**SQLProcedures**|수준 1|  
|**SQLPutData**|코어|  
|**SQLRowCount**|코어|  
|**SQLSetConnectAttr**|코어 [2]|  
|**SQLSetCursorName**|코어|  
|**SQLSetDescField**|코어 [1]|  
|**SQLSetDescRec**|코어|  
|**SQLSetEnvAttr**|코어 [2]|  
|**SQLSetPos**|수준 1 [1]|  
|**SQLSetStmtAttr**|코어 [2]|  
|**SQLSpecialColumns**|코어 [1]|  
|**SQLStatistics**|코어|  
|**SQLTablePrivileges**|Level 2|  
|**SQLTables**|코어|  
  
 [1]이 함수의 중요 한 기능은 높은 규칙 수준 에서만 사용할 수 있습니다.  
  
 [2] 규칙 수준에 따라 특정 특성을 기본값이 아닌 값으로 설정 합니다. 자세한 내용은 다음 섹션인 [특성 규칙](../../../odbc/reference/develop-app/attribute-conformance.md)을 참조 하세요.
