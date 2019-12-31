---
title: 축 지정 (SQLXML)
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], axes
- XPath queries [SQLXML], location paths
- self axis
- attribute axis [SQLXML]
- axis [SQLXML]
- child axis
- parent axis
- location path for XPath query
- axes [SQLXML]
ms.assetid: 65631795-3389-40cf-90ea-85e9438956c5
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a219c2093832b979171584d5559da359b574552e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75253060"
---
# <a name="specifying-an-axis-sqlxml-40"></a>축 지정(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
    
-   축은 위치 단계에서 선택되는 노드와 컨텍스트 노드 간의 트리 관계를 지정합니다. 다음 축이 지원 됩니다. **자식**  
  
     컨텍스트 노드의 자식을 포함합니다.  
  
     다음 XPath 식 (위치 경로)은 현재 컨텍스트 노드에서 모든 ** \<고객>** 자식을 선택 합니다.  
  
    ```  
    child::Customer  
    ```  
  
     다음 XPath 쿼리에서`child`는 축이고 
  `Customer`는 노드 테스트입니다.  
  
-   **부모**  
  
     컨텍스트 노드의 부모를 포함합니다.  
  
     다음 XPath 식은 ** \<Order>** 자식의 모든 ** \<고객>** 부모를 선택 합니다.  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     이것은 `child::Customer`를 지정하는 것과 같습니다. 이 XPath 쿼리에서 `child`와 `parent`는 축이고 
  `Customer`와 `Order`는 노드 테스트입니다.  
  
-   **특성도**  
  
     컨텍스트 노드의 특성을 포함합니다.  
  
     다음 XPath 식은 컨텍스트 노드의 **CustomerID** 특성을 선택 합니다.  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   **자체**  
  
     컨텍스트 노드 자신을 포함합니다.  
  
     다음 XPath 식은 ** \<Order>** 노드인 경우 현재 노드를 선택 합니다.  
  
    ```  
    self::Order  
    ```  
  
     이 XPath 쿼리에서 `self`는 축이고 `Order`는 노드 테스트입니다.  
  
  
