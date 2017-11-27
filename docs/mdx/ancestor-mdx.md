---
title: Ancestor (MDX) | Microsoft Docs
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
- ANCESTOR
dev_langs:
- kbMDX
helpviewer_keywords:
- Ancestor function
ms.assetid: b5bf2ce4-20df-4ebc-97eb-e44a6f64cc50
caps.latest.revision: 46
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a9aad080913e792291f8d72281afe522704042e5
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="ancestor-mdx"></a>Ancestor(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정된 수준이나 지정된 멤버로부터 지정된 거리만큼 떨어진 수준에서 지정된 멤버의 상위 항목을 반환하는 함수입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Level syntax  
Ancestor(Member_Expression, Level_Expression)  
  
Numeric syntax  
Ancestor(Member_Expression, Distance)  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
 *Level_Expression*  
 수준을 반환하는 유효한 MDX 식입니다.  
  
 *거리*  
 지정된 멤버와의 거리를 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>주의  
 와 **상위** 함수를 제공 하는 함수 MDX 멤버 식을 사용 하 여 고 멤버의 상위 항목인 수준의 MDX 식 또는 해당 멤버 위의 수준 수를 나타내는 숫자 식을 제공 합니다. 이 정보는 **상위** 함수는 해당 수준의 상위 멤버를 반환 합니다.  
  
> [!NOTE]  
>  상위 멤버 뿐 아니라 상위 멤버를 포함 하는 집합을 반환 하려면 사용 된 [상위 요소 &#40; Mdx&#41; ](../mdx/ancestors-mdx.md) 함수입니다.  
  
 수준 식이 지정 되는 **상위** 함수는 지정된 된 수준에서 지정 된 멤버의 상위 항목을 반환 합니다. 지정된 멤버가 지정된 수준과 동일한 계층 내에 없으면 이 함수는 오류를 반환합니다.  
  
 거리를 지정 하는 경우는 **상위** 함수는 멤버 식으로 지정 된 계층에서 지정 된 단계 수를 지정된 된 멤버의 상위 항목을 반환 합니다. 멤버는 특성 계층, 사용자 정의 계층 또는 경우에 따라 부모-자식 계층의 멤버로 지정될 수 있습니다. 숫자 1은 멤버의 부모를 반환하고 숫자 2는 멤버의 최상위 항목(있는 경우)을 반환합니다. 숫자 0은 해당 멤버 자체만 반환합니다.  
  
> [!NOTE]  
>  이 형식을 사용 하 여는 **상위** 함수 경우은 부모의 수준을 알 수 없는 또는 명명할 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 수준 식을 사용하고 Australia의 각 State-Province에 대한 Internet Sales Amount와 Australia의 총 Internet Sales Amount에 대한 이 값의 백분율을 반환합니다.  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   (  
   [Measures].[Internet Sales Amount],    
      Ancestor   
         (  
         [Customer].[Customer Geography].CurrentMember,  
            [Customer].[Customer Geography].[Country]  
         )  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{  
   Descendants   
      (  
        [Customer].[Customer Geography].[Country].&[Australia],  
           [Customer].[Customer Geography].[State-Province], SELF   
      )  
} ON 1  
FROM [Adventure Works]  
```  
  
 다음 예에서는 숫자 식을 사용하고 Australia의 각 State-Province에 대한 Internet Sales Amount와 모든 국가의 총 Internet Sales Amount에 대한 이 값의 백분율을 반환합니다.  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   (  
      [Measures].[Internet Sales Amount],  
         Ancestor   
            ([Customer].[Customer Geography].CurrentMember, 2)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{  
   Descendants   
      (  
         [Customer].[Customer Geography].[Country].&[Australia],  
            [Customer].[Customer Geography].[State-Province], SELF   
      )  
} ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

