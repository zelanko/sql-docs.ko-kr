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
manager: kfile
ms.openlocfilehash: a2ed3251b5bf8bc17e832f87947cfc41231d35c0
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743432"
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
  
 *재귀*  
 선택 사항입니다. 집합의 재귀 비교를 나타내는 키워드입니다. **ToggleDrillState** 함수는의 조합 된 **DrillupMember** 및 **DrilldownMember** 함수입니다. 재귀 멤버 중인 경우에 적용 된 **DrilldownMember** 상태입니다.  
  
 *Include_calc_members*  
 선택 사항입니다. 드릴다운 수준에서 계산된 구성원 포함 여부(존재하는 경우)를 나타내는 플래그입니다.  
  
## <a name="remarks"></a>Remarks  
 **ToggleDrillState** 함수는 첫 번째 집합에 있는 두 번째 집합의 각 멤버의 드릴 상태를 토글합니다. 첫 번째 집합에는 모든 차원의 튜플이 포함될 수 있지만 두 번째 집합에는 단일 차원의 멤버만 포함되어야 합니다. **ToggleDrillState** 함수는의 조합 된 **DrillupMember** 및 **DrilldownMember** 함수입니다. 경우 멤버를 *m*, 두 번째 집합은 첫 번째 집합에 나타나는 및 해당 멤버는 드릴 다운 됩니다 (즉,에 바로 뒤에 하위 항목이) 다음 `DrillupMember(Set_Expression1, {m})` 첫 번째 집합의 튜플 또는 멤버에 적용 됩니다. 경우 해당 *m* 멤버가 드릴업 (즉,의 하위 항목이 없는 *m* 바로 다음에 오는 *m*), `DrilldownMember(Set_Expression1, {m}[, RECURSIVE])` 첫 번째 집합에 적용 됩니다.  
  
 경우 선택적 **재귀** 플래그를 사용, 드릴업과 드릴 다운이 재귀적으로 적용된 됩니다. 재귀 플래그에 대 한 자세한 내용은 참조는 [DrillupMember](../mdx/drillupmember-mdx.md) 및 [DrilldownMember](../mdx/drilldownmember-mdx.md) 함수입니다.  
  
 XMLA 속성 MdpropMdxDrillFunctions 쿼리는 서버에서 드릴 함수;에 제공 하는 지원 수준을 확인할 수 있습니다. 참조 [XMLA 속성 지원 &#40;XMLA&#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) 세부 정보에 대 한 합니다.  
  
 참조 [데이터베이스 저널: MDX 집합 함수: Toggledrillstate () 함수](http://go.microsoft.com/fwlink/?LinkId=517759) 시나리오 및 예제를 보려면이이 함수와 관련 된 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
