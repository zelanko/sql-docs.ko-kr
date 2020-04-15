---
title: ODBC API 참조 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apitype: dllExport
ms.assetid: b7a49774-f458-44ce-9a04-a0457501405b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6065db0ea99efaec11190902ec9268db63a6d255
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298937"
---
# <a name="odbc-api-reference"></a>ODBC API 참조
이 섹션의 항목은 각 ODBC 함수를 알파벳 순으로 설명합니다. 각 함수는 C 프로그래밍 언어 함수로 정의됩니다. 설명에는 다음이 포함됩니다.  
  
-   용도  
  
-   ODBC 버전  
  
-   표준 CLI 적합성 수준  
  
-   구문  
  
-   인수  
  
-   반환 값  
  
-   진단  
  
-   사용 및 구현에 대한 의견  
  
-   코드 예제  
  
-   관련 기능에 대한 참조  
  
 표준 CLI 적합성 수준은 ISO 92, 오픈 그룹, ODBC 또는 더 이상 사용되지 않는 수준 중 하나일 수 있습니다. 오픈 그룹은 ISO 92의 순수 한 슈퍼 집합이기 때문에 ISO 92 준수로 태그된 함수도 Open 그룹 버전 1에 나타납니다. Open 그룹 준수로 태그가 지정된 함수도 ODBC 3에 나타납니다. *X,* ODBC 3 때문에. *x는* 오픈 그룹 버전 1의 순수 한 슈퍼 세트입니다. ODBC 를 준수하는 것으로 태그가 지정된 함수는 표준에 나타나지 않습니다. 더 이상 사용되지 않은 것으로 태그가 지정된 함수는 ODBC 3에서 더 이상 사용되지 않습니다. *x*.  
  
 진단 정보의 처리는 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 함수 설명에 설명되어 있습니다. SQLSTATE 값과 연결된 텍스트는 조건에 대한 설명을 제공하기 위해 포함되어 있지만 특정 텍스트를 규정하기 위한 것은 아닙니다.  
  
> [!NOTE]  
>  ODBC 기능에 대한 드라이버 관련 정보는 드라이버 섹션을 참조하십시오.  
  
 이 섹션에는 다음 기능에 대한 항목이 포함되어 있습니다.  
  
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
  
-   [SQLDescribeParam 함수(SQLDescribeParam Function)](../../../odbc/reference/syntax/sqldescribeparam-function.md)  
  
-   [SQLDisconnect 함수](../../../odbc/reference/syntax/sqldisconnect-function.md)  
  
-   [SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)  
  
-   [SQLDrivers 함수](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [SQLEndTran 함수(SQLEndTran Function)](../../../odbc/reference/syntax/sqlendtran-function.md)  
  
-   [SQLError 함수](../../../odbc/reference/syntax/sqlerror-function.md)  
  
-   [SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)  
  
-   [SQL실행 함수](../../../odbc/reference/syntax/sqlexecute-function.md)  
  
-   [SQLExtendedFetch 함수](../../../odbc/reference/syntax/sqlextendedfetch-function.md)  
  
-   [SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)  
  
-   [SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)  
  
-   [SQLForeignKeys 함수](../../../odbc/reference/syntax/sqlforeignkeys-function.md)  
  
-   [SQLFreeConnect 함수](../../../odbc/reference/syntax/sqlfreeconnect-function.md)  
  
-   [SQLFreeEnv 함수](../../../odbc/reference/syntax/sqlfreeenv-function.md)  
  
-   [SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
-   [SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)  
  
-   [SQLGetConnectAttr 함수(SQLGetConnectAttr Function)](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLGetConnectOption 함수](../../../odbc/reference/syntax/sqlgetconnectoption-function.md)  
  
-   [SQLGetCursorName 함수](../../../odbc/reference/syntax/sqlgetcursorname-function.md)  
  
-   [SQLGetData 함수(SQLGetData Function)](../../../odbc/reference/syntax/sqlgetdata-function.md)  
  
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
  
-   [SQLNativeSql 함수(SQLNativeSql Function)](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
-   [SQLNumParams 함수](../../../odbc/reference/syntax/sqlnumparams-function.md)  
  
-   [SQLNumResultCols 함수](../../../odbc/reference/syntax/sqlnumresultcols-function.md)  
  
-   [SQLParamData 함수](../../../odbc/reference/syntax/sqlparamdata-function.md)  
  
-   [SQLParamOptions 함수](../../../odbc/reference/syntax/sqlparamoptions-function.md)  
  
-   [SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)  
  
-   [SQLPrimaryKeys 함수](../../../odbc/reference/syntax/sqlprimarykeys-function.md)  
  
-   [SQLProcedureColumns 함수](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)  
  
-   [SQLProcedures 함수](../../../odbc/reference/syntax/sqlprocedures-function.md)  
  
-   [SQLPutData 함수](../../../odbc/reference/syntax/sqlputdata-function.md)  
  
-   [SQLRowCount 함수(SQLRowCount Function)](../../../odbc/reference/syntax/sqlrowcount-function.md)  
  
-   [SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)  
  
-   [SQLSetConnectOption 함수](../../../odbc/reference/syntax/sqlsetconnectoption-function.md)  
  
-   [SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)  
  
-   [SQLSetDesc필드 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)  
  
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
