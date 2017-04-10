---
title: "MDX 쿼리 기본 사항(Analysis Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "문 [MDX]"
  - "Multidimensional Expression [Analysis Services], 문"
  - "Multidimensional Expression [Analysis Services], 쿼리"
  - "MDX [Analysis Services], 문"
  - "MDX 쿼리 [Analysis Services]"
  - "MDX [Analysis Services], 쿼리"
  - "쿼리 [MDX]"
ms.assetid: a560383b-bb58-472e-95f5-65d03d8ea08b
caps.latest.revision: 31
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 30
---
# MDX 쿼리 기본 사항(Analysis Services)
  MDX를 사용하면 큐브와 같은 다차원 개체를 쿼리하여 큐브의 데이터를 포함하는 다차원 셀 집합을 반환할 수 있습니다. 이 항목 및 하위 항목에서는 MDX 쿼리에 대한 개요를 제공합니다.  
  
 다음 항목에서는 MDX 쿼리 및 쿼리가 만드는 셀 집합에 대해 설명하고 기본적인 MDX 구문에 대한 자세한 정보를 제공합니다.  
  
> [!NOTE]  
>  MDX 쿼리 및 계산과 관련된 성능 문제에 대한 자세한 내용은 [SQL Server 2005 Analysis Services 성능 가이드(SQL Server 2005 Analysis Services Performance Guide)](http://go.microsoft.com/fwlink/?LinkId=81621)의 "효율적인 MDX 작성(Writing Efficient MDX)" 섹션을 참조하십시오.  
  
## 섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[기본 MDX 쿼리&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-query-mdx.md)|MDX SELECT 문의 기본 구문에 대한 정보를 제공합니다.|  
|[쿼리 및 Slicer 축으로 쿼리 제한&#40;MDX&#41;](../Topic/Restricting%20the%20Query%20with%20Query%20and%20Slicer%20Axes%20\(MDX\).md)|쿼리 및 slicer 축의 의미 및 지정 방법을 설명합니다.|  
|[쿼리에 큐브 컨텍스트 설정&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)|MDX SELECT 문에서 FROM 절을 사용하는 목적을 설명합니다.|  
|[명명된 집합을 MDX로 작성&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/building-named-sets-in-mdx-mdx.md)|MDX에서 명명된 집합을 사용하는 목적과 MDX 쿼리에서 명명된 집합을 만들고 사용하는 데 필요한 기술을 설명합니다.|  
|[계산 멤버를 MDX로 작성&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/building-calculated-members-in-mdx-mdx.md)|MDX의 계산 멤버에 대해 설명하고 MDX 식에서 계산 멤버를 만들고 사용하는 데 필요한 기술을 설명합니다.|  
|[MDX로 셀 계산 작성&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/building-cell-calculations-in-mdx-mdx.md)|계산 셀을 만들고 사용하는 과정을 설명합니다.|  
|[속성 값 만들기 및 사용&#40;MDX&#41;](../Topic/Creating%20and%20Using%20Property%20Values%20\(MDX\).md)|차원, 수준, 멤버 및 셀 속성을 만들고 사용하는 과정을 설명합니다.|  
|[데이터 조작&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/manipulating-data-mdx.md)|드릴스루 및 롤업을 사용하는 데이터 조작법에 대한 기본 지식 및 MDX의 패스 순서 및 계산 순서를 설명합니다.|  
|[데이터 수정&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/modifying-data-mdx.md)|쓰기 저장(writeback)을 사용하여 다차원 데이터를 일시적 또는 영구적으로 변경하는 방법을 설명합니다.|  
|[변수 및 매개 변수 사용&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/using-variables-and-parameters-mdx.md)|MDX 쿼리에서 변수와 매개 변수를 사용하는 방법을 설명합니다.|  
  
## 관련 항목:  
 [MDX&#40;Multidimensional Expression&#41; 참조](../../../mdx/multidimensional-expressions-mdx-reference.md)  
  
  