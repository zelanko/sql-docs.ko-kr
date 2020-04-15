---
title: 행 스크롤 및 가져오기 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0ae9f1079f329951045d4b3f61b39c12efc153fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302499"
---
# <a name="scrolling-and-fetching-rows"></a>행 스크롤 및 인출
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  스크롤형 커서를 사용하려면 ODBC 애플리케이션에서 다음을 수행해야 합니다.  
  
-   [SQLSetStmtAttr을](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)사용하여 커서 기능을 설정합니다.  
  
-   **SQLExecute** 또는 **SQLExecDirect를**사용하여 커서를 엽니다.  
  
-   SQLFetch 또는 **SQLFetchScroll** 를 사용하여 [행을](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)스크롤하고 가져옵니다.  
  
 **SQLFetch** 및 **SQLFetchSroll** 모두 한 번에 행 블록을 가져올 수 있습니다. 반환되는 행 수는 **SQLSetStmtAttr을** 사용하여 SQL_ATTR_ROW_ARRAY_SIZE 매개 변수를 설정하여 지정됩니다.  
  
 ODBC 응용 프로그램은 **SQLFetch를** 사용하여 정방향 전용 커서를 통해 가져올 수 있습니다.  
  
 **SQLFetchScroll커서** 주위를 스크롤하는 데 사용됩니다. **SQLFetchScroll는** 상대 가져오기(현재 행 집합의 시작부터 행 *집합 n* 행을 가져오기) 및 절대 페칭(행 *n에서*시작하는 행 집합 가져오기)과 함께 다음, 이전, 첫 번째 및 마지막 행 집합을 가져오는 것을 지원합니다. 절대 가져오기에서 *n이* 음수이면 행은 결과 집합의 끝에서 계산됩니다. 예를 들어 이 숫자가 -1이면 결과 집합의 마지막 행에서 시작하는 행 집합이 인출됩니다.  
  
 보고서와 같은 블록 커서 기능에 대해서만 **SQLFetchScroll를** 사용하는 응용 프로그램은 다음 행 집합을 가져오는 옵션만 사용하여 결과 집합을 한 번 통과할 수 있습니다. 반면에 화면 기반 응용 프로그램은 **SQLFetchScroll**의 모든 기능을 활용할 수 있습니다. 응용 프로그램이 행 집합 크기를 화면에 표시되는 행 수로 설정하고 화면 버퍼를 결과 집합에 바인딩하면 스크롤 막대 작업을 **SQLFetchScroll**에 대한 호출로 직접 변환할 수 있습니다.  
  
|스크롤 막대 작업|SQLFetchScroll 스크롤 옵션|  
|--------------------------|-------------------------------------|  
|페이지 위로|SQL_FETCH_PRIOR|  
|페이지 아래로|SQL_FETCH_NEXT|  
|줄 위로|fetchOffset이 -1과 SQL_FETCH_RELATIVE|  
|줄 아래로|FetchOffset이 1인 SQL_FETCH_RELATIVE|  
|스크롤 상자 맨 위로|SQL_FETCH_FIRST|  
|스크롤 상자 맨 아래로|SQL_FETCH_LAST|  
|임의 스크롤 상자 위치|SQL_FETCH_ABSOLUTE|  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [ODBC의 행 집합에 책갈피 설정](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;커서 사용](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
