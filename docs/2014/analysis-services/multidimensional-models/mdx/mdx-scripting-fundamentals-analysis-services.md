---
title: MDX 스크립팅 기본 사항 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], scripts
- calculations [Analysis Services], scripts
- MDX [Analysis Services], scripts
- scripts [MDX]
- cubes [Analysis Services], calculations
- Multidimensional Expressions [Analysis Services], scripts
ms.assetid: fdecb3ce-7c87-4bab-8000-532ba7a29f96
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e4bb0ae80034108a423349cd1bffead3f40a349f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62725327"
---
# <a name="mdx-scripting-fundamentals-analysis-services"></a>MDX 스크립팅 기본 사항(Analysis Services)
   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 MDX(Multidimensional Expressions) 스크립트는 계산으로 큐브를 채우는 한 개 이상의 MDX 식 또는 문으로 구성됩니다.  
  
 MDX 스크립트는 큐브의 계산 프로세스를 정의합니다. MDX 스크립트는 또한 큐브 자체의 일부로 간주됩니다. 따라서 큐브와 관련된 MDX 스크립트를 변경하면 해당 큐브의 계산 프로세스가 즉시 변경됩니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]의 큐브 디자이너에서 MDX 스크립트를 작성할 수 있습니다. 자세한 내용은 [할당 및 기타 스크립트 명령 정의](../define-assignments-and-other-script-commands.md) 및 [Microsoft SQL Server 2005의 MDX 스크립팅 소개](https://go.microsoft.com/fwlink/?LinkId=81892)를 참조하세요.  
  
 MDX 쿼리 및 계산과 관련된 성능 문제에 대한 자세한 내용은 [SQL Server Analysis Services 성능 가이드](https://go.microsoft.com/fwlink/p/?LinkId=399050)(영문)의 MDX 최적화 섹션을 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[기본 MDX 스크립트 & #40; Mdx& #41;](the-basic-mdx-script-mdx.md)|각 큐브에서 제공되는 기본 MDX 스크립트 및 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 큐브 안에서 MDX 스크립트가 작동하는 방식을 포함하여 기본 MDX 스크립트에 대해 설명합니다.|  
|[범위 및 컨텍스트 관리&#40;MDX&#41;](managing-scope-and-context-mdx.md)|[CALCULATE](/sql/mdx/mdx-scripting-calculate) 문, [SCOPE](/sql/mdx/mdx-scripting-scope) 문, 그리고 [This](/sql/mdx/this-mdx) 함수를 사용하여 MDX 스크립트에서 컨텍스트 및 범위를 관리하는 방법을 설명합니다.|  
|[변수 및 매개 변수 사용&#40;MDX&#41;](using-variables-and-parameters-mdx.md)|MDX 스크립트에서 변수 및 매개 변수를 사용하는 방법을 설명합니다.|  
|[오류 처리&#40;MDX&#41;](error-handling-mdx.md)|MDX 스크립트 내의 오류 처리 방법을 설명합니다.|  
|[지원되는 MDX&#40;MDX&#41;](supported-mdx-mdx.md)|MDX 스크립트에서 지원되는 MDX 연산자, 문 및 함수 목록을 제공합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [MDX 언어 참조&#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)  
  
  
