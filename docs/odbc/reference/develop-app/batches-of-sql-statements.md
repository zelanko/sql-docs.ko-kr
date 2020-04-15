---
title: SQL 문 일괄 처리 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC]
- SQL statements [ODBC], batches
- batches [ODBC], about batches
ms.assetid: 766488cc-450c-434c-9c88-467f6c57e17c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d68ea1c13655ca7c57ba076823f461a4b2e22055
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283513"
---
# <a name="batches-of-sql-statements"></a>SQL 문의 일괄 처리
SQL 문 일괄 처리는 둘 이상의 SQL 문 또는 두 개 이상의 SQL 문 그룹과 동일한 영향을 주는 단일 SQL 문의 그룹입니다. 일부 구현에서는 결과를 사용할 수 있기 전에 전체 일괄 처리 문이 실행됩니다. 네트워크 트래픽을 줄일 수 있고 데이터 원본이 SQL 문 일괄 처리를 최적화할 수 있기 때문에 문을 별도로 제출하는 것보다 더 효율적인 경우가 많습니다. 다른 구현에서는 **SQLMoreResults호출이** 일괄 처리에서 다음 문의 실행을 트리거합니다. ODBC는 다음과 같은 유형의 일괄 처리를 지원합니다.  
  
-   **명시적 일괄 처리** *명시적 일괄 처리는* 세미콜론(;)으로 구분된 두 개 이상의 SQL 문입니다. 예를 들어 다음 SQL 문 일괄 처리는 새 판매 주문을 엽니다. 이렇게 하려면 주문 테이블과 행 테이블에 행을 삽입해야 합니다. 마지막 문 이후에 세미콜론이 없습니다.  
  
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
  
-   **수속 절차** 프로시저가 두 개 이상의 SQL 문을 포함하는 경우 SQL 문의 일괄 처리로 간주됩니다. 예를 들어 다음 SQL Server 관련 문은 고객에 대한 정보가 포함된 결과 집합과 해당 고객에 대한 모든 열린 판매 주문을 나열하는 결과 집합을 반환하는 프로시저를 만듭니다.  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     **CREATE 프로시저** 문 자체는 SQL 문의 일괄 처리가 아닙니다. 그러나 만드는 절차는 SQL 문의 일괄 처리입니다. **CREATE 프로시저** 문은 SQL Server에만 해당되며 SQL Server는 **CREATE 프로시저** 문에서 여러 문을 구분하기 위해 세미콜론이 필요하지 않기 때문에 두 **SELECT** 문을 분리하는 세미콜론은 없습니다.  
  
-   **매개 변수 배열** 매개 변수 배열은 대량 작업을 수행하는 효과적인 방법으로 매개 변수화된 SQL 문과 함께 사용할 수 있습니다. 예를 들어 다음 **INSERT** 문과 함께 매개 변수 배열을 사용하여 단일 SQL 문만 실행하는 동안 Lines 테이블에 여러 행을 삽입할 수 있습니다.  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     데이터 원본이 매개 변수 배열을 지원하지 않는 경우 드라이버는 각 매개 변수 집합에 대해 SQL 문을 한 번 실행하여 매개 변수를 에뮬레이트할 수 있습니다. 자세한 내용은 이 섹션의 다음 부분의 [매개 변수](../../../odbc/reference/develop-app/statement-parameters.md) 및 매개 [변수 값 배열을](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)참조하십시오.  
  
 서로 다른 유형의 일괄 처리는 상호 운용 가능한 방식으로 혼합할 수 없습니다. 즉, 응용 프로그램이 프로시저 호출을 포함하는 명시적 일괄 처리, 매개 변수 배열을 사용하는 명시적 일괄 처리 및 매개 변수 배열을 사용하는 프로시저 호출이 드라이버에 따라 달라지는 결과를 결정하는 방법입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [결과 생성 및 결과 없는 명령문](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [일괄 처리 실행](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [오류 및 일괄 처리](../../../odbc/reference/develop-app/errors-and-batches.md)
