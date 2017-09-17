---
title: "SQL 예제를 포함 합니다. | Microsoft Docs"
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
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- embedded SQL [ODBC]
ms.assetid: b8a26e05-3c82-4c5f-8f01-9de0edb645e9
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e9f19c26cf77e0f5cfbff8a8ebad193ba9e9cdf2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="embedded-sql-example"></a>포함 된 SQL 예제
다음 코드는 간단한 포함 된 SQL 프로그램을 C 언어로 작성 된 프로그램은 아니지만 많은 중는 포함 된 SQL 기술을 보여 줍니다. 프로그램 주문 번호에 대 한 사용자 요청 하 고, 고객 번호, 영업 사원, 및는 주문 상태를 검색 하 고, 검색 된 정보 화면에 표시 합니다.  
  
```  
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
  
 이 프로그램에 대 한 다음 note:  
  
-   **호스트 변수** 호스트 변수가 포함 되는 섹션에서 선언 되었습니다는 **시작 선언 섹션** 및 **끝 선언 섹션** 키워드입니다. 포함 된 SQL 문에 표시 되 면 각 호스트 변수 이름은 콜론 (:)가 붙은 합니다. 콜론은 호스트 변수 및 테이블 및 열 같은 이름을 가진 같은 데이터베이스 개체를 구분 하려면 프리 수 있습니다.  
  
-   **데이터 형식** DBMS와 호스트 언어에서 지 원하는 데이터 형식 매우 다를 수 있습니다. 이중 역할을 수행 하기 때문에 호스트 변수를 영향을 줍니다. 한편으로 호스트 변수는 프로그램 변수를 선언 하 고 호스트 언어 문에 의해 조작. 반면에 데이터베이스 데이터를 검색 하려면 포함 된 SQL 문에서 사용 됩니다. DBMS 데이터 형식에 해당 하는 호스트 언어 유형이 경우 DBMS의 데이터를 자동으로 변환 합니다. 그러나 규칙 및 변환 프로세스와 관련 된 고유한 특징에는 각 DBMS에 있으므로 호스트 변수 형식은 선택 해야 신중 하 게 합니다.  
  
-   **오류 처리** The DBMS는 SQL 통신 영역 또는 SQLCA을 통해 응용 프로그램에 런타임에 오류를 보고 합니다. 위의 코드 예제에서는 첫 번째 포함 된 SQL 문이 포함 SQLCA 경우 프로그램에서 SQLCA 구조를 포함 하도록 프리를 인지를 나타냅니다. 프로그램은 DBMS에 의해 반환 되는 오류를 처리할 때마다 이것이 필요 합니다. WHENEVER 중... GOTO 문의 분기를 특정 레이블 때 오류가 발생 하는 오류 처리 코드를 생성 하려면 프리를 지시 합니다.  
  
-   **단일 선택** 데이터를 반환 하는 데 사용 하는 문을 단일 SELECT 문입니다; 즉, 데이터의 단일 행만을 반환 합니다. 따라서이 코드 예제에서는 선언 않거나 커서를 사용 합니다.
