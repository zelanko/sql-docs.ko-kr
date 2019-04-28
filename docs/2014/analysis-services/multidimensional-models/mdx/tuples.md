---
title: 튜플 | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 35b629ae-b1ef-44b1-b556-96956aeb56e7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8e6565d727ad6fd3f11e2332f53e32fb2c942687
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62725167"
---
# <a name="tuples"></a>튜플
  튜플은 큐브의 데이터 조각을 고유하게 식별합니다. 동일한 계층에 속하는 둘 이상의 멤버가 없는 경우 튜플은 차원 멤버의 조합으로 구성됩니다.  
  
## <a name="implicit-or-default-attribute-members-in-a-tuple"></a>튜플의 암시적 또는 기본 특성 멤버  
 MDX 쿼리 또는 식에서 튜플을 정의할 때 각 특성 계층의 특성 멤버를 명시적으로 포함할 필요는 없습니다. 쿼리나 식에 특성 계층의 멤버가 명시적으로 포함되어 있지 않으면 해당 특성 계층의 기본 멤버가 암시적으로 튜플에 포함됩니다. 큐브에 명시적으로 달리 정의되어 있지 않고 (All) 멤버가 있는 경우 모든 특성 계층의 기본 멤버는 (All) 멤버입니다. 특성 계층 내에 (All) 멤버가 없는 경우 기본 멤버는 해당 특성 계층의 최상위 수준 멤버입니다. 또한 기본 측정값이 명시적으로 정의되지 않은 경우 큐브에 지정된 첫 번째 측정값이 기본 측정값이 됩니다. 자세한 내용은 [기본 멤버 정의](../attribute-properties-define-a-default-member.md) 및 [DefaultMember&#40;MDX&#41;](/sql/mdx/defaultmember-mdx)를 참조하세요.  
  
 예를 들어 다음 튜플은 Adventure Works 데이터베이스에서 Measures 차원의 단일 멤버만을 명시적으로 정의하여 단일 셀을 식별합니다.  
  
```  
(Measures.[Reseller Sales Amount])  
```  
  
 이 예에서는 Measures 차원의 Reseller Sales Amount 멤버와 큐브에 있는 각 특성 계층의 기본 멤버로 구성된 셀을 고유하게 식별합니다. Destination Currency 특성 계층을 제외한 모든 특성 계층의 기본 멤버는 (All) 멤버입니다. Destination Currency 계층의 기본 멤버는 US Dollar 멤버입니다. 이 기본 멤버는 Adventure Works 큐브에 대한 MDX 스크립트에 정의되어 있습니다.  
  
 다음 쿼리에서는 앞의 예에서 지정한 튜플이 참조하는 셀의 값($80,450.596.98)을 반환합니다.  
  
```  
SELECT   
Measures.[Reseller Sales Amount] ON COLUMNS   
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  쿼리에서 집합(이 경우 단일 튜플로 구성)의 축을 지정할 때는 먼저 열 집합 축을 지정한 후 행 집합 축을 지정해야 합니다. 열 축은 *axis(0)* 또는 간단히 *0*으로도 참조할 수 있습니다. MDX 쿼리에 대한 자세한 내용은 [기본 MDX 쿼리&#40;MDX&#41;](mdx-query-the-basic-query.md)를 참조하세요.  
  
### <a name="tuples-as-values-or-member-references"></a>값 또는 멤버 참조인 튜플  
 앞의 예에서처럼 쿼리에 튜플을 사용하여 해당 튜플이 참조하는 셀의 값을 반환할 수 있습니다. 또는 식에 튜플을 사용하여 해당 튜플에 지정된 멤버를 명시적으로 참조할 수 있습니다. 쿼리나 식에서는 튜플을 반환하거나 구성하는 함수를 이용할 수 있습니다. 튜플을 사용하면 해당 튜플이 지정하는 셀의 값을 참조할 수 있으며 튜플을 함수에 사용할 경우에는 멤버의 조합을 지정할 수 있습니다.  
  
### <a name="tuple-dimensionality"></a>튜플 차원  
 튜플의 *차원* 은 해당 튜플에서 멤버가 나타나는 순서 또는 시퀀스를 나타냅니다. 암시적 멤버는 항상 동일한 순서로 나타나므로 차원은 대개 튜플에 명시적으로 정의된 멤버의 측면에서 생각할 수 있습니다. 튜플 집합을 정의할 때는 튜플의 멤버 순서가 중요합니다. 다음 예에서는 튜플의 두 멤버를 열 축에 포함합니다.  
  
```  
SELECT   
([Measures].[Reseller Sales Amount],[Date].[Calendar Year].[CY 2004]) ON COLUMNS   
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  둘 이상의 차원에서 튜플의 멤버를 명시적으로 지정할 때는 튜플 전체를 괄호로 묶어야 합니다. 튜플의 단일 멤버만 지정할 때는 괄호로 묶지 않아도 됩니다.  
  
 앞의 예에 나온 쿼리의 튜플은 Measures 차원의 Reseller Sales Amount 측정값과 Date 차원의 Calendar Year 특성 계층 중 CY 2004 멤버가 교차하는 지점의 큐브 셀을 반환하도록 지정합니다.  
  
> [!NOTE]  
>  특성 멤버는 멤버 이름이나 멤버 키로 참조할 수 있습니다. 앞의 예에서 [CY 2004]에 대한 참조는 &[2004]로 바꿀 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDX의 주요 개념&#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)   
 [큐브 공간](cube-space.md)   
 [Autoexists](autoexists.md)   
 [멤버, 튜플 및 집합 작업&#40;MDX&#41;](working-with-members-tuples-and-sets-mdx.md)  
  
  
