---
title: "범위 및 컨텍스트 관리 (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripts [MDX], context
- scope [MDX]
- CALCULATE statement
- This function [MDX]
- SCOPE statement
- scripts [MDX], scope
ms.assetid: 631e7c20-8be9-4c35-8609-76516aef19d1
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 5e07ed3463c73d1eaeb14854e5eb4bc3d8fa81b6
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="managing-scope-and-context-mdx"></a>범위 및 컨텍스트 관리(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 MDX(Multidimensional Expressions) 스크립트는 스크립트 실행의 특정 시점에 전체 큐브나 큐브의 특정 부분에 적용될 수 있습니다. MDX 스크립트는 계산 패스를 사용하여 큐브 내에서의 계산에 계층화된 방법을 취할 수 있습니다.  
  
> [!NOTE]  
>  계산 패스가 계산에 미치는 영향에 대한 자세한 내용은 [패스 순서 및 계산 순서 이해&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md)를 참조하세요.  
  
 MDX 스크립트 내에서 계산 패스, 범위 및 컨텍스트를 제어하려면 특히 CALCULATE 문, **This** 함수 및 SCOPE 문을 사용합니다.  
  
## <a name="using-the-calculate-statement"></a>CALCULATE 문 사용  
 CALCULATE 문은 큐브의 각 셀을 집계된 데이터로 채웁니다. 예를 들어 기본 MDX 스크립트는 스크립트 시작 부분에 CALCULATE 문이 하나 있습니다.  
  
 CALCULATE 문의 구문에 대한 자세한 내용은 [CALCULATE 문&#40;MDX&#41;](../../../mdx/mdx-scripting-calculate.md)을 참조하세요.  
  
> [!NOTE]  
>  스크립트에 CALCULATE 문을 포함한 SCOPE 문이 들어 있는 경우 MDX는 전체 큐브에 대해서가 아니라 SCOPE 문으로 정의되는 하위 큐브의 컨텍스트 내에서 CALCULATE 문을 계산합니다.  
  
## <a name="using-the-this-function"></a>This 함수 사용  
 **This** 함수를 사용하면 MDX 스크립트 내의 현재 하위 큐브를 검색할 수 있습니다. **This** 함수를 사용하여 현재 하위 큐브 내에 있는 셀의 값을 MDX 식으로 빠르게 설정할 수 있습니다. SCOPE 문과 함께 **This** 함수를 사용하여 특정 계산 패스 중에 특정 하위 큐브의 내용을 변경하는 경우도 있습니다.  
  
> [!NOTE]  
>  스크립트에 **This** 함수를 포함한 SCOPE 문이 들어 있는 경우 MDX는 전체 큐브에 대해서가 아니라 SCOPE 문으로 정의되는 하위 큐브의 컨텍스트 내에서 **This** 함수를 계산합니다.  
  
### <a name="this-function-example"></a>This 함수 예  
 다음 MDX 스크립트 명령 예에서는 **This** 함수를 사용하여 [!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)] 샘플 큐브의 Finance 측정값 그룹에 있는 Amount 측정값을 Customer 차원에 있는 Redmond 멤버의 자식에 대해 10% 증가시키는 방법을 보여 줍니다.  
  
```  
/* This SCOPE statement defines the current subcube */  
SCOPE([Customer].&[Redmond].MEMBERS,   
    [Measures].[Amount], *);  
        /* This expression sets the value of the Amount measure */  
        THIS = [Measures].[Amount] * 1.1;  
END SCOPE;  
```  
  
 **This** 함수의 구문에 대한 자세한 내용은 [This&#40;MDX&#41;](../../../mdx/this-mdx.md)를 참조하세요.  
  
## <a name="using-the-scope-statement"></a>SCOPE 문 사용  
 SCOPE 문은 MDX 스크립트 내의 다른 MDX 식과 문을 포함하고 해당 범위를 지정하는 현재 하위 큐브를 정의합니다. MDX는 하위 큐브의 컨텍스트 내에서 **This** 함수와 CALCULATE 문을 포함하여 이런 다른 MDX 식과 문을 계산합니다.  
  
 SCOPE 문은 동적이지만 특성상 반복적이지는 않습니다. SCOPE 문 내에 포함된 문은 한 번 실행되지만 하위 큐브 자체는 동적으로 결정될 수 있습니다. 예를 들어 SampleCube라는 큐브가 있다고 가정합니다. SampleCube 큐브에 대해 다음 SCOPE 문을 적용하여 컨텍스트를 측정값 차원 내의 ALLMEMBERS로 정의하는 하위 큐브를 정의합니다.  
  
 `SCOPE([Measures].ALLMEMBERS);`  
  
 `THIS = [Measures].ALLMEMBERS.COUNT;`  
  
 `END SCOPE;`  
  
 이 SCOPE 문 내부의 문과 식은 한 번 실행됩니다.  
  
 이제 어떤 업무용 사용자가 SampleCube 큐브에 대해 ExistingMeasure라는 측정값을 하나 포함한 다음 MDX 쿼리를 실행합니다.  
  
 `WITH MEMBER [Measures].[NewMeasure] AS '1'`  
  
 `SELECT`  
  
 `[Measures].ALLMEMBERS ON COLUMNS,`  
  
 `[Customer].DEFAULTMEMBER ON ROWS`  
  
 `FROM`  
  
 `[SampleCube]`  
  
 쿼리에서 반환하는 셀 집합은 다음 테이블에 표시된 출력과 비슷한 형태입니다.  
  
||[ExistingMeasure]|[NewMeasure]|  
|-|-------------------------|--------------------|  
|[Customer].[All]|2|2|  
  
 반환된 셀 집합을 보고서 NewMeasure 측정값을 정의한 후 MDX 스크립트 내의 SCOPE 문에 포함된 ExistingMeasure 값이 동적으로 업데이트되는 방법을 검토합니다.  
  
 SCOPE 문은 다른 SCOPE 문 내에 중첩될 수 있습니다. 하지만 SCOPE 문은 반복적이지 않으므로 SCOPE 문을 중첩하는 주 목적은 특수 처리를 위해 하위 큐브를 보다 세분화하는 것입니다.  
  
### <a name="scope-statement-example"></a>SCOPE 문의 예  
 다음 MDX 스크립트 예에서는 SCOPE 문을 사용하여 [!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)] 샘플 큐브의 Finance 측정값 그룹에 있는 Amount 측정값을 Customer 차원에 있는 Redmond 멤버의 자식에 대해 10% 높게 설정하는 방법을 보여 줍니다. 하지만 또 다른 SCOPE 문은 하위 큐브를 변경하여 역년 기준 2002년도의 자식에 대한 Amount 측정값을 포함시킵니다. 마지막으로 Amount 측정값을 해당 하위 큐브에 대해서만 집계하고 다른 역년의 Amount 측정값에 대해 집계된 값은 바꾸지 않고 그대로 둡니다.  
  
```  
/* Calculate the entire cube first. */  
CALCULATE;  
/* This SCOPE statement defines the current subcube */  
SCOPE([Customer].&[Redmond].MEMBERS,   
    [Measures].[Amount], *);  
        /* This expression sets the value of the Amount measure */  
        THIS = [Measures].[Amount] * 1.1;  
END SCOPE;  
```  
  
 SCOPE 문의 구문에 대한 자세한 내용은 [SCOPE 문&#40;MDX&#41;](../../../mdx/mdx-scripting-scope.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 언어 참조 &#40; Mdx&#41;](../../../mdx/mdx-language-reference-mdx.md)   
 [기본 MDX 스크립트 &#40; Mdx&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)   
 [MDX 쿼리 기본 사항 &#40; Analysis Services &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
