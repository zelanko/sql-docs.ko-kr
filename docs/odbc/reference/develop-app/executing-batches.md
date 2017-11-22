---
title: "실행 중인 일괄 처리 | Microsoft Docs"
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
- batches [ODBC], executing
- SQL statements [ODBC], batches
ms.assetid: f082c717-4f82-4820-a2fa-ba607d8fd872
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0ca3a769ca983cae0cb7a2bc629c366b184b067e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="executing-batches"></a>실행 중인 일괄 처리
응용 프로그램이 실행 된 문의 일괄 처리 전에 지원 되는지 여부를 확인 먼저 해야 합니다. 이렇게 하려면 응용 프로그램 호출 **SQLGetInfo** SQL_BATCH_SUPPORT, SQL_PARAM_ARRAY_ROW_COUNTS, 및 SQL_PARAM_ARRAY_SELECTS 옵션을 사용 합니다. 첫 번째 옵션 행 개수 – 생성 하 고 결과 집합 – 생성 문은 명시적 일괄 처리 및 후자 두 옵션에 설정 하는 행 개수 및 결과의 가용성에 대 한 정보를 반환 하는 동안 프로시저에 지원 매개 변수화 여부를 반환 합니다. 실행 합니다.  
  
 문의 일괄 처리를 통해 실행 **SQLExecute** 또는 **SQLExecDirect**합니다. 예를 들어 다음 호출은 새 판매 주문을 열려는 문의 명시적 일괄 처리를 실행 합니다.  
  
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
  
 일괄 처리 결과 생성할 때 문이 실행 됩니다, 하나를 반환 하거나 더 많은 행 개수 또는 결과 설정입니다. 이러한 검색 하는 방법에 대 한 정보를 참조 하십시오. [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)합니다.  
  
 일괄 처리 문의 매개 변수 표식이 있으면 여기에 다른 문을에 있는 것 처럼 매개 변수를 오름차순으로 번호가 지정 됩니다. 예를 들어 다음 일괄 처리 문 중에 1-21;에서 번호가 매겨진 매개 변수 첫 번째에 **삽입** 사용 약관은 번호가 매겨진된 1 ~ 5 요소와 마지막 **삽입** 사용 약관은 번호가 매겨진된 18-21입니다.  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 매개 변수에 대 한 자세한 내용은 참조 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)이 섹션의 뒷부분에 나오는 합니다.
