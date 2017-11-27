---
title: Aggregate (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AGGREGATE
dev_langs:
- kbMDX
helpviewer_keywords:
- Aggregate function
ms.assetid: 9d5e0966-74d1-4cc8-b9f9-47e4dc65d165
caps.latest.revision: 52
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 894891e8341cc66253e9d4e5b952551b8b91071c
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="aggregate-mdx"></a>Aggregate(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  집합 식에 의해 반환된 셀을 집계하여 계산된 숫자를 반환합니다. 숫자 식이 지정되지 않은 경우 이 함수는 각 측정값에 대해 지정된 기본 집계 연산자를 사용하여 현재 쿼리 컨텍스트 내에서 각 측정값을 집계합니다. 숫자 식이 지정된 경우 이 함수는 먼저 지정된 집합의 각 셀에 대해 숫자 식을 계산한 다음 합계를 구합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Aggregate(Set_Expression [ ,Numeric_Expression ])  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 일련의 빈 튜플 또는 빈 집합이 지정되면 이 함수가 빈 값을 반환합니다.  
  
 다음 표에서 설명 방법을 **집계** 여러 집계 함수와 함께 함수의 동작이 변경 되었습니다.  
  
|집계 연산자|결과|  
|--------------------------|------------|  
|합계|집합에서의 값 합계를 반환합니다.|  
|Count|집합에서의 값 개수를 반환합니다.|  
|최대값|집합에서의 최대값을 반환합니다.|  
|Min|집합에서의 최소값을 반환합니다.|  
|반가산적 집계 함수|셰이프를 시간 축으로 나타낸 다음 집합에서의 반가산적 동작의 계산을 반환합니다.|  
|Distinct Count|slicer 축에 집합이 포함될 때 하위 큐브에 속하는 팩트 데이터의 집계를 반환합니다.<br /><br /> 집합의 각 멤버에 대한 고유 카운트를 반환합니다. 결과는 계산에 필요한 셀의 보안이 아니라 집계할 셀의 보안에 따라 달라집니다. 집합의 셀 보안은 오류를 발생시키지만 지정된 집합의 세분성 이하의 셀 보안은 무시됩니다. 해당 집합에 대한 계산은 오류를 발생시킵니다. 해당 집합에 대한 세분성 이하의 계산은 무시됩니다. 멤버와 해당 자식이 하나 이상 포함된 집합의 고유 카운트는 자식 멤버에 속하는 팩트의 고유 카운트를 반환합니다.|  
|집계될 수 없는 특성|값의 합계를 반환합니다.|  
|혼합 집계 함수|지원되지 않으며 오류를 발생시킵니다.|  
|단항 연산자|적용되지 않으며 합계에 의해 값이 집계됩니다.|  
|계산 측정값|계산 측정값이 적용되도록 계산 순서가 설정됩니다.|  
|계산 멤버|일반적인 규칙이 적용됩니다. 즉, 마지막 계산 순서가 우선합니다.|  
|할당|할당은 측정값 집계 함수에 따라 집계합니다. 측정값 집계 함수가 고유 카운트이면 할당의 합계가 계산됩니다.|  
  
## <a name="examples"></a>예  
 합계를 반환 하는 다음 예제에서는 `Measures.[Order Quantity]` 멤버에 포함 된 2003 년의 첫 8 개월 동안 집계는 `Date` 차원에서의 **Adventure Works** 큐브.  
  
```  
WITH MEMBER [Date].[Calendar].[First8Months2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Year],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First8Months2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 다음 예에서는 2003년 하반기 중 첫 2개월 동안의 데이터를 집계합니다.  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Semester],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 다음 예에서는 사용자가 선택한 State-Province 멤버에 대해 Aggregate 함수를 사용하여 계산한 값에 따라 이전 기간에 비해 판매량이 감소한 대리점의 수를 반환합니다. **Hierarchize** 및 **DrillDownLevel** 함수는 Product 차원의 제품 범주에에서 대해 판매량 감소 값을 반환 하는 데 사용 됩니다.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS   
   Count(  
      Filter(  
         Existing(Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] < ([Measures].[Reseller Sales Amount],  
            [Date].Calendar.PrevMember)  
            )  
         )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate (   
      {[Geography].[State-Province].&[WA]&[US],   
      [Geography].[State-Province].&[OR]&[US] }   
         )  
SELECT NON EMPTY Hierarchize (  
   AddCalculatedMembers (  
      {DrillDownLevel({[Product].[All Products]})}  
         )  
   )  
        DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
    [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
    [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>관련 항목:  
 [PeriodsToDate &#40; Mdx&#41;](../mdx/periodstodate-mdx.md)   
 [자식 &#40; Mdx&#41;](../mdx/children-mdx.md)   
 [Hierarchize &#40; Mdx&#41;](../mdx/hierarchize-mdx.md)   
 [Count &#40; 설정 &#41; &#40; Mdx&#41;](../mdx/count-set-mdx.md)   
 [필터 &#40; Mdx&#41;](../mdx/filter-mdx.md)   
 [AddCalculatedMembers &#40; Mdx&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [DrilldownLevel &#40; Mdx&#41;](../mdx/drilldownlevel-mdx.md)   
 [속성 &#40; Mdx&#41;](../mdx/properties-mdx.md)   
 [PrevMember &#40; Mdx&#41;](../mdx/prevmember-mdx.md)   
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

