---
title: Avg (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aa8817e35a589def4631bd455637d05fc62d3a0f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68017016"
---
# <a name="avg-mdx"></a>Avg(MDX)


  집합을 계산하고 집합의 측정값이나 지정된 측정값에 대해 집합에서 비어 있지 않은 셀 값의 평균을 계산하여 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Avg( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 빈 튜플 집합이 나 빈 집합이 지정 된 경우 **Avg** 함수는 빈 값을 반환 합니다.  
  
 **Avg** 함수는 지정 된 집합의 셀에서 값의 합계를 계산한 다음 계산 된 합계를 지정 된 집합의 비어 있지 않은 셀 개수로 나누는 방법으로 지정 된 집합에서 비어 있지 않은 셀 값의 평균을 계산 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]는 숫자 집합의 평균값을 계산할 때 Null을 무시합니다.  
  
 특정 숫자 식 (일반적으로 측정값)을 지정 하지 않으면 **Avg** 함수는 현재 쿼리 컨텍스트 내에서 각 측정값의 평균을 계산 합니다. 특정 측정값이 제공 되는 경우 **Avg** 함수는 먼저 집합에 대해 측정값을 평가한 다음 함수는 지정 된 측정값을 기반으로 평균을 계산 합니다.  
  
> [!NOTE]  
>  계산 멤버 문에서 **currentmember** 함수를 사용 하는 경우 이러한 쿼리 컨텍스트의 현재 좌표에 대 한 기본 측정값이 없으므로 숫자 식을 지정 해야 합니다.  
  
 빈 셀을 강제로 포함 하려면 응용 프로그램이 [CoalesceEmpty](../mdx/coalesceempty-mdx.md) 함수를 사용 하거나 빈 값에 대해 0 값을 제공 하는 유효한 *Numeric_Expression* 를 지정 해야 합니다. 빈 셀에 대한 자세한 내용은 OLE DB 설명서를 참조하십시오.  
  
## <a name="examples"></a>예  
 다음 예에서는 지정된 집합의 측정값 평균을 반환합니다. 측정값은 지정된 집합 멤버의 기본 측정값이나 지정된 측정값일 수 있습니다.  
  
 `WITH SET [NW Region] AS`  
  
 `{[Geography].[State-Province].[Washington]`  
  
 `, [Geography].[State-Province].[Oregon]`  
  
 `, [Geography].[State-Province].[Idaho]}`  
  
 `MEMBER [Geography].[Geography].[NW Region Avg] AS`  
  
 `AVG ([NW Region]`  
  
 `--Uncomment the line below to get an average by Reseller Gross Profit Margin`  
  
 `--otherwise the average will be by whatever the default measure is in the cube,`  
  
 `--or whatever measure is specified in the query`  
  
 `--, [Measures].[Reseller Gross Profit Margin]`  
  
 `)`  
  
 `SELECT [Date].[Calendar Year].[Calendar Year].Members ON 0`  
  
 `FROM [Adventure Works]`  
  
 `WHERE ([Geography].[Geography].[NW Region Avg])`  
  
 다음 예에서는 **놀이 Works** 큐브에서 2003 회계 연도의 `Measures.[Gross Profit Margin]` 각 월 일에 계산 된 측정값의 일일 평균을 반환 합니다. **Avg** 함수는 `[Ship Date].[Fiscal Time]` 계층의 각 월에 포함 된 일 집합의 평균을 계산 합니다. 첫 번째 버전의 계산에서는 평균에서 매출을 기록하지 않은 일을 제외하는 기본 Avg 동작을 보여 주고, 두 번째 버전에서는 평균에 매출이 없는 일을 포함하는 방법을 보여 줍니다.  
  
 `WITH MEMBER Measures.[Avg Gross Profit Margin] AS`  
  
 `Avg(`  
  
 `Descendants(`  
  
 `[Ship Date].[Fiscal].CurrentMember,`  
  
 `[Ship Date].[Fiscal].[Date]`  
  
 `),`  
  
 `Measures.[Gross Profit Margin]`  
  
 `), format_String='percent'`  
  
 `MEMBER Measures.[Avg Gross Profit Margin Including Empty Days] AS`  
  
 `Avg(`  
  
 `Descendants(`  
  
 `[Ship Date].[Fiscal].CurrentMember,`  
  
 `[Ship Date].[Fiscal].[Date]`  
  
 `),`  
  
 `CoalesceEmpty(Measures.[Gross Profit Margin],0)`  
  
 `), Format_String='percent'`  
  
 `SELECT`  
  
 `{Measures.[Avg Gross Profit Margin],Measures.[Avg Gross Profit Margin Including Empty Days]} ON COLUMNS,`  
  
 `[Ship Date].[Fiscal].[Fiscal Year].Members ON ROWS`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Product].&[344])`  
  
 다음 예에서는 **놀이 Works** 큐브에서 2003 회계 연도의 `Measures.[Gross Profit Margin]` 각 반기 일자에 대해 계산 된 측정값의 일일 평균을 반환 합니다.  
  
```  
WITH MEMBER Measures.[Avg Gross Profit Margin] AS  
   Avg(  
      Descendants(  
         [Ship Date].[Fiscal].CurrentMember,   
            [Ship Date].[Fiscal].[Date]  
      ),   
      Measures.[Gross Profit Margin]  
   )  
SELECT  
   Measures.[Avg Gross Profit Margin] ON COLUMNS,  
      [Ship Date].[Fiscal].[Fiscal Year].[FY 2003].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
