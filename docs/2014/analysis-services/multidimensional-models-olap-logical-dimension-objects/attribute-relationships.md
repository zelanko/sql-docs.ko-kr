---
title: 특성 관계 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- member properties [Analysis Services], attribute relationships
- security [Analysis Services], properties
- PROPERTIES keyword
- storage [Analysis Services], attribute relationships
- natural hierarchies [Analysis Services]
- dimensions [Analysis Services], member properties
- queries [MDX], attribute relationships
- user-defined hierarchies [Analysis Services]
- attributes [Analysis Services], relationships
- member properties [Analysis Services]
- members [Analysis Services], attribute relationships
- storing data [Analysis Services], attribute relationships
- relationships [Analysis Services], attributes
ms.assetid: 2491422a-4cf5-4b23-b6ab-289222b22ce8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 81d51c8778cfbc6e3891dfb3b6783db48f0c65a2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62728519"
---
# <a name="attribute-relationships"></a>의 차원 디자이너에 있는 차원 구조 뷰의
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]차원 내의 특성은 항상 키 특성과 직접 또는 간접적으로 관련이 있습니다. 모든 차원 특성이 동일한 관계형 테이블에서 파생되는 별모양 스키마를 기반으로 차원을 정의할 경우 차원의 키 특성과 각각의 키가 아닌 특성 간에 특성 관계가 자동으로 정의됩니다. 그러나 차원 특성이 관련된 여러 테이블에서 파생되는 눈송이 스키마를 기반으로 차원을 정의하면 다음 사이에서 특성 관계가 자동으로 정의됩니다.  
  
-   키 특성과 주 차원 테이블의 열에 바인딩된 각각의 키가 아닌 특성 간  
  
-   키 특성과 기본 차원 테이블을 연결하는 보조 테이블의 외래 키에 바인딩된 특성 간  
  
-   보조 테이블의 외래 키에 바인딩된 특성과 보조 테이블의 열에 바인딩된 각각의 키가 아닌 특성 간  
  
 그러나 다양한 이유로 이러한 기본 특성 관계를 변경하려고 할 수 있습니다. 예를 들어 키가 아닌 특성을 기반으로 자연 계층, 사용자 지정 정렬 순서 또는 차원 세분성을 정의할 수 있습니다. 자세한 내용은 [차원 특성 속성 참조](../multidimensional-models/dimension-attribute-properties-reference.md)를 참조 하세요.  
  
> [!NOTE]  
>  MDX(Multidimensional Expressions)에서는 특성 관계를 멤버 속성이라고 합니다.  
  
## <a name="natural-hierarchy-relationships"></a>자연 계층 관계  
 사용자 정의 계층에 포함된 각 특성이 바로 아래에 있는 특성과 일 대 다 관계를 가질 때 계층은 자연 계층입니다. 예를 들어 다음과 같은 8개의 열이 있는 관계형 원본 테이블을 기반으로 하는 Customer 차원을 고려해 보십시오.  
  
-   CustomerKey  
  
-   CustomerName  
  
-   Age  
  
-   성별  
  
-   메일  
  
-   City  
  
-   국가  
  
-   지역  
  
 해당하는 Analysis Services 차원에는 다음의 7가지 특성이 있습니다.  
  
-   Customer(CustomerKey를 기반으로 하며 CustomerName이 멤버 이름을 제공함)  
  
-   Age, Gender, Email, City, Region, Country  
  
 자연 계층을 나타내는 관계는 수준에 대한 특성 및 아래 수준에 대한 특성 간의 특성 관계를 만들어 적용합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 경우 이를 통해 자연 관계와 잠재적인 집계가 지정됩니다. Customer 차원에 Country, Region, City 및 Customer 특성에 대한 자연 계층이 존재하게 됩니다. `{Country, Region, City, Customer}`에 대한 자연 계층은 다음과 같은 특성 관계를 추가하여 설명합니다.  
  
-   Region 특성에 대한 특성 관계로 Country 특성 추가  
  
-   City 특성에 대한 특성 관계로 Region 특성 추가  
  
-   Customer 특성에 대한 특성 관계로 City 특성 추가  
  
 큐브의 데이터를 탐색 하려는 경우 데이터의 자연 계층을 나타내지 않는 사용자 정의 계층 ( *임시 또는* *보고* 계층 이라고 함)을 만들 수도 있습니다. 예를 들어 `{Age, Gender}`를 기반으로 사용자 정의 계층을 만들 수 있습니다. 자연 계층은 원본 데이터의 자연 관계를 고려 하 여 사용자 로부터 숨겨진 구조를 집계 및 인덱싱할 수 있다는 장점이 있지만 사용자는 두 계층의 동작 방식에 차이가 없습니다.  
  
 수준 차원의 `SourceAttribute` 속성은 수준을 설명하는 데 사용되는 특성을 결정합니다. 특성에 대한 `KeyColumns` 속성은 멤버를 공급하는 데이터 원본 뷰의 열을 지정합니다. 특성에 대한 `NameColumn` 속성은 멤버에 대해 다른 이름 열을 지정할 수 있습니다.  
  
 를 사용 하 여 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]사용자 정의 계층에 수준을 정의 하려면 **차원 디자이너** 를 사용 하 여 차원 특성, 차원 테이블의 열 또는 큐브의 데이터 원본 뷰에 포함 된 관련 테이블의 열을 선택할 수 있습니다. 사용자 정의 계층을 만드는 방법에 대 한 자세한 내용은 [사용자 정의 계층 만들기](../multidimensional-models/user-defined-hierarchies-create.md)를 참조 하세요.  
  
 Analysis Services에서는 멤버의 내용에 대해 대체로 하나의 가정이 이루어집니다. 리프 멤버에는 하위 멤버가 없으며 기본 데이터 원본에서 파생된 데이터가 포함됩니다. 리프가 아닌 멤버에는 하위 멤버가 있고 자식 멤버에 대해 수행된 집계에서 파생된 데이터가 포함됩니다. 집계된 수준에서 멤버는 종속 수준의 집계를 기반으로 합니다. 따라서 수준에 대한 원본 특성에서 `IsAggregatable` 속성을 `False`로 설정한 경우 집계 가능한 특성을 상위 수준으로 추가하면 안 됩니다.  
  
## <a name="defining-an-attribute-relationship"></a>특성 관계 정의  
 특성 관계를 만들 때 주요 제약 조건은 특성 관계에서 참조하는 특성에 특성 관계가 속하는 특성의 멤버에 대한 값이 하나만 있어야 한다는 것입니다. 예를 들어 City 특성과 State 특성 간에 관계를 정의하면 각 도시는 하나의 시와만 관련될 수 있습니다.  
  
## <a name="attribute-relationship-queries"></a>특성 관계 쿼리  
 MDX 쿼리에 MDX `PROPERTIES` 문의 `SELECT` 키워드를 사용하여 특성 관계에서 멤버 속성 형식으로 데이터를 검색할 수 있습니다. MDX를 사용 하 여 멤버 속성을 검색 하는 방법에 대 한 자세한 내용은 [멤버 속성 &#40;mdx&#41;사용 ](../multidimensional-models/mdx/mdx-member-properties.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [특성 및 특성 계층](attributes-and-attribute-hierarchies.md)   
 [차원 특성 속성 참조](../multidimensional-models/dimension-attribute-properties-reference.md)   
 [사용자 계층](user-hierarchies.md)   
 [사용자 계층 속성](user-hierarchies-properties.md)  
  
  
