---
title: 위치 업데이트 및 삭제 명령문 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282364"
---
# <a name="positioned-update-and-delete-statements"></a>현재 위치 업데이트 및 Delete 문
응용 프로그램은 위치가 지정된 업데이트 또는 삭제 문으로 결과 집합에서 현재 행을 업데이트하거나 삭제할 수 있습니다. 위치 가있는 업데이트 및 삭제 문은 일부 데이터 원본에서 지원되지만 일부 데이터 원본에서는 지원되지만 모든 데이터 원본은 지원하지 않습니다. 데이터 원본이 위치 지정 업데이트 및 삭제 문을 지원하는지 여부를 확인하기 위해 응용 프로그램은 *InfoType* SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 또는 SQL_STATIC_CURSOR_ATTRIBUTES1 InfoType(커서의 유형에 따라 다름)을 사용하여 **SQLGetInfo를** 호출합니다. ODBC 커서 라이브러리는 위치 가 있는 업데이트 및 삭제 문을 시뮬레이션합니다.  
  
 위치 가 있는 업데이트 또는 delete 문을 사용하려면 응용 프로그램이 **UPDATE for UPDATE 에 대한 SELECT** 문을 사용하여 결과 집합을 만들어야 합니다. 이 명령문의 구문은 다음과 있습니다.  
  
 **[모두** **&#124; 별개]** *선택 목록* 선택**ALL**  
  
 **에서** *테이블 참조 목록*  
  
 [**어디** *검색 조건*]  
  
 [열*이름* **[,** *열 이름]의* **업데이트에 대 한...]**  
  
 그런 다음 응용 프로그램은 업데이트하거나 삭제할 행의 커서를 배치합니다. 필요한 행이 포함된 행 집합을 검색하기 위해 **SQLFetchScroll를** 호출하고 **SQLSetPos를** 호출하여 행 집합 커서를 해당 행에 배치하여 이 작업을 수행할 수 있습니다. 그런 다음 응용 프로그램은 결과 집합에서 사용 중인 명령문과 다른 문에서 위치 된 업데이트 또는 delete 문을 실행합니다. 이러한 명령문의 구문은 다음과 있습니다.  
  
 **테이블** *이름* 업데이트  
  
 **SET** *열 식별자* **=** {*NULL}* &#124; 식 **NULL**  
  
 ▲ **,** *열 식별자* **=** {*식* &#124; **NULL**}]...  
  
 **여기서** *커서 이름의* 현재  
  
 *커서* 이름의 **현재 테이블** *이름에서* **삭제**  
  
 이러한 문에는 커서 이름이 필요합니다. 응용 프로그램은 결과 집합을 만드는 문을 실행하기 전에 **SQLSetCursorName을** 사용하여 커서 이름을 지정하거나 커서가 생성될 때 데이터 원본이 커서 이름을 자동으로 생성하도록 할 수 있습니다. 후자의 경우 응용 프로그램은 위치 가 있는 업데이트에 사용할 이 커서 이름을 검색하고 **SQLGetCursorName**을 호출하여 문을 삭제합니다.  
  
 예를 들어 다음 코드를 통해 사용자는 고객 테이블을 스크롤하여 고객 레코드를 삭제하거나 주소와 전화 번호를 업데이트할 수 있습니다. **SQLSetCursorName을** 호출하여 고객의 결과 집합을 만들고 결과 집합에 대한 *hstmtCust,* 위치가 지정된 업데이트 문에 대한 *hstmtUpdate* 및 위치가 있는 삭제 문에 대한 *hstmtDelete의* 세 가지 문 핸들을 사용하기 전에 커서 이름을 지정합니다. 코드는 위치 가 있는 update 문의 매개 변수에 별도의 변수를 바인딩할 수 있지만 행 집합 버퍼를 업데이트하고 이러한 버퍼의 요소를 바인딩합니다. 이렇게 하면 업데이트된 데이터와 동기화된 행 집합 버퍼가 유지됩니다.  
  
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
