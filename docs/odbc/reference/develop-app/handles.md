---
title: 핸들 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 713c2a71ec195b75d682b97239413e98d07b5861
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300213"
---
# <a name="handles"></a>핸들
핸들은 특정 항목을 식별하는 불투명한 32비트 값입니다. ODBC에서 이 항목은 환경, 연결, 명령문 또는 설명자일 수 있습니다. 응용 프로그램이 **SQLAllocHandle을**호출하면 드라이버 관리자 또는 드라이버는 지정된 형식의 새 항목을 만들고 해당 핸들을 응용 프로그램에 반환합니다. 응용 프로그램은 나중에 핸들을 사용하여 ODBC 함수를 호출할 때 해당 항목을 식별합니다. 드라이버 관리자와 드라이버는 핸들을 사용하여 항목에 대한 정보를 찾습니다.  
  
 예를 들어 다음 코드는 두 개의 문*핸들(hstmtOrder* 및 *hstmtLine)을*사용하여 판매 주문 및 판매 주문 줄 번호의 결과 집합을 만들 수 있는 문을 식별합니다. 나중에 이러한 핸들을 사용하여 데이터를 가져올 결과 집합을 식별합니다.  
  
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
  
 핸들은 이를 만든 ODBC 구성 요소에만 의미가 있습니다. 즉, 드라이버 관리자만 드라이버 관리자 핸들을 해석할 수 있으며 드라이버만 자체 핸들을 해석할 수 있습니다.  
  
 예를 들어 앞의 예제의 드라이버가 문에 대한 정보를 저장하는 구조를 할당하고 이 구조에 대한 포인터를 명령문 핸들로 반환한다고 가정합니다. 응용 프로그램에서 **SQLPrepare를**호출하면 SQL 문과 판매 주문 줄 번호에 사용되는 명령문의 핸들을 전달합니다. 드라이버는 SQL 문을 데이터 원본으로 보내어 이를 준비하고 액세스 계획 식별자를 반환합니다. 드라이버는 핸들을 사용하여 이 식별자를 저장할 구조를 찾습니다.  
  
 나중에 응용 프로그램에서 **SQLExecute를** 호출하여 특정 판매 주문에 대한 회선 번호의 결과 집합을 생성하면 동일한 핸들을 전달합니다. 드라이버는 핸들을 사용하여 구조에서 액세스 계획 식별자를 검색합니다. 데이터 원본에 식별자를 전송하여 실행할 계획을 알려줍니다.  
  
 ODBC에는 드라이버 관리자 핸들과 드라이버 핸들의 두 가지 수준의 핸들이 있습니다. 응용 프로그램은 드라이버 관리자에서 해당 함수를 호출하기 때문에 ODBC 함수를 호출할 때 드라이버 관리자 핸들을 사용합니다. 드라이버 관리자는 이 핸들을 사용하여 해당 드라이버 핸들을 찾고 드라이버에서 함수를 호출할 때 드라이버 핸들을 사용합니다. 드라이버 및 드라이버 관리자 핸들을 사용하는 방법의 예는 [연결 프로세스에서 드라이버 관리자의 역할을](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)참조하십시오.  
  
 두 가지 수준의 핸들이 있다는 것은 ODBC 아키텍처의 아티팩트입니다. 대부분의 경우 응용 프로그램이나 드라이버와 관련이 없습니다. 일반적으로 그렇게 할 이유가 없지만 응용 프로그램에서 **SQLGetInfo**를 호출하여 드라이버 핸들을 확인할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [환경 핸들](../../../odbc/reference/develop-app/environment-handles.md)  
  
-   [연결 핸들](../../../odbc/reference/develop-app/connection-handles.md)  
  
-   [명령문 핸들](../../../odbc/reference/develop-app/statement-handles.md)  
  
-   [설명자 핸들](../../../odbc/reference/develop-app/descriptor-handles.md)  
  
-   [상태 전환](../../../odbc/reference/develop-app/state-transitions.md)
