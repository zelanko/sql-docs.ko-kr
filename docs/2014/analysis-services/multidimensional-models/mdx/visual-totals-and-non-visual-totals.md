---
title: 보이는 값 합계 및 보이지 않는 값 합계 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: ea9d02f2-a668-4547-ade5-e3d077a2e1bd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc4d831d2c6b42a591dff5fc3c8424a55ac91062
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197053"
---
# <a name="visual-totals-and-non-visual-totals"></a>보이는 값 합계 및 보이지 않는 값 합계
  보이는 값 합계는 열이나 행에서 볼 수 있는 모든 항목이 더해지는 열이나 행의 끝에 있는 합계입니다. 이 동작은 표시된 대부분의 테이블에서 기본 동작입니다. 그러나 사용자가 테이블의 특정 열만 표시하고 표시되지 않은 열을 포함하여 전체 행에 대한 합계를 유지하려는 경우가 있습니다. 이러한 경우를 `Non Visual Totals`라고 하는데 이는 보이는 값과 보이지 않는 값 모두에서 합계가 제공되기 때문입니다.  
  
 다음 시나리오에서는 보이지 않는 값 합계의 동작을 보여 줍니다. 첫 번째 단계에서는 보이는 값 합계의 기본 동작을 보여 줍니다.  
  
 다음 예는 제품 범주가 열이고 대리점 업종이 행인 테이블에서 [Reseller Sales Amount] 수치를 가져오기 위한 [Adventure Works]의 쿼리입니다. 다음 SELECT 문이 실행될 경우 제품과 대리점 둘 다에 대한 합계가 제공됩니다.  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 결과는 다음과 같습니다.  
  
|||||||  
|-|-|-|-|-|-|  
||**All Products**|**Accessories**|**Bikes**|**Clothing**|**Components**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$66,302,381.56**|**$1,777,840.84**|**$11,799,076.66**|  
|**Specialty Bike Shop**|**$6,756,166.18**|**$65,125.48**|**$6,080,117.73**|**$252,933.91**|**$357,989.07**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$30,892,354.33**|**$592,385.71**|**$3,307,774.48**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$29,329,909.50**|**$932,521.23**|**$8,133,313.11**|  
  
## <a name="non-visual-on-rows-and-columns"></a>행과 열에 대한 보이지 않는 값 합계  
 Accessories 및 Clothing 제품과 Value Added Reseller 및 Warehouse 대리점에 대한 데이터만 포함된 테이블을 만들고 전체 합계를 유지하려면 NON VISUAL을 사용하여 다음과 같이 문을 작성할 수 있습니다.  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works])`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 결과는 다음과 같습니다.  
  
|||||  
|-|-|-|-|  
||**All Products**|**Accessories**|**Clothing**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$1,777,840.84**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$592,385.71**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$932,521.23**|  
  
## <a name="non-visual-on-rows"></a>행에 대한 보이지 않는 값 합계  
 열에는 보이는 값 합계만 포함하고 행 합계에는 모든 [Category]의 순 합계를 표시하는 테이블을 만들려면 다음과 같은 쿼리를 실행해야 합니다.  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0`  
  
 `from ( Select {[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 0`  
  
 `from [Adventure Works])`  
  
 `)`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 NON VISUAL이 어떻게 [Category]에만 적용되는지 확인하십시오.  
  
 위 쿼리는 다음과 같은 결과를 생성합니다.  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$73,694,430.80|$506,172.45|$1,524,906.93|  
|Value Added Reseller|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 이전 결과와 비교하면 [All Resellers] 행에는 [Value Added Reseller] 및 [Warehouse]에 표시된 값에 대한 합계가 표시되고 [All Products] 열에는 표시되지 않은 제품을 포함한 모든 제품의 합계 값이 표시되는 것을 알 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDX의 개념을 키 &#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)   
 [Autoexist](autoexists.md)   
 [멤버, 튜플 및 집합 작업 &#40;MDX&#41;](working-with-members-tuples-and-sets-mdx.md)   
 [MDX 쿼리 기본 사항 &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)   
 [기본 MDX 쿼리 &#40;MDX&#41;](mdx-query-the-basic-query.md)   
 [쿼리 및 Slicer 축으로 쿼리 제한 &#40;MDX&#41;](mdx-query-and-slicer-axes-restricting-the-query.md)   
 [쿼리에 큐브 컨텍스트 설정 &#40;MDX&#41;](establishing-cube-context-in-a-query-mdx.md)  
  
  
