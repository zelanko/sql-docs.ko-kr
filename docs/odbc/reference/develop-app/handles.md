---
title: 처리 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- handles [ODBC]
- driver handles [ODBC]
- driver manager [ODBC], handles
- handles [ODBC], about handles
ms.assetid: f663101e-a4cc-402b-b9d7-84d5e975be71
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d31d36f315291d6826712771d0e3b6b1d8fbc496
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139036"
---
# <a name="handles"></a>핸들
핸들은 특정 항목을 식별 하는 불투명 한 32 비트 값 odbc에서이 항목에는 환경, 연결, 문 또는 설명자 수 있습니다. 응용 프로그램을 호출할 때 **SQLAllocHandle**, 드라이버 관리자 또는 드라이버 지정 된 형식의 새 항목을 만들고 응용 프로그램에 해당 핸들을 반환 합니다. 나중에 응용 프로그램 ODBC 함수를 호출할 때 해당 항목을 식별 하는 핸들을 사용 합니다. 드라이버 관리자와 드라이버 핸들을 사용 하 여 항목에 대 한 정보를 찾을 수 있습니다.  
  
 다음 코드에서는 두 가지 문 핸들을 사용 하는 예를 들어, (*hstmtOrder* 하 고 *hstmtLine*) 주문 및 판매 주문 줄 번호를 판매 결과 집합을 만드는 문을 식별 합니다. 나중에 데이터를 가져오기 위해는 결과 집합을 식별 하려면 이러한 핸들을 사용 합니다.  
  
```  
SQLHSTMT      hstmtOrder, hstmtLine; // Statement handles.  
SQLUINTEGER   OrderID;  
SQLINTEGER    OrderIDInd = 0;  
SQLRETURN     rc;  
  
// Prepare the statement that retrieves line number information.  
SQLPrepare(hstmtLine, "SELECT * FROM Lines WHERE OrderID = ?", SQL_NTS);  
  
// Bind OrderID to the parameter in the preceding statement.  
SQLBindParameter(hstmtLine, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
               &OrderID, 0, &OrderIDInd);  
  
// Bind the result sets for the Order table and the Lines table. Bind  
// OrderID to the OrderID column in the Orders table. When each row is  
// fetched, OrderID will contain the current order ID, which will then be  
// passed as a parameter to the statement tofetch line number  
// information. Code not shown.  
  
// Create a result set of sales orders.  
SQLExecDirect(hstmtOrder, "SELECT * FROM Orders", SQL_NTS);  
  
// Fetch and display the sales order data. Code to check if rc equals  
// SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmtOrder)) != SQL_NO_DATA) {  
   // Display the sales order data. Code not shown.  
  
   // Create a result set of line numbers for the current sales order.  
   SQLExecute(hstmtLine);  
  
   // Fetch and display the sales order line number data. Code to check  
   // if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
   while ((rc = SQLFetch(hstmtLine)) != SQL_NO_DATA) {  
      // Display the sales order line number data. Code not shown.  
   }  
  
   // Close the sales order line number result set.  
   SQLCloseCursor(hstmtLine);  
}  
  
// Close the sales order result set.  
SQLCloseCursor(hstmtOrder);  
```  
  
 핸들은 생성 하며 ODBC 구성 요소에만 의미가 즉, 드라이버 관리자만 드라이버 관리자 핸들을 해석할 수 및 드라이버에만 자체 핸들을 해석할 수 있습니다.  
  
 예를 들어 앞의 예제에서 드라이버 문에 대 한 정보를 저장 하는 구조를 할당 하 고이 구조로 문 핸들에 포인터를 반환 합니다. 응용 프로그램을 호출할 때 **SQLPrepare**SQL 문을 전달 하 고 판매 주문 줄 번호에 대 한 문의 핸들을 사용 합니다. 드라이버는 SQL 문을 준비 액세스 계획 식별자를 반환 하는 데이터 원본에 보냅니다. 드라이버에서이 식별자를 저장 하는 구조를 찾으려면 핸들을 사용 합니다.  
  
 나중에 응용 프로그램 호출 **SQLExecute** 줄 번호는 특정 판매 주문에 대 한 결과 집합을 생성 하려면 동일한 핸들을 전달 합니다. 드라이버 구조에서 액세스 계획 식별자를 검색 하는 핸들을 사용 합니다. 계획을 실행 하도록 지시 하려면 데이터 원본 식별자를 보냅니다.  
  
 ODBC에는 두 가지 수준의 핸들에 있습니다. 드라이버 관리자 핸들 및 드라이버입니다. 응용 프로그램 드라이버 관리자에서 해당 함수를 호출 하므로 ODBC 함수를 호출할 때 드라이버 관리자 핸들을 사용 합니다. 드라이버 관리자가이 핸들을 사용 하 여 해당 드라이버 핸들을 검색 하 고 드라이버에서 함수를 호출할 때 드라이버 핸들을 사용 합니다. 드라이버 및 드라이버 관리자 핸들 사용 하는 방법의 예제를 참조 하세요 [연결 프로세스에서 드라이버 관리자의 역할](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)입니다.  
  
 ODBC 아키텍처;에 대 한 아티팩트는 두 가지 수준의 처리는 대부분의 경우에는 응용 프로그램 또는 드라이버 관련이 없습니다. 가 일반적으로 작업을 수행 하지 않아도 이지만 응용 프로그램을 호출 하 여 드라이버 핸들 수를 확인할 수 **SQLGetInfo**합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [환경 핸들](../../../odbc/reference/develop-app/environment-handles.md)  
  
-   [연결 핸들](../../../odbc/reference/develop-app/connection-handles.md)  
  
-   [문 핸들](../../../odbc/reference/develop-app/statement-handles.md)  
  
-   [설명자 핸들](../../../odbc/reference/develop-app/descriptor-handles.md)  
  
-   [상태 전환](../../../odbc/reference/develop-app/state-transitions.md)
