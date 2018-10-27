---
title: DrilldownMemberTop (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3dd1128bfafb052936e742f7ce56529b1222333a
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145258"
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
  
 *Hierarchy*  
 계층을 반환하는 유효한 MDX 식입니다.  
  
 *재귀*  
 집합의 재귀 비교를 나타내는 키워드입니다.  
  
 *Include_Calc_Members*  
 계산 멤버를 드릴다운 결과에 포함할 수 있게 하는 키워드입니다.  
  
## <a name="remarks"></a>Remarks  
 숫자 식이 지정 되는 **DrilldownMemberTop** 일련의 자식에 대해 계산 된 숫자 식의 값에 따라 첫 번째 집합의 각 멤버의 자식을 차례로 내림차순 정렬 함수 멤버입니다. 숫자 식이 지정되지 않은 경우 이 함수는 쿼리 컨텍스트에서 확인된 대로 자식 멤버 집합이 나타내는 셀의 값에 따라 첫 번째 집합에 있는 각 멤버의 자식을 내림차순으로 정렬합니다. 이 동작은 멤버 집합을 정렬하지 않고 일반적인 순서로 반환하는 TopCount 및 Head(MDX) 함수와 비슷합니다.  
  
 정렬 후 합니다 **DrilldownMemberTop** 함수에 지정 된 자식 멤버의 수 및 부모 멤버를 포함 하는 집합을 반환 *개수* 두 집합 모두에 포함 되며 가장 높은 값을 사용 하 여 .  
  
 하는 경우 **재귀** 함수 앞에서 설명한 대로 첫 번째 집합을 정렬 한 다음 두 번째 집합에 대 한 계층에 구성 된 대로 반복 해 서 첫 번째 집합의 멤버를 비교 된*합니다.* 함수는 최상위도 두 번째 집합에 있는 첫 번째 집합의 각 멤버에 대 한 자식 수를 검색 합니다.  
  
 첫 번째 집합에는 멤버 대신 튜플이 포함될 수 있습니다. 튜플 드릴다운은 멤버 대신 튜플 집합을 반환하는 OLE DB의 확장 기능입니다.  
  
 합니다 **DrilldownMemberTop** 함수는 비슷합니다는 [DrilldownMember](../mdx/drilldownmember-mdx.md) 하지만 두 번째 집합에는 에표시되는첫번째집합의각멤버에대해모든자식을포함하는대신**DrilldownMemberTop** 함수 맨 위에 있는 각 멤버에 대 한 자식 멤버 수를 반환 합니다.  
  
 서버에서 드릴 함수;에 제공 하는 지원 수준을 확인할 수 있습니다는 XMLA 속성 MdpropMdxDrillFunctions를 쿼리 합니다. 참조 [지원 되는 XMLA 속성 &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 세부 정보에 대 한 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
