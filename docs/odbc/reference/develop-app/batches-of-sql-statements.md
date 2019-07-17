---
title: SQL 문의 일괄 처리 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3f7264b17c13d6b66bf1be24da81e96a4ca3e8a8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122827"
---
# <a name="batches-of-sql-statements"></a>SQL 문의 일괄 처리
SQL 문의 일괄 처리는 그룹 두 개 이상의 SQL 문 또는 두 개 이상의 SQL 문 그룹으로 동일한 영향을 주지 않는 단일 SQL 문입니다. 일부 구현에서는 모든 결과 사용할 수 전에 전체 일괄 처리 문을 실행 됩니다. 이 대개 더 네트워크 트래픽을 줄일 종종 있습니다 이므로 데이터 원본 수 SQL 문의 일괄 처리의 실행을 최적화할 경우에 따라 문을 개별적으로 전송 하는 보다 효율적입니다. 다른 구현에서는 호출 **SQLMoreResults** 일괄 처리의 다음 문으로 실행을 트리거합니다. ODBC는 다음 유형의 일괄 처리를 지원합니다.  
  
-   **명시적 일괄 처리** 는 *명시적 일괄 처리* 두 개 이상의 SQL 문을 세미콜론 (;)으로 구분 됩니다. 예를 들어, 다음 SQL 문 일괄 처리에 새 판매 주문을 열립니다. 이 경우 주문 및 라인 모두 테이블에 행을 삽입 합니다. 마지막 문 다음에 없는 세미콜론은 참고 합니다.  
  
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
  
-   **프로시저** 프로시저 SQL 문을 여러 개 있으면 SQL 문의 일괄 처리 수으로 간주 됩니다. 예를 들어, 다음 SQL Server 관련 문은 고객과 해당 고객에 대 한 열린 모든 판매 주문을 나열 하는 설정 결과 대 한 정보를 포함 하는 집합 결과 반환 하는 프로시저를 만듭니다.  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     합니다 **CREATE PROCEDURE** 문이나 SQL 문의 일괄 처리 아닙니다. 그러나 만들면 절차는 SQL 문의 일괄 처리 합니다. 두 가지를 구분 하는 세미콜론 없음 **선택** 문 때문에 **CREATE PROCEDURE** 문을 SQL Server 관련 이며 SQL Server에는 여러문을세미콜론필요하지않습니다 **CREATE PROCEDURE** 문입니다.  
  
-   **매개 변수 배열** 매개 변수 배열 대량 작업을 수행 하는 효과적인 방법으로 매개 변수가 있는 SQL 문을 사용 하 여 사용할 수 있습니다. 예를 들어, 매개 변수 배열을 사용 하 여 다음 **삽입** 문을 단일 SQL 문만 실행 하는 동안 줄 테이블에 여러 행을 삽입 합니다.  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     데이터 소스 매개 변수 배열을 지원 하지 않으면, 드라이버 각 매개 변수 집합에 대해 한 번 SQL 문을 실행 하 여이 에뮬레이트할 수 있습니다. 자세한 내용은 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md) 하 고 [매개 변수 값의 배열](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)이 섹션의 뒷부분에 나오는.  
  
 상호 운용 가능한 방식으로 다양 한 유형의 일괄 처리를 혼합할 수 없습니다. 즉, 매개 변수 배열을 사용 하는 명시적 일괄 처리를 호출, 응용 프로그램에서 프로시저를 포함 하는 명시적 일괄 처리 실행의 결과 결정 하는 방법 이며 매개 변수 배열을 사용 하는 프로시저 호출에 드라이버별 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [결과 생성 및 결과 없는 문](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [일괄 처리 실행](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [오류 및 일괄 처리](../../../odbc/reference/develop-app/errors-and-batches.md)
