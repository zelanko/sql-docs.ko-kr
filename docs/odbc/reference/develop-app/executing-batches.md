---
title: 일괄 처리 실행 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], executing
- SQL statements [ODBC], batches
ms.assetid: f082c717-4f82-4820-a2fa-ba607d8fd872
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0ce0c043fcfad41a624ad129a757a047d2c87fb6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305734"
---
# <a name="executing-batches"></a>일괄 처리 실행
응용 프로그램이 문 일괄 처리를 실행하기 전에 먼저 지원되는지 확인해야 합니다. 이렇게 하려면 응용 프로그램은 SQL_BATCH_SUPPORT, SQL_PARAM_ARRAY_ROW_COUNTS 및 SQL_PARAM_ARRAY_SELECTS 옵션을 사용하여 **SQLGetInfo를** 호출합니다. 첫 번째 옵션은 행 개수 생성 및 결과 집합 생성 문이 명시적 일괄 처리 및 프로시저에서 지원되는지 여부를 반환하고, 후자의 두 옵션은 행 개수및 결과 집합의 가용성에 대한 정보를 매개 변수화된 실행으로 반환합니다.  
  
 명령문의 일괄 처리는 **SQLExecute** 또는 **SQLExecDirect**. 예를 들어 다음 호출은 새 판매 주문을 열기 위해 명시적 문 일괄 처리를 실행합니다.  
  
```  
SQLCHAR *BatchStmt =  
   "INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)"  
      "VALUES (2002, 1001, {fn CURDATE()}, 'Garcia', 'OPEN');"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 1, 1234, 10);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 2, 987, 8);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 3, 566, 17);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 4, 412, 500)";  
  
SQLExecDirect(hstmt, BatchStmt, SQL_NTS);  
```  
  
 결과 생성 문의 일괄 처리가 실행되면 하나 이상의 행 개 수 또는 결과 집합을 반환합니다. 이러한 검색 방법에 대한 자세한 내용은 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)를 참조하십시오.  
  
 문 일괄 처리에 매개 변수 마커가 포함된 경우 다른 명령문과 마찬가지로 매개 변수 순서가 증가합니다. 예를 들어, 다음 문 일괄 처리에는 매개 변수가 1부터 21까지 번호가 매겨져 있습니다. 첫 번째 **INSERT** 문에 는 1부터 5까지 번호가 매겨지고 마지막 **INSERT** 문에는 18에서 21까지 번호가 매겨져 있습니다.  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 매개 변수에 대한 자세한 내용은 이 섹션의 다음 부분의 [문 매개 변수를](../../../odbc/reference/develop-app/statement-parameters.md)참조하십시오.
