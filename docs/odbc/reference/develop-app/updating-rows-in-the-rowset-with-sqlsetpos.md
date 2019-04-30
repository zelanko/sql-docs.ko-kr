---
title: SQLSetPos를 사용 하 여 행 집합의 행을 업데이트 하는 중입니다. | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dfb57a6512245c9adb36a511ce48721dd901995c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313097"
---
# <a name="updating-rows-in-the-rowset-with-sqlsetpos"></a>SQLSetPos를 사용하여 행 집합의 행 업데이트
업데이트 작업과 **SQLSetPos** 데이터 원본에서 데이터를 사용 하는 응용 프로그램 버퍼에 바인딩된 각 열에 대 한 (길이/표시기 버퍼의 값 SQL_COLUMN_IGNORE 아닌) 테이블의 하나 이상의 선택한 행을 업데이트 합니다. 바인딩되지 않은 열을 업데이트 되지 않습니다.  
  
 사용 하 여 행을 업데이트 하 **SQLSetPos**, 응용 프로그램에서 다음을 수행 합니다.  
  
1.  행 집합 버퍼에 새 데이터 값을 배치합니다. 긴 데이터를 전송 하는 방법에 대 한 내용은 **SQLSetPos**를 참조 하십시오 [Long 데이터 및 SQLSetPos 및 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)합니다.  
  
2.  필요에 따라 각 열의 길이/표시기 버퍼의 값을 설정 합니다. 이 값은 이진 버퍼를 NULL로 설정할 열에 SQL_NULL_DATA를 바인딩된 열에 대 한 데이터의 바이트 길이 문자열 버퍼에 바인딩된 열에 대 한 데이터 또는 SQL_NTS 바이트 길이입니다.  
  
3.  SQL_COLUMN_IGNORE 업데이트할 필요가 이러한 열의 길이/표시기 버퍼의 값을 설정 합니다. 응용 프로그램이 기존 데이터를 다시 전송 하 여이 단계를 건너뛸 수, 있지만이 비효율적 이며 잘렸습니다. 읽을 때 데이터 원본에 값을 보내는 위험 합니다.  
  
4.  호출 **SQLSetPos** 사용 하 여 *작업* SQL_UPDATE로 설정 하 고 *RowNumber* 업데이트할 행의 수로 설정 합니다. 하는 경우 *RowNumber* 가 0 이면 행 집합의 모든 행이 업데이트 됩니다.  
  
 이후에 **SQLSetPos** 업데이트 된 행에 설정 된 현재 행을 반환 합니다.  
  
 행 집합의 모든 행을 업데이트 하는 경우 (*RowNumber* 0), 응용 프로그램 (가리키는 SQL_ATTR_ROW_OPERATION_PTR 행 작업 배열의 해당 요소를 설정 하 여 특정 행의 업데이트를 비활성화할 수 있습니다 문 특성) SQL_ROW_IGNORE 하 합니다. 행 작업 배열을 크기 (SQL_ATTR_ROW_STATUS_PTR 문 특성에서 가리키는) 행 상태 배열 요소의 수에 해당 합니다. 성공적으로 인출 된 행 집합에서 삭제 되지 않은 결과 집합의 행에만 업데이트 하려면 응용 프로그램에서는 행 상태 배열에 행 작업 배열을로 행 집합을 인출 하는 함수에서 **SQLSetPos**.  
  
 업데이트로 데이터 원본에 전송 되는 모든 행에 대해 응용 프로그램 버퍼가 유효한 행 데이터가 있어야 합니다. 응용 프로그램 버퍼를 인출 하 여 채워진 및 행 상태 배열이 유지 된 경우 이러한 각 행 위치에 해당 값은 SQL_ROW_DELETED, SQL_ROW_ERROR 또는 SQL_ROW_NOROW 되지 않습니다.  
  
 예를 들어, 다음 코드를 Customers 테이블을 통해 스크롤 및 업데이트, 삭제 또는 새 행을 추가 할 수 있습니다. 새 데이터를 호출 하기 전에 행 집합 버퍼에 배치 **SQLSetPos** 를 업데이트 하거나 새 행을 추가 합니다. 추가 행을 끝에 새 행을 포함 하는 행 집합 버퍼가 할당 이렇게 하면 기존 데이터를 버퍼에 새 행에 대 한 데이터를 배치 하면 덮어쓰지 않습니다.  
  
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
