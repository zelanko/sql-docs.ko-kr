---
title: 행 와이즈 바인딩 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304274"
---
# <a name="row-wise-binding"></a>행 단위 바인딩
행 별 바인딩을 사용하는 경우 응용 프로그램은 데이터를 반환할 각 열에 대해 하나 또는 두 개 또는 세 개의 요소를 포함하는 구조를 정의합니다. 첫 번째 요소는 데이터 값을 보유하고 두 번째 요소는 길이/표시기 버퍼를 보유합니다. 표시기 및 길이 값은 SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 설명자 필드를 다른 값으로 설정하여 별도의 버퍼에 저장할 수 있습니다. 이렇게 하면 구조에 세 번째 요소가 포함됩니다. 그런 다음 응용 프로그램은 행 집합에 행이 있는 만큼많은 요소를 포함하는 이러한 구조의 배열을 할당합니다.  
  
 응용 프로그램은 SQL_ATTR_ROW_BIND_TYPE 문 특성을 사용하여 구조체의 크기를 드라이버에 선언하고 배열의 첫 번째 요소에서 각 멤버의 주소를 바인딩합니다. 따라서 드라이버는 특정 행 및 열에 대한 데이터의 주소를 다음과 같이 계산할 수 있습니다.  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size)  
```  
  
 여기서 행에 번호가 1에서 행 집합 크기로 번호가 매겨져 있습니다. (C의 배열 인덱싱은 0을 기준으로 하기 때문에 행 번호에서 하나가 차감됩니다.) 다음 그림에서는 행 별 바인딩의 작동 방식을 보여 주시면 됩니다. 일반적으로 바인딩할 열만 구조에 포함됩니다. 구조체에는 결과 집합 열과 관련이 없는 필드가 포함될 수 있습니다. 열은 구조에 임의의 순서로 배치할 수 있지만 명확성을 위해 순차적으로 표시됩니다.  
  
 ![행&#45;현명한 바인딩 표시](../../../odbc/reference/develop-app/media/pr22.gif "pr22")  
  
 예를 들어 다음 코드는 OrderID, SalesPerson 및 상태 열에 대한 데이터를 반환하는 요소와 영업 사원 및 상태 열에 대한 길이/표시기를 포함하는 구조를 만듭니다. 이러한 구조중 10개에 할당하고 OrderID, SalesPerson 및 상태 열에 바인딩합니다.  
  
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
