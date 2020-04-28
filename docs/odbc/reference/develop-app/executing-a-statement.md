---
title: 문 실행 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305744"
---
# <a name="executing-a-statement"></a>명령문 실행
다음 네 가지 방법으로 문을 실행 하는 방법에 따라 데이터베이스 엔진에서 컴파일 (준비) 하 고 정의 하는 방법을 사용할 수 있습니다.  
  
-   **직접 실행** 응용 프로그램은 SQL 문을 정의 합니다. 단일 단계에서 런타임에 준비 되 고 실행 됩니다.  
  
-   **준비 된 실행** 응용 프로그램은 SQL 문을 정의 합니다. 별도의 단계에서 런타임에 준비 되 고 실행 됩니다. 문을 한 번 준비한 후 여러 번 실행할 수 있습니다.  
  
-   **프로시저** 응용 프로그램은 개발 시 하나 이상의 SQL 문을 정의 하 고 컴파일하고 이러한 문을 데이터 원본에 프로시저로 저장할 수 있습니다. 프로시저는 런타임에 한 번 이상 실행 됩니다. 응용 프로그램은 카탈로그 함수를 사용 하 여 사용 가능한 저장 프로시저를 열거할 수 있습니다.  
  
-   **카탈로그 함수** 드라이버 작성기는 미리 정의 된 결과 집합을 반환 하는 함수를 만듭니다. 일반적으로이 함수는 미리 정의 된 SQL 문을 전송 하거나이 목적으로 만들어진 프로시저를 호출 합니다. 함수는 런타임에 한 번 이상 실행 됩니다.  
  
 문 핸들에 의해 식별 되는 특정 문은 횟수에 관계 없이 실행할 수 있습니다. 문은 다양 한 SQL 문을 사용 하 여 실행 하거나 동일한 SQL 문을 사용 하 여 반복적으로 실행할 수 있습니다. 예를 들어 다음 코드는 동일한 문 핸들 (*hstmt1*)을 사용 하 여 Sales 데이터베이스의 테이블을 검색 하 고 표시 합니다. 그런 다음이 핸들을 다시 사용 하 여 사용자가 선택한 테이블의 열을 검색 합니다.  
  
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
  
 다음 코드에서는 단일 핸들을 사용 하 여 테이블에서 행을 삭제 하는 동일한 문을 반복적으로 실행 하는 방법을 보여 줍니다.  
  
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
  
 많은 드라이버의 경우 문을 할당 하는 작업은 비용이 많이 들기 때문에 이러한 방식으로 동일한 문을 다시 사용 하는 것은 기존 문을 해제 하 고 새 문을 할당 하는 것 보다 더 효율적입니다. 문에 대 한 결과 집합을 만드는 응용 프로그램은 문을 다시 실행 하기 전에 결과 집합 위에 커서를 닫도록 주의 해야 합니다. 자세한 내용은 [커서 닫기](../../../odbc/reference/develop-app/closing-the-cursor.md)를 참조 하세요.  
  
 문을 다시 사용 하면 한 번에 활성화할 수 있는 문 수의 일부 드라이버에서 응용 프로그램의 제한이 발생 하지 않습니다. "활성"의 정확한 정의는 드라이버별 이지만 준비 또는 실행 되 고 여전히 사용 가능한 결과가 포함 된 문을 참조 하는 경우가 많습니다. 예를 들어 **INSERT** 문이 준비 된 후에는 일반적으로 활성화 된 것으로 간주 됩니다. **SELECT** 문이 실행 되 고 커서가 계속 열려 있으면 일반적으로 활성화 된 것으로 간주 됩니다. **CREATE TABLE** 문을 실행 한 후에는 일반적으로 활성화 된 것으로 간주 되지 않습니다.  
  
 응용 프로그램은 SQL_MAX_CONCURRENT_ACTIVITIES 옵션으로 **SQLGetInfo** 를 호출 하 여 한 번에 하나의 연결에서 활성화 될 수 있는 문 수를 결정 합니다. 응용 프로그램은 데이터 원본에 대 한 여러 연결을 열어이 제한 보다 더 많은 활성 문을 사용할 수 있습니다. 그러나 연결은 비용이 많이 들 수 있으므로 성능에 대 한 영향을 고려해 야 합니다.  
  
 응용 프로그램은 문이 SQL_ATTR_QUERY_TIMEOUT 문 특성을 사용 하 여 실행 되도록 할당 된 시간을 제한할 수 있습니다. 데이터 원본에서 결과 집합을 반환 하기 전에 제한 시간이 만료 되 면 SQL 문을 실행 하는 함수가 SQLSTATE HYT00 (Timeout 만료 됨)를 반환 합니다. 기본적으로 시간 제한은 없습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [직접 실행](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [준비된 실행](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [절차](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [SQL 문의 일괄 처리](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [카탈로그 함수 실행](../../../odbc/reference/develop-app/executing-catalog-functions.md)
