---
title: 위치 경로 지정 (SQLXML)
description: SQLXML 4.0 XPath 쿼리에서 위치 경로를 지정 하 여 컨텍스트 노드에 상대적인 노드 집합을 선택 하 고 노드 집합을 생성 하는 방법에 대해 알아봅니다.
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
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9dedf4df4aa43f79ca4146da6f1183b0ee06286b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97431348"
---
# <a name="specifying-a-location-path-sqlxml-40"></a>위치 경로 지정(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  XPath 쿼리는 식 형식으로 지정합니다. 식에는 다양한 종류가 있습니다. 위치 경로는 컨텍스트 노드에 상대적인 노드 집합을 선택하는 식이고 위치 경로에 대한 평가 결과는 노드 집합입니다.  
  
## <a name="types-of-location-paths"></a>위치 경로 유형  
 위치 경로는 다음 중 한 가지 형식으로 지정할 수 있습니다.  
  
-   **절대 위치 경로**  
  
     절대 위치 경로는 문서의 루트 노드에서 시작되고 슬래시 표시(/)와 그 뒤에 상대 위치 경로(옵션)로 구성됩니다. 슬래시 표시(/)는 문서의 루트 노드를 선택합니다.  
  
-   **상대 위치 경로**  
  
     상대 위치 경로는 문서의 컨텍스트 노드에서 시작되고 슬래시 표시(/)로 구분된 하나 이상의 위치 단계의 시퀀스로 구성됩니다. 각 단계는 컨텍스트 노드에 상대적인 노드 집합을 선택합니다. 초기 단계 시퀀스는 컨텍스트 노드에 상대적인 노드 집합을 선택합니다. 이 집합의 각 노드는 다음 단계에 대한 컨텍스트 노드로 사용됩니다. 해당 단계로 식별되는 노드 집합은 서로 조인되어 있습니다. 예를 들어 **child:: Order/child:: OrderDetail** 은 **\<OrderDetail>** **\<Order>** 컨텍스트 노드의 요소 자식의 요소 자식을 선택 합니다.  
  
    > [!NOTE]  
    >  SQLXML 4.0의 XPath 구현에서는 명시적으로 절대 XPath가 아닌 XPath까지 포함하여 모든 XPath 쿼리가 루트 컨텍스트에서 시작됩니다. 예를 들어 "Customer"로 시작하는 XPath 쿼리는 "/Customer"로 처리됩니다. XPath query **customer [Order]** 에서 고객은 루트 컨텍스트에서 시작 하지만 Order는 고객 컨텍스트에서 시작 됩니다. 자세한 내용은 [&#40;는 XPath 쿼리 사용 소개 SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/introduction-to-using-xpath-queries-sqlxml-4-0.md)를 참조 하세요.  
  
## <a name="location-steps"></a>위치 단계  
 위치 경로(절대 또는 상대)는 다음의 세 부분을 포함하는 위치 단계로 구성됩니다.  
  
-   **축**  
  
     축은 위치 단계에서 선택되는 노드와 컨텍스트 노드 간의 트리 관계를 지정합니다. **부모**, **자식**, **특성** 및 **자체** 축이 지원 됩니다. 위치 경로에 **자식** 축이 지정 된 경우 쿼리에서 선택한 모든 노드가 컨텍스트 노드의 자식 노드가 됩니다. **부모** 축이 지정 된 경우 선택 된 노드는 컨텍스트 노드의 부모 노드입니다. **특성** 축이 지정 된 경우 선택 된 노드는 컨텍스트 노드의 특성입니다.  
  
-   **노드 테스트**  
  
     노드 테스트는 위치 단계에서 선택되는 노드 유형을 지정합니다. 모든 축 (**자식**, **부모**, **특성** 및 **자체**)에는 주 노드 유형이 있습니다. **특성** 축의 경우 주 노드 형식은 **\<attribute>** 입니다. **부모**, **자식** 및 **자체** 축의 경우 주 노드 형식은 **\<element>** 입니다.  
  
     예를 들어 위치 경로가 **child:: Customer** 를 지정 하는 경우 **\<Customer>** 컨텍스트 노드의 자식 요소가 선택 됩니다. **자식** 축은 **\<element>** 주 노드 유형 이므로 customer가 노드인 경우 노드 테스트는 TRUE입니다 **\<element>** .  
  
-   **선택 조건자(0개 이상)**  
  
     조건자는 축을 기준으로 노드 집합을 필터링합니다. XPath 식에서 선택 조건자를 지정하는 것은 SELECT 문에서 WHERE 절을 지정하는 것과 비슷합니다. 조건자는 대괄호로 묶어서 지정합니다. 선택 조건자에 지정된 테스트를 적용하면 노드 테스트에서 반환되는 노드가 필터링됩니다. 노드 집합의 각 노드를 필터링하기 위해 해당 노드가 컨텍스트 노드로 사용되고 노드 집합의 노드 수가 컨텍스트 크기로 사용되어 조건자 식이 평가됩니다. 노드에 대한 조건자 식이 TRUE로 평가되면 해당 노드가 결과 노드 집합에 포함됩니다.  
  
     위치 단계의 구문은 두 개의 콜론(::)으로 구분된 축 이름과 노드 테스트, 그리고 각각 대괄호로 묶인 0개 이상의 식으로 구성됩니다. 예를 들어 XPath 식 (위치 경로) **child:: Customer [ @CustomerID = ' ALFKI ']** 는 **\<Customer>** 컨텍스트 노드의 모든 요소 자식을 선택 합니다. 그런 다음 조건자의 테스트가 **\<Customer>** 해당 **CustomerID** 특성에 대해 특성 값이 ' ALFKI ' 인 요소 노드만 반환 하는 노드 집합에 적용 됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [&#40;SQLXML 4.0&#41;축을 지정 합니다. ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-an-axis-sqlxml-4-0.md)  
 축을 지정하는 예를 제공합니다.  
  
 [위치 경로에 노드 테스트 지정 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-a-node-test-in-the-location-path-sqlxml-4-0.md)  
 노드 테스트를 지정하는 예를 제공합니다.  
  
 [위치 경로에서 선택 조건자 지정 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-selection-predicates-in-the-location-path-sqlxml-4-0.md)  
 선택 조건자를 지정하는 예를 제공합니다.  
  
  
