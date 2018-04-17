---
title: 행 스크롤 및 인출 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-cursors
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- scrollable cursors [SQL Server]
- SQL Server Native Client ODBC driver, cursors
- SQLFetchScroll function
- ODBC applications, cursors
- cursors [ODBC], fetching rows
- ODBC cursors, fetching rows
- cursors [ODBC], scrolling rows
- fetching [ODBC]
- ODBC cursors, scrolling rows
ms.assetid: 9109f10d-326b-4a6d-8c97-831f60da8c4c
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3b2824c0b21c845fe2925fec00e58ea46d0cf4d8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="scrolling-and-fetching-rows"></a>행 스크롤 및 인출
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  스크롤형 커서를 사용하려면 ODBC 응용 프로그램에서 다음을 수행해야 합니다.  
  
-   사용 하 여 커서 기능을 설정 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)합니다.  
  
-   사용 하 여 커서를 열고 **SQLExecute** 또는 **SQLExecDirect**합니다.  
  
-   사용 하 여 행을 스크롤하고 인출 **SQLFetch** 또는 [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)합니다.  
  
 둘 다 **SQLFetch** 및 **SQLFetchSroll** 행 블록을 한 번에 인출할 수 있습니다. 사용 하 여 지정 된 행 수가 반환 **SQLSetStmtAttr** SQL_ATTR_ROW_ARRAY_SIZE 매개 변수를 설정 합니다.  
  
 ODBC 응용 프로그램 צ ְ ײ **SQLFetch** 를 정방향 전용 커서를 통해 인출 합니다.  
  
 **SQLFetchScroll** 커서를 스크롤 하는 데 사용 됩니다. **SQLFetchScroll** 다음 인출 지원 상대 인출 하는 것 외에도 이전, 첫 번째 및 마지막 행 집합 (행 집합을 인출할 *n* 현재 행 집합의 시작 부분부터 행)과 절대 인출 (인출 된 행 집합 행에서 시작 *n*). 경우 *n* 는 절대 인출에서 음수 이면 행 결과 집합의 끝에서 계산 됩니다. 예를 들어 이 숫자가 -1이면 결과 집합의 마지막 행에서 시작하는 행 집합이 인출됩니다.  
  
 사용 하는 응용 프로그램 **SQLFetchScroll** 해당 블록에 대 한 보고서와 같이 커서 기능 가능성이 결과 집합을 한 번 통과 옵션을 사용 하 여 다음 행 집합을 인출 하 합니다. 화면 기반 응용 프로그램, 반면에 활용할 수의 모든 기능 **SQLFetchScroll**합니다. 스크롤 막대 작업에 대 한 호출에 직접 변환할 수 있으며이 경우 응용 프로그램이 화면에 표시 되는 행의 수는 행 집합 크기를 설정 하 고 화면 버퍼를 결과 집합에 바인딩합니다를 **SQLFetchScroll**합니다.  
  
|스크롤 막대 작업|SQLFetchScroll 스크롤 옵션|  
|--------------------------|-------------------------------------|  
|페이지 위로|SQL_FETCH_PRIOR|  
|페이지 아래로|SQL_FETCH_NEXT|  
|줄 위로|FetchOffset이-1 인 SQL_FETCH_RELATIVE|  
|줄 아래로|FetchOffset이 1인 SQL_FETCH_RELATIVE|  
|스크롤 상자 맨 위로|SQL_FETCH_FIRST|  
|스크롤 상자 맨 아래로|SQL_FETCH_LAST|  
|임의 스크롤 상자 위치|SQL_FETCH_ABSOLUTE|  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [ODBC의 행에 책갈피 설정](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>관련 항목:  
 [커서 & #40; ODBC & #41;를 사용 하 여](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
