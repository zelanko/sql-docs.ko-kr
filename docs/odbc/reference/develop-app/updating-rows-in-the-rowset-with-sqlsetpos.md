---
title: SQLSetPos로 행 업데이트 행 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating rows
ms.assetid: d83a8c2a-5aa8-4f19-947c-79a817167ee1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4851d4ba741379fc188b2b88c895a378ef3bb80d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298973"
---
# <a name="updating-rows-in-the-rowset-with-sqlsetpos"></a>SQLSetPos를 사용하여 행 집합의 행 업데이트
**SQLSetPos의** 업데이트 작업은 데이터 원본이 각 바인딩된 열에 대한 응용 프로그램 버퍼의 데이터를 사용하여 테이블의 하나 이상의 선택된 행을 업데이트하도록 합니다(길이/표시기 버퍼의 값이 SQL_COLUMN_IGNORE 않는 한). 바인딩되지 않은 열은 업데이트되지 않습니다.  
  
 **SQLSetPos로**행을 업데이트하려면 응용 프로그램은 다음을 수행합니다.  
  
1.  행 집합 버퍼에 새 데이터 값을 배치합니다. **SQLSetPos를**사용하여 긴 데이터를 보내는 방법에 대한 자세한 내용은 [긴 데이터 및 SQLSetPos 및 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)를 참조하십시오.  
  
2.  필요에 따라 각 열의 길이/표시기 버퍼의 값을 설정합니다. 문자열 버퍼에 바인딩된 열에 대한 데이터 또는 SQL_NTS 바이트 길이, 이진 버퍼에 바인딩된 열에 대한 데이터의 바이트 길이 및 NULL로 설정될 모든 열에 대한 SQL_NULL_DATA.  
  
3.  SQL_COLUMN_IGNORE 업데이트할 수 없는 열의 길이/표시기 버퍼에 값을 설정합니다. 응용 프로그램이 이 단계를 건너뛰고 기존 데이터를 다시 보낼 수 있지만 이는 비효율적이며 읽을 때 잘린 데이터 원본으로 값을 보낼 위험이 있습니다.  
  
4.  *작업을* 사용하여 **SQLSetPos를** SQL_UPDATE 로 설정하고 *RowNumber를* 업데이트할 행 수로 설정합니다. *RowNumber가* 0이면 행 집합의 모든 행이 업데이트됩니다.  
  
 **SQLSetPos가** 반환되면 현재 행이 업데이트된 행으로 설정됩니다.  
  
 행 집합의 모든 행을 업데이트할*때(RowNumber가* 0과 같음) 응용 프로그램은 행 작업 배열의 해당 요소(SQL_ATTR_ROW_OPERATION_PTR 문 특성으로 가리키는)를 SQL_ROW_IGNORE 설정하여 특정 행의 업데이트를 비활성화할 수 있습니다. 행 작업 배열은 행 상태 배열(SQL_ATTR_ROW_STATUS_PTR 문 특성으로 가리키는)에 대한 요소의 크기와 수에 해당합니다. 성공적으로 가져온 결과 집합의 해당 행만 업데이트하고 행 집합에서 삭제되지 않은 경우 응용 프로그램은 행 집합을 가져온 함수의 행 상태 배열을 **SQLSetPos로**가져옵니다.  
  
 업데이트로 데이터 원본으로 전송되는 모든 행에 대해 응용 프로그램 버퍼에는 유효한 행 데이터가 있어야 합니다. 응용 프로그램 버퍼가 가져오기로 채워지고 행 상태 배열이 유지된 경우 이러한 각 행 위치의 해당 값은 SQL_ROW_DELETED, SQL_ROW_ERROR 또는 SQL_ROW_NOROW 않아야 합니다.  
  
 예를 들어 다음 코드를 통해 사용자는 Customers 테이블을 스크롤하여 새 행을 업데이트, 삭제 또는 추가할 수 있습니다. **SQLSetPos를** 호출하기 전에 행 집합 버퍼에 새 데이터를 배치하여 새 행을 업데이트하거나 추가합니다. 행 집합 버퍼의 끝에 새 행을 보유하는 추가 행이 할당됩니다. 이렇게 하면 새 행의 데이터가 버퍼에 배치될 때 기존 데이터가 덮어쓰지 않습니다.  
  
```  
#define UPDATE_ROW   100  
#define DELETE_ROW   101  
#define ADD_ROW      102  
  
SQLUINTEGER    CustIDArray[11];  
SQLCHAR        NameArray[11][51], AddressArray[11][51],   
               PhoneArray[11][11];  
SQLINTEGER     CustIDIndArray[11], NameLenOrIndArray[11],   
               AddressLenOrIndArray[11],  
               PhoneLenOrIndArray[11];  
SQLUSMALLINT   RowStatusArray[10], Action, RowNum;  
SQLRETURN      rc;  
SQLHSTMT       hstmt;  
  
// Set the SQL_ATTR_ROW_BIND_TYPE statement attribute to use column-wise   
// binding. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE   
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement   
// attribute to point to the row status array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_KEYSET_DRIVEN, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, SQL_BIND_BY_COLUMN, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, 10, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
  
// Bind arrays to the CustID, Name, Address, and Phone columns.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, CustIDArray, 0, CustIDIndArray);  
SQLBindCol(hstmt, 2, SQL_C_CHAR, NameArray, sizeof(NameArray[0]), NameLenOrIndArray);  
SQLBindCol(hstmt, 3, SQL_C_CHAR, AddressArray, sizeof(AddressArray[0]),  
            AddressLenOrIndArray);  
SQLBindCol(hstmt, 4, SQL_C_CHAR, PhoneArray, sizeof(PhoneArray[0]),  
            PhoneLenOrIndArray);  
  
// Execute a statement to retrieve rows from the Customers table.  
SQLExecDirect(hstmt, "SELECT CustID, Name, Address, Phone FROM Customers", SQL_NTS);  
  
// Fetch and display the first 10 rows.  
rc = SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
DisplayData(CustIDArray, CustIDIndArray, NameArray, NameLenOrIndArray, AddressArray,  
            AddressLenOrIndArray, PhoneArray, PhoneLenOrIndArray, RowStatusArray);  
  
// Call GetAction to get an action and a row number from the user.  
while (GetAction(&Action, &RowNum)) {  
   switch (Action) {  
  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmt, Action, RowNum);  
         DisplayData(CustIDArray, CustIDIndArray,  
                     NameArray, NameLenOrIndArray,  
                     AddressArray, AddressLenOrIndArray,  
                     PhoneArray, PhoneLenOrIndArray, RowStatusArray);  
         break;  
  
      case UPDATE_ROW:  
         // Place the new data in the rowset buffers and update the   
         // specified row.  
         GetNewData(&CustIDArray[RowNum - 1], &CustIDIndArray[RowNum - 1],  
                  NameArray[RowNum - 1], &NameLenOrIndArray[RowNum - 1],  
                  AddressArray[RowNum - 1], &AddressLenOrIndArray[RowNum - 1],  
                  PhoneArray[RowNum - 1], &PhoneLenOrIndArray[RowNum - 1]);  
         SQLSetPos(hstmt, RowNum, SQL_UPDATE, SQL_LOCK_NO_CHANGE);  
         break;  
  
      case DELETE_ROW:  
         // Delete the specified row.  
         SQLSetPos(hstmt, RowNum, SQL_DELETE, SQL_LOCK_NO_CHANGE);  
         break;  
  
      case ADD_ROW:  
         // Place the new data in the rowset buffers at index 10.   
         // This is an extra element for new rows so rowset data is   
         // not overwritten. Insert the new row. Row 11 corresponds   
         // to index 10.  
         GetNewData(&CustIDArray[10], &CustIDIndArray[10],  
                     NameArray[10], &NameLenOrIndArray[10],  
                     AddressArray[10], &AddressLenOrIndArray[10],  
                     PhoneArray[10], &PhoneLenOrIndArray[10]);  
         SQLSetPos(hstmt, 11, SQL_ADD, SQL_LOCK_NO_CHANGE);  
         break;  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
