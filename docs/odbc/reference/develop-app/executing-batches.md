---
title: 실행 중인 일괄 처리 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 46b224e8167587c4e4860f171b132d23539143e8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47695039"
---
# <a name="executing-batches"></a>일괄 처리 실행
응용 프로그램의 문 일괄 처리를 실행 하기 전에 지원 되는지 여부를 확인 먼저 해야 합니다. 이렇게 하려면 응용 프로그램 호출 **SQLGetInfo** SQL_BATCH_SUPPORT, SQL_PARAM_ARRAY_ROW_COUNTS, 및 SQL_PARAM_ARRAY_SELECTS 옵션을 사용 하 여 합니다. 첫 번째 옵션은 행 개수 – 생성 하 고 결과 집합 – 생성 문은 명시적 일괄 처리는 후자의 두 가지 옵션에 설정 하는 행 개수 및 결과의 가용성에 대 한 정보를 반환 하는 동안 프로시저에 지원 매개 변수화 여부를 반환 합니다. 실행 합니다.  
  
 문의 일괄 처리를 통해 실행 됩니다 **SQLExecute** 하거나 **SQLExecDirect**합니다. 예를 들어, 다음 호출의 새 판매 주문을 엽니다 문 명시적 일괄 처리를 실행 합니다.  
  
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
  
 일괄 처리 결과 생성 하는 경우 문이 실행 됩니다, 하나를 반환 하거나 더 많은 행 개수 또는 결과 설정입니다. 이러한 검색 하는 방법에 대 한 정보를 참조 하세요 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)합니다.  
  
 문 일괄 처리 매개 변수 표식에 이러한 다른 문이 있는 것 처럼 매개 변수를 오름차순으로 번호가 지정 됩니다. 예를 들어 다음 일괄 처리 문에 1 ~ 21;에서 번호가 매겨진 매개 변수 첫 번째 범위에서 해당 **삽입** 문에 번호가 매겨진된 1 ~ 5, 마지막에 다른 **삽입** 문에 21 통해 번호가 매겨진된 18입니다.  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 매개 변수에 대 한 자세한 내용은 참조 하십시오 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)이 섹션의 뒷부분에 나오는.
