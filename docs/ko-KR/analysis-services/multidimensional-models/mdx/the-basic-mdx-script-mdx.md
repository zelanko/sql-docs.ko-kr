---
title: 기본 MDX 스크립트 (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f7b6971037be41c0aabcc310940b597dda2ed950
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="the-basic-mdx-script-mdx"></a>기본 MDX 스크립트(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  MDX(Multidimensional Expressions) 스크립트는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에 있는 큐브에 대한 계산 프로세스를 정의합니다. 다음과 같은 두 가지 유형의 MDX 스크립트가 있습니다.  
  
 **기본 MDX 스크립트**  
 큐브를 만드는 시점에 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 는 해당 큐브에 대해 기본 MDX 스크립트를 만듭니다. 이 스크립트는 전체 큐브에 대한 계산 패스를 정의합니다.  
  
 **사용자 정의 MDX 스크립트**  
 큐브를 만든 후 큐브의 계산 기능을 확장하는 사용자 정의 MDX 스크립트를 추가할 수 있습니다.  
  
## <a name="the-default-mdx-script"></a>기본 MDX 스크립트  
 큐브를 정의할 때 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 가 만드는 기본 MDX 스크립트는 단 하나의 CALCULATE 문을 포함합니다. 이 단일 CALCULATE 문은 기본 MDX 스크립트 시작 부분에 있고 첫 번째 계산 패스 중에 전체 큐브를 계산해야 함을 나타냅니다.  
  
 또한 기본 MDX 스크립트에는 큐브 디자이너에서 만든 명명된 집합, 대입 식 및 계산 멤버를 만드는 스크립트 명령도 포함됩니다.  
  
-   [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]는 기본 MDX 스크립트에 스크립트 명령을 직접 추가합니다.  
  
-   큐브에 있는 각각의 명명된 집합의 경우 해당 CREATE SET 문이 기본 MDX 스크립트에 존재합니다.  
  
-   큐브에서 정의한 각각의 계산 멤버의 경우 해당 CREATE MEMBER 문이 기본 MDX 스크립트에 존재합니다.  
  
 큐브 디자이너의 **계산** 탭을 사용하여 기본 MDX 스크립트에 있는 스크립트 명령, 명명된 집합 및 계산 멤버의 순서를 제어할 수 있습니다. 기본 MDX 스크립트에 저장된 계산 정의에 대한 자세한 내용은 [다차원 모델의 계산](../../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)을 참조하세요.  
  
 큐브와 연결된 MDX 스크립트가 없는 경우 큐브는 기본 MDX 스크립트를 사용합니다. 큐브는 MDX 스크립트에 따라 계산 동작을 결정하므로 큐브는 최소한 하나 이상의 MDX 스크립트와 연결되어야 합니다. 즉, MDX 스크립트와 연결되지 않았거나 빈 MDX 스크립트와 연결된 큐브는 어떤 셀도 계산하지 못할뿐더러 계산하지 않습니다. ASSL(Analysis Services Scripting Language) 명령 또는 AMO(Analysis Management Objects)를 사용하여 프로그래밍 방식으로 큐브를 만드는 경우에는 해당 큐브에 대해 단일 CALCULATE 문을 포함한 기본 MDX 스크립트를 만드는 것이 좋습니다.  
  
## <a name="mdx-script-content"></a>MDX 스크립트 내용  
 MDX 스크립트는 다음 문과 식을 포함할 수 있습니다.  
  
 모든 MDX 스크립팅 문  
 MDX 스크립트에서 MDX 스크립팅 문은 계산의 컨텍스트 및 범위를 제어하고 MDX 스크립트에 있는 다른 문의 동작을 관리합니다. 이 범주에는 다음 문이 포함됩니다.  
  
-   [계산](../../../mdx/mdx-scripting-calculate.md)  
  
-   [고정](../../../mdx/mdx-scripting-freeze.md)  
  
-   [범위](../../../mdx/mdx-scripting-scope.md)  
  
 MDX 스크립팅 문에 대한 자세한 내용은 [MDX 스크립팅 문&#40;MDX&#41;](../../../mdx/mdx-scripting-statements-mdx.md)을 참조하세요.  
  
 [멤버 만들기](../../../mdx/mdx-data-definition-create-member.md)  
 CREATE MEMBER 문은 계산 멤버를 만듭니다. 계산 멤버 작성 방법에 대한 자세한 내용은 [계산 멤버를 MDX로 작성&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md)을 참조하세요.  
  
 [집합 만들기](../../../mdx/mdx-data-definition-create-set.md)  
 CREATE SET 문은 명명된 집합을 만듭니다. 명명된 집합을 만드는 방법에 대한 자세한 내용은 [명명된 집합을 MDX로 작성&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md)을 참조하세요.  
  
 조건문  
 조건문은 MDX 스크립트에 조건부 논리를 추가합니다. 이 범주로는 [CASE](../../../mdx/case-statement-mdx.md) 및 [IF](../../../mdx/mdx-scripting-if.md) 문이 포함됩니다.  
  
 대입 식  
 대입 식은 제약이 있는 하위 큐브에 값과 같이 식을 대입합니다. 제약이 있는 하위 큐브 식은 MDX 스크립트 내에 있는 하위 큐브의 "가장자리"를 정의하는 제약이 있는 집합 식의 컬렉션입니다. 다음 코드에서는 제약이 있는 하위 큐브 식에 대한 구문을 보여 줍니다.  
  
```  
<Constrained subcube> ::= (   
    ( <Constrained set> [<Crossjoin operator> <Constrained set>...] |  
    <ROOT function> |  
    <TREE function> |  
    LEAVES() |  
    * ) [, <Constrained subcube>...]  
<Constrained set> ::=   
    <Natural hierarchy>.MEMBERS |   
    <Natural hierarchy>.LEVEL(<numeric expression>).MEMBERS |   
    { <Natural hierarchy member> } |   
    DESCENDANTS( <Natural hierarchy member>, <Level expression>, ( SELF | AFTER | SELF_AND_AFTER ) ) |   
    DESCENDANTS( <Natural hierarchy member>, , LEAVES )  
<Natural hierarchy> ::= <Hierarchy identifier>  
<Natural hierarchy member> ::= <Natural hierarchy>.<identifier>[.<identifier>...]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 언어 참조 & #40; Mdx& #41;](../../../mdx/mdx-language-reference-mdx.md)   
 [MDX 스크립팅 기본 사항 & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
  
