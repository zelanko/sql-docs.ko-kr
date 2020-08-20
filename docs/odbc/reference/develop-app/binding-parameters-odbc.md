---
description: 바인딩 매개 변수 ODBC
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9893d6611ad2bfc7107df1cd2d4ffe72dbf32fad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499956"
---
# <a name="binding-parameters-odbc"></a>바인딩 매개 변수 ODBC
문을 실행 하기 전에 SQL 문의 각 매개 변수를 응용 프로그램의 변수에 연결 하거나 *바인딩해야* 합니다. 응용 프로그램은 변수에 변수를 바인딩하는 경우 해당 변수 주소, C 데이터 형식 등을 드라이버에 설명 합니다. 또한 매개 변수 자체, 즉 SQL 데이터 형식, 전체 자릿수 등을 설명 합니다. 드라이버는 해당 문에 대해 유지 관리 되는 구조에이 정보를 저장 하 고 문을 실행할 때이 정보를 사용 하 여 변수에서 값을 검색 합니다.  
  
 문이 실행 되기 전에 언제 든 지 매개 변수를 바인딩하거나 바인딩할 수 있습니다. 문이 실행 된 후 매개 변수가 다시 바인딩되는 경우 문이 다시 실행 될 때까지 바인딩이 적용 되지 않습니다. 매개 변수를 다른 변수에 바인딩하려면 응용 프로그램은 단순히 매개 변수를 새 변수로 다시 바인딩합니다. 이전 바인딩이 자동으로 해제 됩니다.  
  
 변수는 SQL_RESET_PARAMS 옵션을 사용 하 여 **SQLFreeStmt** 를 호출 하거나 문이 해제 될 때까지 다른 변수가 매개 변수에 바인딩될 때까지 매개 변수에 바인딩되어 있습니다. 이러한 이유로 응용 프로그램은 바인딩 해제 될 때까지 변수가 해제 되지 않도록 해야 합니다. 자세한 내용은 [버퍼 할당 및 해제](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)를 참조 하세요.  
  
 매개 변수 바인딩은 문에 대해 드라이버에서 유지 관리 되는 구조에 저장 된 정보 이기 때문에 순서에 관계 없이 설정할 수 있습니다. 또한 실행 되는 SQL 문과는 독립적입니다. 예를 들어 응용 프로그램에서 세 개의 매개 변수를 바인딩한 후 다음 SQL 문을 실행 한다고 가정 합니다.  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 응용 프로그램에서 SQL 문을 즉시 실행 하는 경우  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 동일한 문 핸들에서 **INSERT** 문에 대 한 매개 변수 바인딩은 문 구조에 저장 되는 바인딩입니다. 대부분의 경우이는 잘못 된 프로그래밍 습관 이므로 피해 야 합니다. 대신 응용 프로그램은 SQL_RESET_PARAMS 옵션을 사용 하 여 **SQLFreeStmt** 를 호출 하 여 모든 이전 매개 변수의 바인딩을 해제 한 다음 새 매개 변수를 바인딩해야 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [바인딩 매개 변수 표식](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [이름으로 매개 변수 바인딩(명명된 매개 변수)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [매개 변수 바인딩 오프셋](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [매개 변수 설명](../../../odbc/reference/develop-app/describing-parameters.md)
