---
title: "패스 순서 및 계산 순서 (MDX) 이해 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- evaluation order [MDX]
- calculation order [MDX]
- SOLVE_ORDER property
- queries [MDX], solve orders
- solve orders [MDX]
- pass orders [MDX]
- expressions [MDX], solve orders
ms.assetid: 7ed7d4ee-4644-4c5d-99a4-c4b429d0203c
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7e1f07fa57c0c4c16dd1cbbeeac504b59a250912
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="mdx-data-manipulation---understanding-pass-order-and-solve-order"></a>MDX 데이터 조작-이해 패스 순서 및 계산 순서
  MDX 스크립트 결과로 계산될 때 큐브는 사용되는 여러 계산 관련 기능에 따라 여러 계산 단계를 거칠 수 있습니다. 이러한 각 단계를 계산 패스라고 합니다.  
  
 계산 패스는 계산 패스 번호라는 서수 위치로 참조될 수 있습니다. 큐브의 모든 셀 계산을 완전히 마치는 데 필요한 계산 패스 개수를 큐브의 계산 패스 깊이라고 합니다.  
  
 팩트 테이블 및 쓰기 저장 데이터는 패스 0에만 영향을 줍니다. 스크립트는 패스 0 이후의 데이터를 채우며 스크립트에서 각 대입식 및 계산 문은 새로운 패스를 만듭니다. MDX 스크립트 외부에서 절대 패스 0에 대한 참조는 큐브의 스크립트에서 만든 마지막 패스를 참조합니다.  
  
 계산 멤버는 모든 패스에서 생성되지만 식은 현재 패스에 적용됩니다. 이전 패스에는 계산 측정값이 포함되지만 Null 값이 들어 있습니다.  
  
## <a name="solve-order"></a>계산 순서  
 계산 순서는 식을 완료하는 경우 계산의 우선 순위를 확인합니다. 단일 패스 내에서 계산 순서는 다음 두 가지를 확인합니다.  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에서 차원, 멤버, 계산 멤버, 사용자 지정 롤업 및 계산 셀을 평가하는 순서  
  
-   [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에서 사용자 지정 멤버, 계산 멤버, 사용자 지정 롤업 및 계산 셀을 계산하는 순서  
  
 계산 순서가 가장 높은 멤버가 우선 순위가 가장 높습니다.  
  
> [!NOTE]  
>  집계 함수는 이러한 우선 순위에서 제외됩니다. 집계 함수의 계산 멤버는 교차하는 계산 측정값 보다 계산 순서가 낮습니다.  
  
## <a name="solve-order-values-and-precedence"></a>계산 순서 값 및 우선 순위  
 계산 순서 값의 범위는 -8181에서 65535 사이입니다. 이 범위에서 일부 계산 순서 값은 다음 표에서와 같이 특정 유형의 계산에 해당합니다.  
  
|계산|계산 순서|  
|-----------------|-----------------|  
|사용자 지정 멤버 수식|-5119|  
|단항 연산자|-5119|  
|보이는 합계 계산|-4096|  
|그 외 모든 계산(특별히 지정되지 않은 경우)|0|  
  
 계산 순서 값을 설정할 때는 양의 정수만 사용하는 것이 좋습니다. 이전 테이블에서 표시된 계산 순서 값보다 낮은 값을 지정하면 계산 패스를 예측하지 못할 수 있습니다. 예를 들어 계산 멤버에 대한 계산에 기본 사용자 지정 롤업 수식 값인 -5119보다 낮은 계산 순서 값이 사용됩니다. 이러한 낮은 계산 순서 값은 계산 멤버가 사용자 지정 롤업 수식보다 먼저 계산되도록 하므로 잘못된 결과가 발생할 수 있습니다.  
  
### <a name="creating-and-changing-solve-order"></a>계산 순서 만들기 및 바꾸기  
 큐브 디자이너의 **계산**창에서 계산 순서를 바꿔서 계산 멤버 및 계산 셀에 대한 계산 순서를 바꿀 수 있습니다.  
  
 MDX에서는 **SOLVE_ORDER** 키워드를 사용하여 계산 멤버 및 계산 셀을 만들거나 바꿀 수 있습니다.  
  
## <a name="solve-order-examples"></a>계산 순서 예  
 계산 순서의 복잡성을 설명하기 위해 다음 일련의 MDX 쿼리는 각각 계산 순서가 문제시 되지 않는 두 개의 쿼리로 시작합니다. 그런 다음 이 두 쿼리는 계산 순서가 필요한 하나의 쿼리로 조합됩니다.  
  
> [!NOTE]  
>  Adventure Works 예제 다차원 데이터베이스에 대해 이러한 MDX 쿼리를 실행할 수 있습니다. codeplex 사이트에서 [AdventureWorks 다차원 모델 SQL Server 2012](http://msftdbprodsamples.codeplex.com/releases/view/55330) 예제를 다운로드할 수 있습니다.  
  
### <a name="query-1differences-in-income-and-expenses"></a>쿼리 1 - 수입과 비용 차이  
 첫 번째 MDX 쿼리에서는 다음 예와 비슷한 간단한 MDX 쿼리를 구성하여 각 해의 판매액 및 비용 차이를 계산합니다.  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] )  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 이 쿼리에는 계산 멤버가 `Year Difference`하나만 있습니다. 계산 멤버가 하나뿐이기 때문에 큐브에 계산 멤버가 사용되지 않으면 계산 순서가 문제가 되지 않습니다.  
  
 이 MDX 쿼리는 다음 표와 비슷한 결과 집합을 생성합니다.  
  
||Internet Sales Amount|Internet Total Product Cost|  
|-|---------------------------|---------------------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|  
|**Year Difference**|($20,160.56)|$2,878.06|  
  
### <a name="query-2percentage-of-income-after-expenses"></a>쿼리 2 - 비용에 따른 수입 백분율  
 두 번째 쿼리에서는 다음 MDX 쿼리를 사용하여 각 해의 비용에 따른 수입 백분율을 계산합니다.  
  
```  
WITH   
MEMBER  
[Measures].[Profit Margin] AS   
([Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent"  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 이 MDX 쿼리에는 이전 쿼리와 같이 계산 멤버가 `Profit Margin`하나만 있으며, 따라서 계산 순서와 관련된 복잡한 문제가 없습니다.  
  
 이 MDX 쿼리는 다음 표와 비슷한 약간 다른 결과 집합을 생성합니다.  
  
||Internet Sales Amount|Internet Total Product Cost|이익률|  
|-|---------------------------|---------------------------------|-------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|41.60%|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|41.45%|  
  
 결과 집합에서 첫 번째 쿼리와 두 번째 쿼리의 차이는 계산 멤버의 배치 차이로 인해 비롯됩니다. 첫 번째 쿼리에서 계산 멤버는 두 번째 쿼리에 표시된 COLUMNS 축이 아니라 ROWS 축의 일부입니다. 이러한 배치 차이는 두 계산 멤버를 단일 MDX 쿼리로 조합하는 다음 쿼리에서 중요해집니다.  
  
### <a name="query-3combined-year-difference-and-net-income-calculations"></a>쿼리 3 - 조합된 연간 차이 및 순수입 계산  
 이 마지막 쿼리에서는 이전 예에서의 두 쿼리를 단일 MDX 쿼리로 조합하며 열과 행 모두에 대한 계산 때문에 계산 순서가 중요해집니다. 올바른 순서로 계산되도록 보장하기 위해 **SOLVE_ORDER** 키워드를 사용하여 계산이 발생하는 순서를 정의합니다.  
  
 **SOLVE_ORDER** 키워드는 MDX 쿼리 또는 **CREATE MEMBER** 명령의 계산 멤버에 대한 계산 순서를 지정합니다. **SOLVE_ORDER** 키워드에 사용된 정수 값은 상대적이며 0부터 시작할 필요가 없으며 연속적일 필요도 없습니다. 이 값은 MDX에서 단순히 더 큰 값의 멤버 계산으로부터 파생된 값에 따라 멤버를 계산하도록 지정합니다. 계산 멤버가 **SOLVE_ORDER** 키워드 없이 정의된 경우 해당 계산 멤버의 기본값은 0입니다.  
  
 예를 들어 처음 두 쿼리 예에서 사용된 값을 조합할 경우 두 계산 멤버인 `Year Difference` 및 `Profit Margin`은 MDX 쿼리 예의 결과 데이터 집합에 있는 단일 셀에서 교차합니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에서 이 셀을 계산하는 방법은 계산 순서에 의해서만 결정할 수 있습니다. 이 셀을 구성하는 데 사용된 수식은 두 계산 멤버의 계산 순서에 따라 서로 다른 결과를 생성합니다.  
  
 먼저 처음 두 쿼리에 사용된 계산을 다음 MDX 쿼리에서 조합해 보십시오.  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] ) ,  
SOLVE_ORDER = 1  
MEMBER  
[Measures].[Profit Margin] AS   
( [Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent" ,  
SOLVE_ORDER = 2  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 이 조합된 MDX 쿼리 예에서 `Profit Margin` 은 계산 순서가 가장 높기 때문에 두 식이 교차할 때 우선 순위를 갖습니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 는 `Profit Margin` 수식을 사용하여 문제의 셀을 계산합니다. 이 중첩된 계산의 결과는 다음 표에 표시된 것과 같습니다.  
  
||Internet Sales Amount|Internet Total Product Cost|이익률|  
|-|---------------------------|---------------------------------|-------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|41.60%|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|41.45%|  
|**Year Difference**|($20,160.56)|$2,878.06|114.28%|  
  
 공유 셀의 결과는 `Profit Margin`에 대한 수식을 기반으로 합니다. 즉, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 는 `Year Difference` 데이터로 공유 셀의 결과를 계산하여 다음 수식을 만듭니다(쉽게 구분할 수 있도록 결과가 반올림됨).  
  
```  
((9,770,899.74 - 9,791,060.30) - (5,721,205.24 - 5,718,327.17)) / (9,770,899.74 - 9,791,060.30) = 1.14275744   
```  
  
 또는  
  
```  
(23,038.63) / (20,160.56) = 114.28%  
```  
  
 확실하게 잘못되었습니다. 하지만 MDX 쿼리에서 계산 멤버에 대한 계산 순서를 바꾸면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 는 공유 셀의 결과를 다르게 계산합니다. 다음 조합 MDX 쿼리는 계산 멤버에 대한 계산 순서를 반대로 바꿉니다.  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] ) ,  
SOLVE_ORDER = 2  
MEMBER  
[Measures].[Profit Margin] AS   
( [Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent" ,  
SOLVE_ORDER = 1  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 계산 멤버의 순서가 바뀌면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 는 다음 표에 표시된 것과 같이 `Year Difference` 수식을 사용하여 셀을 계산합니다.  
  
||Internet Sales Amount|Internet Total Product Cost|이익률|  
|-|---------------------------|---------------------------------|-------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|41.60%|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|41.45%|  
|**Year Difference**|($20,160.56)|$2,878.06|(0.15%)|  
  
 이 쿼리에는 `Year Difference` 데이터와 함께 `Profit Margin` 수식이 사용되기 때문에 공유 셀에 대한 수식은 다음 계산과 비슷합니다.  
  
```  
(($9,770,899.74 - 5,721,205.24) / $9,770,899.74) - ((9,791,060.30 - 5,718,327.17) / 9,791,060.30) = -0.15   
```  
  
 또는  
  
```  
0.4145 - 0.4160= -0.15  
```  
  
## <a name="additional-considerations"></a>기타 고려 사항  
 계산 멤버, 사용자 지정 롤업 수식 또는 계산 셀이 포함된 차원 수가 높은 큐브에서는 특히 계산 순서를 다루기가 매우 복잡할 수 있습니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에서 MDX 쿼리를 계산할 때 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 는 MDX 쿼리에 지정된 큐브의 차원을 비롯하여 지정된 패스 내에 관련된 모든 사항에 대한 계산 순서 값을 고려합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [CalculationCurrentPass&#40;MDX&#41;](../../../mdx/calculationcurrentpass-mdx.md)   
 [CalculationPassValue &#40; Mdx&#41;](../../../mdx/calculationpassvalue-mdx.md)   
 [CREATE MEMBER 문&#40;MDX&#41;](../../../mdx/mdx-data-definition-create-member.md)   
 [데이터 조작&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)  
  
  
