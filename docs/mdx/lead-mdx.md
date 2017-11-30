---
title: Lead (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: LEAD
dev_langs: kbMDX
helpviewer_keywords: Lead function
ms.assetid: f3250092-7b98-40b5-8dca-77e3b50734a0
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 03512a3e07e9b041f794bbdc75ba067539a28e24
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="lead-mdx"></a>Lead(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  멤버 수준을 따라 지정한 위치 번호만큼 지정한 멤버의 뒤에 있는 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression.Lead( Index )  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
 *Index*  
 멤버 위치 번호를 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>주의  
 수준 내의 멤버 위치는 특성 계층의 일반적인 순서에 따라 결정됩니다. 위치를 나타내는 번호는 0부터 시작합니다.  
  
 지정한 간격이 영 (0) 하는 경우는 **발생할** 함수는 지정된 된 멤버를 반환 합니다.  
  
 지정한 간격이 음수 이면는 **발생할** 함수는 이전 멤버를 반환 합니다.  
  
 `Lead(1)`해당 하는 [NextMember](../mdx/nextmember-mdx.md) 함수입니다. `Lead(-1)`해당 하는 [PrevMember](../mdx/prevmember-mdx.md) 함수입니다.  
  
 **발생할** 함수는 비슷합니다는 [지연](../mdx/lag-mdx.md) 함수와 **지연** 반대 방향으로 함수를 찾습니다는 **발생할** 함수입니다. 즉, `Lead(n)`은 `Lag(-n)`과 동일합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 2001년 12월의 값을 반환합니다.  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(-2) ON 0  
FROM [Adventure Works]  
  
```  
  
 다음 예에서는 2002년 3월의 값을 반환합니다.  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
