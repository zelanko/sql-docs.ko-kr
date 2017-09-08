---
title: "계산 컨텍스트 | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: aec8aa98-b77d-4f8f-9684-2618b1d8e970
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6101305123e48bf5194313c852f2a24e45e5847a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="calculation-context"></a>계산 컨텍스트
  계산 컨텍스트는 식이 계산되고 모든 좌표가 명시적으로 알려지거나 식에서 파생될 수 있는 큐브의 알려진 하위 공간입니다.  
  
## <a name="determining-the-calculation-context"></a>계산 컨텍스트 확인  
 모든 집합, 멤버, 튜플, 또는 숫자 함수는 MDX 식 또는 문 전체의 컨텍스트에서 실행됩니다. 튜플과 같은 인수가 함수에 전달될 때는 큐브 공간의 일부 좌표만 명시적으로 제공됩니다. 다른 좌표는 현재 계산 컨텍스트에 따라 얻습니다.  
  
 지정되지 않은 셀 좌표 및 특성 멤버의 계산 컨텍스트는 다음 순서에 따라 결정됩니다.  
  
1.  FROM 절(해당되는 경우) - 이 절은 큐브 전체를 지정하거나 SELECT 문 형식으로 하위 큐브를 지정할 수 있습니다.  
  
2.  WHERE 절(해당되는 경우) - 이 절은 *slicer 축*이라고도 하며 쿼리에서 열 및 행 축에 반환되는 멤버를 제한하는 집합, 튜플 또는 멤버를 지정하는 데 사용됩니다. 개념적으로 열 또는 행 축에 명시적으로 지정되지 않은 모든 특성 계층의 기본 멤버는 slicer 축의 일부입니다.  
  
    > [!NOTE]  
    >  특정 특성의 셀 좌표가 slicer 축과 다른 축 모두에서 지정된 경우 축의 집합 멤버를 결정할 때는 함수에 지정된 좌표가 우선합니다. [Filter(MDX)](../../../mdx/filter-mdx.md) 및 [Order(MDX)](../../../mdx/order-mdx.md) 함수가 이러한 함수의 예입니다. 즉, WHERE 절이나 FROM 절의 SELECT 문을 사용하여 계산 컨텍스트에서 제외된 특성 멤버를 기준으로 결과를 필터링하거나 정렬할 수 있습니다.  
  
3.  쿼리 또는 식에 정의된 명명된 집합 및 계산 멤버  
  
4.  행 및 열 축에 지정된 튜플과 집합. 이때 행, 열 또는 slicer 축에 나타나지 않는 특성에는 기본 멤버를 사용합니다.  
  
5.  각 축의 큐브 또는 하위 큐브 셀. 이때 축의 빈 튜플은 제거하고 HAVING 절을 적용합니다.  
  
6.  자세한 내용은 [쿼리에 큐브 컨텍스트 설정&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)을 참조하세요.  
  
 다음 쿼리에서 행 축의 계산 컨텍스트는 WHERE 절에 지정된 Country 특성 멤버와 Calendar Year 특성 멤버에 의해 제한됩니다.  
  
```  
SELECT Customer.City.City.Members ON 0  
FROM [Adventure Works]  
WHERE (Customer.Country.France, [Date].[Calendar].[Calendar Year].[CY 2004],  
   Measures.[Internet Sales Amount])  
```  
  
 그러나 행 축에 **FILTER** 함수를 지정하여 이 쿼리를 수정하고 **FILTER** 함수에서 Calendar Year 특성 계층 멤버를 사용하면 열 축의 집합 멤버에 대한 계산 컨텍스트를 지정하는 데 사용된 Calendar Year 특성 계층의 특성 멤버가 수정될 수 있습니다.  
  
```  
SELECT FILTER  
   (  
      Customer.City.City.Members,   
         ([Date].[Calendar].[Calendar Year].[CY 2003],  
            Measures.[Internet Order Quantity]) > 75   
   ) ON 0  
FROM [Adventure Works]  
WHERE (Customer.Country.France,  
   [Date].[Calendar].[Calendar Year].[CY 2004],  
   Measures.[Internet Sales Amount])  
```  
  
 이 쿼리에서 Calendar Year 특성 계층의 명목적 계산 컨텍스트는 CY 2004이지만 열 축에 나타나는 튜플의 셀에 대한 계산 컨텍스트는 Calendar Year 특성 계층의 CY 2003 멤버에 따라 필터링됩니다. 또한 이 계산 컨텍스트는 Internet Order Quantity 측정값에 따라서도 필터링됩니다. 그러나 열 축의 집합 멤버가 설정되고 나면 해당 축에 나타나는 멤버의 값에 대한 계산 컨텍스트는 다시 WHERE 절에 따라 결정됩니다.  
  
> [!IMPORTANT]  
>  쿼리 성능을 향상시키려면 멤버와 튜플을 확인 과정에서 가능한 한 빨리 제거해야 합니다. 이렇게 하면 쿼리할 때 최종 멤버 집합에 대한 복잡한 계산이 가능한 가장 적은 수의 셀에 대해 수행됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [쿼리에 큐브 컨텍스트 설정&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)   
 [MDX 쿼리 기본 사항 &#40; Analysis Services &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [MDX의 주요 개념&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)  
  
  
