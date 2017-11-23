---
title: "MDX (MDX)로 하위 큐브 작성 | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
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
- queries [MDX], subcubes
- subcubes [MDX]
- filtered views [MDX]
- MDX [Analysis Services], subcubes
- Multidimensional Expressions [Analysis Services], subcubes
- CREATE SUBCUBE statement
ms.assetid: 5403a62b-99ac-4d83-b02a-89bf78bf0f46
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d56fe149317939cfb0b184dcd20b1411514f2ca9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="building-subcubes-in-mdx-mdx"></a>MDX로 하위 큐브 작성(MDX)
  하위 큐브는 기본 데이터의 필터링된 뷰를 나타내는 큐브의 하위 집합입니다. 큐브를 하위 큐브로 제한하여 쿼리 성능을 높일 수 있습니다.  
  
 하위 큐브를 정의하려면 이 항목에서 설명하는 바와 같이 [CREATE SUBCUBE](../../../mdx/mdx-data-definition-create-subcube.md) 문을 사용합니다.  
  
## <a name="create-subcube-syntax"></a>CREATE SUBCUBE 구문  
 다음 구문을 사용하여 하위 큐브를 만듭니다.  
  
```  
CREATE SUBCUBE Subcube_Identifier AS Subcube_Expression  
```  
  
 CREATE SUBCUBE 구문은 꽤 간단합니다. *Subcube_Identifier* 매개 변수는 하위 큐브의 기반이 되는 큐브를 식별합니다. *Subcube_Expression* 매개 변수는 하위 큐브가 될 큐브의 해당 부분을 선택합니다.  
  
 하위 큐브를 만들고 난 후 해당 하위 큐브는 세션을 닫거나 [DROP SUBCUBE](../../../mdx/mdx-data-definition-drop-subcube.md) 문을 실행할 때까지는 모든 MDX 쿼리에 대한 컨텍스트가 됩니다.  
  
### <a name="what-a-subcube-contains"></a>하위 큐브가 포함하는 것  
 CREATE SUBCUBE 문은 간단하게 사용할 수 있지만 이 문 자체가 하위 큐브의 일부가 되는 멤버들을 모두 명시적으로 표시하지는 않습니다. 하위 큐브를 정의할 때 다음 규칙을 적용합니다.  
  
-   어떤 계층의 **(All)** 멤버를 포함하면 해당 계층의 모든 멤버가 포함됩니다.  
  
-   임의의 멤버를 포함하면 해당 멤버의 상위 항목과 하위 항목이 포함됩니다.  
  
-   어떤 계층의 모든 멤버를 포함하면 그 계층의 모든 멤버가 포함됩니다. 다른 계층의 멤버가 해당 수준(예를 들어 고객을 포함하지 않은 도시와 같이 균형이 맞지 않는 계층)의 멤버와 공존하지 않는 경우에는 제외됩니다.  
  
-   하위 큐브는 항상 큐브의 모든 **(All)** 멤버를 포함합니다.  
  
 또한 하위 큐브 내의 집계 값은 시각적으로 합쳐집니다. 예를 들어 하위 큐브는 `USA`, `WA`및 `OR`을 포함합니다. `USA` 및 `{WA,OR}` 이 하위 큐브에 의해 정의된 유일한 주이므로 `WA` 에 대한 집계 값은 `OR` 의 합계가 됩니다. 다른 모든 주는 무시합니다.  
  
 또한 하위 큐브 외부의 셀에 대한 명시적 참조는 전체 큐브의 컨텍스트에서 계산되는 셀 값을 반환합니다. 예를 들어 현재 연도로 제한되는 하위 큐브를 만듭니다. 그런 다음 [ParallelPeriod](../../../mdx/parallelperiod-mdx.md) 함수를 사용하여 현재 연도를 이전 연도와 비교합니다. 이전 연도 값은 하위 큐브 외부에 있지만 두 값의 차이가 반환됩니다.  
  
 마지막으로 원래 컨텍스트를 덮어쓰지 않은 경우 하위 SELECT에서 계산된 집합 함수는 하위 SELECT의 컨텍스트에서 계산됩니다. 컨텍스트를 덮어쓴 경우 집합 함수는 전체 큐브의 컨텍스트에서 계산됩니다.  
  
## <a name="create-subcube-example"></a>CREATE SUBCUBE 예  
 다음 예에서는 예산 큐브를 4200 및 4300 계정으로만 한정하는 하위 큐브를 만드는 방법을 보여 줍니다.  
  
 `CREATE SUBCUBE Budget AS SELECT {[Account].[Account].&[4200], [Account].[Account].&[4300] } ON 0 FROM Budget`  
  
 해당 세션에 대한 하위 큐브를 만들면 이후의 쿼리는 전체 큐브가 아니라 그 하위 큐브에 대해서만 적용됩니다. 예를 들어 다음 쿼리를 실행하십시오. 이 쿼리는 4200 및 4300 계정의 멤버만 반환합니다.  
  
 `SELECT [Account].[Account].Members ON 0, Measures.Members ON 1 FROM Budget`  
  
## <a name="see-also"></a>관련 항목:  
 [쿼리에 큐브 컨텍스트 설정&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)   
 [MDX 쿼리 기본 사항&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
