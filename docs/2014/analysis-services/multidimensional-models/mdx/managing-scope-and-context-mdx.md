---
title: 범위 및 컨텍스트 관리 (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- scripts [MDX], context
- scope [MDX]
- CALCULATE statement
- This function [MDX]
- SCOPE statement
- scripts [MDX], scope
ms.assetid: 631e7c20-8be9-4c35-8609-76516aef19d1
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a712947ef820a573eed7839bb20329ee15180f23
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080541"
---
# <a name="managing-scope-and-context-mdx"></a>범위 및 컨텍스트 관리(MDX)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 MDX(Multidimensional Expressions) 스크립트는 스크립트 실행의 특정 시점에 전체 큐브나 큐브의 특정 부분에 적용될 수 있습니다. MDX 스크립트는 계산 패스를 사용하여 큐브 내에서의 계산에 계층화된 방법을 취할 수 있습니다.  
  
> [!NOTE]  
>  계산 패스가 계산에 미치는 영향에 대한 자세한 내용은 [패스 순서 및 계산 순서 이해&#40;MDX&#41;](mdx-data-manipulation-understanding-pass-order-and-solve-order.md)를 참조하세요.  
  
 계산 패스, 범위 및 MDX 스크립트 내에서 컨텍스트를 제어 하려면 특히 CACULATE 문을 사용 된 `This` 함수 및 SCOPE 문입니다.  
  
## <a name="using-the-calculate-statement"></a>CALCULATE 문 사용  
 CALCULATE 문은 큐브의 각 셀을 집계된 데이터로 채웁니다. 예를 들어 기본 MDX 스크립트는 스크립트 시작 부분에 CALCULATE 문이 하나 있습니다.  
  
 CALCULATE 문의 구문에 대한 자세한 내용은 [CALCULATE 문&#40;MDX&#41;](/sql/mdx/mdx-scripting-calculate)을 참조하세요.  
  
> [!NOTE]  
>  스크립트에 CALCULATE 문을 포함한 SCOPE 문이 들어 있는 경우 MDX는 전체 큐브에 대해서가 아니라 SCOPE 문으로 정의되는 하위 큐브의 컨텍스트 내에서 CALCULATE 문을 계산합니다.  
  
## <a name="using-the-this-function"></a>This 함수 사용  
 `This` 함수를 사용하면 MDX 스크립트 내의 현재 하위 큐브를 검색할 수 있습니다. 사용할 수는 `This` 함수 신속 하 게 설정할 현재 하위 큐브 내에 있는 셀의 값을 MDX 식입니다. 자주 사용 하 여 `This` 특정 계산 패스 중 특정 하위 큐브의 내용을 변경 하는 SCOPE 문과 함께에서 함수입니다.  
  
> [!NOTE]  
>  스크립트를 포함 한 SCOPE 문이 포함 되어 있는 경우는 `This` 함수를 MDX 계산에서 `This` 함수는 전체 큐브에 대해서가 아니라 SCOPE 문으로 정의 되는 하위 큐브의 컨텍스트 내에서.  
  
### <a name="this-function-example"></a>This 함수 예  
 사용 하 여 다음 MDX 스크립트 명령 예제는 `This` Finance 측정값 그룹에 있는 Amount 측정값의 값을 늘리려면 다음 함수는 [!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)] 샘플 큐브의 Customer 차원에 있는 Redmond 멤버의 자식에 대해 10%:  
  
```  
/* This SCOPE statement defines the current subcube */  
SCOPE([Customer].&[Redmond].MEMBERS,   
    [Measures].[Amount], *);  
        /* This expression sets the value of the Amount measure */  
        THIS = [Measures].[Amount] * 1.1;  
END SCOPE;  
```  
  
 구문에 대 한 자세한 내용은 `This` 함수, 참조 [이 &#40;MDX&#41;](/sql/mdx/this-mdx)합니다.  
  
## <a name="using-the-scope-statement"></a>SCOPE 문 사용  
 SCOPE 문은 MDX 스크립트 내의 다른 MDX 식과 문을 포함하고 해당 범위를 지정하는 현재 하위 큐브를 정의합니다. MDX는 하위 큐브의 컨텍스트 내에서 `This` 함수와 CALCULATE 문을 포함하여 이런 다른 MDX 식과 문을 계산합니다.  
  
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
  
 SCOPE 문의 구문에 대한 자세한 내용은 [SCOPE 문&#40;MDX&#41;](/sql/mdx/mdx-scripting-scope)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [MDX 언어 참조 &#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)   
 [기본 MDX 스크립트 &#40;MDX&#41;](the-basic-mdx-script-mdx.md)   
 [MDX 쿼리 기본 사항 &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
