---
description: 행 스크롤 및 인출
title: 행 스크롤 및 페치 | Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 16caf538ea5406ea4d5f23d4fbd05b2a646a0ba7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473674"
---
# <a name="scrolling-and-fetching-rows"></a>행 스크롤 및 인출
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  스크롤형 커서를 사용하려면 ODBC 애플리케이션에서 다음을 수행해야 합니다.  
  
-   [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)를 사용 하 여 커서 기능을 설정 합니다.  
  
-   **Sqlexecute** 또는 **sqlexecdirect** 를 사용 하 여 커서를 엽니다.  
  
-   **Sqlfetch** 또는 [sqlfetchscroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)을 사용 하 여 행을 스크롤하고 페치합니다.  
  
 **Sqlfetch** 와 **Sqlfetchsroll** 은 모두 한 번에 행 블록을 페치할 수 있습니다. 반환 되는 행 수는 **SQLSetStmtAttr** 를 사용 하 여 SQL_ATTR_ROW_ARRAY_SIZE 매개 변수를 설정 하 여 지정 합니다.  
  
 ODBC 응용 프로그램은 **Sqlfetch** 를 사용 하 여 앞 으로만 이동 가능한 커서를 통해 인출할 수 있습니다.  
  
 **Sqlfetchscroll** 은 커서 주위의 스크롤에 사용 됩니다. **Sqlfetchscroll** 은 상대 인출 (현재 행 집합의 시작 부분에서 행 집합 *n* 행 인출) 및 절대 인출 (행 *n* 에서 시작 하는 행 집합 인출) 외에도 다음, 이전, 첫 번째 및 마지막 행 집합을 인출 하는 것을 지원 합니다. 절대 인출에서 *n* 이 음수 이면 결과 집합의 끝에서 행이 계산 됩니다. 예를 들어 이 숫자가 -1이면 결과 집합의 마지막 행에서 시작하는 행 집합이 인출됩니다.  
  
 보고서와 같은 블록 커서 기능에 대해서만 **Sqlfetchscroll** 을 사용 하는 응용 프로그램은 다음 행 집합을 인출 하는 옵션만 사용 하 여 결과 집합을 한 번에 전달할 수 있습니다. 반면에 화면 기반 응용 프로그램은 **Sqlfetchscroll** 의 모든 기능을 활용할 수 있습니다. 응용 프로그램에서 행 집합 크기를 화면에 표시 되는 행 수로 설정 하 고 화면 버퍼를 결과 집합에 바인딩하는 경우 스크롤 막대 작업을 **Sqlfetchscroll** 에 대 한 호출로 직접 변환할 수 있습니다.  
  
|스크롤 막대 작업|SQLFetchScroll 스크롤 옵션|  
|--------------------------|-------------------------------------|  
|페이지 위로|SQL_FETCH_PRIOR|  
|페이지 아래로|SQL_FETCH_NEXT|  
|줄 위로|FetchOffset이-1과 같은 SQL_FETCH_RELATIVE|  
|줄 아래로|FetchOffset이 1인 SQL_FETCH_RELATIVE|  
|스크롤 상자 맨 위로|SQL_FETCH_FIRST|  
|스크롤 상자 맨 아래로|SQL_FETCH_LAST|  
|임의 스크롤 상자 위치|SQL_FETCH_ABSOLUTE|  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [ODBC의 행 집합에 책갈피 설정](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;커서 사용 ](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
