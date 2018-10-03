---
title: CSDL BI 주석에 대 한 기술 참조 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 63b3e069-6ba5-474e-b769-47b7cc87b7dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6e0a166f1c81b9e010d7e9cfd7a0547c3a4b9c72
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48094193"
---
# <a name="technical-reference-for-bi-annotations-to-csdl"></a>CSDL용 BI 주석에 대한 기술 참조
  이 섹션에서는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 테이블 형식 모델을 나타내는 데 사용되는 CSDL의 요소, 특성 및 속성을 보여 줍니다. 일부 요소는 새로 추가된 요소이고, 나머지는 BI 확장을 지원하도록 주석이 추가되거나 확장된 요소입니다.  
  
 테이블 형식 모델 및 CSDL에서 엔터티, 관계 및 수식을 나타내는 하는 방법의 개요를 참조 하세요 [비즈니스 인텔리전스에 대 한 CSDL 주석 &#40;CSDLBI&#41;](../csdl-annotations-for-business-intelligence-csdlbi.md)합니다.  
  
## <a name="extended-csdl-elements-complex-types"></a>확장된 CSDL 요소: 복합 유형  
 CSDL의 다음 요소는 테이블 형식 및 다차원 비즈니스 인텔리전스 데이터 모델을 지원하도록 추가 또는 확장된 요소입니다.  
  
-   [AssociationSet 요소 &#40;CSDLBI&#41;](associationset-element-csdlbi.md)  
  
-   [BaseProperty 요소 &#40;CSDLBI&#41;](property-element-csdlbi.md)  
  
-   [DefaultDetails 요소 &#40;CSDLBI&#41;](defaultdetails-element-csdlbi.md)  
  
-   [DisplayKey 요소 &#40;CSDLBI&#41;](displaykey-element-csdlbi.md)  
  
-   [EntityContainer 요소 &#40;CSDLBI&#41;](entitycontainer-element-csdlbi.md)  
  
-   [EntitySet 요소 &#40;CSDLBI&#41;](entityset-element-csdlbi.md)  
  
-   [EntityType 요소 &#40;CSDLBI&#41;](entitytype-element-csdlbi.md)  
  
-   [Hierarchy 요소 &#40;CSDLBI&#41;](hierarchy-element-csdlbi.md)  
  
-   [KPI 요소 &#40;CSDLBI&#41;](kpi-element-csdlbi.md)  
  
-   [KpiGoal 요소 &#40;CSDLBI&#41;](kpigoal-element-csdlbi.md)  
  
-   [KpiStatus 요소 &#40;CSDLBI&#41;](kpistatus-element-csdlbi.md)  
  
-   [요소 &#40;CSDLBI&#41;](level-element-csdlbi.md)  
  
-   [요소를 측정 합니다. &#40;CSDLBI&#41;](measure-element-csdlbi.md)  
  
-   [Member 요소 &#40;CSDLBI&#41;](member-element-csdlbi.md)  
  
-   [MemberRef 요소 &#40;CSDLBI&#41;](memberref-element-csdlbi.md)  
  
-   [NavigationProperty 요소 &#40;CSDLBI&#41;](navigationproperty-element-csdlbi.md)  
  
-   [Property 요소 &#40;CSDLBI&#41;](property-element-csdlbi.md)  
  
-   [PropertyRef 요소 &#40;CSDLBI&#41;](propertyref-element-csdlbi.md)  
  
## <a name="simple-type-and-subtypes"></a>단순 유형 및 하위 유형  
 다음 표에서는 몇 가지 단순 유형과 위에 나열된 복합 유형의 정의에 해당하는 간단한 복합 유형을 몇 가지 보여 줍니다. 왼쪽 열의 단순 유형 또는 하위 유형 각각에 대한 설명은 오른쪽 열의 부모 요소에 있습니다.  
  
|단순 유형|항목에 있음|  
|-----------------|--------------------|  
|맞춤|[BaseProperty 요소 &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|CompareOptions|[EntityContainer 요소 &#40;CSDLBI&#41;](entitycontainer-element-csdlbi.md)|  
|내용|[EntityType 요소 &#40;CSDLBI&#41;](entitytype-element-csdlbi.md)|  
|ContextualNameRule|[Member 요소 &#40;CSDLBI&#41;](member-element-csdlbi.md)|  
|DefaultAggregationFunction|[Property 요소 &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|DirectQueryMode|[EntityContainer 요소 &#40;CSDLBI&#41;](entitycontainer-element-csdlbi.md)|  
|GroupingBehavior|[Property 요소 &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|MemberRefs|[MemberRef 요소 &#40;CSDLBI&#41;](memberref-element-csdlbi.md)|  
|PropertyRefs|[PropertyRef 요소 &#40;CSDLBI&#41;](propertyref-element-csdlbi.md)|  
|SortDirection|[BaseProperty 요소 &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|State|[AssociationSet 요소 &#40;CSDLBI&#41;](associationset-element-csdlbi.md)|  
|안정성|[Property 요소 &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|SortDirection|[BaseProperty 요소 &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
  
## <a name="see-also"></a>관련 항목  
 [CSDLBI 개념](../csdlbi-concepts.md)  
  
  
