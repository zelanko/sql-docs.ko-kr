---
title: 위치 경로 (SQLXML 4.0)를 지정 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- absolute location path
- node-set [SQLXML]
- XPath queries [SQLXML], location paths
- relative location path [SQLXML]
- location path for XPath query
ms.assetid: a23a2b75-bc69-49f0-99db-05e14dc15bc0
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e4de99ac84f9c961a75d59c2951c61bdc6256642
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47681271"
---
# <a name="specifying-a-location-path-sqlxml-40"></a>위치 경로 지정(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XPath 쿼리는 식 형식으로 지정합니다. 식에는 다양한 종류가 있습니다. 위치 경로는 컨텍스트 노드에 상대적인 노드 집합을 선택하는 식이고 위치 경로에 대한 평가 결과는 노드 집합입니다.  
  
## <a name="types-of-location-paths"></a>위치 경로 유형  
 위치 경로는 다음 중 한 가지 형식으로 지정할 수 있습니다.  
  
-   **절대 위치 경로**  
  
     절대 위치 경로는 문서의 루트 노드에서 시작되고 슬래시 표시(/)와 그 뒤에 상대 위치 경로(옵션)로 구성됩니다. 슬래시 표시(/)는 문서의 루트 노드를 선택합니다.  
  
-   **상대 위치 경로**  
  
     상대 위치 경로는 문서의 컨텍스트 노드에서 시작되고 슬래시 표시(/)로 구분된 하나 이상의 위치 단계의 시퀀스로 구성됩니다. 각 단계는 컨텍스트 노드에 상대적인 노드 집합을 선택합니다. 초기 단계 시퀀스는 컨텍스트 노드에 상대적인 노드 집합을 선택합니다. 이 집합의 각 노드는 다음 단계에 대한 컨텍스트 노드로 사용됩니다. 해당 단계로 식별되는 노드 집합은 서로 조인되어 있습니다. 예를 들어 **child:: order/child::OrderDetail** 를 선택 합니다  **\<OrderDetail >** 요소 자식을  **\<순서 >** 요소 컨텍스트 노드의 자식입니다.  
  
    > [!NOTE]  
    >  SQLXML 4.0의 XPath 구현에서는 명시적으로 절대 XPath가 아닌 XPath까지 포함하여 모든 XPath 쿼리가 루트 컨텍스트에서 시작됩니다. 예를 들어 "Customer"로 시작하는 XPath 쿼리는 "/Customer"로 처리됩니다. XPath 쿼리에서 **Customer [Order]** Customer는 루트 컨텍스트에서 시작 되지만 Order는 Customer 컨텍스트에서 시작 합니다. 자세한 내용은 [XPath 쿼리 사용 소개 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/introduction-to-using-xpath-queries-sqlxml-4-0.md)합니다.  
  
## <a name="location-steps"></a>위치 단계  
 위치 경로(절대 또는 상대)는 다음의 세 부분을 포함하는 위치 단계로 구성됩니다.  
  
-   **Axis**  
  
     축은 위치 단계에서 선택되는 노드와 컨텍스트 노드 간의 트리 관계를 지정합니다. 합니다 **부모**를 **자식**를 **특성**, 및 **자체** 축이 지원 됩니다. 경우는 **자식** 축 위치 경로에 지정 된 컨텍스트 노드의 자식인 쿼리에서 선택한 모든 노드. 경우는 **부모** 축을 지정 하면 선택 되는 노드가 컨텍스트 노드의 부모 노드. 경우는 **특성** 축을 지정 하면 선택 되는 노드가 컨텍스트 노드의 특성입니다.  
  
-   **노드 테스트**  
  
     노드 테스트는 위치 단계에서 선택되는 노드 유형을 지정합니다. 모든 축 (**자식**를 **부모**를 **특성**, 및 **자체**) 주 노드 형식이 있습니다. 에 대 한 합니다 **특성** 축의 주 노드 유형은입니다  **\<특성 >** 합니다. 에 대 한 합니다 **부모**, **자식**, 및 **셀프** 축 주 노드 유형은입니다  **\<요소 >** 합니다.  
  
     예를 들어 위치 경로 지정 하는 경우 **child::Customer**서  **\<고객 >** 컨텍스트 노드의 요소 자식이 선택 됩니다. 때문에 합니다 **자식** 축은  **\<요소 >** 해당 주 노드 형식으로 노드 테스트 Customer는 TRUE 고객은는  **\<요소 >** 노드.  
  
-   **선택 조건자 (0 개 이상)**  
  
     조건자는 축을 기준으로 노드 집합을 필터링합니다. XPath 식에서 선택 조건자를 지정하는 것은 SELECT 문에서 WHERE 절을 지정하는 것과 비슷합니다. 조건자는 대괄호로 묶어서 지정합니다. 선택 조건자에 지정된 테스트를 적용하면 노드 테스트에서 반환되는 노드가 필터링됩니다. 노드 집합의 각 노드를 필터링하기 위해 해당 노드가 컨텍스트 노드로 사용되고 노드 집합의 노드 수가 컨텍스트 크기로 사용되어 조건자 식이 평가됩니다. 노드에 대한 조건자 식이 TRUE로 평가되면 해당 노드가 결과 노드 집합에 포함됩니다.  
  
     위치 단계의 구문은 두 개의 콜론(::)으로 구분된 축 이름과 노드 테스트, 그리고 각각 대괄호로 묶인 0개 이상의 식으로 구성됩니다. 예를 들어, XPath 식 (위치 경로) **child::Customer [@CustomerID= 'ALFKI']** 모두 선택 합니다  **\<고객 >** 컨텍스트 노드의 요소 자식을 합니다. 조건자의 테스트가 노드 집합에만 반환 하는에 적용 됩니다는  **\<고객 >** 특성을 사용 하 여 요소 노드 값 'ALFKI' 해당 **CustomerID** 특성입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [축 지정 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-an-axis-sqlxml-4-0.md)  
 축을 지정하는 예를 제공합니다.  
  
 [위치 경로에서 노드 테스트 지정 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-a-node-test-in-the-location-path-sqlxml-4-0.md)  
 노드 테스트를 지정하는 예를 제공합니다.  
  
 [위치 경로에서 선택 조건자 지정 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-selection-predicates-in-the-location-path-sqlxml-4-0.md)  
 선택 조건자를 지정하는 예를 제공합니다.  
  
  
