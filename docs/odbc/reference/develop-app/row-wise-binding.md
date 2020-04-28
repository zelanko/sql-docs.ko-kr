---
title: 행 단위 바인딩 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4f622cf4-0603-47a1-a48b-944c4ef46364
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a63565590bbafc6f3a8740dd7cf7d4acbfd4f80
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304274"
---
# <a name="row-wise-binding"></a>행 단위 바인딩
행 단위 바인딩을 사용 하는 경우 응용 프로그램은 데이터가 반환 되는 각 열에 대해 하나 또는 두 개의 요소를 포함 하는 구조체를 정의 합니다. 첫 번째 요소는 데이터 값을 보유 하 고 두 번째 요소는 길이/지표 버퍼를 보유 합니다. SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 설명자 필드를 서로 다른 값으로 설정 하 여 표시기 및 길이 값을 별도의 버퍼에 저장할 수 있습니다. 이 작업이 수행 되 면 구조체에 세 번째 요소가 포함 됩니다. 그런 다음 응용 프로그램은 행 집합의 행 수 만큼의 요소를 포함 하는 이러한 구조의 배열을 할당 합니다.  
  
 응용 프로그램은 SQL_ATTR_ROW_BIND_TYPE statement 특성을 사용 하 여 구조체의 크기를 드라이버에 선언 하 고 배열의 첫 번째 요소에 있는 각 멤버의 주소를 바인딩합니다. 따라서 드라이버는 특정 행 및 열에 대 한 데이터 주소를  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size)  
```  
  
 행 번호는 1에서 행 집합의 크기에 해당 합니다. C의 배열 인덱싱은 0부터 시작 하므로 행 번호에서 1을 뺍니다. 다음 그림에서는 행 단위 바인딩의 작동 방식을 보여 줍니다. 일반적으로 바인딩되는 열만 구조에 포함 됩니다. 구조는 결과 집합 열과 관련이 없는 필드를 포함할 수 있습니다. 열은 임의의 순서로 구조에 배치 될 수 있지만 명확 하 게 하기 위해 순차적으로 표시 됩니다.  
  
 ![행&#45;단위 바인딩을 표시 합니다.](../../../odbc/reference/develop-app/media/pr22.gif "pr22")  
  
 예를 들어 다음 코드는 OrderID, 판매원 및 상태 열에 대 한 데이터를 반환 하는 요소와 판매원 및 상태 열에 대 한 길이/표시기를 포함 하는 구조체를 만듭니다. 이러한 구조를 10 개 할당 하 고 OrderID, 영업 사원 및 상태 열에 바인딩합니다.  
  
```  
#define ROW_ARRAY_SIZE 10  
  
// Define the ORDERINFO struct and allocate an array of 10 structs.  
typedef struct {  
   SQLUINTEGER   OrderID;  
   SQLINTEGER    OrderIDInd;  
   SQLCHAR       SalesPerson[11];  
   SQLINTEGER    SalesPersonLenOrInd;  
   SQLCHAR       Status[7];  
   SQLINTEGER    StatusLenOrInd;  
} ORDERINFO;  
ORDERINFO OrderInfoArray[ROW_ARRAY_SIZE];  
  
SQLULEN    NumRowsFetched;  
SQLUSMALLINT   RowStatusArray[ROW_ARRAY_SIZE], i;  
SQLRETURN      rc;  
SQLHSTMT       hstmt;  
  
// Specify the size of the structure with the SQL_ATTR_ROW_BIND_TYPE  
// statement attribute. This also declares that row-wise binding will  
// be used. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE  
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement  
// attribute to point to the row status array. Set the  
// SQL_ATTR_ROWS_FETCHED_PTR statement attribute to point to  
// NumRowsFetched.  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, sizeof(ORDERINFO), 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, ROW_ARRAY_SIZE, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROWS_FETCHED_PTR, &NumRowsFetched, 0);  
  
// Bind elements of the first structure in the array to the OrderID,  
// SalesPerson, and Status columns.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, &OrderInfoArray[0].OrderID, 0, &OrderInfoArray[0].OrderIDInd);  
SQLBindCol(hstmt, 2, SQL_C_CHAR, OrderInfoArray[0].SalesPerson,  
            sizeof(OrderInfoArray[0].SalesPerson),  
            &OrderInfoArray[0].SalesPersonLenOrInd);  
SQLBindCol(hstmt, 3, SQL_C_CHAR, OrderInfoArray[0].Status,  
            sizeof(OrderInfoArray[0].Status), &OrderInfoArray[0].StatusLenOrInd);  
  
// Execute a statement to retrieve rows from the Orders table.  
SQLExecDirect(hstmt, "SELECT OrderID, SalesPerson, Status FROM Orders", SQL_NTS);  
  
// Fetch up to the rowset size number of rows at a time. Print the actual  
// number of rows fetched; this number is returned in NumRowsFetched.  
// Check the row status array to print only those rows successfully  
// fetched. Code to check if rc equals SQL_SUCCESS_WITH_INFO or  
// SQL_ERRORnot shown.  
while ((rc = SQLFetchScroll(hstmt,SQL_FETCH_NEXT,0)) != SQL_NO_DATA) {  
   for (i = 0; i < NumRowsFetched; i++) {  
      if (RowStatusArray[i] == SQL_ROW_SUCCESS|| RowStatusArray[i] ==   
         SQL_ROW_SUCCESS_WITH_INFO) {  
         if (OrderInfoArray[i].OrderIDInd == SQL_NULL_DATA)  
            printf(" NULL      ");  
         else  
            printf("%d\t", OrderInfoArray[i].OrderID);  
         if (OrderInfoArray[i].SalesPersonLenOrInd == SQL_NULL_DATA)  
            printf(" NULL      ");  
         else  
            printf("%s\t", OrderInfoArray[i].SalesPerson);  
         if (OrderInfoArray[i].StatusLenOrInd == SQL_NULL_DATA)  
            printf(" NULL\n");  
         else  
            printf("%s\n", OrderInfoArray[i].Status);  
      }  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
