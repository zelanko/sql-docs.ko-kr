---
title: DrilldownLevelBottom (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2ddfb32ec5d7d5fb93e6dff12c41e56a7f789604
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970064"
---
# <a name="drilldownlevelbottom-mdx"></a>DrilldownLevelBottom(MDX)


  집합의 가장 아래쪽 구성원을 지정한 수준에서 한 수준 아래로 드릴다운합니다.  
  
## <a name="syntax"></a>구문  
  
```  
DrilldownLevelBottom(Set_Expression, Count [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *개수*  
 반환할 튜플 수를 지정하는 유효한 숫자 식입니다.  
  
 *Level_Expression*  
 수준을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression*  
 (선택 사항) 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
 *Include_Calc_Members*  
 (선택 사항) 계산 멤버를 드릴다운 결과에 추가하는 키워드입니다.  
  
## <a name="remarks"></a>설명  
 숫자 식이 지정 된 경우 **DrilldownLevelBottom** 함수는 자식 멤버 집합에 대해 평가 되는 지정 된 값에 따라 지정 된 집합에 있는 각 멤버의 자식을 오름차순으로 정렬 합니다. 숫자 식이 지정되지 않은 경우 이 함수는 쿼리 컨텍스트에서 확인된 대로 자식 구성원 집합이 나타내는 셀의 값에 따라 지정된 집합에 있는 각 구성원의 자식을 오름차순으로 정렬합니다. 이 동작은 구성원 집합을 정렬하지 않고 일반적인 순서로 반환하는 BottomCount 및 Tail(MDX) 함수와 비슷합니다.  
  
 정렬 후 **DrilldownLevelBottom** 함수는 부모 멤버가 포함 된 집합과 *Count*에 지정 된 자식 멤버의 수를 가장 낮은 값으로 반환 합니다.  
  
 **DrilldownLevelBottom** 함수는 [DrilldownLevel](../mdx/drilldownlevel-mdx.md) 함수와 비슷하지만 지정 된 수준에서 각 멤버에 대 한 모든 자식을 포함 하는 대신 **DrilldownLevelBottom** 함수는 최하위 수의 자식 멤버를 반환 합니다.  
  
 XMLA 속성 MdpropMdxDrillFunctions를 쿼리하면 서버에서 드릴링 함수에 대해 제공 하는 지원 수준을 확인할 수 있습니다. 자세한 내용은 [지원 되는 Xmla 속성 &#40;xmla&#41;](https://docs.microsoft.com/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 를 참조 하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 기본 측정값을 기준으로 Product Category 수준에서 하위 세 개의 자식을 반환합니다. Adventure Works 샘플 큐브에서 Accessories의 맨 아래 세 하위는 Tires and Tubes, Pumps 및 Panniers입니다. Management Studio의 MDX 쿼리 창에서 Products | Product Categories | Members | All Products | Accessories로 이동하여 전체 목록을 볼 수 있습니다. Count 인수를 늘려 더 많은 구성원을 반환할 수 있습니다.  
  
```  
SELECT DrilldownLevelBottom   
   ([Product].[Product Categories].children,  
   3,  
   [Product].[Product Categories].[Category])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 다음 예에서는 드릴 다운 수준에 계산 멤버를 포함 하는 데 사용 되는 **include_calc_members** 플래그를 사용 하는 방법을 보여 줍니다. 측정값이 해당 측정값으로 정렬 되도록 하기 위해 [재판매인 Order Count] 측정값이 **DrilldownLevelBottom** 문에 추가 됩니다. 계산된 구성원을 보려면 Count를 적어도 9까지 늘려야 합니다.  
  
```  
WITH MEMBER   
[Product].[Product Categories].[Category].&[3].[Premium Clothes] AS  
[Product].[Product Categories].[Subcategory].&[18] +  
[Product].[Product Categories].[Subcategory].&[21]  
SELECT [Measures].[Reseller Order Count] ON 0,  
DRILLDOWNLEVELBOTTOM(  
  [Product].[Product Categories].children ,  
  9,  
  [Product].[Product Categories].[Category] ,  
  [Measures].[Reseller Order Count],  
  INCLUDE_CALC_MEMBERS ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
