---
title: 행 단위 바인딩은 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4f622cf4-0603-47a1-a48b-944c4ef46364
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d5f36f33773a10212c37eac5087327935981a9c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="row-wise-binding"></a>행 단위 바인딩
행 단위 바인딩은 사용할 경우 응용 프로그램 하나 또는 두 개가 포함 된 구조체를 정의 또는 경우에 따라 3 개의 데이터 반환 되는 각 열에 대 한 요소입니다. 첫 번째 요소는 데이터 값을 보유 하 고 두 번째 요소가 고 길이/표시기 버퍼입니다. 표시기 및 길이 값에에서 저장할 수 별도 버퍼 SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 설명자 필드; 있는 다른 값을 설정 하 여 이 도구를 실행 하는 경우 구조는 세 번째 요소를 포함 합니다. 그런 다음 응용 프로그램은 행 집합의 행이 더 많은 요소를 포함 하는 이러한 구조 배열을 할당 합니다.  
  
 응용 프로그램 SQL_ATTR_ROW_BIND_TYPE 문 특성을 사용 하 여 드라이버를 구조체의 크기를 선언 하 고 배열의 첫 번째 요소에 각 멤버의 주소를 바인딩합니다. 따라서 드라이버 특정 행과 열으로에 대 한 데이터의 주소를 계산할 수 있습니다.  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size)  
```  
  
 여기서 행은 행 집합의 크기에 1부터 매겨집니다. (1에서 뺍니다 행 번호 배열 인덱싱 C에는 0부터 시작 하므로.) 다음 그림에서는 어떻게 행 단위 바인딩의 작동 보여 줍니다. 일반적으로 연결 되는 열에만 구조에 포함 됩니다. 구조는 결과 집합 열의에 연결 되지 않은 필드를 포함할 수 있습니다. 열 순서에 관계 없이 구조에 배치할 수 있습니다 하지만 쉽게 구별할 수 있도록 순서 대로 표시 됩니다.  
  
 ![에서는 행&#45;현명한 바인딩](../../../odbc/reference/develop-app/media/pr22.gif "pr22")  
  
 예를 들어 다음 코드를 반환할 OrderID, 영업 사원, 및 상태 열에 대 한 데이터와 영업 사원 및 상태 열에 대 한 길이/표시기에서 요소는 구조를 만듭니다. 이러한 구조를 10를 할당 하 고 OrderID, 영업 사원, 및 상태 열에 바인딩합니다.  
  
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
