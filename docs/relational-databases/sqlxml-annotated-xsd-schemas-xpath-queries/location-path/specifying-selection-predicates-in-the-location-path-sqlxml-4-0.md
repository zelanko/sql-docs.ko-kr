---
title: 위치 경로에서 선택 조건자 설정 (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], predicates
- predicates [SQLXML]
- position-based filtering [SQLXML]
- XPath queries [SQLXML], location paths
- filtering [SQLXML]
- location path for XPath query
ms.assetid: dbef4cf4-a89b-4d7e-b72b-4062f7b29a80
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 84a3eade8a706e95b3ddba72d96e37d8fabf1fd3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75256003"
---
# <a name="specifying-selection-predicates-in-the-location-path-sqlxml-40"></a>위치 경로에서 선택 조건자 지정(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  조건자는 SELECT 문의 WHERE 절과 유사하게 축을 기준으로 노드 집합을 필터링합니다. 조건자는 대괄호로 묶어서 지정합니다. 노드 집합의 각 노드를 필터링하기 위해 해당 노드가 컨텍스트 노드로 사용되고 노드 집합의 노드 수가 컨텍스트 크기로 사용되어 조건자 식이 평가됩니다. 노드에 대한 조건자 식이 TRUE로 평가되면 해당 노드가 결과 노드 집합에 포함됩니다.  
  
 XPath에서도 위치 기반 필터링이 가능합니다. 숫자로 계산되는 조건자 식이 필요한 서수 노드를 선택합니다. 예를 들어 위치 경로 `Customer[3]`은 세 번째 고객을 반환하지만, 이와 같은 숫자 조건자는 지원되지 않고 부울 결과를 반환하는 조건자 식만 지원됩니다.  
  
> [!NOTE]  
>  Xpath의 xpath 구현에 대 한 제한 사항 및이를 W3C 사양 간의 차이점에 대 한 자세한 내용은 [&#40;Xpath 쿼리 사용 소개&#41;SQLXML 4.0 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/introduction-to-using-xpath-queries-sqlxml-4-0.md)을 참조 하세요.  
  
## <a name="selection-predicate-example-1"></a>선택 조건자: 예 1  
 다음 XPath 식 (위치 경로)은 현재 컨텍스트 노드에서 ALFKI 값이 인 **CustomerID** 특성이 있는 모든 ** \<Customer>** 요소 자식을 선택 합니다.  
  
```  
/child::Customer[attribute::CustomerID="ALFKI"]  
```  
  
 이 XPath 쿼리에서 `child` 및 `attribute`는 축 이름이고, `Customer``Customer` 는 노드 테스트 (는 요소가 `child` 축에 대 한 주 노드 유형 ** \<>** 이므로가 ** \<>요소 노드인 **경우 TRUE)입니다. 
  `attribute::CustomerID="ALFKI"`는 조건자입니다. `attribute` 조건자에서 `CustomerID` 는 축이 고는 노드 테스트 (특성 ** \<>** 는 **특성** 축의 주 노드 유형 이므로 **CustomerID** 가 컨텍스트 노드의 특성인 경우 TRUE)입니다.  
  
 축약형 구문을 사용하여 XPath 쿼리를 다음과 같이 지정할 수도 있습니다.  
  
```  
/Customer[@CustomerID="ALFKI"]  
```  
  
## <a name="selection-predicate-example-2"></a>선택 조건자: 예 2  
 다음 XPath 식 (위치 경로)은 현재 컨텍스트 노드에서 값이 1 인 **SalesOrderID** 특성이 있는 모든 ** \<Order>** 손자를 선택 합니다.  
  
```  
/child::Customer/child::Order[attribute::SalesOrderID="1"]  
```  
  
 이 XPath 식에서 `child` 및 `attribute`는 축 이름입니다. 
  `Customer`, `Order` 및 `SalesOrderID`는 노드 테스트이고, 
  `attribute::OrderID="1"`는 조건자입니다.  
  
 축약형 구문을 사용하여 XPath 쿼리를 다음과 같이 지정할 수도 있습니다.  
  
```  
/Customer/Order[@SalesOrderID="1"]  
```  
  
## <a name="selection-predicate-example-3"></a>선택 조건자: 예제 3  
 다음 XPath 식 (위치 경로)은 현재 컨텍스트 노드에서 ** \<ContactName>** 자식이 하나 이상 있는 모든 ** \<고객>** 자식을 선택 합니다.  
  
```  
child::Customer[child::ContactName]  
```  
  
 이 예에서는 ** \<ContactName>** 가 주석이 추가 된 XSD 스키마에서 *요소 중심 매핑* 이라고 하는 XML 문서의 ** \<Customer>** 요소에 대 한 자식 요소인 것으로 가정 합니다.  
  
 이 XPath 식에서 `child`는 축 이름이고, `Customer`는 노드 테스트 `Customer` (가 `child` ** \<요소>** 노드인 경우 TRUE)입니다. ** \<요소>** 는 축에 대 한 주 노드 형식 이기 때문입니다. 
  `child::ContactName`는 조건자입니다. 조건자에서는 축 `child` 이 고 `ContactName` 는 노드 테스트 (가 ** \<요소>** 노드) `ContactName` 인 경우 TRUE입니다.  
  
 이 **식은 \<ContactName>** 요소 자식이 있는 컨텍스트 노드의 ** \<Customer>** 요소 자식만 반환 합니다.  
  
 축약형 구문을 사용하여 XPath 쿼리를 다음과 같이 지정할 수도 있습니다.  
  
```  
Customer[ContactName]  
```  
  
## <a name="selection-predicate-example-4"></a>선택 조건자: 예제 4  
 다음 XPath 식은 ** \<ContactName>** 요소 자식이 없는 컨텍스트 노드의 ** \<Customer>** 요소 자식을 선택 합니다.  
  
```  
child::Customer[not(child::ContactName)]  
```  
  
 이 예에서는 ** \<ContactName>** 이 XML 문서에서 ** \<Customer>** 요소의 자식 요소이 고 데이터베이스에 ContactName 필드가 필요 하지 않다고 가정 합니다.  
  
 이 예에서 `child`는 축이고, `Customer`노드 테스트 (가 `Customer` \<요소> 노드) 인 경우 TRUE입니다. 
  `not(child::ContactName)`는 조건자입니다. 조건자에서는 축 `child` 이 고 `ContactName` 는 노드 테스트 (가 `ContactName` \<요소> 노드) 인 경우 TRUE입니다.  
  
 축약형 구문을 사용하여 XPath 쿼리를 다음과 같이 지정할 수도 있습니다.  
  
```  
Customer[not(ContactName)]  
```  
  
## <a name="selection-predicate-example-5"></a>선택 조건자: 예제 5  
 다음 XPath 식은 현재 컨텍스트 노드에서 **CustomerID** 특성이 있는 모든 ** \<고객>** 자식을 선택 합니다.  
  
```  
child::Customer[attribute::CustomerID]  
```  
  
 이 예제 `child` 에서는 축과 `Customer` 노드 테스트 (가 `Customer` \<요소> 노드) 인 경우 TRUE입니다. 
  `attribute::CustomerID`는 조건자입니다. 조건자에서는 축 `attribute` 이 고 `CustomerID` 는 조건자 (가 ** \<특성>** 노드) `CustomerID` 인 경우 TRUE입니다.  
  
 축약형 구문을 사용하여 XPath 쿼리를 다음과 같이 지정할 수도 있습니다.  
  
```  
Customer[@CustomerID]  
```  
  
## <a name="selection-predicate-example-6"></a>선택 조건자: 예제 6  
 다음 예에서 볼 수 있는 것처럼 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0은 조건자에 교차곱을 포함하는 XPath 쿼리를 지원합니다.  
  
```  
Customer[Order/@OrderDate=Order/@ShipDate]  
```  
  
 이 쿼리는 `Order`가 `OrderDate` 중 하나의 `ShipDate`와 동일한 `Order`가 있는 모든 고객을 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLXML 4.0&#41;&#40;주석이 추가 된 XSD 스키마 소개](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)   
 [클라이언트 쪽 XML 서식 지정 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)  
  
  
