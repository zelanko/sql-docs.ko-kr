---
description: DrilldownMemberTop(MDX)
title: DrilldownMemberTop (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d90c382ca34316225760c1a25288034ba26ab726
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193506"
---
# <a name="drilldownmembertop-mdx"></a>DrilldownMemberTop(MDX)


  지정한 집합의 멤버 중 두 번째 지정한 집합에 있는 멤버를 드릴다운합니다. 결과 집합은 지정된 멤버 수로 제한됩니다. 또는 첫 번째 튜플 계층이나 선택적으로 지정된 계층을 사용하여 튜플 집합을 드릴다운합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DrillDownMemberTop(<Set_Expression1>, <Set_Expression2>, <Count> [,[<Numeric_Expression>] [,[<Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression1*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Set_Expression2*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Count*  
 반환할 튜플 수를 지정하는 유효한 숫자 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
 *계층 구조*  
 계층을 반환하는 유효한 MDX 식입니다.  
  
 *폴더*  
 집합의 재귀 비교를 나타내는 키워드입니다.  
  
 *Include_Calc_Members*  
 계산 멤버를 드릴다운 결과에 포함할 수 있게 하는 키워드입니다.  
  
## <a name="remarks"></a>설명  
 숫자 식이 지정 된 경우 **DrilldownMemberTop** 함수는 자식 멤버 집합에 대해 계산 된 숫자 식의 값에 따라 첫 번째 집합에 있는 각 멤버의 자식을 내림차순으로 정렬 합니다. 숫자 식이 지정되지 않은 경우 이 함수는 쿼리 컨텍스트에서 확인된 대로 자식 멤버 집합이 나타내는 셀의 값에 따라 첫 번째 집합에 있는 각 멤버의 자식을 내림차순으로 정렬합니다. 이 동작은 멤버 집합을 정렬하지 않고 일반적인 순서로 반환하는 TopCount 및 Head(MDX) 함수와 비슷합니다.  
  
 정렬 후 **DrilldownMemberTop** 함수는 부모 멤버가 포함 된 집합과 *Count* 에 지정 된 자식 멤버의 수를 반환 합니다 .이 집합은 가장 높은 값을 가지 며 두 집합에 모두 포함 됩니다.  
  
 **RECURSIVE** 가 지정 된 경우 함수는 앞에서 설명한 대로 첫 번째 집합을 정렬 한 다음 계층에 구성 된 대로 첫 번째 집합의 멤버를 두 번째 집합에 대해 재귀적으로 비교 합니다. 함수는 첫 번째 집합에서 두 번째 집합에도 있는 각 멤버에 대 한 최상위 자식의 수를 검색 합니다.  
  
 첫 번째 집합에는 멤버 대신 튜플이 포함될 수 있습니다. 튜플 드릴다운은 멤버 대신 튜플 집합을 반환하는 OLE DB의 확장 기능입니다.  
  
 **DrilldownMemberTop** 함수는 [DrilldownMember](../mdx/drilldownmember-mdx.md) 함수와 유사 하지만 첫 번째 집합의 각 멤버에 대해 두 번째 집합에도 있는 모든 자식을 포함 하는 대신 **DrilldownMemberTop** 함수는 각 멤버에 대 한 최상위 자식 멤버 수를 반환 합니다.  
  
 XMLA 속성 MdpropMdxDrillFunctions를 쿼리하면 서버에서 드릴링 함수에 대해 제공 하는 지원 수준을 확인할 수 있습니다. 자세한 내용은 [지원 되는 Xmla 속성 &#40;xmla&#41;](/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 를 참조 하세요.  
  
## <a name="example"></a>예제  
 다음 예제에서는 의류 범주로 드릴다운하여 운송된 주문 수량이 가장 많은 의류의 세 하위 범주를 반환합니다.  
  
```  
SELECT DrilldownMemberTop   ({[Product].[Product Categories].[All Products],        
[Product].[Product Categories].[Category].Bikes,        
[Product].[Product Categories].[Category].Clothing},     
{[Product].[Product Categories].[Category].Clothing},     
3,     
[Measures].[Reseller Order Quantity])     
ON 0     
FROM [Adventure Works]     
WHERE [Measures].[Reseller Order Quantity]  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
