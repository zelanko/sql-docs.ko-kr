---
title: 위치 지정 업데이트 및 Delete 문 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: 0eafba50-02c7-46ca-a439-ef3307b935dc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6e5316bee7057b30eace326b3ca82b30b75741fb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282364"
---
# <a name="positioned-update-and-delete-statements"></a>현재 위치 업데이트 및 Delete 문
응용 프로그램은 위치 지정 update 또는 delete 문을 사용 하 여 결과 집합에서 현재 행을 업데이트 하거나 삭제할 수 있습니다. 위치 지정 update 및 delete 문은 일부 데이터 원본에서 지원 되지만 일부 데이터 원본에서는 지원 되지 않습니다. 데이터 원본에서 위치 지정 update 및 delete 문을 지원 하는지 확인 하기 위해 응용 프로그램은 커서의 유형에 따라 SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 또는 SQL_STATIC_CURSOR_ATTRIBUTES1 *InfoType* 를 사용 하 여 **SQLGetInfo** 를 호출 합니다. ODBC 커서 라이브러리는 위치 지정 update 및 delete 문을 시뮬레이트합니다.  
  
 위치 지정 update 또는 delete 문을 사용 하려면 응용 프로그램에서 **SELECT FOR update** 문을 사용 하 여 결과 집합을 만들어야 합니다. 이 문의 구문은 다음과 같습니다.  
  
 [**모두** &#124; **고유**] 선택 *목록* **선택**  
  
 **FROM** *테이블 참조 목록* 에서  
  
 [**WHERE** *검색 조건*]  
  
 [*열 이름* [**,** *열 이름*] ...] **의 업데이트**  
  
 그런 다음 응용 프로그램은 업데이트 하거나 삭제할 행에 커서를 놓습니다. 이렇게 하려면 **Sqlfetchscroll** 을 호출 하 여 필요한 행을 포함 하는 행 집합을 검색 하 고 **SQLSetPos** 를 호출 하 여 행 집합 커서를 해당 행에 배치 합니다. 그런 다음 응용 프로그램은 결과 집합에 사용 되는 문과 다른 문에서 위치 지정 update 또는 delete 문을 실행 합니다. 이러한 문의 구문은 다음과 같습니다.  
  
 **UPDATE** *테이블 이름* 업데이트  
  
 **SET** *열 식별자* **=** {*expression* &#124; **NULL**} 설정  
  
 [**,** *열 식별자* **=** {*expression* &#124; **NULL**}] ...  
  
 **현재** *커서 이름*  
  
 테이블 **에서 삭제** *-이름* **현재** *커서 이름* 입니다.  
  
 이러한 문에는 커서 이름이 필요 합니다. 응용 프로그램은 결과 집합을 만드는 문을 실행 하기 전에 **SQLSetCursorName** 를 사용 하 여 커서 이름을 지정 하거나 커서를 만들 때 데이터 소스에서 커서 이름을 자동으로 생성 하도록 할 수 있습니다. 후자의 경우 응용 프로그램은 **SQLGetCursorName**를 호출 하 여 위치 지정 update 및 delete 문에 사용할 커서 이름을 검색 합니다.  
  
 예를 들어, 다음 코드를 사용 하 여 사용자는 Customers 테이블을 스크롤하고 고객 레코드를 삭제 하거나 주소와 전화 번호를 업데이트할 수 있습니다. **SQLSetCursorName** 를 호출 하 여 고객의 결과 집합을 생성 하기 전에 커서 이름을 지정 하 고 세 개의 문 핸들을 사용 합니다. 결과 집합에는 *hstmtCust* , 위치 지정 update 문에는 *hstmtUpdate* , 배치 된 delete 문에 대해서는 *hstmtDelete* 를 사용 합니다. 코드는 위치 지정 update 문의 매개 변수에 별도의 변수를 바인딩할 수 있지만 행 집합 버퍼를 업데이트 하 고 이러한 버퍼의 요소를 바인딩합니다. 이렇게 하면 행 집합 버퍼가 업데이트 된 데이터와 동기화 된 상태로 유지 됩니다.  
  
```  
#define POSITIONED_UPDATE 100  
#define POSITIONED_DELETE 101  
  
SQLUINTEGER    CustIDArray[10];  
SQLCHAR        NameArray[10][51], AddressArray[10][51],   
               PhoneArray[10][11];  
SQLINTEGER     CustIDIndArray[10], NameLenOrIndArray[10],   
               AddressLenOrIndArray[10],  
               PhoneLenOrIndArray[10];  
SQLUSMALLINT   RowStatusArray[10], Action, RowNum;  
SQLHSTMT       hstmtCust, hstmtUpdate, hstmtDelete;  
  
// Set the SQL_ATTR_BIND_TYPE statement attribute to use column-wise   
// binding. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE   
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement   
// attribute to point to the row status array.  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_BIND_TYPE, SQL_BIND_BY_COLUMN, 0);  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_ARRAY_SIZE, 10, 0);  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
  
// Bind arrays to the CustID, Name, Address, and Phone columns.  
SQLBindCol(hstmtCust, 1, SQL_C_ULONG, CustIDArray, 0, CustIDIndArray);  
SQLBindCol(hstmtCust, 2, SQL_C_CHAR, NameArray, sizeof(NameArray[0]),  
            NameLenOrIndArray);  
SQLBindCol(hstmtCust, 3, SQL_C_CHAR, AddressArray, sizeof(AddressArray[0]),  
         AddressLenOrIndArray);  
SQLBindCol(hstmtCust, 4, SQL_C_CHAR, PhoneArray, sizeof(PhoneArray[0]),  
            PhoneLenOrIndArray);  
  
// Set the cursor name to Cust.  
SQLSetCursorName(hstmtCust, "Cust", SQL_NTS);  
  
// Prepare positioned update and delete statements.  
SQLPrepare(hstmtUpdate,  
   "UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust",  
   SQL_NTS);  
SQLPrepare(hstmtDelete, "DELETE FROM Customers WHERE CURRENT OF Cust", SQL_NTS);  
  
// Execute a statement to retrieve rows from the Customers table.  
SQLExecDirect(hstmtCust,  
   "SELECT CustID, Name, Address, Phone FROM Customers FOR UPDATE OF Address, Phone",  
   SQL_NTS);  
  
// Fetch and display the first 10 rows.  
SQLFetchScroll(hstmtCust, SQL_FETCH_NEXT, 0);  
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
         SQLFetchScroll(hstmtCust, Action, RowNum);  
         DisplayData(CustIDArray, CustIDIndArray, NameArray, NameLenOrIndArray,  
                     AddressArray, AddressLenOrIndArray, PhoneArray,  
                     PhoneLenOrIndArray, RowStatusArray);  
         break;  
  
      case POSITIONED_UPDATE:  
         // Get the new data and place it in the rowset buffers.  
         GetNewData(AddressArray[RowNum - 1], &AddressLenOrIndArray[RowNum - 1],  
                     PhoneArray[RowNum - 1], &PhoneLenOrIndArray[RowNum - 1]);  
  
         // Bind the elements of the arrays at position RowNum-1 to the   
         // parameters of the positioned update statement.  
         SQLBindParameter(hstmtUpdate, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                           50, 0, AddressArray[RowNum - 1], sizeof(AddressArray[0]),  
                           &AddressLenOrIndArray[RowNum - 1]);  
         SQLBindParameter(hstmtUpdate, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                           10, 0, PhoneArray[RowNum - 1], sizeof(PhoneArray[0]),  
                           &PhoneLenOrIndArray[RowNum - 1]);  
  
         // Position the rowset cursor. The rowset is 1-based.  
         SQLSetPos(hstmtCust, RowNum, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
  
         // Execute the positioned update statement to update the row.  
         SQLExecute(hstmtUpdate);  
         break;  
  
      case POSITIONED_DELETE:  
         // Position the rowset cursor. The rowset is 1-based.  
         SQLSetPos(hstmtCust, RowNum, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
  
         // Execute the positioned delete statement to delete the row.  
         SQLExecute(hstmtDelete);  
         break;  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmtCust);  
```
