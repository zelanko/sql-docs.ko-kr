---
title: "SQL 문의 일괄 처리 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- batches [ODBC]
- SQL statements [ODBC], batches
- batches [ODBC], about batches
ms.assetid: 766488cc-450c-434c-9c88-467f6c57e17c
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7966552f130ce8ab4825c77929c5fd4599fd6209
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="batches-of-sql-statements"></a>SQL 문의 일괄 처리
SQL 문의 일괄 처리는 그룹 두 개 이상의 SQL 문 또는 두 개 이상의 SQL 문 그룹 것과 동일한 결과가 단일 SQL 문입니다. 일부 구현에서는 전체 일괄 처리 문은 사용할 수 있는 모든 결과가 전에 실행 됩니다. 이 대개 더 네트워크 트래픽이 감소 종종 수를 데이터 소스 SQL 문의 일괄 처리의 실행을 최적화 때로는 수 때문에 문을 개별적으로 전송 하는 보다 효율적입니다. 다른 구현에서는 호출 **SQLMoreResults** 일괄 처리의 다음 문으로 실행을 트리거합니다. ODBC는 다음과 같은 유형의 일괄 처리를 지원합니다.  
  
-   **명시적 일괄 처리** 는 *명시적 일괄 처리* 두 개 이상의 SQL 문을 세미콜론 (;)으로 구분 됩니다. 예를 들어 다음 일괄 처리의 SQL 문 새로운 판매 주문을 열립니다. 이렇게 하려면 주문과 줄 테이블에 행을 삽입 합니다. 참고 마지막 문 다음 없습니다 semicolon입니다.  
  
    ```  
    INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
       VALUES (2002, 1001, {fn CURDATE()}, 'Garcia', 'OPEN');  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 1, 1234, 10);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 2, 987, 8);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 3, 566, 17);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 4, 412, 500)  
    ```  
  
-   **프로시저** 둘 이상의 SQL 문을 포함 하는 프로시저를 SQL 문의 일괄 처리 되도록 간주 됩니다. 예를 들어 다음 SQL Server 관련 문은 고객과 결과 해당 고객에 대 한 열린 모든 판매 주문을 나열 하는 집합에 대 한 정보를 포함 한 결과 집합을 반환 하는 프로시저를 만듭니다.  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     **CREATE PROCEDURE** 자체 문은 일괄 처리 SQL 문의 아닙니다. 그러나 생성 하는 절차는 SQL 문의 일괄 처리 합니다. 세미콜론 두 **선택** 문 때문에 **CREATE PROCEDURE** 문을 특정 SQL Server에 적용 되며 SQL Server는 에서여러문을구분하려면세미콜론을사용하지않아도 **CREATE PROCEDURE** 문.  
  
-   **매개 변수 배열을** 대량 작업을 수행 하는 효과적인 방법으로 매개 변수가 있는 SQL 문을 사용 하 여 매개 변수 배열을 사용할 수 있습니다. 예를 들어 매개 변수 배열을 사용 하 여 다음 **삽입** 문을 단일 SQL 문만 실행 하는 동안 줄 테이블에 여러 행을 삽입할 수 있습니다.  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     데이터 원본에는 매개 변수 배열을 지원 하지 않으면, 드라이버에서 SQL 문을 각 매개 변수 집합에 대해 한 번 실행 하 여이 에뮬레이트할 수 있습니다. 자세한 내용은 참조 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md) 및 [매개 변수 값의 배열](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)이 섹션의 뒷부분에 나오는 합니다.  
  
 상호 운용 가능한 방식으로 다양 한 유형의 일괄 처리를 혼합할 수 없습니다. 즉, 호출 응용 프로그램에서 프로시저를 포함 하는 명시적 일괄 처리를 실행 한 결과 확인 하는 방법을 매개 변수 배열을 사용 하는 명시적 일괄 처리 하 여 프로시저 호출 매개 변수 배열을 사용 하는 드라이버에 따라 다릅니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [결과 생성 및 결과 없는 문](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [일괄 처리 실행](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [오류 및 일괄 처리](../../../odbc/reference/develop-app/errors-and-batches.md)
