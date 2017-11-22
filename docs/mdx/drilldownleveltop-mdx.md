---
title: DrilldownLevelTop (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: DRILLDOWNLEVELTOP
dev_langs: kbMDX
helpviewer_keywords: DrilldownLevelTop function
ms.assetid: b3b45dd6-2ade-4dd7-83dd-849231e2e517
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: fae4ccfb75bef024930d6831f5d81b49360b3dbb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="drilldownleveltop-mdx"></a>DrilldownLevelTop(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  집합의 최상위 구성원을 지정한 수준에서 한 수준 아래로 드릴다운합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DrilldownLevelTop(<Set_Expression>, <Count> [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *개수*  
 반환할 튜플 수를 지정하는 유효한 숫자 식입니다.  
  
 *Level_Expression*  
 수준을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
 *Include_Calc_Members*  
 계산 멤버를 드릴다운 결과에 추가하기 위한 키워드입니다.  
  
## <a name="remarks"></a>주의  
 숫자 식이 지정 되는 **DrilldownLevelTop** 내림차순으로 된 숫자 식의 값에 따라 지정된 된 집합의 각 멤버의 자식을 자식 멤버의 집합에 대해 계산 된 정렬 작동 합니다. 숫자 식이 지정되지 않은 경우 이 함수는 쿼리 컨텍스트에서 확인된 대로 자식 구성원 집합이 나타내는 셀의 값에 따라 지정된 집합에 있는 각 구성원의 자식을 내림차순으로 정렬합니다.  
  
 정렬 후는 **DrilldownLevelTop** 함수 부모 멤버와 지정 된 자식 멤버의 수를 포함 하는 집합을 반환 *개수,* 가장 높은 값으로.  
  
 **DrilldownLevelTop** 함수는 비슷합니다는 [DrilldownLevel](../mdx/drilldownlevel-mdx.md) 함수 하지만 지정 된 수준의 각 멤버에 대해 모든 자식을 포함 하는 **DrilldownLevelTop** 함수 맨 위에 있는 자식 멤버 수를 반환 합니다.  
  
 XMLA 속성 MdpropMdxDrillFunctions 쿼리는 서버에서 드릴 함수;에 제공 하는 지원 수준을 확인할 수 있습니다. 참조 [지원 XMLA 속성 &#40; XMLA &#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) 대 한 자세한 내용은 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 기본 측정값을 기준으로 Product Category 수준에서 맨 위에 있는 세 하위를 반환합니다. Adventure Works 샘플 큐브에서 Accessories의 맨 위에 있는 세 하위는 Bike Racks, Bike Stands 및 Bottles and Cages입니다. Management Studio의 MDX 쿼리 창에서 Products | Product Categories | Members | All Products | Accessories로 이동하여 전체 목록을 볼 수 있습니다. Count 인수를 늘려 더 많은 구성원을 반환할 수 있습니다.  
  
```  
SELECT DrilldownLevelTop   
   ([Product].[Product Categories].children,  
   3,  
   [Product].[Product Categories].[Category])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 다음 예제에서는 사용 하 여는 **include_calc_members** 플래그를 드릴 다운 수준에에서 계산된 멤버를 포함 하는 데 사용 합니다. [Reseller Order Count] 측정값에 포함 되어는 **DrilldownLevelTop** 문을 반환 값으로 해당 측정값으로 정렬 되도록 합니다.  
  
```  
WITH MEMBER   
[Product].[Product Categories].[Category].&[3].[Premium Clothes] AS  
[Product].[Product Categories].[Subcategory].&[18] +  
[Product].[Product Categories].[Subcategory].&[21]  
SELECT [Measures].[Reseller Order Count] ON 0,  
DRILLDOWNLEVELTOP(  
  [Product].[Product Categories].children ,  
  2,  
  [Product].[Product Categories].[Category] ,  
  [Measures].[Reseller Order Count],  
  INCLUDE_CALC_MEMBERS ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [DrilldownLevel &#40; Mdx&#41;](../mdx/drilldownlevel-mdx.md)   
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
