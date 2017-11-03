---
title: "Update 및 Delete 문을 배치 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: 0eafba50-02c7-46ca-a439-ef3307b935dc
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 45bb604f0226ac05eab0fd99bdbef41704cc8de8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="positioned-update-and-delete-statements"></a>위치 지정된 Update 및 Delete 문은
응용 프로그램 업데이트 또는 위치 지정된 업데이트 된 결과 집합의 현재 행을 삭제 또는 delete 문의 수 있습니다. 위치 update 및 delete 문이에서 일부 데이터 원본의 경우에 지원 됩니다. 데이터 원본에서 지 원하는 배치 update 및 delete 문 여부를 확인 하려면 응용 프로그램이 호출 **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ 특성을 1 또는 SQL_STATIC_CURSOR_ATTRIBUTES1 *정보 항목* (커서 유형)에 따라 다름. 배치에서 ODBC 커서 라이브러리를 시뮬레이션 하는 참고 update 및 delete 문입니다.  
  
 를 현재 위치 업데이트를 사용 하거나 delete 문 응용 프로그램 결과 집합을 만들어야는 **업데이트에 대 한 선택** 문. 이 문의 구문은 다음과 같습니다.  
  
 **선택** [**모든** &#124; **DISTINCT**] *선택 목록*  
  
 **보낸 사람** *테이블 참조 목록*  
  
 [**여기서** *검색 조건*]  
  
 **업데이트에 대 한** [*열 이름* [**,** *열 이름*]...]  
  
 그런 다음 응용 프로그램을 업데이트 하거나 삭제할 행에 커서를 놓습니다. 호출 하 여 이렇게 하려면 **SQLFetchScroll** 를 호출 하 고 필요한 행을 포함 하는 행 집합 검색 **SQLSetPos** 해당 행의 행 집합 커서의 위치를 합니다. 그런 다음 응용 프로그램에서 결과 집합에서 사용 하 고 문보다 다른 문이 위치 지정된 update 또는 delete 문이 실행 합니다. 이러한 문의 구문은 다음과 같습니다.  
  
 **업데이트** *테이블 이름*  
  
 **설정** *열 식별자*  **=**  {*식* &#124; **NULL**}  
  
 [**,** *열 식별자*  **=**  {*식* &#124; **NULL**}]...  
  
 **WHERE CURRENT OF** *커서 이름*  
  
 **DELETE FROM** *테이블 이름* **WHERE CURRENT OF** *커서 이름*  
  
 이러한 문은 커서 이름이 필요할 수 있는지를 확인 합니다. 응용 프로그램 수 지정 하거나 사용 하 여 커서 이름을 **SQLSetCursorName** 집합 결과 만드는 문을 실행 하거나 데이터 소스를 자동으로 할 수 전에 커서를 만들 때 커서 이름을 생성 합니다. 호출 하 여 응용 프로그램은 검색에서 위치 지정된 update 및 delete 문을 사용 하기 위해이 커서 이름을 후자의 경우 **SQLGetCursorName**합니다.  
  
 예를 들어 다음 코드에는 Customers 테이블을 스크롤할 및 고객 레코드를 삭제 하거나 해당 주소 및 전화 번호를 업데이트 하는 사용자 수 있습니다. 호출 **SQLSetCursorName** 하려면 고객의 결과 집합 만들고 세 개의 문 핸들을 사용 하 여 커서 이름을 지정: *hstmtCust* 결과 집합에 대 한 *hstmtUpdate* 위치 지정된 update 문에 대 한 및 *hstmtDelete* 는 위치 지정에 대 한 delete 문입니다. 코드는 별도 변수 위치 지정된 update 문의 매개 변수에 바인딩할 수 있지만 행 집합 버퍼를 업데이트 하 고이 버퍼의 요소를 바인딩합니다. 업데이트 된 데이터와 동기화 하는 행 집합 버퍼를 유지 합니다.  
  
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

