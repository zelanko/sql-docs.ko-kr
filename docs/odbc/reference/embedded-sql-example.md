---
title: Embedded SQL 예제 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eeab20c5385b02a874908cc941c1c69910efa228
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536668"
---
# <a name="embedded-sql-example"></a>Embedded SQL 예제
다음 코드는 간단한 embedded SQL 프로그램, C로 작성 된 프로그램에는 아니지만 많은 전부는 아님 포함 된 SQL 기술을 보여 줍니다. 프로그램 주문 번호에 대 한 라는 메시지를 고객 번호, 영업 사원, 및는 주문 상태를 검색 하며 화면에 검색된 된 정보를 표시 합니다.  
  
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
  
 이 프로그램에 대 한 다음 note:  
  
-   **호스트 변수** 묶어 섹션에서 선언 된 호스트 변수를 **선언 섹션 시작** 및 **최종 선언 섹션** 키워드. 에 포함 된 SQL 문을 표시 하는 경우 각 호스트 변수 이름에 콜론 (:) 접두사로 추가 됩니다. 콜론 프리를 호스트 변수 및 테이블과 동일한 이름을 가진 열 같은 데이터베이스 개체를 구별할 수 있습니다.  
  
-   **데이터 형식** DBMS 및 호스트 언어에서 지원 되는 데이터 형식 매우 다를 수 있습니다. 이러한 역할을 이중 때문에 호스트 변수를 영향을 줍니다. 한편으로 호스트 변수는 프로그램 변수를 선언 하 고 호스트 언어 문으로 조작. 반면에 데이터베이스 데이터를 검색에 포함 된 SQL 문에서 사용 됩니다. DBMS 데이터 형식에 해당 하는 호스트 언어 유형이 없는 경우 DBMS는 자동으로 데이터를 변환 합니다. 그러나 각 DBMS 자체 규칙 및 변환 프로세스에 연결 된 고유한 특징이 있으므로 호스트 변수 형식은 선택 해야 신중 하 게 합니다.  
  
-   **오류 처리** The DBMS SQL 통신 영역 또는 SQLCA를 통해 응용 프로그램에 런타임 오류를 보고 합니다. 앞의 코드 예제에 포함된 된 첫 번째 SQL 문을 포함 SQLCA 경우 프로그램에서 SQLCA 구조를 포함 하도록 다르거나를 인지를 나타냅니다. 이 프로그램 DBMS에 의해 반환 되는 오류를 처리할 때마다 수행 해야 합니다. WHENEVER... GOTO 문 시 특정 레이블로 분기 발생 하는 오류 처리 코드를 생성할 다르거나 알려 줍니다.  
  
-   **단일 선택** 문이 데이터를 반환 하는 데 사용 하는 단일 SELECT 문, 즉, 데이터의 단일 행만을 반환 합니다. 따라서 코드 예제에서는 않습니다 하지 선언 또는 커서를 사용 합니다.
