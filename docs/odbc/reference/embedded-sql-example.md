---
title: 임베디드 SQL 예제 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- embedded SQL [ODBC]
ms.assetid: b8a26e05-3c82-4c5f-8f01-9de0edb645e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39ec504c423817c6a3e11bc954555b201b8b09c6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294174"
---
# <a name="embedded-sql-example"></a>Embedded SQL 예제
다음 코드는 C로 작성된 간단한 임베디드 SQL 프로그램입니다. 이 프로그램은 포함된 SQL 기술의 전부는 아니지만 많은 것을 보여 줍니다. 이 프로그램은 주문 번호를 사용자에게 묻고, 고객 번호, 판매원 및 주문 상태를 검색하고, 검색된 정보를 화면에 표시합니다.  
  
```cpp  
int main() {  
   EXEC SQL INCLUDE SQLCA;  
   EXEC SQL BEGIN DECLARE SECTION;  
      int OrderID;         /* Employee ID (from user)         */  
      int CustID;            /* Retrieved customer ID         */  
      char SalesPerson[10]   /* Retrieved salesperson name      */  
      char Status[6]         /* Retrieved order status        */  
   EXEC SQL END DECLARE SECTION;  
  
   /* Set up error processing */  
   EXEC SQL WHENEVER SQLERROR GOTO query_error;  
   EXEC SQL WHENEVER NOT FOUND GOTO bad_number;  
  
   /* Prompt the user for order number */  
   printf ("Enter order number: ");  
   scanf_s("%d", &OrderID);  
  
   /* Execute the SQL query */  
   EXEC SQL SELECT CustID, SalesPerson, Status  
      FROM Orders  
      WHERE OrderID = :OrderID  
      INTO :CustID, :SalesPerson, :Status;  
  
   /* Display the results */  
   printf ("Customer number:  %d\n", CustID);  
   printf ("Salesperson: %s\n", SalesPerson);  
   printf ("Status: %s\n", Status);  
   exit();  
  
query_error:  
   printf ("SQL error: %ld\n", sqlca->sqlcode);  
   exit();  
  
bad_number:  
   printf ("Invalid order number.\n");  
   exit();  
}  
```  
  
 이 프로그램에 대한 다음 사항  
  
-   **호스트 변수** 호스트 변수는 **시작 선언 섹션으로** 둘러싸인 섹션과 **선언 섹션 종료** 키워드로 둘러싸인 섹션에 선언됩니다. 각 호스트 변수 이름은 콜론(:) 포함된 SQL 문에 나타날 때 콜론을 사용하면 프리컴파일러가 동일한 이름을 가진 호스트 변수와 테이블 및 열과 같은 데이터베이스 개체를 구분할 수 있습니다.  
  
-   **데이터 유형** DBMS 및 호스트 언어에서 지원하는 데이터 형식은 매우 다를 수 있습니다. 이는 호스트 변수가 이중 역할을 하기 때문에 영향을 줍니다. 한편호스트 변수는 호스트 언어 문으로 선언되고 조작된 프로그램 변수입니다. 반면에 데이터베이스 데이터를 검색하기 위해 포함된 SQL 문에 사용됩니다. DBMS 데이터 형식에 해당하는 호스트 언어 유형이 없는 경우 DBMS는 자동으로 데이터를 변환합니다. 그러나 각 DBMS에는 변환 프로세스와 관련된 고유한 규칙과 특이성을 가지고 있으므로 호스트 변수 형식을 신중하게 선택해야 합니다.  
  
-   **오류 처리** DBMS는 SQL 통신 영역 또는 SQLCA를 통해 응용 프로그램 프로그램에 런타임 오류를 보고합니다. 앞의 코드 예제에서 첫 번째 포함된 SQL 문은 포함 SQLCA입니다. 이렇게 하면 사전 컴파일러가 프로그램에 SQLCA 구조를 포함하도록 지시합니다. 이는 프로그램이 DBMS에서 반환되는 오류를 처리할 때마다 필요합니다. 언제 든 지... GOTO 문은 사전 컴파일러에 오류가 발생할 때 특정 레이블로 분기하는 오류 처리 코드를 생성하도록 지시합니다.  
  
-   **싱글톤 셀렉팅** 데이터를 반환하는 데 사용되는 문은 singleton SELECT 문입니다. 즉, 단일 데이터 행만 반환합니다. 따라서 코드 예제에서는 커서를 선언하거나 사용하지 않습니다.
