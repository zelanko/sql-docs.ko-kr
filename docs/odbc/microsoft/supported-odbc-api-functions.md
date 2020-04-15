---
title: 지원되는 ODBC API 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC, API functions
- ODBC SQL grammar, API functions mapped to driver (table) [ODBC]
ms.assetid: b28a8ed6-09b1-4acf-bf3e-f90bb32422de
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec6ceaf57d8fe3c5325f85a9644cf4c8016663e4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304104"
---
# <a name="supported-odbc-api-functions"></a>지원되는 ODBC API 함수
평준화의 목적은 드라이버에서 사용할 수 있는 기능을 응용 프로그램에 알리는 것입니다. Microsoft ODBC 데스크톱 데이터베이스 드라이버는 모든 코어 및 수준 1 기능을 지원합니다.  
  
 함수 및 문법에 대한 적합성 수준에 대한 자세한 내용은 *ODBC 프로그래머 참조의* [적합성 수준을](../../odbc/reference/develop-app/conformance-levels.md) 참조하십시오.  
  
 ODBC API 함수의 지원은 사용된 드라이버에 따라 달라질 수 있습니다. 다음 표에는 함수에 대한 지원이 요약됩니다. 맨 왼쪽 열은 각 함수에 대한 일반 참조 페이지에 대한 링크를 제공합니다. 이러한 참조 페이지는 [ODBC 프로그래머](../../odbc/reference/syntax/odbc-api-reference.md) 참조 아래ODBC API 참조 [섹션에](../../odbc/reference/odbc-programmer-s-reference.md)사전순으로 나열됩니다. 오른쪽 의 열은 지원되는 각 함수에 대한 드라이버 별 메모에 대한 링크를 제공합니다. 이러한 드라이버 관련 항목은 각 드라이버의 "기타 프로그래밍 세부 정보" 섹션에 나열됩니다. 또는 함수에 대한 동일한 설명이 모든 ODBC 데스크톱 데이터베이스 드라이버에 적용되는 경우 가장 오른쪽 열은 해당 기능에 대한 데스크톱 데이터베이스 드라이버의 지원을 요약하는 항목에 대한 링크를 제공합니다. 이러한 항목은 현재 섹션의 끝에 나열됩니다("지원되는 ODBC API 함수").  
  
|ODBC 기능|드라이버 별 참고 사항 액세스|dBASE 드라이버별 참고 사항|역설 드라이버 관련 노트|텍스트 파일 드라이버 관련 참고 사항|엑셀 드라이버 별 노트|모든 드라이버와 관련된 참고 사항|  
|-------------------|-----------------------------------|----------------------------------|------------------------------------|--------------------------------------|----------------------------------|-----------------------------------|  
|[SQLBindParameter](../../odbc/reference/syntax/sqlbindparameter-function.md)|||||[Excel](../../odbc/microsoft/sqlbindparameter-excel-driver.md)||  
|[SQLCol속성](../../odbc/reference/syntax/sqlcolattributes-function.md)|[액세스](../../odbc/microsoft/sqlcolattributes-access-driver.md)|[Dbase](../../odbc/microsoft/sqlcolattributes-dbase-driver.md)|[역설](../../odbc/microsoft/sqlcolattributes-paradox-driver.md)|[텍스트 파일](../../odbc/microsoft/sqlcolattributes-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlcolattributes-excel-driver.md)||  
|[SQLColumns](../../odbc/reference/syntax/sqlcolattributes-function.md)|[액세스](../../odbc/microsoft/sqlcolattributes-access-driver.md)|[Dbase](../../odbc/microsoft/sqlcolattributes-dbase-driver.md)|[역설](../../odbc/microsoft/sqlcolattributes-paradox-driver.md)|[텍스트 파일](../../odbc/microsoft/sqlcolattributes-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlcolattributes-excel-driver.md)||  
|[SQLConfigDataSource](../../odbc/reference/syntax/sqlconfigdatasource-function.md)|[액세스](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)|[Dbase](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)|[역설](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)|[텍스트 파일](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)|[Excel](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)||  
|[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)|[액세스](../../odbc/microsoft/sqldriverconnect-access-driver.md)|[Dbase](../../odbc/microsoft/sqldriverconnect-dbase-driver.md)|[역설](../../odbc/microsoft/sqldriverconnect-paradox-driver.md)|[텍스트 파일](../../odbc/microsoft/sqldriverconnect-text-file-driver.md)|[Excel](../../odbc/microsoft/sqldriverconnect-excel-driver.md)||  
|[SQLGetCursorName](../../odbc/reference/syntax/sqlgetcursorname-function.md)||||||[모든 드라이버](../../odbc/microsoft/sqlgetcursorname-desktop-database-drivers.md)|  
|[SQLGetData](../../odbc/reference/syntax/sqlgetdata-function.md)||||||[모든 드라이버](../../odbc/microsoft/sqlgetdata-desktop-database-drivers.md)|  
|[SQLGetInfo](../../odbc/reference/syntax/sqlgetinfo-function.md)|[액세스](../../odbc/microsoft/sqlgetinfo-access-driver.md)|[Dbase](../../odbc/microsoft/sqlgetinfo-dbase-driver.md)|[역설](../../odbc/microsoft/sqlgetinfo-paradox-driver.md)|[텍스트 파일](../../odbc/microsoft/sqlgetinfo-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlgetinfo-excel-driver.md)|
|[SQLGetStmt옵션](../../odbc/reference/syntax/sqlgetstmtoption-function.md)||||||[모든 드라이버](../../odbc/microsoft/sqlgetstmtoption-desktop-database-drivers.md)|  
|[SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md)|[액세스](../../odbc/microsoft/sqlgettypeinfo-access-driver.md)|[Dbase](../../odbc/microsoft/sqlgettypeinfo-dbase-driver.md)|[역설](../../odbc/microsoft/sqlgettypeinfo-paradox-driver.md)|[텍스트 파일](../../odbc/microsoft/sqlgettypeinfo-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlgettypeinfo-excel-driver.md)||  
|[SQLMoreResults](../../odbc/reference/syntax/sqlmoreresults-function.md)||||||[모든 드라이버](../../odbc/microsoft/sqlmoreresults-desktop-database-drivers.md)|  
|[SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md)||||||[모든 드라이버](../../odbc/microsoft/sqlprepare-desktop-database-drivers.md)|  
|[SQLProcedureColumns](../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|[액세스](../../odbc/microsoft/sqlprocedurecolumns-access-driver.md)||||||  
|[SQLProcedures](../../odbc/reference/syntax/sqlprocedures-function.md)||||||[모든 드라이버](../../odbc/microsoft/sqlprocedures-desktop-database-drivers.md)|  
|[SQLSet연결옵션](../../odbc/reference/syntax/sqlsetconnectoption-function.md)|[액세스](../../odbc/microsoft/sqlsetconnectoption-access-driver.md)|[Dbase](../../odbc/microsoft/sqlsetconnectoption-dbase-driver.md)|[역설](../../odbc/microsoft/sqlsetconnectoption-paradox-driver.md)|[텍스트 파일](../../odbc/microsoft/sqlsetconnectoption-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlsetconnectoption-excel-driver.md)||  
|[SQLSetCursorName](../../odbc/reference/syntax/sqlsetcursorname-function.md)||||||[모든 드라이버](../../odbc/microsoft/sqlsetcursorname-desktop-database-drivers.md)|  
|[SQLSetPos](../../odbc/reference/syntax/sqlsetpos-function.md)||||||[모든 드라이버](../../odbc/microsoft/sqlsetpos-desktop-database-drivers.md)|  
|[SQLSet스크롤 옵션](../../odbc/reference/syntax/sqlsetscrolloptions-function.md)||||||[모든 드라이버](../../odbc/microsoft/sqlsetscrolloptions-desktop-database-drivers.md)|  
|[SQLSetStmt옵션](../../odbc/reference/syntax/sqlsetstmtoption-function.md)||||||[모든 드라이버](../../odbc/microsoft/sqlsetstmtoption-desktop-database-drivers.md)|  
|[SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md)||||||[모든 드라이버](../../odbc/microsoft/sqlspecialcolumns-desktop-database-drivers.md)|  
|[SQLStatistics](../../odbc/reference/syntax/sqlstatistics-function.md)|[액세스](../../odbc/microsoft/sqlstatistics-access-driver.md)|[Dbase](../../odbc/microsoft/sqlstatistics-dbase-driver.md)|[역설](../../odbc/microsoft/sqlstatistics-paradox-driver.md)|[텍스트 파일](../../odbc/microsoft/sqlstatistics-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlstatistics-excel-driver.md)||  
|[SQLTables](../../odbc/reference/syntax/sqltables-function.md)|[액세스](../../odbc/microsoft/sqltables-access-driver.md)|[Dbase](../../odbc/microsoft/sqltables-dbase-driver.md)|[역설](../../odbc/microsoft/sqltables-paradox-driver.md)|[텍스트 파일](../../odbc/microsoft/sqltables-text-file-driver.md)|[Excel](../../odbc/microsoft/sqltables-excel-driver.md)|  
|[SQLTransact](../../odbc/reference/syntax/sqltransact-function.md)|[액세스](../../odbc/microsoft/sqltransact-access-driver.md)|[Dbase](../../odbc/microsoft/sqltransact-dbase-driver.md)|[역설](../../odbc/microsoft/sqltransact-paradox-driver.md)|[텍스트 파일](../../odbc/microsoft/sqltransact-text-file-driver.md)|[Excel](../../odbc/microsoft/sqltransact-excel-driver.md)||  
  
 다음 항목에서는 ODBC 함수에 대한 설명이 있습니다. 이러한 설명은 모든 ODBC 데스크톱 데이터베이스 드라이버에 적용됩니다.  
  
-   [SQLGetData(데스크톱 데이터베이스 드라이버)](../../odbc/microsoft/sqlgetdata-desktop-database-drivers.md)  
  
-   [SQLGetStmt옵션(데스크톱 데이터베이스 드라이버)](../../odbc/microsoft/sqlgetstmtoption-desktop-database-drivers.md)  
  
-   [SQLMoreResults(데스크톱 데이터베이스 드라이버)](../../odbc/microsoft/sqlmoreresults-desktop-database-drivers.md)  
  
-   [SQLPrepare(데스크톱 데이터베이스 드라이버)](../../odbc/microsoft/sqlprepare-desktop-database-drivers.md)  
  
-   [SQLProcedures(데스크톱 데이터베이스 드라이버)](../../odbc/microsoft/sqlprocedures-desktop-database-drivers.md)  
  
-   [SQLSetCursorName(데스크톱 데이터베이스 드라이버)](../../odbc/microsoft/sqlsetcursorname-desktop-database-drivers.md)  
  
-   [SQLSetPos(데스크톱 데이터베이스 드라이버)](../../odbc/microsoft/sqlsetpos-desktop-database-drivers.md)  
  
-   [SQLSetScrollOptions(데스크톱 데이터베이스 드라이버)](../../odbc/microsoft/sqlsetscrolloptions-desktop-database-drivers.md)  
  
-   [SQLSetStmtOption(데스크톱 데이터베이스 드라이버)](../../odbc/microsoft/sqlsetstmtoption-desktop-database-drivers.md)  
  
-   [SQLSpecialColumns(데스크톱 데이터베이스 드라이버)](../../odbc/microsoft/sqlspecialcolumns-desktop-database-drivers.md)
