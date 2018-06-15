---
title: MDX 스크립팅 기본 사항 (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9ca77b9c10f1dba24127e35e5fe55d7ffcdad3dc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34021730"
---
# <a name="mdx-scripting-fundamentals-analysis-services"></a>MDX 스크립팅 기본 사항(Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 MDX(Multidimensional Expressions) 스크립트는 계산으로 큐브를 채우는 한 개 이상의 MDX 식 또는 문으로 구성됩니다.  
  
 MDX 스크립트는 큐브의 계산 프로세스를 정의합니다. MDX 스크립트는 또한 큐브 자체의 일부로 간주됩니다. 따라서 큐브와 관련된 MDX 스크립트를 변경하면 해당 큐브의 계산 프로세스가 즉시 변경됩니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]의 큐브 디자이너에서 MDX 스크립트를 작성할 수 있습니다. 자세한 내용은 [할당 및 기타 스크립트 명령 정의](../../../analysis-services/multidimensional-models/define-assignments-and-other-script-commands.md) 및 [Microsoft SQL Server 2005의 MDX 스크립팅 소개](http://go.microsoft.com/fwlink/?LinkId=81892)를 참조하세요.  
  
 MDX 쿼리 및 계산과 관련된 성능 문제에 대한 자세한 내용은 [SQL Server Analysis Services 성능 가이드](http://go.microsoft.com/fwlink/p/?LinkId=399050)(영문)의 MDX 최적화 섹션을 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[기본 MDX 스크립트 & #40; Mdx& #41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)|각 큐브에서 제공되는 기본 MDX 스크립트 및 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 큐브 안에서 MDX 스크립트가 작동하는 방식을 포함하여 기본 MDX 스크립트에 대해 설명합니다.|  
|[관리 범위 및 컨텍스트 & #40; Mdx& #41;](../../../analysis-services/multidimensional-models/mdx/managing-scope-and-context-mdx.md)|[CALCULATE](../../../mdx/mdx-scripting-calculate.md) 문, [SCOPE](../../../mdx/mdx-scripting-scope.md) 문, 그리고 [This](../../../mdx/this-mdx.md) 함수를 사용하여 MDX 스크립트에서 컨텍스트 및 범위를 관리하는 방법을 설명합니다.|  
|[변수 및 매개 변수 사용 & #40;를 사용 하 여 Mdx& #41;](../../../analysis-services/multidimensional-models/mdx/using-variables-and-parameters-mdx.md)|MDX 스크립트에서 변수 및 매개 변수를 사용하는 방법을 설명합니다.|  
|[오류 처리 & #40; Mdx& #41;](../../../analysis-services/multidimensional-models/mdx/error-handling-mdx.md)|MDX 스크립트 내의 오류 처리 방법을 설명합니다.|  
|[지원 되는 MDX & #40; Mdx& #41;](../../../analysis-services/multidimensional-models/mdx/supported-mdx-mdx.md)|MDX 스크립트에서 지원되는 MDX 연산자, 문 및 함수 목록을 제공합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 언어 참조 & #40; Mdx& #41;](../../../mdx/mdx-language-reference-mdx.md)  
  
  
