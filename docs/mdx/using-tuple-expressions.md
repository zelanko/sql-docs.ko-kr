---
title: "튜플 식을 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- single-member tuples [MDX]
- expressions [MDX], tuples
- one-member tuples
- tuples
- implicit tuples
ms.assetid: 0b802b76-9123-405e-ae43-d438754724ba
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f0d24279e896bc71faef81c5901d6d52069b717c
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="using-tuple-expressions"></a>튜플 식 사용
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  튜플은 큐브 내에 포함된 모든 차원에서 하나씩 선택한 멤버로 구성됩니다. 따라서 튜플은 해당 큐브 내의 단일 셀을 고유하게 식별합니다.  
  
> [!NOTE]  
>  잘못된 하나 이상의 멤버를 참조하는 튜플을 빈 튜플이라고 합니다.  
  
 튜플 식별자를 완전히 표현한 식은 다음과 같이 괄호로 둘러싸인 하나 이상의 명시적으로 지정된 멤버로 구성됩니다.  
  
 (*Member_expression* [,*Member_expression* ...])  
  
 튜플은 완전히 정규화하거나 암시적인 멤버를 포함하거나 단일 멤버를 포함할 수 있습니다.  
  
## <a name="tuples-and-implicit-members"></a>튜플과 암시적 멤버  
 한 큐브 내에 포함된 각 차원에서 단일 멤버를 명시적으로 지정하는 튜플을 정규화된 튜플이라고 합니다. 하지만 튜플은 정규화할 필요가 없습니다.  
  
 튜플 내에서 명시적으로 참조하지 않는 차원은 암시적으로 참조합니다. 암시적으로 참조하는 차원에 대한 멤버는 해당 차원의 구조 및 해당 구조 내에 정의된 특성 관계에 따라 다릅니다. 암시적으로 참조하는 계층과 동일한 차원의 계층에 대한 명시적 참조가 있으며 명시적으로 참조하는 계층과 암시적으로 참조하는 계층 간에 직접 또는 간접 관계가 정의되어 있는 경우 튜플은 명시적으로 참조하는 계층의 멤버와 함께 존재하는 암시적으로 참조하는 계층의 멤버를 포함하는 것처럼 작동합니다. 예를 들어 큐브에 City 및 Country 특성을 가진 Customer 차원이 포함되어 있으며 City에 Country가 하나 있고 Country에 City가 많이 있을 수 있도록 이 두 특성 간에 관계가 정의되어 있는 경우 튜플에 'London'이라는 City를 명시적으로 포함하면 'United Kingdom'이라는 Country를 암시적으로 참조하게 됩니다. 그러나 특성 관계가 정의되어 있지 않으며 관계가 반대 방향인 경우(예: City에 Country와의 관계가 있지만 고객의 거주 Country를 아는 것만으로는 해당 고객의 거주 City를 파악할 수 없는 경우) 또는 두 특성 간에 직접 관계가 정의되어 있지 않은 경우(Customer와 City 간의 관계 및 Customer와 Country 간의 관계는 정의되어 있지만 City와 Country 간의 관계는 정의되어 있지 않은 경우) 다음 규칙이 적용됩니다.  
  
-   암시적으로 참조하는 계층에 기본 멤버가 있는 경우 해당 기본 멤버를 튜플에 추가합니다.  
  
-   암시적으로 참조 하는 계층에 기본 멤버가 없는 경우는 **(All)** 기본 계층의 멤버는 사용할 수 있습니다.  
  
-   암시적으로 참조하는 계층에 기본 멤버가 없는 경우 계층의 최상위 수준에 있는 첫 번째 멤버를 사용합니다.  
  
## <a name="one-member-tuples"></a>단일 멤버 튜플  
 튜플 식에 단 하나의 멤버가 있는 경우 MDX는 식을 평가할 목적으로 이 멤버를 단일 멤버 튜플로 변환합니다. 즉, 튜플 식 대신 `[Measures].[TestMeasure]`라는 멤버 식을 쓰면 `( [Measures].[TestMeasure] ).`라는 튜플 식을 쓰는 것과 기능적으로 동일합니다.  
  
## <a name="see-also"></a>참고 항목  
 [식 &#40; Mdx&#41;](../mdx/expressions-mdx.md)   
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

