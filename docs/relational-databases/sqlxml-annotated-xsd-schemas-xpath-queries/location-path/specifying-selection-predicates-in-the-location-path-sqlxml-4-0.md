---
title: 선택 조건자 지정 (SQLXML 4.0) 위치 경로에서 | Microsoft Docs
ms.custom: ''
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4ace1b9a52853ed96ccc9cf74099760c30332dfd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62720026"
---
# <a name="specifying-selection-predicates-in-the-location-path-sqlxml-40"></a>위치 경로에서 선택 조건자 지정(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  조건자는 SELECT 문의 WHERE 절과 유사하게 축을 기준으로 노드 집합을 필터링합니다. 조건자는 대괄호로 묶어서 지정합니다. 노드 집합의 각 노드를 필터링하기 위해 해당 노드가 컨텍스트 노드로 사용되고 노드 집합의 노드 수가 컨텍스트 크기로 사용되어 조건자 식이 평가됩니다. 노드에 대한 조건자 식이 TRUE로 평가되면 해당 노드가 결과 노드 집합에 포함됩니다.  
  
 XPath에서도 위치 기반 필터링이 가능합니다. 숫자로 계산되는 조건자 식이 필요한 서수 노드를 선택합니다. 예를 들어 위치 경로 `Customer[3]`은 세 번째 고객을 반환하지만, 이와 같은 숫자 조건자는 지원되지 않고 부울 결과를 반환하는 조건자 식만 지원됩니다.  
  
> [!NOTE]  
>  XPath의이 XPath 구현 제한 사항에 대 한 정보 및 고 W3C 사양과 차이점 [XPath 쿼리 사용 소개 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/introduction-to-using-xpath-queries-sqlxml-4-0.md)합니다.  
  
## <a name="selection-predicate-example-1"></a>선택 조건자: 예제 1  
 모든 현재 컨텍스트 노드에서 다음 XPath 식 (위치 경로)를 선택 합니다  **\<고객 >** 요소 자식을 합니다 **CustomerID** ALFKI의 값을 사용 하 여 특성:  
  
```  
/child::Customer[attribute::CustomerID="ALFKI"]  
```  
  
 이 XPath 쿼리에서 `child` 및 `attribute`는 축 이름이고, `Customer` 노드 테스트 (TRUE 이면 `Customer` 은  **\<요소 노드 >** 이므로  **\<요소 >** 주 노드 형식입니다.는 `child` 축). `attribute::CustomerID="ALFKI"`는 조건자입니다. 조건자에서 `attribute` 는 축이고와 `CustomerID` 는 노드 테스트 (TRUE 이면 **CustomerID** 이므로 컨텍스트 노드의 특성  **\<특성 >** 보안 주체 노드 유형의 **특성** 축).  
  
 축약형 구문을 사용하여 XPath 쿼리를 다음과 같이 지정할 수도 있습니다.  
  
```  
/Customer[@CustomerID="ALFKI"]  
```  
  
## <a name="selection-predicate-example-2"></a>선택 조건자: 예제 2  
 모든 현재 컨텍스트 노드에서 다음 XPath 식 (위치 경로)를 선택 합니다  **\<순서 >** 손자를 합니다 **SalesOrderID** 값 1 사용 하 여 특성:  
  
```  
/child::Customer/child::Order[attribute::SalesOrderID="1"]  
```  
  
 이 XPath 식에서 `child` 및 `attribute`는 축 이름입니다. `Customer`, `Order` 및 `SalesOrderID`는 노드 테스트이고, `attribute::OrderID="1"`는 조건자입니다.  
  
 축약형 구문을 사용하여 XPath 쿼리를 다음과 같이 지정할 수도 있습니다.  
  
```  
/Customer/Order[@SalesOrderID="1"]  
```  
  
## <a name="selection-predicate-example-3"></a>선택 조건자: 예 3  
 모든 현재 컨텍스트 노드에서 다음 XPath 식 (위치 경로)를 선택 합니다  **\<고객 >** 하나 이상의 자식을  **\<ContactName >** 자식:  
  
```  
child::Customer[child::ContactName]  
```  
  
 이 가정 합니다  **\<ContactName >** 의 자식 요소는  **\<고객 >** 이라고 하는 XML 문서의 요소  *요소 중심 매핑* 주석이 추가 된 XSD 스키마에서입니다.  
  
 이 XPath 식에서 `child`는 축 이름이고, `Customer` 노드 테스트 (TRUE 이면 `Customer` 되는  **\<요소 >** 노드를 때문에  **\<요소 >** 주 노드 형식입니다. `child` 축). `child::ContactName`는 조건자입니다. 조건자에서 `child` 는 축이고 및 `ContactName` 는 노드 테스트 (TRUE 이면 `ContactName` 되는  **\<요소 >** 노드).  
  
 이 식만 반환 합니다  **\<고객 >** 는 컨텍스트 노드의 요소 자식을  **\<ContactName >** 요소 자식을 합니다.  
  
 축약형 구문을 사용하여 XPath 쿼리를 다음과 같이 지정할 수도 있습니다.  
  
```  
Customer[ContactName]  
```  
  
## <a name="selection-predicate-example-4"></a>선택 조건자: 예제 4  
 다음 XPath 식은 선택  **\<고객 >** 하지 않은 컨텍스트 노드의 요소 자식을  **\<ContactName >** 요소 자식을:  
  
```  
child::Customer[not(child::ContactName)]  
```  
  
 이 예에서는 가정  **\<ContactName >** 의 자식 요소는  **\<고객 >** XML 문서의 요소와 ContactName 필드가 필요 하지 않습니다는 데이터베이스입니다.  
  
 이 예에서 `child`는 축이고, `Customer` 노드 테스트 (TRUE 이면 `Customer` 되는 \<요소 > 노드). `not(child::ContactName)`는 조건자입니다. 조건자에서 `child` 는 축이고와 `ContactName` 는 노드 테스트 (TRUE 이면 `ContactName` 는 \<요소 > 노드).  
  
 축약형 구문을 사용하여 XPath 쿼리를 다음과 같이 지정할 수도 있습니다.  
  
```  
Customer[not(ContactName)]  
```  
  
## <a name="selection-predicate-example-5"></a>선택 조건자: 예제 5  
 다음 XPath 식은 현재 컨텍스트 노드의 모든 선택 된  **\<고객 >** 자식을 합니다 **CustomerID** 특성:  
  
```  
child::Customer[attribute::CustomerID]  
```  
  
 이 예에서 `child` 는 축이고 및 `Customer` 는 노드 테스트 (TRUE 이면 `Customer` 가 \<요소 > 노드). `attribute::CustomerID`는 조건자입니다. 조건자에서 `attribute` 는 축이고 및 `CustomerID` 는 조건자 (TRUE 이면 `CustomerID` 되는  **\<특성 >** 노드).  
  
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
  
## <a name="see-also"></a>관련 항목  
 [주석이 추가 된 XSD 스키마 소개 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)   
 [클라이언트 쪽 XML 서식 지정 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)  
  
  
