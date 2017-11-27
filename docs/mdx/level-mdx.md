---
title: Level (MDX) | Microsoft Docs
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
- LEVEL
dev_langs:
- kbMDX
helpviewer_keywords:
- Level function
ms.assetid: 10bbe4ac-44bc-45c7-81a1-85423fbeaab1
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 311bbd9138a12d7f4013bd5e21538f9acae59ec9
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="level-mdx"></a>Level(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  멤버의 수준을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression.Level  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
### <a name="examples"></a>예  
 다음 예제에서는 **수준** Adventure Works 큐브의 모든 월을에서 반환 하는 함수입니다.  
  
```  
SELECT[Date].[Fiscal].[Month].[February 2002].Level.Members ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
 다음 예제에서는 **수준** Adventure Works 큐브에 있는 Model Name 특성 계층의 All-Purpose Bike Stand에 대 한 수준 이름을 반환 하는 함수입니다.  
  
```  
WITH MEMBER Measures.x AS   
   [Product].[Model Name].[All-Purpose Bike Stand].Level.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

