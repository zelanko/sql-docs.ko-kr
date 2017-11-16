---
title: "MDX 쿼리 기본 사항 (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- statements [MDX]
- Multidimensional Expressions [Analysis Services], statements
- Multidimensional Expressions [Analysis Services], queries
- MDX [Analysis Services], statements
- MDX queries [Analysis Services]
- MDX [Analysis Services], queries
- queries [MDX]
ms.assetid: a560383b-bb58-472e-95f5-65d03d8ea08b
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cefad04fdadd4475863dccca5cba5f3e9cf4f48c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-query-fundamentals-analysis-services"></a>MDX 쿼리 기본 사항(Analysis Services)
  MDX를 사용하면 큐브와 같은 다차원 개체를 쿼리하여 큐브의 데이터를 포함하는 다차원 셀 집합을 반환할 수 있습니다. 이 항목 및 하위 항목에서는 MDX 쿼리에 대한 개요를 제공합니다.  
  
 다음 항목에서는 MDX 쿼리 및 쿼리가 만드는 셀 집합에 대해 설명하고 기본적인 MDX 구문에 대한 자세한 정보를 제공합니다.  
  
> [!NOTE]  
>  MDX 쿼리 및 계산과 관련된 성능 문제에 대한 자세한 내용은 [SQL Server 2005 Analysis Services 성능 가이드(SQL Server 2005 Analysis Services Performance Guide)](http://go.microsoft.com/fwlink/?LinkId=81621)의 "효율적인 MDX 작성(Writing Efficient MDX)" 섹션을 참조하십시오.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[기본 MDX 쿼리&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)|MDX SELECT 문의 기본 구문에 대한 정보를 제공합니다.|  
|[쿼리 및 Slicer 축 &#40;으로 쿼리 제한 Mdx&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md)|쿼리 및 slicer 축의 의미 및 지정 방법을 설명합니다.|  
|[쿼리에 큐브 컨텍스트 설정&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)|MDX SELECT 문에서 FROM 절을 사용하는 목적을 설명합니다.|  
|[명명된 집합을 MDX로 작성&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md)|MDX에서 명명된 집합을 사용하는 목적과 MDX 쿼리에서 명명된 집합을 만들고 사용하는 데 필요한 기술을 설명합니다.|  
|[계산 멤버를 MDX로 작성&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md)|MDX의 계산 멤버에 대해 설명하고 MDX 식에서 계산 멤버를 만들고 사용하는 데 필요한 기술을 설명합니다.|  
|[MDX로 셀 계산 작성&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations.md)|계산 셀을 만들고 사용하는 과정을 설명합니다.|  
|[속성 값 만들기 및 사용&#40;MDX&#41;](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)|차원, 수준, 멤버 및 셀 속성을 만들고 사용하는 과정을 설명합니다.|  
|[데이터 조작&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)|드릴스루 및 롤업을 사용하는 데이터 조작법에 대한 기본 지식 및 MDX의 패스 순서 및 계산 순서를 설명합니다.|  
|[데이터 수정&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-modification-modifying-data.md)|쓰기 저장(writeback)을 사용하여 다차원 데이터를 일시적 또는 영구적으로 변경하는 방법을 설명합니다.|  
|[변수 및 매개 변수 사용&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/using-variables-and-parameters-mdx.md)|MDX 쿼리에서 변수와 매개 변수를 사용하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [MDX&#40;Multidimensional Expression&#41; 참조](../../../mdx/multidimensional-expressions-mdx-reference.md)  
  
  

