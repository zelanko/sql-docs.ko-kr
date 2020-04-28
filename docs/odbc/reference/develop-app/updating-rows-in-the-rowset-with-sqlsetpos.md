---
title: SQLSetPos를 사용 하 여 행 집합의 행 업데이트 Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298973"
---
# <a name="updating-rows-in-the-rowset-with-sqlsetpos"></a>SQLSetPos를 사용하여 행 집합의 행 업데이트
**SQLSetPos** 의 업데이트 작업을 수행 하면 데이터 원본에서 각 바인딩된 열에 대해 응용 프로그램 버퍼의 데이터를 사용 하 여 하나 이상의 선택 된 행을 업데이트 합니다 (길이/지표 버퍼의 값이 SQL_COLUMN_IGNORE 되지 않은 경우). 바인딩되지 않은 열은 업데이트 되지 않습니다.  
  
 **SQLSetPos**를 사용 하 여 행을 업데이트 하기 위해 응용 프로그램은 다음을 수행 합니다.  
  
1.  새 데이터 값을 행 집합 버퍼에 배치 합니다. **SQLSetPos**를 사용 하 여 long 데이터를 전송 하는 방법에 대 한 자세한 내용은 [Long data And SQLSetPos and SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)을 참조 하세요.  
  
2.  필요에 따라 각 열의 길이/표시기 버퍼에 값을 설정 합니다. 이는 문자열 버퍼에 바인딩된 열에 대 한 데이터 또는 SQL_NTS 바이트 길이, 이진 버퍼에 바인딩된 열의 데이터 바이트 길이, NULL로 설정 될 열에 대 한 SQL_NULL_DATA입니다.  
  
3.  SQL_COLUMN_IGNORE 업데이트 하지 않을 열의 길이/표시기 버퍼에 값을 설정 합니다. 응용 프로그램에서이 단계를 건너뛰고 기존 데이터를 다시 보낼 수 있지만이는 데이터를 읽을 때 잘린 데이터 원본에 값을 보내는 위험과 비효율적입니다.  
  
4.  *작업* 을 SQL_UPDATE로 설정 하 고 *RowNumber* 를 업데이트할 행 번호로 설정 하 여 **SQLSetPos** 를 호출 합니다. *RowNumber* 가 0 이면 행 집합의 모든 행이 업데이트 됩니다.  
  
 **SQLSetPos** 가 반환 된 후 현재 행이 업데이트 된 행으로 설정 됩니다.  
  
 행 집합의 모든 행을 업데이트할 때 (*RowNumber* 가 0 인 경우) 응용 프로그램은 행 작업 배열의 해당 요소 (SQL_ATTR_ROW_OPERATION_PTR statement 특성에 의해 가리키는)를 SQL_ROW_IGNORE로 설정 하 여 특정 행의 업데이트를 비활성화할 수 있습니다. Row 작업 배열은 행 상태 배열에 대 한 요소의 크기 및 수에 해당 하며 SQL_ATTR_ROW_STATUS_PTR statement 특성에서 가리킵니다. 성공적으로 인출 되었고 행 집합에서 삭제 되지 않은 결과 집합의 행만 업데이트 하기 위해 응용 프로그램은 행 집합을 인출 하는 함수의 행 상태 배열을 **SQLSetPos**로 사용 합니다.  
  
 데이터 원본에 업데이트로 전송 되는 모든 행의 경우 응용 프로그램 버퍼에 올바른 행 데이터가 있어야 합니다. 페치를 통해 응용 프로그램 버퍼를 채우고 행 상태 배열이 유지 된 경우 이러한 각 행 위치에 있는 값을 SQL_ROW_DELETED, SQL_ROW_ERROR 또는 SQL_ROW_NOROW 하지 않아야 합니다.  
  
 예를 들어 다음 코드를 사용 하 여 사용자는 Customers 테이블을 스크롤하고 새 행을 업데이트, 삭제 또는 추가할 수 있습니다. **SQLSetPos** 를 호출 하기 전에 새 데이터를 행 집합 버퍼에 배치 하 여 새 행을 업데이트 하거나 추가 합니다. 새 행을 저장 하기 위해 행 집합 버퍼의 끝에 추가 행이 할당 됩니다. 이렇게 하면 새 행에 대 한 데이터가 버퍼에 배치 될 때 기존 데이터를 덮어쓰지 않습니다.  
  
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
