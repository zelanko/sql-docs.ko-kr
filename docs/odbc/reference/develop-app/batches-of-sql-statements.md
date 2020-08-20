---
description: SQL 문의 일괄 처리
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e342fd7eaef721f8fb0033a5ae022ca8de74cda1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465935"
---
# <a name="batches-of-sql-statements"></a>SQL 문의 일괄 처리
SQL 문 일괄 처리는 둘 이상의 sql 문 또는 두 개 이상의 SQL 문 그룹과 동일한 영향을 주는 단일 SQL 문 그룹입니다. 일부 구현에서는 전체 일괄 처리 문이 실행 되어 결과를 사용할 수 있습니다. 이는 일반적으로 네트워크 트래픽을 줄일 수 있고 데이터 원본에서 SQL 문 일괄 처리의 실행을 최적화할 수 있기 때문에 문을 개별적으로 전송 하는 것 보다 더 효율적입니다. 다른 구현에서 **SQLMoreResults** 를 호출 하면 일괄 처리에서 다음 문의 실행이 트리거됩니다. ODBC는 다음과 같은 유형의 일괄 처리를 지원 합니다.  
  
-   **명시적 일괄 처리** *명시적 일괄 처리* 는 세미콜론 (;)으로 구분 된 두 개 이상의 SQL 문입니다. 예를 들어 다음 SQL 문 일괄 처리는 새 판매 주문을 엽니다. 이렇게 하려면 Orders 테이블과 Lines 테이블 모두에 행을 삽입 해야 합니다. 마지막 문 뒤에 세미콜론이 없습니다.  
  
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
  
-   **프로시저** 프로시저에 SQL 문이 두 개 이상 포함 되어 있으면 SQL 문이 일괄 처리 된 것으로 간주 됩니다. 예를 들어 다음 SQL Server 문은 고객에 대 한 정보를 포함 하는 결과 집합을 반환 하는 프로시저와 해당 고객의 모든 오픈 판매 주문을 나열 하는 결과 집합을 만듭니다.  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     **CREATE PROCEDURE** 문은 SQL 문이 일괄 처리 되지 않습니다. 그러나 생성 되는 프로시저는 SQL 문을 일괄 처리 합니다. **CREATE procedure** 문은 SQL Server에만 적용 되 SQL Server 고 **create** procedure 문에서 여러 문을 구분 하기 위해 세미콜론을 요구 하지 않으므로 두 **SELECT** 문을 세미콜론으로 구분 하지 않습니다.  
  
-   **매개 변수 배열** 매개 변수가 있는 SQL 문에 매개 변수 배열을 사용 하 여 대량 작업을 효율적으로 수행할 수 있습니다. 예를 들어 다음 **INSERT** 문에 매개 변수 배열을 사용 하 여 단일 SQL 문만 실행 하면서 여러 행을 Lines 테이블에 삽입할 수 있습니다.  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     데이터 원본에서 매개 변수 배열을 지원 하지 않는 경우 드라이버는 각 매개 변수 집합에 대해 SQL 문을 한 번씩 실행 하 여이를 에뮬레이트할 수 있습니다. 자세한 내용은이 섹션의 뒷부분에 나오는 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md) 및 [매개 변수 값 배열](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)을 참조 하세요.  
  
 서로 다른 유형의 일괄 처리는 상호 운용 가능한 방식으로 혼합할 수 없습니다. 즉, 응용 프로그램에서 프로시저 호출을 포함 하는 명시적 일괄 처리를 실행 한 결과를 확인 하는 방법, 매개 변수 배열을 사용 하는 명시적 일괄 처리 및 매개 변수 배열을 사용 하는 프로시저 호출이 드라이버와 관련 된 것입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [결과 생성 및 결과 없는 명령문](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [일괄 처리 실행](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [오류 및 일괄 처리](../../../odbc/reference/develop-app/errors-and-batches.md)
