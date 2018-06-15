---
title: 바인딩 매개 변수 ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- binding parameters [ODBC]
ms.assetid: 7538a82b-b08b-4c8f-9809-e4ccea16db11
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc39c8183c996dd4d011d9bcdaba6dfe1f94cc05
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909304"
---
# <a name="binding-parameters-odbc"></a>바인딩 매개 변수 ODBC
SQL 문의 각 매개 변수에 연결, 해야 또는 *바인딩되는 경우,* 문이 실행 되기 전에 응용 프로그램의 변수에 합니다. 해당 변수를 설명 응용 프로그램 변수에 매개 변수를 바인딩할 때-주소, C 데이터 형식 등에-driver. 매개 변수 자체에 대해서도 설명 — SQL 데이터 형식, 정밀도 및 등입니다. 드라이버는 해당 문에 대 한 유지 관리 하 고는 문이 실행 될 때 변수에서 값을 검색 하는 정보를 사용 하 여 구조에이 정보를 저장 합니다.  
  
 매개 변수는 연결 또는 문이 실행 되는 전에 언제 든 지 다시 바인딩할 수 있습니다. 매개 변수는 문을 실행 한 후 다시 바인딩 문을 다시 실행 될 때까지 바인딩이 적용 되지 않습니다. 매개 변수가 다른 변수에 바인딩할 응용 프로그램 다시 바인딩합니다 새 변수;의 매개 변수를 이전 바인딩은 자동으로 해제 됩니다.  
  
 모든 매개 변수는 호출 하 여 바인딩 해제 될 때까지 다른 변수는 매개 변수를 바인딩할 때까지 한 변수는 매개 변수에 바인딩된 **SQLFreeStmt** 문을 해제 될 때까지 또는 SQL_RESET_PARAMS 옵션을 사용 합니다. 이러한 이유로 응용 프로그램이 바인딩된 후 변수 될 때까지 해제 되지 않은 확인 해야 합니다. 자세한 내용은 참조 [Allocating 및 버퍼 해제](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)합니다.  
  
 매개 변수 바인딩이 문에 대 한 드라이버에 의해 보존 된 구조에 저장 된 정당한 정보 이기 때문에 어떤 순서로 든 설정할 수 있습니다. 독립적으로 실행 되는 SQL 문을 수도 있습니다. 예를 들어 응용 프로그램 세 개의 매개 변수를 바인딩하고 다음 SQL 문을 실행 합니다.  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 그런 다음 응용 프로그램에 즉시 SQL 문을 실행 하는 경우  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 동일한 문 핸들에 대 한 매개 변수 바인딩에서는 **삽입** 문은 바인딩을 문의 구조에 저장 되는 데 사용 합니다. 대부분의 경우에서 낮은 프로그래밍 관행 이며 피해 야 합니다. 대신, 응용 프로그램을 호출 해야 **SQLFreeStmt** 오래 된 모든 매개 변수 바인딩 해제 하 고 다음 새 캠페인을 바인딩할 SQL_RESET_PARAMS 옵션을 사용 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [바인딩 매개 변수 표식](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [이름으로 매개 변수 바인딩(명명된 매개 변수)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [매개 변수 바인딩 오프셋](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [매개 변수 설명](../../../odbc/reference/develop-app/describing-parameters.md)
