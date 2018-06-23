---
title: 축 (SQLXML 4.0)를 지정 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f3b9f58369cea876bc345300a945f85260b4326a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088134"
---
# <a name="specifying-an-axis-sqlxml-40"></a>축 지정(SQLXML 4.0)
    
-   축은 위치 단계에서 선택되는 노드와 컨텍스트 노드 간의 트리 관계를 지정합니다. 다음 축이 지원 됩니다.  `child`  
  
     컨텍스트 노드의 자식을 포함합니다.  
  
     다음 XPath 식 (위치 경로) 모든 현재 컨텍스트 노드에서 선택 된  **\<고객 >** 자식을:  
  
    ```  
    child::Customer  
    ```  
  
     다음 XPath 쿼리에서`child`는 축이고 `Customer`는 노드 테스트입니다.  
  
-   `parent`  
  
     컨텍스트 노드의 부모를 포함합니다.  
  
     다음 XPath 식은 모든 선택은  **\<고객 >** 의 부모는  **\<순서 >** 자식을:  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     이것은 `child::Customer`를 지정하는 것과 같습니다. 이 XPath 쿼리에서 `child`와 `parent`는 축이고 `Customer`와 `Order`는 노드 테스트입니다.  
  
-   `attribute`  
  
     컨텍스트 노드의 특성을 포함합니다.  
  
     다음 XPath 식은 선택은 **CustomerID** 컨텍스트 노드의 특성:  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   `self`  
  
     컨텍스트 노드 자신을 포함합니다.  
  
     이 경우 다음 XPath 식은 현재 노드를 선택는  **\<순서 >** 노드:  
  
    ```  
    self::Order  
    ```  
  
     이 XPath 쿼리에서 `self`는 축이고 `Order`는 노드 테스트입니다.  
  
  