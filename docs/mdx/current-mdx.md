---
title: Current (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: CURRENT
dev_langs: kbMDX
helpviewer_keywords: Current function
ms.assetid: 6f689742-f9b6-4339-a691-31ff28582c36
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 826457b678e249c3c578c229f726e6fde7a4692a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="current-mdx"></a>Current(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  반복하는 동안 집합에서 현재 튜플을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set_Expression.Current   
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 반복 중 각 단계에서 수행되는 튜플은 현재 튜플입니다. **현재** 함수는이 튜플을 반환 합니다. 이 함수는 집합에 대해 반복하는 동안에만 유효합니다.  
  
 포함 하는 집합에서 반복 되는 MDX 함수는 [생성](../mdx/generate-mdx.md) 함수입니다.  
  
> [!NOTE]  
>  이 함수는 집합 별칭을 사용하거나 명명된 집합을 정의함으로써 명명된 집합에 대해서만 사용할 수 있습니다.  
  
## <a name="examples"></a>예  
 사용 하는 방법을 보여 주는 다음 예제는 **현재** 함수 내 **생성**:  
  
 `WITH`  
  
 `//Creates a set of tuples consisting of all Calendar Years crossjoined with`  
  
 `//all Product Categories`  
  
 `SET MyTuples AS CROSSJOIN(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS,`  
  
 `[Product].[Category].[Category].MEMBERS)`  
  
 `//Iterates through each tuple in the set and returns the name of the Calendar`  
  
 `//Year in each tuple`  
  
 `MEMBER MEASURES.CURRENTDEMO AS`  
  
 `GENERATE(MyTuples, MyTuples.CURRENT.ITEM(0).NAME, ", ")`  
  
 `SELECT MEASURES.CURRENTDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
