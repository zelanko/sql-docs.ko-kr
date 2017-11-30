---
title: Descendants (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: DESCENDANTS
dev_langs: kbMDX
helpviewer_keywords: Descendants function
ms.assetid: d103b0f5-e794-4828-aa57-43f6918a0749
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 6ca101464d62d1a3e07f8d02e457e974b498a3bc
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="descendants-mdx"></a>Descendants(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 수준 또는 거리에서 멤버의 하위 항목 집합을 반환합니다. 다른 수준의 하위 항목은 포함하거나 제외할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member expression syntax using a level expression  
Descendants(Member_Expression [ , Level_Expression [ ,Desc_Flag ] ] )  
  
Member expression syntax using a numeric expression  
Descendants(Member_Expression [ , Distance [ ,Desc_Flag ] ] )  
  
Set expression syntax using a level expression  
Descendants(Set_Expression [ , Level_Expression [ ,Desc_Flag ] ] )  
  
Member expression syntax using a numeric expression  
Descendants(Set_Expression [ , Distance [ ,Desc_Flag ] ] )  
  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Level_Expression*  
 수준을 반환하는 유효한 MDX 식입니다.  
  
 *거리*  
 지정된 멤버와의 거리를 지정하는 유효한 숫자 식입니다.  
  
 *Desc_Flag*  
 가능한 각 하위 항목 집합을 구별할 수 있는 설명 플래그를 지정하는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>주의  
 수준이 지정 된 경우는 **하위 항목** 함수에 지정 된 플래그에 의해 수정 필요에 따라 지정 된 수준에서 지정된 된 집합의 멤버나 지정된 된 멤버의 하위 항목을 포함 하는 집합을 반환 *Desc_Flag*합니다.  
  
 경우 *거리* 지정는 **하위 항목** 함수 수준에서 지정 된 플래그로 수정 필요에 따라, 지정된 된 멤버의 계층 구조에서 지정 된 수 만큼 위에 있는 지정된 된 집합의 멤버 또는 지정된 된 멤버의 하위 항목을 포함 하는 집합을 반환 *Desc_Flag*합니다. 일반적으로 이 함수와 Distance 인수를 사용하면 비정형 계층을 처리할 수 있습니다. 지정된 거리가 0인 경우 이 함수는 지정된 멤버나 지정된 집합으로만 구성된 집합을 반환합니다.  
  
 집합 식이 지정 된 경우는 **하위 항목** 함수는 집합의 각 멤버에 대해 개별적으로 확인 하 고 집합 다시 생성 됩니다. 즉,에 사용 되는 구문에서 **하위 항목** 함수는 MDX 기능적으로 동일 [생성](../mdx/generate-mdx.md) 함수입니다.  
  
 함수에서 사용 되는 수준에 대 한 기본값은 호출 하 여 결정 수준 또는 거리를 지정 하는 경우는 [수준](../mdx/level-mdx.md) 함수 (<\<멤버 >> 합니다. 수준)를 호출 하거나 (멤버가 지정 된 경우) 지정 된 멤버는 **수준** (집합이 지정 된 경우) 지정된 된 집합의 각 멤버에 대해 작동 합니다. 수준 식, 거리 또는 플래그가 지정되지 않은 경우 이 함수가 수행하는 작업은 다음 구문이 사용된 경우와 같습니다.  
  
 `Descendants`  
  
 `(`  
  
 `Member_Expression ,`  
  
 `Member_Expression.Level ,`  
  
 `SELF_BEFORE_AFTER`  
  
 `)`  
  
 수준만 지정되고 설명 플래그는 지정되지 않은 경우 이 함수가 수행하는 작업은 다음 구문이 사용된 경우와 같습니다.  
  
 `Descendants`  
  
 `(`  
  
 `Member_Expression ,`  
  
 `Level_Expression,`  
  
 `SELF`  
  
 `)`  
  
 설명 플래그 값을 변경하여 지정된 수준 또는 거리에서 하위 항목을 포함하거나 제외할 수 있습니다. 지정된 수준 또는 거리의 전/후에 있는 자식(리프 노드까지)은 물론, 지정한 수준이나 거리에 관계없이 리프 자식 항목을 포함 또는 제외할 수 있습니다. 다음 표에서 설명에 허용 되는 플래그는 *Desc_Flag* 인수입니다.  
  
|플래그|Description|  
|----------|-----------------|  
|SELF|지정된 수준 또는 지정된 거리에 있는 하위 멤버만 반환합니다. 이 함수는 지정된 수준이 지정된 멤버의 수준인 경우 지정된 멤버를 포함합니다.|  
|AFTER|지정된 수준에 종속되거나 지정된 거리에 있는 모든 수준의 하위 멤버를 반환합니다.|  
|BEFORE|지정된 멤버와 지정된 수준 사이에 있거나 지정된 거리에 있는 모든 수준의 하위 멤버를 반환합니다. 이 함수는 지정된 멤버만 포함하고 지정된 수준이나 거리의 멤버는 포함하지 않습니다.|  
|BEFORE_AND_AFTER|지정된 멤버의 수준에 종속된 모든 수준의 하위 멤버를 반환합니다. 이 함수는 지정된 멤버만 포함하고 지정된 수준이나 지정된 거리의 멤버는 포함하지 않습니다.|  
|SELF_AND_AFTER|지정된 수준 또는 지정된 거리의 하위 멤버와 지정된 수준에 종속되거나 지정된 거리에 있는 모든 수준의 하위 멤버를 반환합니다.|  
|SELF_AND_BEFORE|지정된 수준 또는 지정된 거리에 있는 하위 멤버와, 지정된 멤버와 지정된 수준 사이 또는 지정된 거리에 있는 모든 수준의 하위 멤버를 반환하며, 지정된 멤버를 포함합니다.|  
|SELF_BEFORE_AFTER|지정된 멤버의 수준에 종속된 모든 수준의 하위 멤버를 반환하며, 지정된 멤버를 포함합니다.|  
|LEAVES|지정된 멤버와 지정된 수준 사이에 있거나 지정된 거리에 있는 리프 하위 멤버를 반환합니다.|  
  
## <a name="examples"></a>예  
 다음 예에서는 지정된 멤버(United States)와 지정된 수준(City)의 이전 수준 멤버 사이에 있는 멤버와 지정된 멤버(United States)를 반환합니다. 이 예에서는 지정된 멤버(United States)와 State-Province 수준(City 수준의 이전 수준)의 멤버를 반환합니다. 이 예에는 이 함수의 다른 인수를 쉽게 테스트할 수 있도록 주석으로 처리된 인수가 포함되어 있습니다.  
  
```  
SELECT Descendants  
   ([Geography].[Geography].[Country].&[United States]  
      //, [Geography].[Geography].[Country]  
   , [Geography].[Geography].[City]  
      //, [Geography].[Geography].Levels (3)  
      //, SELF   
      //, AFTER  
      , BEFORE  
      // BEFORE_AND_AFTER  
      //, SELF_AND_AFTER  
      //, SELF_AND_BEFORE  
      //,SELF_BEFORE_AFTER  
      //,LEAVES   
   ) ON 0  
FROM [Adventure Works]   
```  
  
 일일 평균을 반환 하는 다음 예제는 `Measures.[Gross Profit Margin]` 에서 2003 회계 연도에서 각 월의 일에 대해 계산 측정값은 **Adventure Works** 큐브. **하위 항목** 의 현재 멤버 로부터 결정 된 일 집합을 반환 하는 함수는 `[Date].[Fiscal]` 계층입니다.  
  
```  
WITH MEMBER Measures.[Avg Gross Profit Margin] AS Avg  
   (  
      Descendants( [Date].[Fiscal].CurrentMember,   
           [Date].[Fiscal].[Date]  
          ),   
        Measures.[Gross Profit Margin]  
   )  
SELECT  
   Measures.[Avg Gross Profit Margin] ON COLUMNS,  
   [Date].[Fiscal].[Month].Members ON ROWS  
FROM [Adventure Works]  
WHERE ([Date].[Fiscal Year].&[2003])  
```  
  
 다음 예에서는 수준 식을 사용하고 Australia의 각 State-Province에 대한 Internet Sales Amount와 Australia의 각 State-Province별 총 Internet Sales Amount의 백분율을 반환합니다. 이 예에서는 Item 함수를 사용 하 여에서 반환 되는 집합에서 첫 번째 (및만) 튜플을 추출할는 **상위** 함수입니다.  
  
```  
WITH MEMBER Measures.x AS   
   [Measures].[Internet Sales Amount] /   
   ( [Measures].[Internet Sales Amount],  
      Ancestors   
         ( [Customer].[Customer Geography].CurrentMember,   
           [Customer].[Customer Geography].[Country]  
         ).Item (0)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{Descendants   
   ( [Customer].[Customer Geography].[Country].&[Australia],   
     [Customer].[Customer Geography].[State-Province], SELF   
   )    
} ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
