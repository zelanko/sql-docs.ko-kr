---
title: 문을 실행 | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], executing
ms.assetid: e5f0d2ee-0453-4faf-b007-12978dd300a1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c98df5ef5b7c3d544744931f771bd803b9e8b17a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="executing-a-statement"></a>문 실행
네 가지 방법으로 컴파일되는 경우 데이터베이스 엔진 및 사용자 정의 하 여 (준비)에 따라 문을 실행 하려면:  
  
-   **직접 실행** 응용 프로그램에는 SQL 문을 정의 합니다. 준비 되며 런타임에 한 번 실행 합니다.  
  
-   **준비 된 실행** 응용 프로그램에는 SQL 문을 정의 합니다. 준비 되며 런타임에 별도의 단계로 실행 합니다. 문은 한 번 준비 하 고 여러 번을 실행할 수 있습니다.  
  
-   **프로시저** 개발에서 더 이상 SQL 문을 시간 및 이러한 문을 프로시저 데이터 원본의 저장 또는 응용 프로그램 정의 업데이트 하 고 하나를 컴파일할 수 있습니다. 프로시저 실행 시 한 번 이상 실행 됩니다. 응용 프로그램 카탈로그 함수를 사용 하 여 사용 가능한 저장된 프로시저를 열거할 수 있습니다.  
  
-   **카탈로그 함수** 드라이버 작성자는 미리 정의 된 결과 집합을 반환 하는 함수를 만듭니다. 일반적으로이 함수 미리 정의 된 SQL 문을 제출 하거나이 용도로 만든 프로시저를 호출 합니다. 함수는 런타임에 한 번 이상 실행 합니다.  
  
 특정 문 (해당 문 핸들으로 식별) 수 있습니다. 여러 번 실행 합니다. 문이 다양 한 서로 다른 SQL 문 실행할 수 있습니다 또는 동일한 SQL 문을 사용 하 여 반복적으로 실행할 수 있습니다. 다음 코드에서는 동일한 문 핸들을 사용 하는 예를 들어 (*hstmt1*) 검색 하 고 Sales 데이터베이스에 테이블을 표시 합니다. 이 핸들을 사용자가 선택한 테이블의 열을 검색 한 다음 다시 사용 합니다.  
  
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
  
 및 다음 코드는 단일 핸들을 반복적으로 동일한 문을 실행 하는 테이블에서 행을 삭제 하는 방법을 보여 줍니다.  
  
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
  
 대부분의 드라이버에 대 한 할당 문을 더 비용이 많이 드는 작업을 다시 이와에서 동일한 문을 사용 하 여 기존 문와 새로 할당 하는 중 보다 대개 효율적 이므로. 문에서 결과 집합을 만드는 응용 프로그램 커서를 닫으려면 문을; 종료할지 하기 전에 설정 결과 대해 주의 해야 합니다. 자세한 내용은 참조 [커서를 닫으면](../../../odbc/reference/develop-app/closing-the-cursor.md)합니다.  
  
 문 한 번에 활성화 될 수 있는 숫자의 일부 드라이버의 제한 사항을 방지 하기 위해 응용 프로그램을 강제로 문을 다시 사용 합니다. "활성"의 정확한 정의 드라이버 관련 있지만 종종 실행 또는 준비 된 문에 참조 및 아직 결과 사용할 수 있습니다. 예를 들어, 이후에 **삽입** 준비 된 문, 활성; 일반적으로 간주 됩니다 후는 **선택** 문이 실행 된 하 고 커서가 열려 있는, 일반적으로 간주 됩니다 활성; 후 한 **CREATE TABLE** 문이 실행 된, 상태인 것으로 일반적으로 간주 되지 않습니다.  
  
 응용 프로그램에서 결정 하는 개수 문을 호출 하 여 한 번에 단일 연결에서 활성화 될 수 있습니다 **SQLGetInfo** SQL_MAX_CONCURRENT_ACTIVITIES 옵션을 사용 합니다. 응용 프로그램은 데이터 소스에 대 한 여러 연결을 열어이 제한 보다 더 활성 문을 사용할 수 있습니다. 그러나 연결 일 수 있으므로 비용이 많이 드는 성능에 미치는 영향 고려 되어야 합니다.  
  
 응용 프로그램을 SQL_ATTR_QUERY_TIMEOUT 문 특성을 사용 하 여 실행 하는 문에 할당 된 시간을 제한할 수 있습니다. 결과 집합을 반환 하는 데이터 원본 시간 제한 기간이 만료 되 면, SQL 문 실행 반환 하 고 SQLSTATE HYT00 (제한 시간 만료 됨). 기본적으로는 시간 제한이 없습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [직접 실행](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [준비된 실행](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [절차](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [SQL 문의 일괄 처리](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [카탈로그 함수 실행](../../../odbc/reference/develop-app/executing-catalog-functions.md)
