---
description: Embedded SQL 예제
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fec0f3e3776b8ac70e85042c565343b35f8a893e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429065"
---
# <a name="embedded-sql-example"></a>Embedded SQL 예제
다음 코드는 C로 작성 된 간단한 임베디드 SQL 프로그램입니다. 이 프로그램은 포함 된 SQL 기술 중 일부를 보여 줍니다. 프로그램은 사용자에 게 주문 번호를 묻는 메시지를 표시 하 고, 고객 번호, 영업 사원 및 주문 상태를 검색 하 고, 검색 된 정보를 화면에 표시 합니다.  
  
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
  
 이 프로그램에 대 한 다음 사항에 유의 하세요.  
  
-   **호스트 변수** 호스트 변수는 **BEGIN DECLARE section** 및 **END declare section** 키워드를 포함 하는 섹션에서 선언 됩니다. 각 호스트 변수 이름 앞에 콜론 (:) 포함 된 SQL 문에 표시 되는 경우 콜론을 사용 하면 미리 컴파일된에서 호스트 변수와 동일한 이름을 가진 데이터베이스 개체 (예: 테이블 및 열)를 구분할 수 있습니다.  
  
-   **데이터 형식** DBMS 및 호스트 언어에서 지원 되는 데이터 형식은 매우 다를 수 있습니다. 이는 이중 역할을 하기 때문에 호스트 변수에 영향을 줍니다. 호스트 변수는 호스트 언어 문에 의해 선언 되 고 조작 되는 프로그램 변수입니다. 반면에 이러한 데이터베이스는 포함 된 SQL 문에서 데이터베이스 데이터를 검색 하는 데 사용 됩니다. DBMS 데이터 형식에 해당 하는 호스트 언어 형식이 없으면 DBMS에서 자동으로 데이터를 변환 합니다. 그러나 각 DBMS에는 변환 프로세스와 관련 된 자체 규칙 및 고유한 특징이 있으므로 호스트 변수 유형을 신중 하 게 선택 해야 합니다.  
  
-   **오류 처리** DBMS는 SQL 통신 영역 또는 SQLCA를 통해 응용 프로그램 프로그램에 런타임 오류를 보고 합니다. 위의 코드 예제에서 첫 번째 포함 된 SQL 문은 SQLCA를 포함 합니다. 그러면 미리 컴파일된에 게 프로그램에 SQLCA 구조가 포함 됩니다. 프로그램이 DBMS에서 반환 하는 오류를 처리할 때마다 필요 합니다. 언제 든 지 ... GOTO 문은 오류가 발생할 때 특정 레이블로 분기 되는 오류 처리 코드를 미리 컴파일된에 게 알립니다.  
  
-   **단일 항목 선택** 데이터를 반환 하는 데 사용 되는 문은 단일 SELECT 문입니다. 즉, 단일 데이터 행만 반환 합니다. 따라서 코드 예제는 커서를 선언 하거나 사용 하지 않습니다.
