---
title: 바인딩 매개 변수 ODBC | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6e314bb9e3a1a979976a450e2a45a286ec54dfe7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306384"
---
# <a name="binding-parameters-odbc"></a>바인딩 매개 변수 ODBC
SQL 문의 각 매개 변수는 문이 실행되기 전에 응용 프로그램의 변수에 연결되거나 *바인딩되어야* 합니다. 응용 프로그램이 변수를 매개 변수에 바인딩할 때 해당 변수(주소, C 데이터 형식 등)를 드라이버에 설명합니다. 또한 매개 변수 자체(SQL 데이터 형식, 정밀도 등)에 대해서도 설명합니다. 드라이버는 이 정보를 해당 문에 대해 유지 관리하는 구조에 저장하고 이 정보를 사용하여 문이 실행될 때 변수에서 값을 검색합니다.  
  
 매개 변수는 문이 실행되기 전에 언제든지 바인딩되거나 리바운드될 수 있습니다. 문이 실행된 후 매개 변수가 리바운드되면 문이 다시 실행될 때까지 바인딩이 적용되지 않습니다. 매개 변수를 다른 변수에 바인딩하기 위해 응용 프로그램은 매개 변수를 새 변수로 바인딩하기만 하면 됩니다. 이전 바인딩이 자동으로 해제됩니다.  
  
 다른 변수가 매개 변수에 바인딩될 때까지, 모든 매개 변수가 SQL_RESET_PARAMS 옵션으로 **SQLFreeStmt를** 호출하거나 문이 해제될 때까지 매개 변수에 바인딩된 상태로 유지됩니다. 따라서 응용 프로그램은 변수가 언바운드될 때까지 해제되지 않았는지 확인해야 합니다. 자세한 내용은 [버퍼 할당 및 해제 를](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)참조하십시오.  
  
 매개 변수 바인딩은 명령문에 대해 드라이버가 유지 관리하는 구조에 저장된 정보일 뿐이므로 순서에 따라 설정할 수 있습니다. 또한 실행되는 SQL 문과독립적입니다. 예를 들어 응용 프로그램이 세 가지 매개 변수를 바인딩한 다음 다음 SQL 문을 실행한다고 가정합니다.  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 응용 프로그램이 SQL 문을 즉시 실행하는 경우  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 동일한 문 핸들에서 **INSERT** 문의 매개 변수 바인딩은 문 구조에 저장된 바인딩이기 때문에 사용됩니다. 대부분의 경우 이는 프로그래밍 관행이 좋지 않으며 피해야 합니다. 대신 응용 프로그램은 모든 이전 매개 변수를 바인딩 해제한 다음 새 매개 변수를 바인딩할 SQL_RESET_PARAMS 옵션으로 **SQLFreeStmt를** 호출해야 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [바인딩 매개 변수 표식](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [이름으로 매개 변수 바인딩(명명된 매개 변수)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [매개 변수 바인딩 오프셋](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [매개 변수 설명](../../../odbc/reference/develop-app/describing-parameters.md)
