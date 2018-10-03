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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5660cfe2f264e0971d30cd2eaf1aadf68581321e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792971"
---
# <a name="executing-a-statement"></a>명령문 실행
컴파일되는 경우 데이터베이스 엔진 및 정의 하는 (준비)에 따라 문을 실행 하는 방법은 네 가지 있습니다.  
  
-   **직접 실행** 응용 프로그램에서 SQL 문을 정의 합니다. 준비 하 고 런타임에 한 번에 실행 됩니다.  
  
-   **준비 된 실행** 응용 프로그램에서 SQL 문을 정의 합니다. 하도록 준비 되 고 별도 단계에서 런타임 시 실행 합니다. 문은 한 번만 준비 하 고 여러 번 실행 될 수 있습니다.  
  
-   **프로시저** 개발에 더 많은 SQL 문 시간 및 이러한 문을 프로시저 데이터 원본의 저장 또는 응용 프로그램 정의 업데이트 하 고 하나를 컴파일할 수 있습니다. 프로시저 실행 시 한 번 이상 실행 됩니다. 응용 프로그램 카탈로그 함수를 사용 하 여 사용 가능한 저장된 프로시저를 열거할 수 있습니다.  
  
-   **카탈로그 함수** 드라이버 작성자는 미리 정의 된 결과 집합을 반환 하는 함수를 만듭니다. 일반적으로이 함수는 미리 정의 된 SQL 문을 제출 또는이 목적을 위해 만든 프로시저를 호출 합니다. 함수는 런타임에 한 번 이상 실행 됩니다.  
  
 특정 문에 (해당 문 핸들에서 식별 됨) 될 수 있습니다 임의의 횟수 만큼 실행 합니다. 다양 한 다른 SQL 문 사용 하 여 문을 실행할 수 있습니다 하거나 동일한 SQL 문을 사용 하 여 반복적으로 실행할 수 있습니다. 예를 들어, 다음 코드에서는 동일한 문 핸들 (*hstmt1*) 검색 하 고 Sales 데이터베이스에 테이블을 표시 합니다. 그런 다음 사용자가 선택한 테이블의 열을 검색 하려면이 핸들을 다시 사용 합니다.  
  
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
  
 및 다음 코드는 반복적으로 동일한 문을 실행 하 여 테이블에서 행을 삭제 하는 단일 핸들을 사용 하는 방법을 보여 줍니다.  
  
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
  
 대부분의 드라이버에 대 한 문을 할당 이므로 비용이 많이 드는 작업을이 방식으로 동일한 문에서 다시 사용 하는 것은 일반적으로 기존 문과 새로 할당 해제 보다 더 효율적입니다. 문에서 결과 집합을 만드는 응용 프로그램을 종료할지; 문 전에 resultset 커서를 주의 해야 합니다. 자세한 내용은 [커서 닫기](../../../odbc/reference/develop-app/closing-the-cursor.md)합니다.  
  
 일부 드라이버의 문 한 번에 활성화 될 수 있는 개수에 제한 하지 않으려면 응용 프로그램을 강제로 문을 다시 사용 합니다. "활성"의 정확한 정의 드라이버 관련 이지만 종종 준비 되거나 실행 된 문에 참조 아직 사용할 수 있는 결과 및 합니다. 예를 들어 후는 **삽입** 준비 된 문, 활성; 일반적으로 간주 됩니다 후를 **선택** 문이 실행 된 커서가 열려를 일반적으로 간주 됩니다 활성; 후에 **CREATE TABLE** 문이 실행 된, 활성으로 일반적으로 간주 되지 않습니다.  
  
 응용 프로그램 확인 횟수 문을 호출 하 여 한 번에 단일 연결에서 활성화 될 수 있습니다 **SQLGetInfo** SQL_MAX_CONCURRENT_ACTIVITIES 옵션을 사용 합니다. 응용 프로그램은 데이터 소스에 여러 연결을 열어이 제한 보다 더 많은 활성 문을 사용할 수 있습니다. 그러나 연결 일 수 있으므로 비용이 많이 드는 성능에 미치는 영향 고려 되어야 합니다.  
  
 응용 프로그램 SQL_ATTR_QUERY_TIMEOUT 문 특성을 사용 하 여 실행 하는 문을에 할당 된 시간을 제한할 수 있습니다. SQL 문을 실행 하는 함수 반환 SQLSTATE HYT00 결과 집합을 반환 하는 데이터 원본 시간 제한 기간이 만료 되 면, (제한 시간 만료 됨). 기본적으로 있는 시간 제한은 없습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [직접 실행](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [준비된 실행](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [절차](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [SQL 문의 일괄 처리](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [카탈로그 함수 실행](../../../odbc/reference/develop-app/executing-catalog-functions.md)
