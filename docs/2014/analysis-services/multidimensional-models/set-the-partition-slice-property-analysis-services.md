---
title: 파티션 조각 속성 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 08/05/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- partitions [Analysis Services], data slices
- data slices [Analysis Services]
ms.assetid: 507b91e5-7f85-4c22-be97-4d7a676e6667
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c94ac9865540016020bf1853bc318881defdaea7
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53374065"
---
# <a name="set-the-partition-slice-property-analysis-services"></a>파티션 조각 속성 설정(Analysis Services)
  데이터 조각은 적절한 파티션의 데이터에 대한 직접적인 쿼리를 돕는 중요한 최적화 기능입니다. Slice 속성을 명시적으로 설정하면 MOLAP 및 HOLAP 파티션에 대해 생성된 기본 조각을 재정의하여 쿼리 성능을 향상시킬 수 있습니다. 또한 Slice 속성은 파티션을 처리할 때 추가 유효성 검사를 제공합니다.  
  
 파티션을 만든 후 처리하기 전에 Slice 속성을 사용하여 데이터 조각을 지정할 수 있습니다. 파티션 탭에서 측정값 그룹을 확장하고 파티션을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
## <a name="defining-a-slice"></a>조각 정의  
 Slice 속성으로 유효한 값은 MDX 멤버, 집합 또는 튜플입니다. 다음 예에서는 유효한 조각 구문을 보여 줍니다.  
  
|조각|멤버, 집합 또는 튜플|  
|-----------|--------------------------|  
|[Date].[Calendar].[Calendar Year].&[2010]|2010년의 팩트를 포함하는 파티션에 이 조각을 지정합니다. 이때 모델에 Calendar Year 계층이 있고 2010이 멤버인 Date 차원이 포함되어 있는 것으로 가정합니다. 파티션 원본 WHERE 절 또는 테이블이 이미 2010을 기준으로 필터링할 수 있지만 Slice를 지정하면 처리하는 중에 추가 검사뿐 아니라 쿼리 실행 중에 더 구체적으로 대상이 지정된 검색도 제공됩니다.|  
|{ [Sales Territory].[Sales Territory Country].&[Australia], [Sales Territory].[Sales Territory Country].&[Canada] }|영업 지역 정보를 포함하는 팩트가 포함된 파티션에 이 조각을 지정합니다. 조각은 두 개 이상의 멤버로 구성된 MDX 집합일 수 있습니다.|  
|[Measures].[Sales Amount Quota] > '5000'|이 조각은 MDX 식을 보여 줍니다.|  
  
 파티션의 데이터 조각에는 파티션의 데이터가 아주 자세히 반영되어야 합니다. 예를 들어 파티션이 2012년 데이터로 제한되는 경우에는 파티션의 데이터 조각이 시간 차원의 2012년 멤버를 지정해야 합니다. 파티션의 내용을 정확히 반영하는 데이터 조각을 지정하는 것이 항상 가능한 것은 아닙니다. 예를 들어 파티션에는 1월과 2월에 대한 데이터만 있지만 시간 차원의 수준은 Year, Quarter, Month인 경우에는 파티션 마법사로 1월과 2월 멤버를 모두 선택할 수 있는 방법이 없습니다. 이러한 경우에는 파티션의 내용이 반영된 멤버의 부모를 선택합니다. 이 예에서는 Quarter 1을 선택합니다.  
  
 데이터 조각의 이점에 대한 설명은 [SSAS 큐브 파티션에 조각 설정](https://go.microsoft.com/fwlink/?LinkId=317783)을 참조하십시오.  
  
> [!NOTE]  
>  동적 MDX 함수(예: [Generate&#40;MDX&#41;](/sql/mdx/generate-mdx) 또는 [Except&#40;MDX&#41;](/sql/mdx/except-mdx-function))는 파티션에 대한 Slice 속성에서 지원되지 않습니다. 명시적 튜플 또는 멤버 참조를 사용하여 조각을 정의해야 합니다.  
>   
>  예를 들어, 사용 하는 대신 합니다 [: &#40;범위&#41; &#40;MDX&#41; ](/sql/mdx/range-mdx) 범위를 정의 하는 함수, 특정 연도별로 각 멤버를 열거 해야 합니다.  
>   
>  복잡한 조각을 정의해야 하는 경우 XMLA Alter 스크립트를 사용하여 조각에서 튜플을 정의하는 것이 좋습니다. 그런 다음 ascmd 명령줄 도구 또는 SSIS [Analysis Services Execute DDL Task](../../integration-services/control-flow/analysis-services-execute-ddl-task.md) 를 사용하여 스크립트를 실행하고 지정된 멤버 집합을 만든 후 곧바로 파티션을 처리할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [로컬 파티션 만들기 및 관리&#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md)  
  
  
