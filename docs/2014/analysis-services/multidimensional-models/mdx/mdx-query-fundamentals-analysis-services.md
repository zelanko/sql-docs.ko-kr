---
title: MDX 쿼리 기본 사항 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- statements [MDX]
- Multidimensional Expressions [Analysis Services], statements
- Multidimensional Expressions [Analysis Services], queries
- MDX [Analysis Services], statements
- MDX queries [Analysis Services]
- MDX [Analysis Services], queries
- queries [MDX]
ms.assetid: a560383b-bb58-472e-95f5-65d03d8ea08b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 42c4d8581374c9805c28ce577249995427fd5c7e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66073887"
---
# <a name="mdx-query-fundamentals-analysis-services"></a>MDX 쿼리 기본 사항(Analysis Services)
  MDX를 사용하면 큐브와 같은 다차원 개체를 쿼리하여 큐브의 데이터를 포함하는 다차원 셀 집합을 반환할 수 있습니다. 이 항목 및 하위 항목에서는 MDX 쿼리에 대한 개요를 제공합니다.  
  
 다음 항목에서는 MDX 쿼리 및 쿼리가 만드는 셀 집합에 대해 설명하고 기본적인 MDX 구문에 대한 자세한 정보를 제공합니다.  
  
> [!NOTE]  
>  MDX 쿼리 및 계산과 관련 된 성능 문제에 대 한 자세한 내용은 [SQL Server 2005 Analysis Services 성능 가이드](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide)의 "효율적인 MDX 작성" 섹션을 참조 하십시오.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[MDX &#40;기본 MDX 쿼리&#41;](mdx-query-the-basic-query.md)|MDX SELECT 문의 기본 구문에 대한 정보를 제공합니다.|  
|[쿼리 및 Slicer 축을 사용 하 여 쿼리를 제한 &#40;MDX&#41;](mdx-query-and-slicer-axes-restricting-the-query.md)|쿼리 및 slicer 축의 의미 및 지정 방법을 설명합니다.|  
|[MDX&#41;&#40;쿼리에 큐브 컨텍스트 설정](establishing-cube-context-in-a-query-mdx.md)|MDX SELECT 문에서 FROM 절을 사용하는 목적을 설명합니다.|  
|[Mdx &#40;명명 된 집합 작성 MDX&#41;](mdx-named-sets-building-named-sets.md)|MDX에서 명명된 집합을 사용하는 목적과 MDX 쿼리에서 명명된 집합을 만들고 사용하는 데 필요한 기술을 설명합니다.|  
|[Mdx로 계산 멤버 작성 &#40;MDX&#41;](mdx-calculated-members-building-calculated-members.md)|MDX의 계산 멤버에 대해 설명하고 MDX 식에서 계산 멤버를 만들고 사용하는 데 필요한 기술을 설명합니다.|  
|[Mdx로 셀 계산 작성 &#40;MDX&#41;](../../multidimensional-models-olap-logical-cube-objects/calculations.md)|계산 셀을 만들고 사용하는 과정을 설명합니다.|  
|[MDX&#41;&#40;속성 값 만들기 및 사용](../../creating-and-using-property-values-mdx.md)|차원, 수준, 멤버 및 셀 속성을 만들고 사용하는 과정을 설명합니다.|  
|[MDX&#41;데이터 &#40;조작](mdx-data-manipulation-manipulating-data.md)|드릴스루 및 롤업을 사용하는 데이터 조작법에 대한 기본 지식 및 MDX의 패스 순서 및 계산 순서를 설명합니다.|  
|[MDX&#41;데이터 &#40;수정](mdx-data-modification-modifying-data.md)|쓰기 저장(writeback)을 사용하여 다차원 데이터를 일시적 또는 영구적으로 변경하는 방법을 설명합니다.|  
|[변수 및 매개 변수를 사용 하 여 MDX &#40;&#41;](using-variables-and-parameters-mdx.md)|MDX 쿼리에서 변수와 매개 변수를 사용하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [MDX&#41; 참조 &#40;다차원 식](/sql/mdx/multidimensional-expressions-mdx-reference)  
  
  
