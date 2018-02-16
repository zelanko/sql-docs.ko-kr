---
title: "사용자 계층 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- members [Analysis Services], hierarchies
- dimensions [Analysis Services], hierarchies
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], attribute
- attributes [Analysis Services], hierarchies
- parent-child hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
- ragged hierarchies [Analysis Services]
- balanced hierarchies [Analysis Services]
- hierarchies [Analysis Services]
- OLAP objects [Analysis Services], hierarchies
- multilevel hierarchies [Analysis Services]
- unbalanced hierarchies [Analysis Services]
ms.assetid: 9394e9a3-2242-4f0e-85e0-25d499d2d3b6
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 01f5e5b5a73a8888d24d3ee46127c67327ec75da
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="user-hierarchies"></a>사용자 계층
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
사용자 정의 계층에 사용 되는 특성의 사용자 정의 계층은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 를 계층 구조로 차원의 멤버를 구성 하 고 큐브의 탐색 경로 제공 합니다. 예를 들어 다음 표에서는 시간 차원에 대한 차원 테이블을 정의합니다. 차원 테이블은 Year, Quarter 및 Month라는 3가지 특성을 지원합니다.  
  
|Year|Quarter|Month|  
|----------|-------------|-----------|  
|1999|분기 1|1월|  
|1999|분기 1|2월|  
|1999|분기 1|3월|  
|1999|분기 2|4월|  
|1999|분기 2|5월|  
|1999|분기 2|6월|  
|1999|3 1/4|7월|  
|1999|3 1/4|8월|  
|1999|3 1/4|9월|  
|1999|4사분기|Oct|  
|1999|4사분기|11월|  
|1999|4사분기|Dec|  
  
 Year, Quarter 및 Month 특성은 시간 차원에서 Calendar라는 사용자 정의 계층을 구성하는 데 사용됩니다. Calendar 차원(일반 차원)의 수준과 멤버 간의 관계는 아래 다이어그램에 표시되어 있습니다.  
  
 ![시간 차원에 대 한 수준 및 구성원 계층](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/media/as-levelconcepts.gif "시간 차원에 대 한 수준 및 구성원 계층")  
  
> [!NOTE]  
>  기본 두 수준 특성 계층 이외의 모든 계층을 사용자 정의 계층이라고 합니다. 특성 계층에 대 한 자세한 내용은 참조 [특성 및 특성 계층](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)합니다.  
  
## <a name="member-structures"></a>멤버 구조  
 부모-자식 계층은 제외하고 계층 구조 내에서 멤버 위치는 계층 정의의 특성 순서로 제어됩니다. 계층 정의에 포함된 각 특성이 계층의 수준이 됩니다. 수준 내에서 멤버의 위치는 수준을 만드는 데 사용된 특성의 순서에 따라 결정됩니다. 사용자 정의 계층의 멤버 구조는 멤버 간의 상호 관련 방식에 따라 다음과 같은 4가지 기본 형태 중 하나를 따릅니다.  
  
### <a name="balanced-hierarchies"></a>균형 계층 구조  
 균형 계층 구조에서는 계층 구조의 모든 분기가 동일한 수준으로 이어지며 각 멤버의 바로 위에 있는 수준이 해당 멤버의 논리적 부모가 됩니다. [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 예제 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 있는 Product 차원의 Product Categories 계층이 균형 계층 구조의 좋은 예입니다. Product Name 수준의 각 멤버에게는 Subcategory 수준의 부모 멤버가 있으며 이 부모 멤버에게는 Category 수준의 부모 멤버가 있습니다. 또한 이 계층 구조의 모든 분기에는 Product Name 수준의 리프 멤버가 있습니다.  
  
### <a name="unbalanced-hierarchies"></a>불균형 계층 구조  
 불균형 계층 구조에서는 계층 구조의 분기들이 서로 다른 수준으로 이어집니다.  부모-자식 계층 구조는 불균형 계층 구조입니다. 예를 들어 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 예제 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스의 Organization 차원은 각 직원에 대한 멤버를 포함합니다. CEO가 계층 구조의 최상위 멤버이며 각 부서장과 비서 실장이 CEO 바로 아래 위치합니다. 부서장에게는 부하 멤버들이 있지만 비서 실장에게는 없습니다.  
  
 최종 사용자가 불균형 계층 구조와 비정형 계층 구조를 구분하는 것은 불가능합니다. 그러나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 여러 가지 기술과 속성을 사용하여 이러한 두 가지 유형의 계층 구조를 지원할 수 있습니다. 자세한 내용은 참조 [비정형 계층](../../analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md), 및 [부모-자식 계층의 특성](../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md)합니다.  
  
### <a name="ragged-hierarchies"></a>비정형 계층 구조  
 비정형 계층 구조에서는 최소한 한 멤버의 논리적 부모 멤버가 해당 멤버 바로 위 수준에 있지 않습니다. 이로 인해 계층 구조의 분기들이 서로 다른 수준으로 이어질 수 있습니다. 예를 들어 Geography 차원에 Continent, CountryRegion, City의 순서로 수준이 정의된 경우 계층 구조의 최상위 수준에는 Europe 멤버가 나타나고 중간 수준에는 France 멤버가 나타나고 최하위 수준에는 Paris 멤버가 나타납니다. France가 Europe보다 구체적이고 Paris가 France보다 더 구체적입니다. 이 일반 계층 구조는 다음과 같이 변경됩니다.  
  
-   CountryRegion 수준에 Vatican City 멤버가 추가됩니다.  
  
-   여러 멤버가 City 수준에 추가되고 CountryRegion 수준의 Vatican City 멤버와 연결됩니다.  
  
-   Province라는 이름의 수준이 CountryRegion과 City 수준 사이에 추가됩니다.  
  
 Province 수준은 CountryRegion 수준의 다른 멤버와 연결된 멤버로 채워지고 City 수준의 멤버는 Province 수준의 해당 멤버와 연결됩니다. 그러나 CountryRegion 수준의 Vatican City 멤버에게는 Province 수준의 연결된 멤버가 없기 때문에 City 수준의 멤버가 CountryRegion 수준의 Vatican City 멤버에 직접 연결되어야 합니다. 이러한 변경으로 인해 이 차원은 비정형 계층 구조가 됩니다. CountryRegion의 Vatican City가 City의 Vatican City 부모가 되는데 이것은 City 수준에서 Vatican City 멤버 바로 위에 있는 수준에 있지 않습니다. 자세한 내용은 [비정형 계층 구조](../../analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md)를 참조하세요.  
  
### <a name="parent-child-hierarchies"></a>부모-자식 계층 구조  
 차원의 부모-자식 계층 구조는 멤버 상호 간의 관련 방식을 결정하는 부모 특성이라고 하는 특수한 특성을 사용하여 정의합니다. 부모 특성은 차원 주 테이블 내의 *자체 참조 관계*또는 *셀프 조인*을 설명합니다. 부모-자식 계층은 단일 부모 특성에서 생성됩니다. 계층에 존재하는 수준은 부모 특성과 관련된 멤버 간 부모-자식 관계에서 가져오므로 부모-자식 계층에는 하나의 수준만 할당됩니다. 부모-자식 계층의 차원 스키마는 차원 주 테이블에 있는 자체 참조 관계에 따라 다릅니다. 예를 들어 다음 다이어그램에서는 **DimOrganization** 차원 주 테이블에는 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 예제 데이터베이스.  
  
 ![DimOrganization 테이블의 자체 참조 조인](../../analysis-services/multidimensional-models/media/dimorganization.gif "DimOrganization 테이블의 자체 참조 조인")  
  
 이 차원 테이블에서 **ParentOrganizationKey** 열은 **OrganizationKey** 기본 키 열과 외래 키 관계에 있습니다. 즉, 이 테이블의 각 레코드는 부모-자식 관계를 통해 테이블의 다른 레코드와 관련될 수 있습니다. 이러한 종류의 자체 조인은 일반적으로 부서 내 직원 관리 구조와 같은 조직 엔터티 데이터를 나타내는 데 사용됩니다.  
  
 부모-자식 계층 구조를 만들 경우 두 특성이 나타내는 열의 데이터 형식은 같아야 합니다. 또한 두 특성이 모두 같은 테이블에 있어야 합니다. 기본적으로 부모 키가 자신의 멤버 키 또는 Null, 0(영), 멤버 키 열에 없는 값과 동일한 모든 멤버는 (All) 수준을 제외한 최상위 수준의 멤버로 가정합니다.  
  
 부모-자식 계층 구조의 깊이는 계층 분기에 따라 다를 수 있습니다. 즉, 부모-자식 계층 구조는 불균형 계층 구조로 간주됩니다.  
  
 계층 수준의 개수가 최종 사용자에게 표시될 수 있는 수준의 개수를 결정하는 사용자 정의 계층 구조와 달리 부모-자식 계층 구조는 특성 계층의 단일 수준과 사용자에게 표시되는 다중 수준을 생성하는 단일 수준의 값으로 정의됩니다. 표시되는 수준의 개수는 멤버 키와 부모 키가 저장된 차원 테이블 열의 내용에 따라 달라집니다. 차원 테이블의 데이터가 변경되면 수준의 개수가 변경될 수 있습니다. 자세한 내용은 참조 [부모-자식 차원은](../../analysis-services/multidimensional-models/parent-child-dimension.md), 및 [부모-자식 계층의 특성](../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [사용자 정의 계층 만들기](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)   
 [사용자 계층 속성](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [차원 특성 속성 참조](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
