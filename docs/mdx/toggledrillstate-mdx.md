---
title: ToggleDrillState (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8d027a76a82de3fd82b6c0c81c54ace08167039b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036615"
---
# <a name="toggledrillstate-mdx"></a>ToggleDrillState(MDX)


  멤버의 드릴 상태를 드릴다운 모드와 드릴업 모드 간에 토글합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ToggleDrillState(Set_Expression1,Set_Expression2 [, [RECURSIVE] [,INCLUDE_CALC_MEMBERS] ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression1*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Set_Expression2*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *폴더*  
 (선택 사항). 집합의 재귀 비교를 나타내는 키워드입니다. **ToggleDrillState** 함수는 **DrillupMember** 및 **DrilldownMember** 함수의 조합입니다. 재귀는 멤버가 **DrilldownMember** 상태인 경우에만 적용 됩니다.  
  
 *Include_calc_members*  
 (선택 사항). 드릴다운 수준에서 계산된 구성원 포함 여부(존재하는 경우)를 나타내는 플래그입니다.  
  
## <a name="remarks"></a>설명  
 **ToggleDrillState** 함수는 첫 번째 집합에 있는 두 번째 집합의 각 멤버에 대 한 드릴 상태를 전환 합니다. 첫 번째 집합에는 모든 차원의 튜플이 포함될 수 있지만 두 번째 집합에는 단일 차원의 멤버만 포함되어야 합니다. **ToggleDrillState** 함수는 **DrillupMember** 및 **DrilldownMember** 함수의 조합입니다. 두 번째 집합의 멤버 *m*이 첫 번째 집합에 있고 해당 멤버가 드릴 다운 된 경우 (즉, 바로 다음에 하위 항목이 있는 경우) `DrillupMember(Set_Expression1, {m})` 는 첫 번째 집합의 멤버나 튜플에 적용 됩니다. *M 멤버가 드릴업* 된 경우 (즉, m 바로 뒤에 오는 *m* 의 하위 항목이 없는 *경우)* `DrilldownMember(Set_Expression1, {m}[, RECURSIVE])` 는 첫 번째 집합에 적용 됩니다.  
  
 선택적 **재귀** 플래그를 사용 하면 드릴업 및 드릴 다운이 재귀적으로 적용 됩니다. 재귀 플래그에 대 한 자세한 내용은 [DrillupMember](../mdx/drillupmember-mdx.md) 및 [DrilldownMember](../mdx/drilldownmember-mdx.md) 함수를 참조 하세요.  
  
 XMLA 속성 MdpropMdxDrillFunctions를 쿼리하면 서버에서 드릴링 함수에 대해 제공 하는 지원 수준을 확인할 수 있습니다. 자세한 내용은 [지원 되는 Xmla 속성 &#40;xmla&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 를 참조 하세요.  
  
 이 함수와 관련 된 시나리오 및 예제 [는 데이터베이스 저널: MDX 집합 함수: ToggleDrillState () 함수](https://go.microsoft.com/fwlink/?LinkId=517759) 를 참조 하세요.  
  
## <a name="example"></a>예제  
 다음 예에서는 첫 번째 집합의 Australia 멤버를 드릴다운하고 첫 번째 집합의 United States 멤버를 드릴업합니다.  
  
```  
SELECT ToggleDrillState  
   ({[Geography].[Geography].[Country].Members, [Geography].[Geography].[Country].&[United States].Children},  
      {[Geography].[Geography].[Country].[Australia]  
      , [Geography].[Geography].[Country].&[United States]}  
      --, recursive  
      --, include_calc_members  
   ) ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
