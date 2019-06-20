---
title: DrilldownMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f5ab4ee77bad08ab3883645ad5e2628a265aa4e9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62691075"
---
# <a name="drilldownmember-mdx"></a>DrilldownMember(MDX)


  지정된 집합의 멤버 중 두 번째 지정한 집합에 나타나는 멤버를 드릴다운합니다.  
  
 또는 첫 번째 튜플 계층이나 선택적으로 지정된 계층을 사용하여 튜플 집합을 드릴다운합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DrillDownMember(<Set_Expression1>, <Set_Expression2> [,[<Target_Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]])  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression1*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Set_Expression2*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Target_Hierarchy*  
 계층을 반환하는 유효한 MDX 식입니다.  
  
 *재귀*  
 집합의 재귀 비교를 나타내는 키워드입니다.  
  
 *Include_Calc_Members*  
 계산 멤버를 드릴다운 결과에 포함할 수 있게 하는 키워드입니다.  
  
## <a name="remarks"></a>Remarks  
 이 함수는 계층별로 정렬된 자식 멤버의 집합을 반환하며, 첫 번째 집합의 지정된 멤버 중 두 번째 집합에도 있는 멤버를 포함시킵니다. 첫 번째 집합에 부모 멤버와 하나 이상의 자식이 포함된 경우 부모 멤버는 드릴다운되지 않습니다. 첫 번째 집합은 어떠한 차원도 될 수 있지만 두 번째 집합은 1차원 집합을 포함해야 합니다. 이때 함수의 결과 집합에 포함되는 모든 자식 멤버가 해당 부모 멤버 바로 아래에 포함된다는 점만 제외하고 첫 번째 집합의 원래 멤버 순서가 유지됩니다. 이 함수는 첫 번째 집합의 멤버 중 두 번째 집합에도 있는 각 멤버에 대해 자식 항목을 검색하여 결과 집합을 구성합니다. 하는 경우 **재귀** 지정 된 경우 함수는 계속 존재 하는 또한 두 번째 집합에 더 이상 될 때까지 결과 집합의 각 멤버의 자식만 검색 결과의 멤버는 두 번째 집합에 대해 설정 하는 재귀적으로 비교 결과 집합의 멤버를 두 번째 집합에 있습니다.  
  
 쿼리 하는 XMLA 속성인 **MdpropMdxDrillFunctions** 서버에서 드릴 함수에 제공 하는 지원 수준을 확인할 수 있도록 참조 하십시오 [지원 되는 XMLA 속성 &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)세부 정보에 대 한 합니다.  
  
 첫 번째 집합에는 멤버 대신 튜플이 포함될 수 있습니다. 튜플 드릴다운은 멤버 대신 튜플 집합을 반환하는 OLE DB의 확장 기능입니다.  
  
> [!IMPORTANT]  
>  바로 다음에 자식 중 하나가 오는 멤버는 드릴다운되지 않습니다. Drilldown * 및 Drillup 집합에서 멤버의 순서가 중요\* 함수 패밀리입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 첫 번째 집합의 멤버 중 두 번째 집합에도 있는 멤버인 Australia로 드릴다운합니다.  
  
```  
SELECT DrilldownMember   
   ( [Geography].[Geography].Children,  
      {[Geography].[Geography].[Country].[Australia],  
        [Geography].[Geography].[State-Province].[New South Wales]}  
   )  
   ON 0  
   FROM [Adventure Works]  
```  
  
 다음 예에서는 첫 번째 집합의 멤버 중 두 번째 집합에도 있는 멤버인 Australia로 드릴다운합니다. 그러나 RECURSIVE 인수가 사용된 경우 이 함수는 결과 집합의 멤버(State-Province 수준의 멤버)를 두 번째 집합과 비교하는 작업을 재귀적으로 계속하여 결과 집합의 멤버(City 수준의 멤버) 중 두 번째 집합에도 있는 각 멤버에 대한 자식 항목을 검색합니다. 이 작업은 두 번째 집합에서 결과 집합의 멤버를 더 이상 찾을 수 없을 때까지 계속됩니다.  
  
```  
SELECT DrilldownMember   
   ( [Geography].[Geography].Children,  
      {[Geography].[Geography].[Country].[Australia],  
        [Geography].[Geography].[State-Province].[New South Wales]}  
   ,RECURSIVE)  
   ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
