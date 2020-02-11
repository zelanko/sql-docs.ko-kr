---
title: 일괄 처리 실행 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 84d3cf65284d767d437987c8ff2b21793466106e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67901265"
---
# <a name="executing-batches"></a>일괄 처리 실행
응용 프로그램은 문 일괄 처리를 실행 하기 전에 먼저 지원 되는지 여부를 확인 해야 합니다. 이렇게 하기 위해 응용 프로그램은 SQL_BATCH_SUPPORT, SQL_PARAM_ARRAY_ROW_COUNTS 및 SQL_PARAM_ARRAY_SELECTS 옵션으로 **SQLGetInfo** 를 호출 합니다. 첫 번째 옵션은 행 개수 생성 및 결과 집합 생성 문이 명시적 일괄 처리 및 프로시저에서 지원 되는지 여부를 반환 하는 반면 후자 두 옵션은 매개 변수가 있는 행 개수와 결과 집합의 가용성에 대 한 정보를 반환 합니다. 문제점.  
  
 문의 일괄 처리는 **Sqlexecute** 또는 **sqlexecdirect**를 통해 실행 됩니다. 예를 들어 다음 호출은 문의 명시적 일괄 처리를 실행 하 여 새 판매 주문을 엽니다.  
  
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
  
 결과 생성 문의 일괄 처리를 실행 하는 경우 하나 이상의 행 개수 또는 결과 집합을 반환 합니다. 이러한 항목을 검색 하는 방법에 대 한 자세한 내용은 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)를 참조 하세요.  
  
 문 일괄 처리에 매개 변수 표식이 포함 된 경우이는 다른 문에서와 같이 매개 변수 순서를 늘려서 번호가 매겨집니다. 예를 들어 다음 문의 일괄 처리에는 1에서 21 사이의 숫자가 지정 된 매개 변수가 있습니다. 첫 번째 **insert** 문의 숫자는 1에서 5로, 마지막 **insert** 문의 숫자는 18 ~ 21입니다.  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 매개 변수에 대 한 자세한 내용은이 섹션의 뒷부분에 나오는 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)를 참조 하세요.
