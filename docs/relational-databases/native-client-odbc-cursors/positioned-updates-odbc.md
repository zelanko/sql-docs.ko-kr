---
title: "위치 지정 업데이트 (ODBC) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- SQLSetPos function
- SQLSetCursorName function
- ODBC applications, cursors
- cursors [ODBC], positioned updates
- positioned updates [ODBC]
- ODBC cursors, positioned updates
ms.assetid: ff404e02-630f-474d-b5d4-06442b756991
caps.latest.revision: "33"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9fdaa361e1113c2c1602a85af14c1bd74a16550c
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="positioned-updates-odbc"></a>위치 지정 업데이트(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC는 커서에서 위치 지정 업데이트를 수행하는 두 가지 방법을 지원합니다.  
  
-   **SQLSetPos**  
  
-   WHERE CURRENT OF 절  
  
 사용 하는 것 보다 일반적인 방법은 **SQLSetPos**합니다. 여기에는 다음 옵션이 있습니다.  
  
 SQL_POSITION  
 커서를 현재 행 집합의 특정 행에 위치시킵니다.  
  
 SQL_REFRESH  
 커서가 현재 위치한 행으로부터 가져온 값을 갖는 결과 집합 열에 바인딩된 프로그램 변수를 새로 고칩니다.  
  
 SQL_UPDATE  
 결과 집합 열에 바인딩된 프로그램 변수에 저장된 값으로 커서의 현재 행을 업데이트합니다.  
  
 SQL_DELETE  
 커서에서 현재 행을 삭제합니다.  
  
 **SQLSetPos** 모든 문 결과 집합 문 핸들 커서 특성이 서버 커서를 사용 하도록 설정 하는 경우 사용할 수 있습니다. 결과 집합 열은 프로그램 변수에 바인딩되어야 합니다. 호출 응용 프로그램은 행을 인출 하는 즉시 **SQLSetPos**(SQL_POSTION) 행에 커서를 배치 하 합니다. 그런 다음 SQLSetPos(SQL_DELETE)를 호출하여 현재 행을 삭제하거나, 새 데이터 값을 바인딩된 프로그램 변수로 이동하고 SQLSetPos(SQL_UPDATE)를 호출하여 현재 행을 업데이트할 수 있습니다.  
  
 응용 프로그램을 업데이트 하거나 삭제 된 행 집합의 모든 행 **SQLSetPos**합니다. 호출 **SQLSetPos** 편리 하 게 하는 대신 하면 작성 하 고 SQL 문을 실행 합니다. **SQLSetPos** 현재 행 집합에서 작동 하 고에 대 한 호출 후에 사용할 수 있습니다 [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)합니다.  
  
 호출 하 여 행 집합 크기 설정 되어 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) sql_attr_row_array_size 라는 특성 인수를 사용 합니다. **SQLSetPos** 을 호출한 후에 새 행 집합 크기를 사용 하 여 **SQLFetch** 또는 **SQLFetchScroll**합니다. 예를 들어, 행 집합 크기가 변경 되 면 **SQLSetPos** 라고 차례로 **SQLFetch** 또는 **SQLFetchScroll** 호출 됩니다. 에 대 한 호출 **SQLSetPos** 이전 행 집합 크기를 사용 하지만 **SQLFetch** 또는 **SQLFetchScroll** 새 행 집합 크기를 사용 합니다.  
  
 행 집합의 첫 번째 행 번호는 1입니다. RowNumber 인수 **SQLSetPos** ; 행 집합의 행을 식별 해야 해당 값 1 및 가장 최근에 인출 된 행 수 사이의 범위에 있어야 즉, 합니다. 이 값은 행 집합 크기보다 작을 수 있습니다. RowNumber가 0이면 행 집합의 모든 행에 작업이 적용됩니다.  
  
 삭제 작업의 **SQLSetPos** 은 데이터 원본 테이블의 하나 이상의 선택 된 행을 삭제 합니다. 행을 삭제 하려면 **SQLSetPos**, 응용 프로그램 호출 **SQLSetPos** SQL_DELETE로 설정 하는 작업 및 RowNumber 삭제할 행의 수로 설정 합니다. RowNumber가 0이면 행 집합의 모든 행이 삭제됩니다.  
  
 후 **SQLSetPos** 삭제 된 행이 현재 행 및 해당 상태는 sql_row_deleted가 반환 됩니다. 행 추가 위치 지정된 작업을 하는 등에서 사용할 수 없습니다 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 또는 **SQLSetPos**합니다.  
  
 응용 프로그램이 드라이버에서의 업데이트 작업에 대 한 것과 마찬가지로 행 작업 배열을 사용 하 여 특정 행을 삭제 하지 못할 수 있습니다 (RowNumber가 0) 행 집합의 모든 행을 삭제 하면 **SQLSetPos**합니다.  
  
 삭제되는 모든 행은 결과 집합에 있는 행이여야 합니다. 인출로 인해 응용 프로그램 버퍼가 가득 차고 행 상태 배열이 유지되는 경우 이러한 각각의 행 위치에서 값은 SQL_ROW_DELETED, SQL_ROW_ERROR 또는 SQL_ROW_NOROW일 수 없습니다.  
  
 위치 지정 업데이트는 UPDATE, DELETE 및 INSERT 문에 WHERE CURRENT OF 절을 사용하여 수행할 수도 있습니다. 생성는 CURRENT OF가 필요로 하는 커서 이름이 해당 ODBC는 [SQLGetCursorName](../../relational-databases/native-client-odbc-api/sqlgetcursorname.md) 함수 호출 되거나 호출 하 여 지정할 수 있는 **SQLSetCursorName**합니다. 다음은 ODBC 응용 프로그램에서 WHERE CURRENT OF 업데이트를 수행하는 일반적인 단계입니다.  
  
-   호출 **SQLSetCursorName** 문 핸들에 대 한 커서 이름을 설정 합니다.  
  
-   FOR UPDATE OF 절을 사용하여 SELECT 문을 작성하고 실행합니다.  
  
-   호출 **SQLFetchScroll** 를 검색 한 행 집합 또는 **SQLFetch** 행을 가져오려는 합니다.  
  
-   호출 **SQLSetPos** (SQL_POSITION) 행에 커서를 배치 하 합니다.  
  
-   작성 하 고 사용 하 여 설정 커서 이름을 사용 하 여 WHERE CURRENT OF 절이 있는 UPDATE 문을 실행 **SQLSetCursorName**합니다.  
  
 호출할 수 있습니다 **SQLGetCursorName** 호출 하는 대신 SELECT 문을 실행 한 후 **SQLSetCursorName** SELECT 문을 실행 하기 전에. **SQLGetCursorName** 사용 하 여 커서 이름을 설정 하지 않으면 ODBC에서 할당 된 기본 커서 이름을 반환 **SQLSetCursorName**합니다.  
  
 **SQLSetPos** 서버 커서를 사용 하는 경우 WHERE CURRENT OF 보다 선호 됩니다. ODBC 커서 라이브러리에 업데이트 가능한 정적 커서를 사용하면 커서 라이브러리가 기본 테이블의 키 값을 통해 WHERE 절을 추가하는 방법으로 WHERE CURRENT OF 업데이트를 구현합니다. 이 경우 테이블의 키가 고유하지 않으면 불필요한 업데이트가 수행될 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [커서 &#40; ODBC &#41;를 사용 하 여](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
