---
title: MemberValue (MDX) | Microsoft Docs
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
f1_keywords: MEMBERVALUE
dev_langs: kbMDX
helpviewer_keywords: MemberValue function
ms.assetid: f9b2af16-2b81-48e4-ae81-99f64e4bbc98
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2e3489ae5740b28f10a7aebed2b48d35d64c36da
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="membervalue-mdx"></a>MemberValue(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  멤버의 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression.MemberValue  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버로 평가되는 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 반환되는 멤버 값에는 다음 정보가 포함되며 반환 값에 표시되는 순서대로 나열됩니다.  
  
-   정의된 경우 값 바인딩  
  
-   이름 바인딩이 없거나 또는 키 및 캡션이 같은 열에 바인딩되는 경우 원래 데이터 형식의 키  
  
-   멤버의 캡션  
  
## <a name="example"></a>예제  
 다음 예에서는 Adventure Works 큐브에서 Date 차원의 첫 번째 날짜에 대한 값 바인딩, 멤버 키 및 캡션을 반환합니다.  
  
```  
WITH MEMBER Measures.ValueColumn as [Date].[Calendar].[July 1, 2001].MemberValue  
MEMBER Measures.KeyColumn as [Date].[Calendar].[July 1, 2001].Member_Key  
MEMBER Measures.NameColumn as [Date].[Calendar].[July 1, 2001].Member_Name  
  
SELECT {Measures.ValueColumn, Measures.KeyColumn, Measures.NameColumn}  ON 0  
from [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
