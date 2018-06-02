---
title: MDX 구문 요소 (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b530205a5165c9be77710bf86e8600174be890dc
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581025"
---
# <a name="mdx-syntax-elements-mdx"></a>MDX 구문 요소(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  MDX에는 대부분의 문에서 사용되거나 문에 영향을 주는 몇 가지 요소가 있습니다.  
  
|용어|정의|  
|----------|----------------|  
|[식별자](../mdx/identifiers-mdx.md)|식별자는 큐브, 차원, 멤버 및 측정값과 같은 개체의 이름입니다.|  
|**데이터 형식**|셀, 멤버 속성 및 셀 속성에 포함되는 데이터 형식을 정의합니다. MDX는 OLE VARIANT 데이터 형식만 지원합니다. VARIANT 데이터 형식의 강제 변환, 변환 및 조작에 대한 자세한 내용은 플랫폼 SDK 설명서에서 "VARIANT 및 VARIANTARG"를 참조하십시오.|  
|[식 &#40;MDX&#41;](../mdx/expressions-mdx.md)|식이란 구문 단위를 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 단일 (스칼라) 값 이나 개체를 확인할 수 있습니다. 식에는 단일 값, 집합 식 등을 반환하는 함수들이 포함됩니다.|  
|[연산자](../mdx/operators-mdx-syntax.md)|연산자는 하나 이상의 간단한 MDX 식으로 더 복잡한 MDX 식을 만드는 구문 요소입니다.|  
|[함수](../mdx/functions-mdx-syntax.md)|함수는 0개 이상의 입력 값을 받고 스칼라 값 또는 개체를 반환하는 구문 요소입니다. 예로 [Sum](../mdx/sum-mdx.md) 여러 값을 추가 하는 것에 대 한 함수는 [멤버](../mdx/members-set-mdx.md) 에서 차원 또는 수준의 멤버 집합을 반환 하기 위한 작동 하 고 있습니다.|  
|[설명](../mdx/comments-mdx-syntax.md)|주석은 문의 용도를 설명하기 위해 MDX 문 또는 스크립트에 삽입하는 텍스트입니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 주석을 실행 하지 않습니다.|  
|[예약 키워드](../mdx/reserved-keywords-mdx-syntax.md)|예약된 키워드는 MDX에서 사용하도록 예약되어 있으며 MDX 문에서 개체 이름으로 사용할 수 없는 단어입니다.|  
|[멤버, 튜플 및 집합](../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)|멤버, 튜플 및 집합은 MDX 쿼리를 만들기 전에 이해해야 할 다차원 데이터의 핵심 개념입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Multidimensional Expression &#40;MDX&#41; 참조](../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
