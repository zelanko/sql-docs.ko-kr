---
title: ODBC API 구현 세부 정보 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, functions
- SQL Server Native Client ODBC driver, SQL Server-specific behaviors
- ODBC, SQL Server-specific behaviors
- functions [ODBC]
ms.assetid: dca92489-f179-4b1f-997c-adcc46aa17a3
author: rothja
ms.author: jroth
ms.openlocfilehash: b8b27d39327a68a150fe42a0d6f152bd34c0dd4e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022930"
---
# <a name="odbc-api-implementation-details"></a>ODBC API 구현 정보
  이 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버와 함께 사용할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관련 동작을 수행하는 ODBC 함수에 대해 설명합니다. 여기에서 모든 ODBC 함수를 설명하는 것은 아닙니다. 개별 항목에서는 ODBC 함수의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관련 문제에 대해서만 설명합니다. 즉 ODBC 함수에 대한 완전한 참조 자료가 아닙니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 ODBC 3.51 사양을 준수하며, 사용자가 Windows 7 SDK를 사용하고 있는 경우 ODBC 3.8 사양을 준수합니다. 포괄적인 ODBC 참조는 온라인에서 [Odbc 프로그래머 참조](https://go.microsoft.com/fwlink/?LinkId=45250) 를 확인 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [SQLBindCol](sqlbindcol.md)  
  
-   [SQLBindParameter](sqlbindparameter.md)  
  
-   [SQLBrowseConnect](sqlbrowseconnect.md)  
  
-   [SQLCancel](sqlcancel.md)  
  
-   [SQLCloseCursor](sqlclosecursor.md)  
  
-   [SQLColAttribute](sqlcolattribute.md)  
  
-   [SQLColumnPrivileges](sqlcolumnprivileges.md)  
  
-   [SQLColumns](sqlcolumns.md)  
  
-   [SQLConfigDataSource](sqlconfigdatasource.md)  
  
-   [SQLConnect](sqlconnect.md)  
  
-   [SQLDescribeCol](sqldescribecol.md)  
  
-   [SQLDescribeParam](sqldescribeparam.md)  
  
-   [SQLDriverConnect](sqldriverconnect.md)  
  
-   [SQLDrivers](sqldrivers.md)  
  
-   [SQLEndTran](sqlendtran.md)  
  
-   [SQLExecDirect](sqlexecdirect.md)  
  
-   [SQLExecute](sqlexecute.md)  
  
-   [SQLFetch](sqlfetch.md)  
  
-   [SQLFetchScroll](sqlfetchscroll.md)  
  
-   [SQLForeignKeys](sqlforeignkeys.md)  
  
-   [SQLFreeHandle](sqlfreehandle.md)  
  
-   [SQLFreeStmt](sqlfreestmt.md)  
  
-   [SQLGetConnectAttr](sqlgetconnectattr.md)  
  
-   [SQLGetCursorName](sqlgetcursorname.md)  
  
-   [SQLGetData](sqlgetdata.md)  
  
-   [SQLGetDescField](sqlgetdescfield.md)  
  
-   [SQLGetDescRec](sqlgetdescrec.md)  
  
-   [SQLGetDiagField](sqlgetdiagfield.md)  
  
-   [SQLGetFunctions](sqlgetfunctions.md)  
  
-   [SQLGetInfo](sqlgetinfo.md)  
  
-   [SQLGetStmtAttr](sqlgetstmtattr.md)  
  
-   [SQLGetTypeInfo](sqlgettypeinfo.md)  
  
-   [SQLMoreResults](sqlmoreresults.md)  
  
-   [SQLNativeSql](sqlnativesql.md)  
  
-   [SQLNumParams](sqlnumparams.md)  
  
-   [SQLNumResultCols](sqlnumresultcols.md)  
  
-   [SQLParamData](sqlparamdata.md)  
  
-   [SQLPrimaryKeys](sqlprimarykeys.md)  
  
-   [SQLProcedureColumns](sqlprocedurecolumns.md)  
  
-   [SQLProcedures](sqlprocedures.md)  
  
-   [SQLPutData](sqlputdata.md)  
  
-   [SQLRowCount](sqlrowcount.md)  
  
-   [SQLSetConnectAttr](sqlsetconnectattr.md)  
  
-   [SQLSetDescField](sqlsetdescfield.md)  
  
-   [SQLSetDescRec](sqlsetdescrec.md)  
  
-   [SQLSetEnvAttr](sqlsetenvattr.md)  
  
-   [SQLSetStmtAttr](sqlsetstmtattr.md)  
  
-   [SQLSpecialColumns](sqlspecialcolumns.md)  
  
-   [SQLStatistics](../statistics/statistics.md)  
  
-   [SQLTablePrivileges](sqltableprivileges.md)  
  
-   [SQLTables](sqltables.md)  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41; 참조 &#40;SQL Server Native Client](../../database-engine/dev-guide/sql-server-native-client-odbc-reference.md)   
 [SQL Server Native Client를 사용하여 애플리케이션 빌드](../native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
