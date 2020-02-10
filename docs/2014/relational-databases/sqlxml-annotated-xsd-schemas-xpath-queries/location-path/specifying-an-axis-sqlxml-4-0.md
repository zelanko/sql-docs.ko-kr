---
title: 축 지정 (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 8da239fd8a6bbf559f89ba5fd1b0fa0ab10ec190
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66012646"
---
# <a name="specifying-an-axis-sqlxml-40"></a>축 지정(SQLXML 4.0)
    
-   축은 위치 단계에서 선택되는 노드와 컨텍스트 노드 간의 트리 관계를 지정합니다. 다음 축이 지원 됩니다.`child`  
  
     컨텍스트 노드의 자식을 포함합니다.  
  
     다음 XPath 식 (위치 경로)은 현재 컨텍스트 노드에서 모든 ** \<고객>** 자식을 선택 합니다.  
  
    ```  
    child::Customer  
    ```  
  
     다음 XPath 쿼리에서`child`는 축이고 
  `Customer`는 노드 테스트입니다.  
  
-   `parent`  
  
     컨텍스트 노드의 부모를 포함합니다.  
  
     다음 XPath 식은 ** \<Order>** 자식의 모든 ** \<고객>** 부모를 선택 합니다.  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     이것은 `child::Customer`를 지정하는 것과 같습니다. 이 XPath 쿼리에서 `child`와 `parent`는 축이고 
  `Customer`와 `Order`는 노드 테스트입니다.  
  
-   `attribute`  
  
     컨텍스트 노드의 특성을 포함합니다.  
  
     다음 XPath 식은 컨텍스트 노드의 **CustomerID** 특성을 선택 합니다.  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   `self`  
  
     컨텍스트 노드 자신을 포함합니다.  
  
     다음 XPath 식은 ** \<Order>** 노드인 경우 현재 노드를 선택 합니다.  
  
    ```  
    self::Order  
    ```  
  
     이 XPath 쿼리에서 `self`는 축이고 `Order`는 노드 테스트입니다.  
  
  
