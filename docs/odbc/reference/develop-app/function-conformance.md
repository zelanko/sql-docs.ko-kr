---
title: 기능 적합성 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 33cd0ad4269ed59e31c8ab343ddbb01806afce04
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305594"
---
# <a name="function-conformance"></a>함수 적합성
다음 표는 각 ODBC 함수의 적합성 수준을 나타내며, 이 수준은 잘 정의되어 있습니다.  
  
|함수|규칙 수준|  
|--------------|-----------------------|  
|**SQLAlloc핸들**|핵심|  
|**SQLBindCol**|핵심|  
|**SQLBindParameter**|코어[1]|  
|**SQLBrowseConnect**|수준 1|  
|**SQLBulk운영**|수준 1|  
|**SQLCancel**|코어[1]|  
|**SQLCloseCursor**|핵심|  
|**SQLColAttribute**|코어[1]|  
|**SQLColumnPrivileges**|수준 2|  
|**SQLColumns**|핵심|  
|**SQLConnect**|핵심|  
|**SQLCopyDesc**|핵심|  
|**SQLDataSource**|핵심|  
|**SQLDescribeCol**|코어[1]|  
|**SQLDescribeParam**|수준 2|  
|**SQL분리**|핵심|  
|**SQLDriverConnect**|핵심|  
|**SQLDrivers**|핵심|  
|**SQLEndTran**|코어[1]|  
|**SQLExecDirect**|핵심|  
|**SQLExecute**|핵심|  
|**SQLFetch**|핵심|  
|**SQLFetchScroll**|코어[1]|  
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
|**SQLSetConnectAttr**|코어[2]|  
|**SQLSetCursorName**|핵심|  
|**SQLSetDescField**|코어[1]|  
|**SQLSetDescRec**|핵심|  
|**SQLSetEnvAttr**|코어[2]|  
|**SQLSetPos**|레벨 1[1]|  
|**SQLSetStmtAttr**|코어[2]|  
|**SQLSpecialColumns**|코어[1]|  
|**SQLStatistics**|핵심|  
|**SQLTablePrivileges**|수준 2|  
|**SQLTables**|핵심|  
  
 [1] 이 함수의 중요한 기능은 더 높은 적합성 수준에서만 사용할 수 있습니다.  
  
 [2] 특정 특성을 default값이 아닌 값으로 설정하면 적합성 수준에 따라 다릅니다. 자세한 내용은 다음 섹션인 [특성 적합성을](../../../odbc/reference/develop-app/attribute-conformance.md)참조하십시오.
