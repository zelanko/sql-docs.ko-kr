---
title: 바인딩 매개 변수 ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binding parameters [ODBC]
ms.assetid: 7538a82b-b08b-4c8f-9809-e4ccea16db11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d62c0864678e116e30a0673bdf2625d70de0cedd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199602"
---
# <a name="binding-parameters-odbc"></a>바인딩 매개 변수 ODBC
SQL 문의 각 매개 변수에 연결 해야 합니다. 또는 *바인딩된* 문이 실행 되기 전에 응용 프로그램의 변수에 합니다. 응용 프로그램 변수에 매개 변수를 바인딩할 때 해당 변수를-주소, C 데이터 형식 등과-드라이버를 설명 합니다. 또한 매개 변수 자체 SQL 데이터 형식, 전체 자릿수 및 등을 설명합니다. 드라이버는 해당 문에 대 한 유지 관리 하 고 문이 실행 될 때 변수에서 값을 검색 하는 정보를 사용 하 여 구조에이 정보를 저장 합니다.  
  
 매개 변수는 바인딩된 또는 문 실행 전에 언제 든 지 다시 바인딩할 수 있습니다. 문이 실행 된 후 매개 변수는 차츰 회복 되면서 문을 다시 실행 될 때까지 바인딩이 적용 되지 않습니다. 매개 변수를 다른 변수에 바인딩할 응용 프로그램 다시 바인딩합니다; 새 변수를 사용 하 여 매개 변수를 이전 바인딩은 자동으로 해제 됩니다.  
  
 변수까지 매개 변수에 바인딩된 모든 매개 변수는 호출 하 여 바인딩 해제 될 때까지 다른 변수에 매개 변수를 바인딩할 **SQLFreeStmt** 문을 해제 될 때까지 또는 SQL_RESET_PARAMS 옵션을 사용 합니다. 이러한 이유로 응용 프로그램은 바인딩된 후 변수까지 해제 되지 않은 확인 해야 합니다. 자세한 내용은 [Allocating 및 버퍼 해제](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)합니다.  
  
 매개 변수 바인딩 정보만 문에 대해 드라이버에서 유지 관리 구조에 저장 되므로, 순서에 관계 없이 설정할 수 있습니다. 실행 되는 SQL 문의 독립 수도 있습니다. 예를 들어, 응용 프로그램 세 개의 매개 변수를 바인딩하고 다음 SQL 문을 실행 합니다.  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 그런 다음 응용 프로그램은 즉시 SQL 문을 실행 하는 경우  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 에 대 한 매개 변수 바인딩 동일한 문 핸들에 대해 합니다 **삽입** 문을 문의 구조에 저장 된 바인딩을 이기 때문에 사용 됩니다. 대부분의 경우에서 잘못 된 프로그래밍 방법 이며 하지 않아야 합니다. 응용 프로그램 대신 호출 해야 **SQLFreeStmt** 이전 모든 매개 변수를 바인딩 해제 하 고 새로 바인딩하고 SQL_RESET_PARAMS 옵션입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [바인딩 매개 변수 표식](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [이름으로 매개 변수 바인딩(명명된 매개 변수)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [매개 변수 바인딩 오프셋](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [매개 변수 설명](../../../odbc/reference/develop-app/describing-parameters.md)
