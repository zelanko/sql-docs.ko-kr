---
title: "큐브 및 하위 큐브 식을 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- subcubes [MDX]
- cubes [Analysis Services], MDX
- CURRENTCUBE keyword
- expressions [MDX], subcubes
- expressions [MDX], cubes
ms.assetid: 95ae034d-8f88-4820-91c6-205ec424e119
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 71ba6c7d7d5040481ea13d80a160fc19c0704c10
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="using-cube-and-subcube-expressions"></a>큐브 및 하위 큐브 식 사용
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  큐브 또는 하위 큐브의 데이터를 정의, 조작 또는 검색하기 위해 MDX(Multidimensional Expressions) 문에 큐브 및 하위 큐브 식을 사용하는 경우가 있습니다.  
  
## <a name="cube-expressions"></a>큐브 식  
 큐브 식은 큐브 식별자 또는 CURRENTCUBE 키워드를 포함하므로 간단한 식이어야 합니다. 많은 MDX 문에서 현재의 큐브 컨텍스트를 식별하기 위해 큐브 식별자를 요청하는 대신 CURRENTCUBE 키워드를 사용합니다.  
  
 큐브 식별자로 표시 *Cube_Name* 는 MDX 문의 BNF 표기법 설명 합니다.  
  
 큐브 식은 여러 위치에 나타날 수 있습니다. MDX SELECT 문에서 데이터를 검색할 큐브를 지정합니다. 다음 예제 쿼리에서 [Adventure Works] 식은 해당 이름의 큐브를 참조합니다.  
  
 `SELECT [Measures].[Internet Sales Amount] ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
 CREATE MEMBER 문에서 큐브 식은 만드는 계산 멤버가 나타날 큐브를 지정합니다. 다음 예에서 문은 Adventure Works 큐브의 Measures 차원에 계산 멤버를 만듭니다.  
  
 `CREATE MEMBER [Adventure Works].[Measures].[Test] AS 1`  
  
 다음 예와 같이 MDX 스크립트에서 CREATE MEMBER 문을 사용할 때 계산 멤버가 생성되는 큐브가 MDX 스크립트가 속한 큐브와 동일해야 하므로 큐브의 이름이 CURRENTCUBE 키워드로 교체될 수 있습니다.  
  
 `CREATE MEMBER CURRENTCUBE.[Measures].[Test] AS 1;`  
  
 이 경우 큐브 이름이 더 이상 하드 코딩되지 않으므로 보다 쉽게 한 큐브에서 다른 큐브로 계산 멤버 정의를 복사하여 붙여 넣을 수 있습니다.  
  
## <a name="subcube-expressions"></a>하위 큐브 식  
 하위 큐브 식은 하위 큐브 식별자 또는 하위 큐브를 반환하는 MDX 문을 포함할 수 있습니다. 하위 큐브 식에 하위 큐브 식별자가 포함되어 있는 경우 하위 큐브 식은 간단한 식이 됩니다. 하위 큐브 식에 하위 큐브를 반환하는 MDX 문이 포함되어 있는 경우 하위 큐브 식은 복잡한 문입니다. 예를 들어 다음 예와 같이 MDX SELECT 문은 하위 큐브를 반환하므로 하위 큐브 식이 허용되는 곳에 사용할 수 있습니다.  
  
 `SELECT [Measures].MEMBERS ON COLUMNS,`  
  
 `[Date].[Calendar Year].MEMBERS ON ROWS`  
  
 `FROM`  
  
 `(SELECT [Measures].[Internet Sales Amount] ON COLUMNS,`  
  
 `[Date].[Calendar Year].&[2004] ON ROWS`  
  
 `FROM [Adventure Works])`  
  
 FROM 절에서 이렇게 SELECT 문을 사용하는 것을 하위 SELECT라고도 합니다.  
  
 또는 MDX 스크립트에 범위 할당을 수행할 때 일반적으로 하위 큐브 식이 사용됩니다. 다음 예에서는 SCOPE 문을 사용하여 [Measures].[Internet Sales Amount]로 구성된 하위 큐브에 대한 할당을 제한합니다.  
  
 `SCOPE([Measures].[Internet Sales Amount]);`  
  
 `This=1;`  
  
 `END SCOPE;`  
  
 하위 큐브 식별자로 표시 *Subcube_Name*합니다. 나타납니다.  
  
## <a name="see-also"></a>참고 항목  
 [기본 MDX 쿼리 &#40; Mdx&#41;](../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)   
 [MDX &#40;로 하위 큐브 작성 Mdx&#41;](../analysis-services/multidimensional-models/mdx/building-subcubes-in-mdx-mdx.md)   
 [SUBCUBE 문 &#40; 만들기 Mdx&#41;](../mdx/mdx-data-definition-create-subcube.md)   
 [식 &#40; Mdx&#41;](../mdx/expressions-mdx.md)   
 [SCOPE 문 &#40; Mdx&#41;](../mdx/mdx-scripting-scope.md)  
  
  

