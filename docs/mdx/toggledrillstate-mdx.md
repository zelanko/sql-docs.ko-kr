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
ms.openlocfilehash: 58acac77e4826855997791476b0602699452b7b8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63228075"
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
 (선택 사항) 집합의 재귀 비교를 나타내는 키워드입니다. **ToggleDrillState** 함수는 조합 합니다 **DrillupMember** 및 **DrilldownMember** 함수입니다. 재귀는 멤버가 하는 경우에 적용 합니다 **DrilldownMember** 상태입니다.  
  
 *Include_calc_members*  
 (선택 사항) 드릴다운 수준에서 계산된 구성원 포함 여부(존재하는 경우)를 나타내는 플래그입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **ToggleDrillState** 함수는 첫 번째 집합에 있는 두 번째 집합의 각 멤버의 드릴 상태를 토글합니다. 첫 번째 집합에는 모든 차원의 튜플이 포함될 수 있지만 두 번째 집합에는 단일 차원의 멤버만 포함되어야 합니다. **ToggleDrillState** 함수는 조합 합니다 **DrillupMember** 및 **DrilldownMember** 함수입니다. 경우는 멤버 *m*, 두 번째 집합은 첫 번째 집합에 나타나는 및 해당 멤버는 드릴 다운 (바로 다음에 하위 항목이 있는,), 다음 `DrillupMember(Set_Expression1, {m})` 멤버나 첫 번째 집합의 튜플에 적용 됩니다. 있는지 *m* 멤버가 드릴업 (즉, 방법이의 하위 항목이 없는 *m* 바로 다음에 오는 *m*), `DrilldownMember(Set_Expression1, {m}[, RECURSIVE])` 첫 번째 집합에 적용 됩니다.  
  
 경우 선택적 **재귀** 플래그를 사용, 드릴업 및 드릴 다운이 재귀적으로 적용된 됩니다. 재귀 플래그에 대 한 자세한 내용은 참조는 [DrillupMember](../mdx/drillupmember-mdx.md) 하 고 [DrilldownMember](../mdx/drilldownmember-mdx.md) 함수입니다.  
  
 서버에서 드릴 함수;에 제공 하는 지원 수준을 확인할 수 있습니다는 XMLA 속성 MdpropMdxDrillFunctions를 쿼리 합니다. 참조 [지원 되는 XMLA 속성 &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 세부 정보에 대 한 합니다.  
  
 참조 [Database Journal: MDX 함수를 설정합니다. Toggledrillstate () 함수](https://go.microsoft.com/fwlink/?LinkId=517759) 시나리오 및이 함수와 관련 된 예제입니다.  
  
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
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
