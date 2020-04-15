---
title: 성명서 집행 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], executing
ms.assetid: e5f0d2ee-0453-4faf-b007-12978dd300a1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c3ce09809c896a4d1d9333da00367f972655f96b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305744"
---
# <a name="executing-a-statement"></a>명령문 실행
데이터베이스 엔진에서 컴파일(준비)하고 문을 정의하는 사람에 따라 문을 실행하는 네 가지 방법이 있습니다.  
  
-   **직접 실행** 응용 프로그램은 SQL 문을 정의합니다. 단일 단계에서 런타임에 준비하고 실행합니다.  
  
-   **준비된 실행** 응용 프로그램은 SQL 문을 정의합니다. 별도의 단계로 런타임에 준비되고 실행됩니다. 명령문은 한 번 준비하고 여러 번 실행할 수 있습니다.  
  
-   **수속 절차** 응용 프로그램은 개발 시 하나 이상의 SQL 문을 정의하고 컴파일하고 이러한 문을 데이터 원본에 프로시저로 저장할 수 있습니다. 프로시저는 런타임에 하나 이상의 실행됩니다. 응용 프로그램은 카탈로그 함수를 사용하여 사용 가능한 저장 프로시저를 열거할 수 있습니다.  
  
-   **카탈로그 기능** 드라이버 작성기는 미리 정의된 결과 집합을 반환하는 함수를 만듭니다. 일반적으로 이 함수는 미리 정의된 SQL 문을 제출하거나 이 목적을 위해 만든 프로시저를 호출합니다. 함수는 런타임에 하나 이상의 실행됩니다.  
  
 특정 명령문(해당 명령문 핸들로 식별됨)은 여러 번 실행할 수 있습니다. 문은 다양한 SQL 문으로 실행하거나 동일한 SQL 문으로 반복적으로 실행할 수 있습니다. 예를 들어 다음 코드는 동일한 명령문*핸들(hstmt1)을*사용하여 Sales 데이터베이스의 테이블을 검색하고 표시합니다. 그런 다음 이 핸들을 다시 사용하여 사용자가 선택한 테이블의 열을 검색합니다.  
  
```  
SQLHSTMT    hstmt1;  
SQLCHAR *   Table;  
  
// Create a result set of all tables in the Sales database.  
SQLTables(hstmt1, "Sales", SQL_NTS, "sysadmin", SQL_NTS, NULL, 0, NULL, 0);  
  
// Fetch and display the table names; then close the cursor.  
// Code not shown.  
  
// Have the user select a particular table.  
SelectTable(Table);  
  
// Reuse hstmt1 to create a result set of all columns in Table.  
SQLColumns(hstmt1, "Sales", SQL_NTS, "sysadmin", SQL_NTS, Table, SQL_NTS, NULL, 0);  
  
// Fetch and display the column names in Table; then close the cursor.  
// Code not shown.  
```  
  
 다음 코드는 단일 핸들을 사용하여 동일한 문을 반복적으로 실행하여 테이블에서 행을 삭제하는 방법을 보여 주며 있습니다.  
  
```  
SQLHSTMT      hstmt1;  
SQLUINTEGER   OrderID;  
SQLINTEGER    OrderIDInd = 0;  
  
// Prepare a statement to delete orders from the Orders table.  
SQLPrepare(hstmt1, "DELETE FROM Orders WHERE OrderID = ?", SQL_NTS);  
  
// Bind OrderID to the parameter for the OrderID column.  
SQLBindParameter(hstmt1, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &OrderID, 0, &OrderIDInd);  
  
// Repeatedly execute hstmt1 with different values of OrderID.  
while ((OrderID = GetOrderID()) != 0) {  
   SQLExecute(hstmt1);  
}  
```  
  
 많은 드라이버의 경우 문을 할당하는 것은 비용이 많이 드는 작업이므로 이러한 방식으로 동일한 문을 다시 사용하는 것이 일반적으로 기존 문을 해제하고 새 문을 할당하는 것보다 더 효율적입니다. 명령문에 결과 집합을 만드는 응용 프로그램은 문을 다시 실행하기 전에 결과 집합에 대한 커서를 닫아야 합니다. 자세한 내용은 [커서 닫기](../../../odbc/reference/develop-app/closing-the-cursor.md)를 참조하십시오.  
  
 또한 문을 다시 사용하면 한 번에 활성화할 수 있는 명령문 수의 일부 드라이버에 제한이 없도록 응용 프로그램이 강제로 사용됩니다. "활성"의 정확한 정의는 드라이버에 따라 다르지만 준비되었거나 실행되었지만 여전히 결과를 사용할 수 있는 문을 참조하는 경우가 많습니다. 예를 들어 **INSERT** 문을 준비한 후에는 일반적으로 활성 으로 간주됩니다. **SELECT** 문이 실행되고 커서가 여전히 열려 있는 후에는 일반적으로 활성 으로 간주됩니다. CREATE **TABLE** 문이 실행된 후에는 일반적으로 활성 으로 간주되지 않습니다.  
  
 응용 프로그램은 SQL_MAX_CONCURRENT_ACTIVITIES 옵션으로 **SQLGetInfo를** 호출하여 한 번에 단일 연결에서 활성화할 수 있는 명령문 수를 결정합니다. 응용 프로그램은 데이터 원본에 대한 여러 연결을 열어 이 제한보다 더 많은 활성 문을 사용할 수 있습니다. 그러나 연결비용이 많이 들 수 있으므로 성능에 미치는 영향을 고려해야 합니다.  
  
 응용 프로그램은 SQL_ATTR_QUERY_TIMEOUT 명령문 특성으로 실행하기 위해 문에 할당된 시간을 제한할 수 있습니다. 데이터 원본이 결과 집합을 반환하기 전에 시간 지정 기간이 만료되면 SQL 문을 실행하는 함수가 SQLSTATE HYT00(시간 지정 만료)을 반환합니다. 기본적으로 시간 제한은 없습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [직접 실행](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [준비된 실행](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [프로시저](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [SQL 문의 일괄 처리](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [카탈로그 함수 실행](../../../odbc/reference/develop-app/executing-catalog-functions.md)
