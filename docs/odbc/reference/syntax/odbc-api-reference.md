---
title: ODBC API 참조 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: dllExport
ms.assetid: b7a49774-f458-44ce-9a04-a0457501405b
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ef5e5ed116a2bdc3392821404099d870477575a2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-api-reference"></a>ODBC API 참조
이 섹션의 항목은 알파벳 순서로 각 ODBC 기능에 설명 합니다. 각 함수는 C 언어 기능을 프로그래밍으로 정의 됩니다. 설명은 다음과 같습니다.  
  
-   용도  
  
-   ODBC 버전  
  
-   표준 CLI 규칙 수준  
  
-   구문  
  
-   인수  
  
-   반환 값  
  
-   진단  
  
-   사용 및 구현에 대 한 설명  
  
-   코드 예제  
  
-   관련 된 기능에 대 한 참조  
  
 표준 CLI 규칙 수준에서 다음 중 하나일 수 있습니다: 92 ISO, Open Group, ODBC 또는 사용 되지 않습니다. Open Group ISO 92의 순수 상위 집합 이므로 ISO 92 –와 호환 되는 또한 Open Group 버전 1에 나타나는 태그를 지정 하는 함수입니다. Open 그룹 규격으로 태그가 지정 된 함수 ODBC 3에도 나타납니다. *x*때문에 ODBC 3. *x* Open Group 버전 1의 순수 상위 집합입니다. ODBC 호환으로 태그를 지정 하는 함수는 모두 표준에 나타납니다. 사용 중단으로 태그가 지정 된 함수에서에서 사용 되지 ODBC 3. *x*합니다.  
  
 진단 정보 처리에 설명 된 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 함수 설명 합니다. SQLSTATE 값과 연결 된 텍스트 조건에 대 한 설명을 제공 포함 되었지만 특정 텍스트를 지시할 위한 용도가 아닙니다.  
  
> [!NOTE]  
>  드라이버 관련 ODBC 함수에 대 한 정보를 드라이버에 대 한 섹션을 참조 합니다.  
  
 이 섹션에는 다음과 같은 기능에 대 한 항목이 포함 되어 있습니다.  
  
-   [SQLAllocConnect 함수](../../../odbc/reference/syntax/sqlallocconnect-function.md)  
  
-   [SQLAllocEnv 함수](../../../odbc/reference/syntax/sqlallocenv-function.md)  
  
-   [SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [SQLAllocStmt 함수](../../../odbc/reference/syntax/sqlallocstmt-function.md)  
  
-   [SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)  
  
-   [SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)  
  
-   [SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)  
  
-   [SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md)  
  
-   [SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md)  
  
-   [SQLCloseCursor 함수](../../../odbc/reference/syntax/sqlclosecursor-function.md)  
  
-   [SQLColAttribute 함수](../../../odbc/reference/syntax/sqlcolattribute-function.md)  
  
-   [SQLColAttributes 함수](../../../odbc/reference/syntax/sqlcolattributes-function.md)  
  
-   [SQLColumnPrivileges 함수](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)  
  
-   [SQLColumns 함수](../../../odbc/reference/syntax/sqlcolumns-function.md)  
  
-   [SQLCompleteAsync 함수](../../../odbc/reference/syntax/sqlcompleteasync-function.md)  
  
-   [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)  
  
-   [SQLCopyDesc 함수](../../../odbc/reference/syntax/sqlcopydesc-function.md)  
  
-   [SQLDataSources 함수](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)  
  
-   [SQLDescribeParam 함수](../../../odbc/reference/syntax/sqldescribeparam-function.md)  
  
-   [SQLDisconnect 함수](../../../odbc/reference/syntax/sqldisconnect-function.md)  
  
-   [SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)  
  
-   [SQLDrivers 함수](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)  
  
-   [SQLError 함수](../../../odbc/reference/syntax/sqlerror-function.md)  
  
-   [SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)  
  
-   [SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)  
  
-   [SQLExtendedFetch 함수](../../../odbc/reference/syntax/sqlextendedfetch-function.md)  
  
-   [SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)  
  
-   [SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)  
  
-   [SQLForeignKeys 함수](../../../odbc/reference/syntax/sqlforeignkeys-function.md)  
  
-   [SQLFreeConnect 함수](../../../odbc/reference/syntax/sqlfreeconnect-function.md)  
  
-   [SQLFreeEnv 함수](../../../odbc/reference/syntax/sqlfreeenv-function.md)  
  
-   [SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
-   [SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)  
  
-   [SQLGetConnectAttr 함수](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLGetConnectOption 함수](../../../odbc/reference/syntax/sqlgetconnectoption-function.md)  
  
-   [SQLGetCursorName 함수](../../../odbc/reference/syntax/sqlgetcursorname-function.md)  
  
-   [SQLGetData 함수](../../../odbc/reference/syntax/sqlgetdata-function.md)  
  
-   [SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md)  
  
-   [SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)  
  
-   [SQLGetDiagField 함수](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [SQLGetDiagRec 함수](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [SQLGetEnvAttr 함수](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [SQLGetFunctions 함수](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [SQLGetInfo 함수](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [SQLGetStmtAttr 함수](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
-   [SQLGetStmtOption 함수](../../../odbc/reference/syntax/sqlgetstmtoption-function.md)  
  
-   [SQLGetTypeInfo 함수](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
-   [SQLMoreResults 함수](../../../odbc/reference/syntax/sqlmoreresults-function.md)  
  
-   [SQLNativeSql 함수](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
-   [SQLNumParams 함수](../../../odbc/reference/syntax/sqlnumparams-function.md)  
  
-   [SQLNumResultCols 함수](../../../odbc/reference/syntax/sqlnumresultcols-function.md)  
  
-   [SQLParamData 함수](../../../odbc/reference/syntax/sqlparamdata-function.md)  
  
-   [SQLParamOptions 함수](../../../odbc/reference/syntax/sqlparamoptions-function.md)  
  
-   [SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)  
  
-   [SQLPrimaryKeys 함수](../../../odbc/reference/syntax/sqlprimarykeys-function.md)  
  
-   [SQLProcedureColumns 함수](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)  
  
-   [SQLProcedures 함수](../../../odbc/reference/syntax/sqlprocedures-function.md)  
  
-   [SQLPutData 함수](../../../odbc/reference/syntax/sqlputdata-function.md)  
  
-   [SQLRowCount 함수](../../../odbc/reference/syntax/sqlrowcount-function.md)  
  
-   [SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)  
  
-   [SQLSetConnectOption 함수](../../../odbc/reference/syntax/sqlsetconnectoption-function.md)  
  
-   [SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)  
  
-   [SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)  
  
-   [SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)  
  
-   [SQLSetEnvAttr 함수](../../../odbc/reference/syntax/sqlsetenvattr-function.md)  
  
-   [SQLSetParam 함수](../../../odbc/reference/syntax/sqlsetparam-function.md)  
  
-   [SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)  
  
-   [SQLSetScrollOptions 함수](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)  
  
-   [SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)  
  
-   [SQLSetStmtOption 함수](../../../odbc/reference/syntax/sqlsetstmtoption-function.md)  
  
-   [SQLSpecialColumns 함수](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)  
  
-   [SQLStatistics 함수](../../../odbc/reference/syntax/sqlstatistics-function.md)  
  
-   [SQLTablePrivileges 함수](../../../odbc/reference/syntax/sqltableprivileges-function.md)  
  
-   [SQLTables 함수](../../../odbc/reference/syntax/sqltables-function.md)  
  
-   [SQLTransact 함수](../../../odbc/reference/syntax/sqltransact-function.md)
