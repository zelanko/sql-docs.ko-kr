---
title: 업데이트 및 Delete 문 배치 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3cf60ccc0e220850f7a83ed2c25db3795c1e7796
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47777745"
---
# <a name="positioned-update-and-delete-statements"></a>현재 위치 업데이트 및 Delete 문
응용 프로그램 업데이트 또는 현재 위치 업데이트를 사용 하 여 결과 집합의 현재 행을 삭제 하거나 delete 문 수 있습니다. 위치 지정 업데이트 및 삭제 문을 여 일부 데이터 원본의 경우에 지원 됩니다. 배치는 데이터 원본 지원 update 및 delete 문의 여부를 확인 하려면 응용 프로그램 호출 **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ 특성을 1 또는 SQL_STATIC_CURSOR_ATTRIBUTES1 *정보 항목* (커서 유형)에 따라 다름. 배치에서 ODBC 커서 라이브러리를 시뮬레이션 하는 참고 update 및 delete 문의 합니다.  
  
 응용 프로그램을 현재 위치 업데이트를 사용 하거나 delete 문의 결과 집합을 만들어야 합니다는 **업데이트에 대 한 선택** 문입니다. 이 문의 구문은 다음과 같습니다.  
  
 **SELECT** [**ALL** &#124; **DISTINCT**] *select-list*  
  
 **FROM** *table-reference-list*  
  
 [**WHERE** *search-condition*]  
  
 **업데이트에 대 한** [*열 이름* [**하십시오** *열 이름*]...]  
  
 그런 다음 응용 프로그램 업데이트 되거나 삭제 될 행에 커서를 놓습니다. 호출 하 여이 수행할 수 **SQLFetchScroll** 를 호출 하 고 필요한 행이 포함 된 행 집합을 검색할 **SQLSetPos** 해당 행의 행 집합 커서의 위치입니다. 그런 다음 응용 프로그램 결과 집합에서 사용 중인 문보다 다른 문에서 위치 지정된 update 또는 delete 문을 실행 합니다. 이러한 문의 구문은 다음과 같습니다.  
  
 **업데이트** *테이블 이름*  
  
 **설정할** *열 식별자* **=** {*식* &#124; **NULL**}  
  
 [**하십시오** *열 식별자* **=** {*식* &#124; **NULL**}]...  
  
 **WHERE CURRENT OF** *커서 이름*  
  
 **DELETE FROM** *테이블 이름* **WHERE CURRENT OF** *커서 이름*  
  
 이러한 문은 커서 이름이 필요는 알 수 있습니다. 응용 프로그램 하거나 지정할 수 있는 커서 이름의 **SQLSetCursorName** 설정 결과 만드는 문을 실행 하거나 자동으로 데이터 원본 수 전에 커서를 만들 때 커서 이름을 생성 합니다. 후자의 경우, 응용 프로그램 검색 위치 지정된 update 및 delete 문을 사용 하 여가 커서 이름을 호출 하 여 **SQLGetCursorName**합니다.  
  
 예를 들어, 다음 코드를 Customers 테이블을 스크롤할 및 고객 레코드를 삭제 하거나 해당 주소 및 전화 번호를 업데이트 할 수 있습니다. 호출한 **SQLSetCursorName** 하려면 고객의 결과 집합을 만들고 세 개의 문 핸들을 사용 하 여 커서 이름을 지정 합니다. *hstmtCust* 결과 집합에 대 한 *hstmtUpdate* 는 위치 지정된 update 문에 대 한 및 *hstmtDelete* 를 배치에 대 한 문을 삭제 합니다. 코드를 별도 변수 위치 지정된 update 문에 매개 변수를 바인딩할 수 있지만 행 집합 버퍼를 업데이트 하 고 이러한 버퍼의 요소를 바인딩합니다. 이 업데이트 된 데이터와 동기화 하는 행 집합 버퍼를 유지 합니다.  
  
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
